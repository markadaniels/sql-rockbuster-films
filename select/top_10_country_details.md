```sql
-- Top 10 country details derived from the top 10 view
SELECT		first_name,
		last_name,
		city,
		Country,
		title AS "film title",
		release_year,
		amount AS Paid,
		rental_rate,
		rental_duration,
		length,
		replacement_cost
FROM 		customer AS C
INNER JOIN	rental AS R
ON		C.customer_id = R.customer_id
INNER JOIN	payment AS P
ON		R.rental_id = P.rental_id
INNER JOIN	inventory AS I
ON		R.inventory_id = I.inventory_id
INNER JOIN	film AS F
ON		I.film_id = F.film_id
INNER JOIN	address AS A
ON		C.address_id = A.address_id
INNER JOIN	city AS CI
ON		A.city_id = CI.city_id
INNER JOIN	country AS CO
ON		CI.country_id = CO.country_id
WHERE		CO.country IN(SELECT country FROM top_10_view)
GROUP BY	first_name,
		last_name,
		city,
		Country,
		title,
		release_year,
		amount,
		rental_rate,
		rental_duration,
		length,
		replacement_cost
ORDER BY	Paid DESC
```
