# DataProject: Lógica. Consultas de SQL
Proyecto 2 - Curso Data Analytics V3

En este proyecto se aplican los conocimientos aprendidos en el módulo "SQL".   
las consultas siguientes se hacen a traves de Dbeaver.

## Estructora del repositorio ##

```bash 
|
|___BBDD_SQL_proyecto2
|    |___BBDD_Proyecto #archivo BBDD SQL
|    |___Diagram_Proyecto_BBDD #imagen.png del diagrama 
|    |___EnunciadoDataProject_SQL.Lógica #lista de consultas a realizar
|    |___README
|   


```

## Consultas ##

**1. Crea el esquema de la BBDD**  

![Diagrama BBDD](Diagram_Proyecto_BBDD.png)



 **2. Muestra los nombres de todas las películas con una clasificación por 
edades de ‘Rʼ**

``` 
SELECT "title",
        "rating"
FROM "film" 
WHERE "rating" = 'R';
```

 **3. Encuentra los nombres de los actores que tengan un “actor_idˮ entre 30 
y 40** 
```
SELECT concat(first_name,' ',last_name )
FROM actor 
WHERE actor_id <= 40 AND actor_id >= 30;
```



 **4. Obtén las películas cuyo idioma coincide con el idioma original**  

Todos los valores de la columna original_language_id son nulos por lo cual no se muestra ningun resultado.

```SELECT title 
FROM film 
WHERE language_id = original_language_id AND original_language_id IS NOT NULL ;`
```


**5. Ordena las películas por duración de forma ascendente**  
```
SELECT  * 
FROM film 
ORDER BY length ASC ;
```

 **6. Encuentra el nombre y apellido de los actores que tengan ‘Allenʼ en su 
apellido**


```
SELECT first_name , last_name 
FROM actor 
WHERE last_name ILIKE 'Allen'
```




**7. Encuentra la cantidad total de películas en cada clasificación de la tabla 
“filmˮ y muestra la clasificación junto con el recuento**

```
SELECT rating, COUNT(*) AS total_peliculas
FROM film
GROUP BY rating
```

 **8. Encuentra el título de todas las películas que son ‘PG-13ʼ o tienen una 
duración mayor a 3 horas en la tabla film**

```
SELECT *
FROM film 
WHERE rating = 'PG-13' OR length > 180
;
```


 **9. Encuentra la variabilidad de lo que costaría reemplazar las películas**

```
SELECT VAR_SAMP(replacement_cost)  AS variabilidad
FROM film 
```

 **10. Encuentra la mayor y menor duración de una película de nuestra BBDD**

```
SELECT max(length ) AS mayor_duracion, min(length ) AS menor_duracion
FROM film ;
```

 **11. Encuentra lo que costó el antepenúltimo alquiler ordenado por día**  

```
SELECT amount  
FROM payment 
ORDER BY payment_date DESC 
LIMIT 1 OFFSET 1;
```


**12. Encuentra el título de las películas en la tabla “filmˮ que no sean ni ‘NC-
 17ʼ ni ‘Gʼ en cuanto a su clasificación**

```
SELECT title 
FROM film   
WHERE rating NOT IN('NC-17','G');
```

**13. Encuentra el promedio de duración de las películas para cada 
clasificación de la tabla film y muestra la clasificación junto con el 
promedio de duración**

``` 
SELECT rating, 
    AVG(length ) AS "promedio_duracion_peliculas"
FROM film 
GROUP BY rating ;
```



 **14. Encuentra el título de todas las películas que tengan una duración mayor 
a 180 minutos**

```
SELECT title 
FROM film 
WHERE length >= '180';

```   


**15. ¿Cuánto dinero ha generado en total la empresa?**

```
SELECT SUM(amount ) AS "total_ingresos"
FROM payment  ;

```




**16. Muestra los 10 clientes con mayor valor de id**

``` 
SELECT customer_id , first_name , last_name 
FROM customer 
ORDER BY customer_id DESC
    LIMIT 10;

```

 **17. Encuentra el nombre y apellido de los actores que aparecen en la 
película con título ‘Egg Igbyʼ**

```
SELECT first_name , last_name 
FROM actor  AS a
INNER JOIN film_actor  AS fa ON a.actor_id = fa.actor_id
INNER JOIN film AS f ON fa.film_id = f.film_id 
WHERE f.title ILIKE 'egg igby';

```


**18. Selecciona todos los nombres de las películas únicos** 

```
SELECT DISTINCT title 
FROM film;
```


**19. Encuentra el título de las películas que son comedias y tienen una 
duración mayor a 180 minutos en la tabla “filmˮ**

```
SELECT title 
FROM film AS f 
INNER JOIN film_category AS fc ON f.film_id = fc.film_id
INNER JOIN category AS c ON c.category_id = fc.category_id
WHERE f.length >= 180 AND c."name" ILIKE 'comedy';
```  


**20. Encuentra las categorías de películas que tienen un promedio de duración superior a 110 minutos y muestra el nombre de la categoría junto con el promedio de duración**  

``` 
SELECT c.name AS categoria, ROUND(AVG(f.length),2) AS promedio_duracion
FROM film f
JOIN film_category fc ON f.film_id = fc.film_id
JOIN category c ON fc.category_id = c.category_id
GROUP BY c.name
HAVING ROUND(AVG(f.length ), 2) > 110;

