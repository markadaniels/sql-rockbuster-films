```sql
-- Top 5 customer details derived from the top 5 customers view (see the "views" folder)
SELECT		C.first_name,
		C.last_name,
	 	CI.city,
 		CO.Country,
	 	F.title AS "film title",
 		F.release_year,
		P.amount AS Paid,
 		F.rental_rate,
	 	F.rental_duration,
 		F.length,
 		F.replacement_cost
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
WHERE		C.customer_id IN (SELECT customer_id FROM top_5_customers_view)
GROUP BY	C.first_name,
		C.last_name,
 		CI.city,
 		CO.Country,
 		F.title,
 		F.release_year,
		P.amount,
 		F.rental_rate,
 		F.rental_duration,
 		F.length,
 		F.replacement_cost
ORDER BY	Paid DESC
```
