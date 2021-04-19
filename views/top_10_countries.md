```sql
-- Top 10 countries with the highest number of customers
CREATE VIEW	top_10_view AS
SELECT		co.country,
                count(cu.customer_id) AS "Customer Count"
FROM		customer cu
JOIN		address ad
ON		cu.address_id = ad.address_id
JOIN		city ci 
ON		ad.city_id = ci.city_id
JOIN		country co 
ON		ci.country_id = co.country_id
GROUP BY	co.country
ORDER BY	count(cu.customer_id) DESC
LIMIT 10;
```
