# Zomato Menu Intelligence & Portfolio Strategy

<img src="images/00_title_card.png" alt="Zomato Menu Intelligence & Portfolio Strategy" width="100%">

<p align="center">
  <a href="https://app.powerbi.com/view?r=eyJrIjoiNjRkZTAwNzQtMGNkNi00NTFjLTg1YjEtOGI3NWZlMmEzZDcxIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9"><strong>Live Power BI Dashboard</strong></a>
</p>

---

## 01 — The Project

This project analyses Zomato menu-item data to understand how **price positioning, customer engagement, product popularity, restaurant performance, cuisine mix, and city-level demand** combine to shape menu portfolio performance.

The objective was not to build another restaurant-rating dashboard.

The analysis was designed to answer a more commercial question:

> **Which parts of a menu portfolio create meaningful customer engagement, which products are underperforming, where does premium demand already exist, and where should management scale, optimize, premiumize, or rationalize the portfolio?**

The analytical chain is:

```text
Menu-Item Data
      ↓
Price Positioning
      ↓
Customer Engagement
      ↓
Popularity Segmentation
      ↓
Product Strategy
      ↓
Cuisine / Restaurant / City Intelligence
      ↓
Portfolio Opportunity
      ↓
Business Action
```

The resulting dashboard therefore moves from **descriptive menu reporting to portfolio-level decision support**.

---

## 02 — Data at a Glance

| Attribute | Detail |
|---|---|
| **Source** | Kaggle — Zomato Restaurants Dataset for Metropolitan Areas |
| **Publisher** | Narsing Rao Goud |
| **Dataset Size** | **123,657 rows × 12 columns** |
| **Geographic Scope** | **13 Indian metropolitan areas** |
| **Data Grain** | Menu-item / restaurant-level records |
| **Core Entities** | Restaurants, menu items, cuisines, cities, pricing, customer votes |
| **Primary Platform** | Microsoft Power BI |
| **Analysis Focus** | Menu pricing, customer engagement, popularity, portfolio strategy |

**Dataset source:**  
https://www.kaggle.com/datasets/narsingraogoud/zomato-restaurants-dataset-for-metropolitan-areas

The source data contains restaurant, menu-item, cuisine, location, pricing, ratings, and voting information. The analysis uses these fields to move from individual menu-item observations to portfolio-level patterns.

The raw source dataset is **not redistributed in this repository**.

---

## 03 — Business Questions

The analysis was designed around decision-oriented questions rather than individual dashboard visuals.

- Which menu items generate the strongest customer engagement?
- How does menu pricing relate to customer demand and popularity?
- Which products successfully combine higher pricing with strong engagement?
- How large is the dormant portion of the menu portfolio?
- Which products should be scaled, optimized, premiumized, or rationalized?
- Which cuisines show the strongest premium opportunity?
- Which cities demonstrate stronger customer engagement and restaurant efficiency?
- Which restaurants provide useful benchmarks for menu and service performance?
- Should menu strategy be standardized nationally or adapted to local market behavior?
- How can the portfolio be managed continuously rather than through one-time menu expansion or cleanup?

The questions deliberately move from **product-level behavior to portfolio-level decisions**.

---

## 04 — Analytical Thinking Behind the Project

This project was deliberately built as an analytical workflow rather than a collection of Power BI visuals.

```text
Business Question
      ↓
Understand the Menu-Item Data
      ↓
Prepare & Validate the Data
      ↓
Establish Price Positioning
      ↓
Measure Customer Engagement
      ↓
Create Popularity Segments
      ↓
Build Product Strategy Segments
      ↓
Analyse Cuisine / Restaurant / City Patterns
      ↓
Identify Portfolio Opportunities
      ↓
Translate Evidence into Business Action
```

The key principle was to avoid evaluating a menu item through a single metric.

A high-priced product is not automatically a premium success.

A highly voted product is not automatically commercially attractive.

A highly rated restaurant is not automatically a strong portfolio benchmark.

The analysis therefore combines **price position + customer engagement + product strategy + market context** before arriving at a recommendation.

> A dashboard can show which products are popular. An analyst should be able to explain **where demand exists, how that demand relates to price, which parts of the portfolio create value, where inefficiency is concentrated, and what the business should do next.**

---

## 05 — Analytical Framework

The analytical framework is built in a deliberate three-layer sequence:

**Price Tier → Popularity Segment → Product Strategy**

The first two dimensions describe the product. The third converts those descriptions into an actionable strategic classification.

### Layer 1 — Price Tier

Price tiers classify menu items according to their menu-price position.

| Tier | Business Definition | Strategic Interpretation |
|---|---:|---|
| **Budget** | ≤ ₹150 | Accessible / volume-oriented |
| **Value** | ₹151–299 | Mainstream portfolio / broader reach |
| **Premium** | ₹300–500 | Higher-value positioning |
| **Luxury** | > ₹500 | Highest price positioning |

