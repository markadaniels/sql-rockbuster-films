```sql
-- Top 10 cities derived from the top 10 countries
CREATE VIEW	top_10_cities_view AS
SELECT		ci.city,
		co.country,
		count(cu.customer_id) AS "Customer Count"
FROM		customer cu
JOIN		address ad
ON		cu.address_id = ad.address_id
JOIN		city ci
ON		ad.city_id = ci.city_id
JOIN		country co
ON		ci.country_id = co.country_id
WHERE		co.country IN (SELECT country FROM top_10_view)
GROUP BY	ci.city,
		co.country
ORDER BY	count(cu.customer_id) DESC
LIMIT 10;
