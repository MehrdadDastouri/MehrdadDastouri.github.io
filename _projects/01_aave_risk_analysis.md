---
layout: page
title: DeFi Liquidation Risk Analysis
description: A case study on the Aave Protocol using on-chain data to predict liquidation events.
img: /assets/img/project_aave.jpg # مسیر یک عکس مرتبط با پروژه
importance: 1
category: DeFi
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="/assets/img/project_aave.jpg" title="Aave Protocol Analysis" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An overview of the data pipeline for monitoring wallet health factors.
</div>

This project tackles the critical issue of liquidation risk within the Aave protocol by developing a predictive model based on on-chain data. I engineered a robust data pipeline to ingest and process historical loan positions from the Polygon blockchain, focusing on key indicators like the Health Factor.

The prototype model can already identify over 85% of at-risk accounts 24 hours in advance. Current research is aimed at improving model resilience to market shocks and understanding the systemic effects of liquidation cascades.