The purpose of the price framework is not simply to label products as cheap or expensive.

It creates a consistent way to ask:

> **Does customer demand justify the product's position in the pricing landscape?**

---

### Layer 2 — Popularity Segment

Popularity is classified using menu-item vote volume.

| Segment | Votes | Interpretation |
|---|---:|---|
| **Dormant Products** | 0 | No recorded customer traction |
| **Niche Products** | 1–15 | Low but existing interest |
| **Popular Products** | 16–50 | Growing acceptance |
| **High-Performing Products** | 51–100 | Strong customer approval |
| **Signature Products** | 101+ | Highest observed engagement |

These thresholds were designed to create interpretable demand bands rather than treating every vote count as an isolated number.

The segmentation allows the analysis to distinguish between:

- no observed engagement,
- early-stage interest,
- established demand,
- strong demand,
- and standout customer favorites.

---

### Layer 3 — Product Strategy

Price Tier and Popularity Segment are then combined through row-level DAX logic to create an actionable portfolio classification.

| Product Strategy | Logic | Strategic Interpretation |
|---|---|---|
| **Volume Drivers** | Budget / Value + Popular / High-Performing / Signature | Scale and protect proven demand |
| **Premium Winners** | Premium / Luxury + Popular / High-Performing / Signature | Strengthen premium positioning |
| **Dormant Premium** | Premium / Luxury + Dormant / Niche | Reposition, reprice, or discontinue |
| **Dormant Core** | Budget / Value + Dormant / Niche | Rationalize and simplify |

This is the central analytical transformation of the project:

```text
Price Tier
     +
Popularity Segment
     ↓
Product Strategy Segment
     ↓
Portfolio Decision
```

The framework transforms a descriptive menu dataset into a **decision-oriented portfolio model**.

---

## 06 — Technical Architecture

### Technology Stack

- **Power BI** — analytical modeling, DAX, interactive analysis and dashboard development
- **Power Query** — source preparation and data transformation
- **DAX** — KPIs, portfolio metrics and segmentation logic
- **Git / GitHub** — version control, documentation and portfolio publication

### Analytical Model

The Power BI solution is centered on the Zomato menu-item dataset and uses calculated analytical logic to create the segmentation framework.

The most important distinction is between:

**Report-facing measures**  
used to produce KPIs, charts and portfolio metrics

and

**Analytical segmentation logic**  
used to classify menu items before the business analysis is performed.

The percentile/distribution calculation measures used during segmentation are supporting analytical machinery. They are intentionally not presented as headline dashboard measures because their role is to establish analytical thresholds rather than directly drive report visuals.

---

### Core DAX Segmentation Logic

#### Price Tier

```DAX
Price Tier =
SWITCH(
    TRUE(),
    Zomato[Prices] <= 150, "Budget",
    Zomato[Prices] <= 299, "Value",
    Zomato[Prices] <= 500, "Premium",
    "Luxury"
)
```

#### Popularity Segment

```DAX
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

#### Product Strategy Segment

```DAX
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

The significance of this logic is not the syntax itself. It is the **business translation encoded into the model**.

The calculated columns establish a repeatable classification system that can then be used consistently across portfolio, cuisine, city, restaurant and pricing analysis.

---

### Selected Analytical Measures

Only the measures that materially support the analytical story are highlighted here.

#### Premium Winner Share

```DAX
Premium Winner Share % =
DIVIDE(
    [Premium Winners Count],
    DISTINCTCOUNT(Zomato[Item Name]),
    0
)
```

This converts Premium Winner volume into a portfolio-level share.

#### Premium Winners Count

```DAX
Premium Winners Count =
CALCULATE(
    DISTINCTCOUNT(Zomato[Item Name]),
    Zomato[Product Strategy Segment] = "Premium Winners"
)
```

#### Volume Drivers

```DAX
Volume Drivers =
CALCULATE(
    DISTINCTCOUNT(Zomato[Item Name]),
    Zomato[Product Strategy Segment] = "Volume Drivers"
)
```

#### Dormant Premium Count

```DAX
Dormant Premium Count =
CALCULATE(
    DISTINCTCOUNT(Zomato[Item Name]),
    Zomato[Product Strategy Segment] = "Dormant Premium"
)
```

#### Dormant Product Share

```DAX
Dormant Product % =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(Zomato[Item Name]),
        Zomato[Popularity Segment] = "Dormant Products"
    ),
    DISTINCTCOUNT(Zomato[Item Name])
)
```

The project deliberately does **not** document every basic aggregation measure. The focus is on the logic that demonstrates analytical design rather than simply proving that Power BI can calculate an average or a count.

---

## 07 — Report Architecture

