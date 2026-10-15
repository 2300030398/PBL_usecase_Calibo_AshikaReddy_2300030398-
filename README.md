# Retail Category Intelligence

Retail Product Performance: Exploratory Data Analysis

A team project from Calibo AI Academy (MUC01, Group 14, January to June 2026). It turns six months of retail transaction data into evidence that a Category Manager can use for shelf-space, discount and promotion decisions.

## Team

| Member | Focus area |
|---|---|
| G. Akash | ETL and data validation |
| M.V. Ashika Reddy | Product and discount analysis |
| A. Manish | Sales timing and trends |
| Rendla Pavithra | Business insights and final presentation |

## Business Problem

**Situation:** A regional 12-store retail chain is preparing for a quarterly supplier review across five categories: Electronics, Apparel, Grocery, Home and Kitchen, and Personal Care. The Category Manager needs evidence for shelf-space and promotional decisions.

**Complication:** The manager has to tell growing, stable and declining categories apart, and find the products that drive or drag each category, before suppliers present their cases.

**Business question:** Which categories are growing or declining? Which products drive or drag each category? Are discounts associated with higher revenue per transaction? When should promotions be timed?

**Success definition:** A defensible category priority, a product and supplier challenge backed by revenue, a discount finding backed by numbers, a promotion timing signal, and a clear statement of limitations.

## Dataset

The supplied MUC01 retail sales transaction dataset, covering January to June 2026. It is the single source of data for the whole analysis.

## Analysis Workflow

```
Business Problem -> ETL and Validation -> Category / Product / Discount / Timing Analysis -> Business Insights
```

1. **Extract:** Inspect the structure of the transaction data.
2. **Transform:** Clean and standardize the data.
3. **Validate:** Check data quality before any analysis begins.
4. **Analyze:** Study categories, products, discounts and timing.
5. **Interpret:** Combine the findings into a business recommendation.

## My Contribution: Product and Discount Analysis

My part of the project moves from category totals to the products driving revenue, and then looks at how discount levels relate to revenue per transaction.

### Product Contribution Across Categories

Revenue by selected products over six months (in millions of rupees):

| Category | Product | Revenue (INR M) |
|---|---|---|
| Electronics | Headphones | 47.70 |
| Electronics | Laptop | 46.55 |
| Electronics | Smart TV | 41.88 |
| Apparel | Saree | 14.16 |
| Apparel | T-Shirt | 14.10 |
| Apparel | Kurta | 13.61 |
| Home and Kitchen | Mixer Grinder | 16.90 |
| Home and Kitchen | Storage Box | 16.68 |
| Home and Kitchen | Water Bottle | 15.83 |
| Grocery | Rice | 8.56 |
| Grocery | Dal | 8.49 |
| Grocery | Sugar | 8.38 |
| Personal Care | Shampoo | 8.17 |
| Personal Care | Body Lotion | 8.11 |
| Personal Care | Sunscreen | 7.59 |

Key observations:

- **Electronics leads:** Headphones are the top product at INR 47.70M, followed closely by Laptop at INR 46.55M.
- **Apparel is close:** Saree (INR 14.16M) and T-Shirt (INR 14.10M) perform almost the same, so growth does not depend on one hero product.
- **Gaps vary by category:** Product-level differences appear in every category, so products within a category do not perform equally.

### Discount Pattern

Average revenue per transaction at each discount level:

| Discount | Average revenue per transaction |
|---|---|
| 0% | INR 4,686 |
| 5% | INR 4,304 |
| 10% | INR 4,006 |
| 15% | INR 4,069 |
| 20% | INR 3,632 |

- Average revenue per transaction fell by about 22.5% from the 0% to the 20% discount level.
- Average units sold stayed almost the same (2.59 at 0%, 2.58 at 20%).
- No transactions had a discount of 25% or more.
- This is an observed relationship, not proof that discounts caused the difference.

## Team Findings

### Category Performance

| Category | Signal |
|---|---|
| Apparel | Revenue up 34.10% from January to June |
| Electronics | 49.27% of total revenue, but revenue down 35.02% from January to June |

Category share and category movement answer different questions: scale versus direction. Electronics has scale but is declining, while Apparel shows strong growth.

### Product Leaders and Laggards (six-month revenue)

| Category | Strongest product | Weakest product |
|---|---|---|
| Electronics | Headphones, INR 47.70M | Smart TV, INR 41.88M |
| Apparel | Saree, INR 14.16M | Kurta, INR 13.61M |
| Grocery | Rice, INR 8.56M | Sugar, INR 8.38M |
| Home and Kitchen | Mixer Grinder, INR 16.90M | Water Bottle, INR 15.83M |
| Personal Care | Shampoo, INR 8.17M | Sunscreen, INR 7.59M |

Apparel's product spread is tight, so its growth is not tied to one product. Electronics has more value concentrated in a few products, and all five Electronics products move down from January to June, which points to category-level pressure rather than one isolated weak product.

### Sales Timing

- **Strongest weekday:** Saturday (highest average daily revenue).
- **Weakest weekday:** Tuesday (lowest average daily revenue).
- **Strongest month:** January.
- **Weakest month:** June, when Electronics also showed a noticeable decline.

## Recommendations for the Category Manager

1. Test controlled promotions in Apparel.
2. Review why Electronics declined, especially Smart TV performance.
3. Test whether deeper discounts create additional demand before using them more widely.
4. Use Saturday as a key day for promotion experiments.

## Limitations

- The findings are observed patterns that support planning discussions. They do not establish causation.
- Before making final profitability decisions, the analysis should be extended with product cost, profit margin, inventory, stock-outs and promotion exposure.

## Conclusion

Apparel is moving in a positive direction, Electronics needs closer attention, discounts need careful testing, and Saturday is a useful signal for promotion timing. The evidence chain runs from a reliable data foundation, to product and discount detail, to timing context, to a clear business interpretation.

## Author

**M.V. Ashika Reddy**
Calibo AI Academy, Group 14 (MUC01)
Email: ashikareddymajjiga@gmail.com
