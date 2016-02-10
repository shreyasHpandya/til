# Avoid Division by Zero with `nullif`

Instead of using `if` one can use `nullif`

For example instead of

```SQL
select id, IF(rating_count = 0, null, rating_sum / rating_count) as average_rating
from document where id in (123);
```

we can use 

```SQL
select id, rating_sum / nullif(rating_count, 0) as average_rating
from document where id = 123;
```
