-- select * from adjust_formatted_tbl  where campaign_id is   null  --- checks nulls -means 'expired attribution'

select * 
  from adjust_table_2026 
where campagin_id = '120225650510640689'

create or replace VIEW adjust_table_2026 as (
 with adj_table AS (
    SELECT
        date,
        EXTRACT(MONTH FROM "date")::int AS month,
        EXTRACT(YEAR FROM "date")::int AS year,
        campaign,
        substring(campaign from '[(]([0-9]+)[)]') AS campaign_id,
        adset, 
        substring(adset from '[(]([0-9]+)[)]') AS adset_id,
        ad,
        substring(ad from '[(]([0-9]+)[)]') AS ad_id,
        CASE WHEN country ='U.S' then 'United States' 
              WHEN country ='U.S.' then 'United States' 
              WHEN country ='US' then 'United States' 
              WHEN country ='AU' then 'Australia' 
              WHEN country ='CA' then 'Canada' else country END AS country_norm,
        os,
        partner,
        sum(spend) AS total_spend,
        sum(impressions) AS total_impressions,
        sum(clicks) AS total_clicks,
        sum(installs) AS total_installs,
        sum(purchases) AS total_purchases,
        sum(purchase_revenue) AS purchase_revenue,
        sum(d0_purchase_revenue) AS day_0,
        -- NULLIF(sum(spend),0)/NULLIF(sum(d0_purchase_revenue),0) AS roas_day_0,
        sum(d30_purchase_revenue) AS day_30
        -- NULLIF(sum(spend),0)/NULLIF(sum(d30_purchase_revenue),0) AS roas_day_30,
        
  FROM adjust_raw_data
    GROUP BY 1, 2, 3, 4, 5, 6, 7, 8, 9,10,11,12) 
    select * from adj_table
    WHERE CAMPAIGN_ID IS NOT NULL
)
