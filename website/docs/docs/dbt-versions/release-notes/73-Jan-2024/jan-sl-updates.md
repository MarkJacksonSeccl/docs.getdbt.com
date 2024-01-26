---
title: "dbt Semantic Layer updates and fixes for January 2024"
description: "January 2024: New Exports feature, Conversion Metrics, Enhanced metrics labels, Support for shorthand to create metrics and Tableau Parameter filters, and bug fixes."
sidebar_label: "Update and fixes: dbt Semantic Layer"
sidebar_position: 08
date: 2024-01-31
---
The dbt Labs team continues to work on adding new features, fixing bugs, and increasing reliability for the [dbt Semantic Layer](/docs/use-dbt-semantic-layer/dbt-sl).

The following list explains the new features, updates, and fixes for January 2024 in more detail.

## New features

- **Introducing Conversion metrics** &mdash; This new metric type allows you to measure conversion events easily. For example, users who viewed a web page and then filled out a form. You can learn more about [conversion metrics in our docs](/docs/build/conversion).
- **Introducing Exports** &mdash; Use Exports to materialize saved queries within the data platform on a schedule. It uses the dbt Cloud job scheduler to execute saved queries for reliable and fast data reporting.
- **Simplified dimension resolution** &mdash; Instead of specifying the fully qualified dimension name (for example, `order__user__country`) in the group by or filter expression, you now only need to provide the primary entity and dimensions name, like `user__county`.
- **Query saved queries** &mdash; You can now query the [saved queries](/docs/build/saved-queries) you've defined in the dbt Semantic Layer in GraphQL, JDBC, and the [dbt Cloud CLI](/docs/cloud/cloud-cli-installation).

## Updates

- **Display `label` for dbt Semantic Layer metrics** &mdash; The YAML spec parameter `label` is now available for Semantic Layer metrics in [JDBC and GraphQL APIs](/docs/dbt-cloud-apis/sl-api-overview). This means you can conveniently use `label` as a display name for your metrics when exposing them.
- **Use shorthand to create metrics** &mdash; Added support for `create_metric=true` for a measure, which is a shorthand to quickly create metrics. This is especially useful in cases when metrics are only used to build other metrics.
- **Support for Tableau Parameter filters** &mdash; Added support for Tableau Parameter filters. You can use [our Tableau connector](docs/use-dbt-semantic-layer/tableau) to create and use parameters with your dbt Semantic Layer data.
- **Additional parameters for GraphQL API** &mdash;  Added support to expose `expr` and `agg` for [Measures](/docs/build/measures) in the [GraphQL API](/docs/dbt-cloud-apis/sl-graphql).
- **Improved error messages** &mdash; When querying a dimension that is not reachable for a given metric, you now have improved error messages returned in the command line interface.

## Bug fixes

- **BigQuery numeric types** &mdash; Numeric types with precision greater than 38 (like `BIGDECIMAL`) in BigQuery are now supported and accepted. Previously, it was unsupported and would return an error.
- **Support for scientific notation** &mdash; Scientific notation for large numbers is displayed and correctly interpreted. Previously, they were unsupported. 
- **Google Sheets dimension values** &mdash; Dimension values are now accurately preserved instead of being inadvertently converted into strings. Previously, dimension values were incorrectly converted into a string.  
- **Multiple derived metrics resolution** &mdash; Resolved issues with naming collisions in queries involving multiple derived metrics using the same metric input. Previously, this could cause a naming collision. Input metrics are now deduplicated, ensuring each is referenced only once.
- **Deduplication of input measures** &mdash; Resolve warnings related to using 2 duplicate input measures in a derived metric. Previously, this would trigger a warning. Input measures are now deduplicated, enhancing query processing and clarity.