The Power BI report is organized into four report experiences.

### 01 — Project Hub

The landing page establishes:

- Project purpose
- Business objectives
- Dashboard structure
- Analytical scope
- Strategic impact areas

It gives the stakeholder context before entering the analytical pages.

### 02 — Menu Intelligence & Portfolio Strategy

This is the **primary analytical dashboard** and the main page showcased in this repository.

It brings together:

- Portfolio KPIs
- City performance
- Cuisine opportunity
- Product Strategy mix
- Customer engagement
- Premium Winner concentration
- Restaurant benchmarks
- City-level engagement
- Price-tier behavior

The dashboard is designed to move from **portfolio-level signals to specific opportunities**.

![Menu Intelligence and Portfolio Strategy dashboard](images/02_menu_portfolio.jpg)

### 03 — Executive Action Plan

The recommendations page translates the analytical findings into ten strategic actions covering:

- Growth and investment
- Portfolio optimization
- Market expansion
- Operational excellence

The detailed recommendation document is available in the `deliverables` folder.

### 04 — Segmentation Framework & Business Definitions

This page acts as a stakeholder reference for:

- Price Tier definitions
- Popularity Segment definitions
- Product Strategy logic
- Strategic interpretation of each segment

It makes the analytical framework transparent rather than leaving the segmentation logic hidden inside the model.

---

## 08 — What the Analysis Found

The analysis produced several portfolio-level signals that materially shaped the recommendations.

### Portfolio Scale

The dashboard covers:

- **914 restaurants**
- **54.96K menu items**
- **3.82 average dining rating**
- **3.96 average delivery rating**
- **₹241 average menu price**
- **1.87K Premium Winners**
- **71.72% dormant portfolio share**

The most important signal is not the size of the menu.

It is the **concentration of customer engagement within a relatively small portion of the portfolio**.

---

### 01 — Proven Demand Is Concentrated

The Product Strategy analysis shows that **Volume Drivers** generate the largest customer-engagement pool, followed by Premium Winners.

The latest dashboard records approximately:

- **2.50M engagement** for Volume Drivers
- **332K engagement** for Premium Winners
- **172K engagement** for Dormant Core
- **43K engagement** for Dormant Premium

This creates two distinct growth engines:

**Volume Drivers** provide reach and established demand.

**Premium Winners** demonstrate that higher-priced products can succeed when customer engagement already exists.

The strategic implication is that growth should not depend on expanding the entire menu uniformly.

---

### 02 — The Dormant Portfolio Is the Largest Structural Opportunity

**71.72% of menu items fall into the dormant portfolio based on the project's popularity definition.**

This does not automatically mean every dormant item should be removed.

It does indicate that a substantial proportion of the menu has little or no recorded customer engagement and therefore deserves review.

The appropriate response is to:

- identify items worth redesigning,
- reprice products where positioning is weak,
- replace low-productivity items with proven alternatives,
- and simplify menus where assortment creates complexity without demand.

---

### 03 — Premium Demand Exists, But It Is Selective

Premium and Luxury products should not be treated as a universal growth opportunity.

The Product Strategy framework identifies **Premium Winners** specifically where higher price positioning is combined with established customer engagement.

The analysis therefore supports **selective premiumization** rather than blanket premium expansion.

The strongest premium opportunity should be pursued where:

**higher pricing + customer demand + market context**

already align.

---

### 04 — Cuisine Opportunity Is Uneven

The cuisine analysis shows meaningful differences in customer engagement and premium opportunity.

The dashboard identifies **Beverages, Desserts, Fast Food, Pizza and Sichuan** among the cuisines requiring closer premium-optimization attention.

Beverages also lead the Premium Winner leaderboard in the current report.

This suggests that premium strategy should be **category-specific**, rather than applied equally across the entire menu portfolio.

---

### 05 — City-Level Demand Is Not Uniform

Hyderabad stands out strongly in the current dashboard.

Customer engagement is approximately:

- **Hyderabad — 803K**
- **Jaipur — 433K**
- **Bangalore — 282K**
- **Kolkata — 277K**
- **Chennai — 229K**

Hyderabad also leads the restaurant engagement-efficiency view.

The implication is important:

> **A national menu strategy may leave market-specific opportunities unexplored.**

Pricing, product launches, promotions and premium offerings should be adapted to local demand patterns.

---

### 06 — Restaurant Benchmarks Matter

The restaurant leaderboard highlights high-performing local operators such as:

- Bawarchi | Hyderabad
- Lucky Restaurant | Hyderabad
- Mehfil | Hyderabad
- 4M Biryani House | Hyderabad
- Zam Zam Restaurant | Kolkata

These restaurants combine meaningful customer engagement with strong dining and delivery ratings.

