```sql
-- Top top 5 customers derived from the top 10 cities
CREATE VIEW	top_5_customers_view AS
SELECT		cu.customer_id,
		cu.first_name,
		cu.last_name,
		ci.city,
		co.country,
		sum(pa.amount) AS "Total Amount Paid"
FROM		customer cu
JOIN		address ad 
ON		cu.address_id = ad.address_id
JOIN		city ci
ON		ad.city_id = ci.city_id
JOIN		country co 
ON		ci.country_id = co.country_id
JOIN		payment pa 
ON		cu.customer_id = pa.customer_id
WHERE		ci.city IN (SELECT city FROM top_10_cities_view)
GROUP BY	cu.customer_id, 
		cu.first_name,
		cu.last_name,
		ci.city, 
		co.country
ORDER BY	sum(pa.amount) DESC
LIMIT 5;
```
