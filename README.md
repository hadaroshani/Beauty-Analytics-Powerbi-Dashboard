# Beauty-Analytics-Powerbi-Dashboard
Power BI + Power Query + DAX project segmenting 8,000+ Sephora products into Prestige/Niche category to analyze pricing and rating patterns across beauty categories.

Sephora Beauty Category Dashboard

Prestige vs. Niche/Mass brand performance, built in Power BI

What this is

I built this dashboard to explore something that comes up constantly in beauty retail: brands get sorted into "Prestige" and "Niche/Mass" tiers, and that label shapes pricing, marketing spend, and growth targets. I wanted to know whether that price gap is actually backed up by better customer sentiment, or whether it's mostly positioning.

I used Sephora's product catalog on Kaggle for this — partly because the category structure (fragrance, makeup, skincare) and the idea of "brand clusters" closely matches how companies like Puig actually talk about their portfolios in consumer insights roles.

What I found

Prestige products average $86.99 vs. $41.83 for Niche/Mass, which is more than double the price. But average ratings are almost identical: 4.23 vs. 4.19 out of 5.

So the price premium doesn't seem to track with how much customers actually like the products. It looks more like a brand equity thing than a quality thing.

Show Image

How I built it

Cleaning the data (Power Query)
Sephora's raw export had 27 columns, most of which I didn't need, like ingredient lists, variation/bundle fields, that kind of thing. I stripped those out. About 278 products had no rating or review count. I left those as blank rather than deleting them or filling in a guess, since a missing rating usually just means a product is new and hasn't been reviewed yet — not that something's wrong. Power BI's AVERAGE() function skips blanks automatically, so it didn't need any extra handling. I also found one row where the data had gotten shifted across columns (a real corrupted record, not a "missing value" situation) and removed it.

Building the Prestige/Niche tier myself
This part wasn't in the original data at all — Sephora doesn't label brands by tier. I put together a list of about 49 well-known Prestige/luxury brands (Chanel, Dior, Charlotte Tilbury, YSL, etc.) based on general industry knowledge — legacy fashion houses, long-standing luxury positioning — and everything else defaulted to Niche/Mass. I merged that list into the main product table with a left join, so every product kept its row even if its brand wasn't on my list.

I ran into a genuinely useful bug here: my first chart came back completely blank. Turned out I was pulling one field from my original lookup table and a measure from the main product table — two tables that weren't actually connected in the data model, even though the data looked related. Fixed it by using the merged version of the column that lived inside the main table instead. Small thing, but it taught me more about how Power BI relationships actually work than any tutorial would have.

The measures and visuals
Standard DAX — average rating, average price, total products, total reviews — plus a comparison bar chart, a donut showing the tier split (78% Niche/Mass, 22% Prestige), a detail table breaking everything down by category, and slicers so you can filter by category or tier.

Tools

Power BI Desktop, Power Query, DAX

What's next

I'd like to go back and expand the brand list beyond my initial 49. I built it as a first pass and expect I missed a few. I'm also working on a second project using a time-series retail dataset (returns, customer value, seasonality) to round out my portfolio with skills that apply beyond beauty specifically.