The analysis therefore treats high-performing local restaurants as potential **operational and portfolio benchmarks**, rather than relying only on broad national comparisons.

---

## 09 — Business Recommendations

The analysis was translated into ten strategic recommendations.

### Growth & Investment

**1. Scale Proven Menu Winners**

Prioritize Volume Drivers and Signature Products across additional restaurants and cities instead of expanding the menu indiscriminately.

**2. Adopt a Dual Portfolio Growth Strategy**

Use Volume Drivers to maximize reach while selectively investing in Premium Winners to strengthen premium positioning and profitability.

**3. Position Hyderabad as an Innovation & Launch Market**

Use Hyderabad as a pilot environment for new menu launches, premium offerings and promotional campaigns before broader rollout.

### Portfolio Optimization

**4. Rationalize the Dormant Portfolio**

Review Dormant Core and Dormant Premium products for removal, redesign, repositioning or replacement.

**5. Optimize Menus Around Customer Demand**

Encourage focused menus built around proven products rather than continuous assortment expansion.

**6. Institutionalize Continuous Portfolio Management**

Use the Product Strategy framework as an ongoing management system, continuously monitoring and reclassifying products as customer demand changes.

### Market Expansion

**7. Replace National Standardization with Local Market Strategy**

Adapt menu composition, pricing and promotion to city-specific customer behavior.

**8. Expand Premium Where Demand Already Exists**

Prioritize premium expansion in cities and categories where customer engagement demonstrates willingness to support higher-value products.

### Operational Excellence

**9. Build Stronger Partnerships with Local Restaurant Leaders**

Use high-performing local restaurants as benchmarks and replicate successful practices where appropriate.

**10. Protect Customer Experience as a Competitive Advantage**

Maintain strong dining and delivery standards because the highest-engagement restaurants consistently demonstrate strong service quality.

The broader strategic conclusion is:

> **Zomato's growth opportunity is not simply to add more menu items. It is to manage the existing menu as a dynamic portfolio — continuously scaling winners, optimizing underperformers, selectively premiumizing, and adapting strategy to local demand.**

---

## 10 — Deliverables

The repository contains the complete analytical project, not only the final dashboard.

```text
zomato-menu-intelligence/
│
├── README.md
│
├── data/
│   └── README.txt
│
├── deliverables/
│   ├── dashboard_export.pdf
│   └── executive_action_plan.pdf
│
├── docs/
│   ├── analytical_methodology.md
│   ├── data_model.md
│   ├── dax_logic.md
│   ├── executive_recommendations.md
│   ├── qa_notes.md
│   ├── report_architecture.md
│   └── source_and_data.md
│
├── images/
│   ├── 00_title_card.png
│   ├── 01_project_hub.jpg
│   ├── 02_menu_portfolio.jpg
│   ├── 03_executive_action_plan.jpg
│   └── 04_segmentation_framework.jpg
│
└── powerbi/
    ├── README.md
    └── Zomato_Menu_Intelligence_Portfolio_Strategy.pbix
```

The repository separates the project into four layers:

**Data → Documentation → Visual Assets → Power BI Deliverable**

This keeps the repository useful both as a portfolio presentation and as a technical project record.

---

## 11 — Tools & Technologies

| Tool | Role |
|---|---|
| **Power BI** | Data modeling, DAX, analysis and dashboard development |
| **Power Query** | Data preparation and transformation |
| **DAX** | KPI logic, calculated columns and portfolio segmentation |
| **Git / GitHub** | Version control, project documentation and publication |
| **Kaggle** | Source dataset |

---

## 12 — Author

**Debanjan Biswas**  
Data Analyst | Excel | Power BI | SQL | Python

Email: bishwasdebanjan99@gmail.com  
LinkedIn: https://linkedin.com/in/biswas-debanjan-2ab011148

This project was developed as a practical analytics portfolio project focused on turning hands-on Power BI work into a business-oriented analytical solution.

---

## 13 — Project Perspective

The purpose of this project was to move beyond a conventional restaurant or menu dashboard.

The analysis connects **price positioning, customer engagement, product popularity, portfolio segmentation, cuisine intelligence, restaurant performance and city-level demand** into one decision-oriented framework.

The central idea is simple:

> **A menu should not be managed as a list of products. It should be managed as a portfolio.**

That means understanding where demand exists, identifying which products deserve investment, recognizing where premiumization is justified, and reducing attention on products that create complexity without meaningful customer engagement.

The resulting decision chain is:

**Understand customer demand → classify portfolio position → identify opportunity → prioritize action → continuously manage the portfolio.**

---

## License & Data Note

This repository contains the analytical model, documentation and project deliverables. The original Zomato dataset is not redistributed here.

Dataset source:

https://www.kaggle.com/datasets/narsingraogoud/zomato-restaurants-dataset-for-metropolitan-areas
