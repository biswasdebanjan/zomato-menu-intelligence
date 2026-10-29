# Technical QA Notes

## Price Tier Boundary — Resolved

The Price Tier calculated column has been aligned with the business-definition framework.

```DAX
Price Tier =
SWITCH(
    TRUE(),
    Zomato[Prices] <= 150, "Budget",
    Zomato[Prices] <= 300, "Value",
    Zomato[Prices] <= 500, "Premium",
    "Luxury"
)
```

The final business definitions are:

- Budget: ≤ ₹150
- Value: ₹151–300
- Premium: ₹301–500
- Luxury: > ₹500

The updated dashboard screenshot reflects the refreshed segmentation results after this boundary correction.
