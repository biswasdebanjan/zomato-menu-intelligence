# Source & Data

## Dataset

**Zomato Restaurants Dataset for Metropolitan Areas**

Source: Kaggle Author: Narsing Rao Goud

Dataset size: **123,657 rows × 12 columns**

Coverage: **13 Indian metropolitan areas**

Source URL:
https://www.kaggle.com/datasets/narsingraogoud/zomato-restaurants-dataset-for-metropolitan-areas

## Source Fields

The source contains 12 fields:

1.  Restaurant Name
2.  Dining Rating
3.  Delivery Rating
4.  Dining Votes
5.  Delivery Votes
6.  Cuisine
7.  Place Name
8.  City
9.  Item Name
10. Best Seller
11. Votes
12. Prices

## Data Grain

The project treats the source as menu-item / restaurant-level records.
Menu-item identity is represented through `Item Name`, while restaurant,
cuisine, city, pricing and engagement attributes provide the analytical
context.

## Power Query Preparation

The PBIX uses a deliberately light Power Query layer:

-   Source ingestion
-   Promoted Headers
-   Changed Type

The source structure was retained largely intact, with the main
analytical transformations implemented through calculated columns and
DAX in Power BI.

## Data Quality / Reproducibility Note

The repository does not redistribute the original Kaggle dataset. Users
should obtain the source from the original Kaggle page and reproduce the
Power BI report using the included PBIX.
