# 
Please use in this order

1. data cleanse and investigation
2. basic groupping
3. meta_view_2026
4. adjust_table_2026 - this is a view of adjust data, same transformations 
5. union_tables - a union at campaign_id level
6. python_testing_only - python script with the same transformations, mapping country table, join on campaign_id, removal of adwords, matching spend and revenue rows for meta, and the 3 countries
