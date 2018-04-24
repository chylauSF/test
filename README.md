```sql
Limit (cost=67735.94..67735.94)
  Sort (cost=67735.94..67735.95)
  Sort Key: po.start_ship_on
    Nested Loop Left Join (cost=5.12..67735.93)
    Filter: ((NOT bd.marked_as_rtv) OR (bd.marked_as_rtv IS NULL))
      Nested Loop (cost=0.71..6.17)
        Index Scan using index_merch_buys_on_style_variant_id on merch_buys mb (cost=0.42..3.64)
        Index Cond: (style_variant_id = 87623)
        Filter: ((cancelled_at IS NULL) AND (closed_at IS NULL))
        Index Scan using purchase_orders_pkey on purchase_orders po (cost=0.29..2.51 rows=1 width=8)
        Index Cond: (id = mb.purchase_order_id)
        Filter: ((cancelled_at IS NULL) AND (closed_at IS NULL))
      Hash Join (cost=4.41..67729.71)
      Hash Cond: (bd.buy_hizzy_allocation_id = bha.id)
        Seq Scan on buy_deliveries bd (cost=0.00..65092.82)
        Hash (cost=4.36..4.36)
        Buckets: 1024
          Index Scan using index_buy_hizzy_allocations_on_merch_buy_id_and_hizzy_id on buy_hizzy_allocations bha  (cost=0.42..4.36)
          Index Cond: (merch_buy_id = mb.id)
```