```

**21. ¿Cuál es la media de duración del alquiler de las películas?**

```

SELECT AVG((return_date - rental_date)) AS duracion_media_alquiler
FROM rental ;
```



**21. Crea una columna con el nombre y apellidos de todos los actores y 
actrices**

```
SELECT concat(first_name , ' ', last_name )
FROM actor 
ORDER BY last_name ASC ;
```


**22. Números de alquiler por día, ordenados por cantidad de alquiler de 
forma descendente**

```
SELECT CAST(rental_date AS DATE) AS fecha_alquiler, COUNT(rental_id) AS cantidad_alquiler_dia
FROM rental 
GROUP BY CAST(rental_date AS DATE)
ORDER BY cantidad_alquiler_dia DESC;
```

 **23. Encuentra las películas con una duración superior al promedio**

 ``` 
 SELECT *
FROM film 
WHERE length > (SELECT AVG(length)
                FROM film) ;
```


**24. Averigua el número de alquileres registrados por mes**


**25. Encuentra el promedio, la desviación estándar y varianza del total 
pagado**


  ¿Qué películas se alquilan por encima del precio medio?
 Muestra el id de los actores que hayan participado en más de 40 
películas.
 Obtener todas las películas y, si están disponibles en el inventario, 
mostrar la cantidad disponible.
 Obtener los actores y el número de películas en las que ha actuado.
 Obtener todas las películas y mostrar los actores que han actuado en 
ellas, incluso si algunas películas no tienen actores asociados.
 Obtener todos los actores y mostrar las películas en las que han 
actuado, incluso si algunos actores no han actuado en ninguna película.
 Obtener todas las películas que tenemos y todos los registros de 
alquiler.
  Encuentra los 5 clientes que más dinero se hayan gastado con nosotros.
  Selecciona todos los actores cuyo primer nombre es 'Johnny'.
  Renombra la columna “first_nameˮ como Nombre y “last_nameˮ como 
Apellido.
 Encuentra el ID del actor más bajo y más alto en la tabla actor.
 Cuenta cuántos actores hay en la tabla “actorˮ.
  Selecciona todos los actores y ordénalos por apellido en orden 
ascendente.
  Selecciona las primeras 5 películas de la tabla “filmˮ.
 Agrupa los actores por su nombre y cuenta cuántos actores tienen el 
mismo nombre. ¿Cuál es el nombre más repetido?
  Encuentra todos los alquileres y los nombres de los clientes que los 
realizaron.
 Muestra todos los clientes y sus alquileres si existen, incluyendo 
aquellos que no tienen alquileres.
  Realiza un CROSS JOIN entre las tablas film y category. ¿Aporta valor 
esta consulta? ¿Por qué? Deja después de la consulta la contestación.
  Encuentra los actores que han participado en películas de la categoría 
'Action'.
  Encuentra todos los actores que no han participado en películas.
  Selecciona el nombre de los actores y la cantidad de películas en las 
que han participado.
 Crea una vista llamada “actor_num_peliculasˮ que muestre los nombres 
de los actores y el número de películas en las que han participado.
 Calcula el número total de alquileres realizados por cada cliente.
 Calcula la duración total de las películas en la categoría 'Action'.
 Crea una tabla temporal llamada “cliente_rentas_temporalˮ para 
almacenar el total de alquileres por cliente.
 Crea una tabla temporal llamada “peliculas_alquiladasˮ que almacene las 
películas que han sido alquiladas al menos 10 veces.
  Encuentra el título de las películas que han sido alquiladas por el cliente 
con el nombre ‘Tammy Sandersʼ y que aún no se han devuelto. Ordena 
los resultados alfabéticamente por título de película.
  Encuentra los nombres de los actores que han actuado en al menos una 
película que pertenece a la categoría ‘Sci-Fiʼ. Ordena los resultados 
alfabéticamente por apellido
 Encuentra el nombre y apellido de los actores que han actuado en 
películas que se alquilaron después de que la película ‘Spartacus 
Cheaperʼ se alquilara por primera vez. Ordena los resultados 
alfabéticamente por apellido.
  Encuentra el nombre y apellido de los actores que no han actuado en 
ninguna película de la categoría ‘Musicʼ.
  Encuentra el título de todas las películas que fueron alquiladas por más 
de 8 días.
  Encuentra el título de todas las películas que son de la misma categoría 
que ‘Animationʼ.
  Encuentra los nombres de las películas que tienen la misma duración 
que la película con el título ‘Dancing Feverʼ. Ordena los resultados 
alfabéticamente por título de película.
  Encuentra los nombres de los clientes que han alquilado al menos 7 
películas distintas. Ordena los resultados alfabéticamente por apellido.
  Encuentra la cantidad total de películas alquiladas por categoría y 
muestra el nombre de la categoría junto con el recuento de alquileres.
  Encuentra el número de películas por categoría estrenadas en 2006.
 Obtén todas las combinaciones posibles de trabajadores con las tiendas 
que tenemos.
  Encuentra la cantidad total de películas alquiladas por cada cliente y 
muestra el ID del cliente, su nombre y apellido junto con la cantidad de 
películas alquiladas