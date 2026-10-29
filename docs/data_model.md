# Data Model

## Model Design

The Power BI project uses a **single analytical data table: `zomato`**.

There are no separate fact and dimension tables and no analytical
relationships between multiple data tables.

``` text
                 ┌────────────────────────────┐
                 │          zomato             │
                 │                            │
                 │ Restaurant Name             │
                 │ Ratings                     │
                 │ Votes                       │
                 │ Cuisine                     │
                 │ Place / City                │
                 │ Item Name                   │
                 │ Best Seller                 │
                 │ Prices                      │
                 │ ...                         │
                 └────────────────────────────┘
```

## Why a Single Table Was Sufficient

The source already contains the attributes required for menu,
restaurant, cuisine, geographic, pricing and engagement analysis. A more
complex relational model would not have added analytical value for this
project.

The complexity therefore sits in the **analytical logic**, not in
multi-table modeling.

## Measure Organization

Two dedicated measure tables organize the DAX layer:

-   `Measures Table (main)` --- core reporting and descriptive measures
-   `Measures Table (p2)` --- strategic portfolio measures

These are **measure containers**, not additional analytical tables and
not relationship-bearing dimensions.

## Model Philosophy

**Minimal model complexity + strong analytical logic** was intentional.
The report demonstrates that sophisticated business analysis does not
require an unnecessarily complicated semantic model when the source
structure already supports the business questions.
