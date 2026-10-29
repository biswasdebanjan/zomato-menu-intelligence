# DAX Logic

## Overview

The DAX layer is divided conceptually into two levels:

1.  **Calculated columns** create the analytical segmentation framework.
2.  **Measures** quantify the resulting strategic groups and support the
    report visuals.

The documentation focuses on the DAX that demonstrates analytical
reasoning rather than every basic aggregation in the PBIX.

------------------------------------------------------------------------

## 1. Popularity Segment --- Calculated Column

``` dax
Popularity Segment =
SWITCH(
    TRUE(),
    Zomato[Votes] = 0, "Dormant Products",
    Zomato[Votes] <= 15, "Niche Products",
    Zomato[Votes] <= 50, "Popular Products",
    Zomato[Votes] <= 100, "High-Performing Products",
    "Signature Products"
)
```

### Business logic

      Votes Segment
  --------- --------------------------
          0 Dormant Products
      1--15 Niche Products
     16--50 Popular Products
    51--100 High-Performing Products
       101+ Signature Products

`SWITCH(TRUE())` allows sequential row-level business rules to be
implemented directly in the calculated column.

------------------------------------------------------------------------

## 2. Price Tier --- Calculated Column

``` dax
Price Tier =
SWITCH(
    TRUE(),
    Zomato[Prices] <= 150, "Budget",
    Zomato[Prices] <= 300, "Value",
    Zomato[Prices] <= 500, "Premium",
    "Luxury"
)
```

### Business definition

The Value tier now includes ₹300, aligning the calculated-column logic
with the displayed business framework:

- Budget: ≤ ₹150
- Value: ₹151–300
- Premium: ₹301–500
- Luxury: > ₹500

------------------------------------------------------------------------

## 3. Product Strategy Segment --- Calculated Column

``` dax
Product Strategy Segment =
SWITCH(
    TRUE(),

    Zomato[Price Tier] IN {"Budget","Value"} &&
    Zomato[Popularity Segment] IN {
        "Popular Products",
        "High-Performing Products",
        "Signature Products"
    },
    "Volume Drivers",

    Zomato[Price Tier] IN {"Premium","Luxury"} &&
    Zomato[Popularity Segment] IN {
        "Popular Products",
        "High-Performing Products",
        "Signature Products"
    },
    "Premium Winners",

    Zomato[Price Tier] IN {"Premium","Luxury"} &&
    Zomato[Popularity Segment] IN {
        "Dormant Products",
        "Niche Products"
    },
    "Dormant Premium",

    Zomato[Price Tier] IN {"Budget","Value"} &&
    Zomato[Popularity Segment] IN {
        "Dormant Products",
        "Niche Products"
    },
    "Dormant Core"
)
```

### Why this matters

This is the central analytical transformation of the project. It
combines **price positioning** and **customer engagement** to determine
the strategic role of each menu item.

------------------------------------------------------------------------

## 4. Strategic Measures

### Premium Winners Count

``` dax
Premium Winners Count =
CALCULATE(
    DISTINCTCOUNT(Zomato[Item Name]),
    Zomato[Product Strategy Segment] = "Premium Winners"
)
```

### Premium Winner Share %

``` dax
Premium Winner Share % =
DIVIDE(
    [Premium Winners Count],
    DISTINCTCOUNT(Zomato[Item Name]),
    0
)
```

### Volume Drivers

``` dax
Volume Drivers =
CALCULATE(
    DISTINCTCOUNT(Zomato[Item Name]),
    Zomato[Product Strategy Segment] = "Volume Drivers"
)
```

### Dormant Premium Count

``` dax
Dormant Premium Count =
CALCULATE(
    DISTINCTCOUNT(Zomato[Item Name]),
    Zomato[Product Strategy Segment] = "Dormant Premium"
)
```

### Dormant Product %

``` dax
Dormant Product % =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(Zomato[Item Name]),
        Zomato[Popularity Segment] = "Dormant Products"
    ),
    DISTINCTCOUNT(Zomato[Item Name])
)
```

### Engagement per Restaurant

``` dax
Engagement per Restaurant =
DIVIDE(
    [Total Votes],
    [Total Restaurants],
    0
)
```

## Measures intentionally not showcased

Basic measures such as average price, average ratings, total votes and
total restaurant counts are used for reporting but are not treated as
technical highlights. The repository focuses on DAX that demonstrates
**segmentation, filter context, portfolio composition and normalized
engagement**.

The `Measures Table (dist)` is treated as an intermediate calculation
layer used for percentile/distribution-based segmentation rather than as
a collection of report-facing metrics.
