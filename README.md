# W3 Project - Building mySQL Data-base

![portada](https://github.com/Calbacho/w3-database-project/blob/main/videoclip2.jpg)

## ⛓️ Índice

1.[✍️ Descripción](#descripción)\
2.[🤓 Análisis general y limpieza](#análisis)\
3.[🗂️ Database](#database)\
4.[🧬 Transformación](#transformación)\
5.[📊 BONUS: Consultas](#consultas)


<a name="descripción"/>

## ✍️ Descripción

(Aquí introduciremos una descripción del proyecto.)

**Las tablas que tenemos inicialmente:**

<details>
<summary>FILM</summary>
<br>

 12 columnas describiendo los atributos más importantes de cada CD, desde el nombre de la película, hasta el lenguaje, el contenido adicional y los costes de alquiler.
 
![films](https://github.com/Calbacho/w3-database-project/blob/main/films.png)

</details>

<details>
<summary>ACTORS</summary>
<br>

ID del actor, nombres y apellidos de los actores.
<br>
<br>
![Actors](https://github.com/Calbacho/w3-database-project/blob/main/Actors.png)

</details>

<details>
<summary>CATEGORY</summary>
<br>

ID de categoria, nombre de categoria (comedia, aventura, romance)
<br>
<br>
![category](https://github.com/Calbacho/w3-database-project/blob/main/category.png)

</details>

<details>
<summary>INVENTORY</summary>
<br>

ID de inventario, ID de pelicula, ID Tienda
<br>
<br>
![inventory](https://github.com/Calbacho/w3-database-project/blob/main/inventory.png)

</details>

<details>
<summary>LANGUAGE</summary>
<br>

ID de lenguaje, nombre de lenguaje (Ingles, Italiano, etc)
<br>
<br>
![language](https://github.com/Calbacho/w3-database-project/blob/main/language.png)

</details>

<details>
<summary>OLD_HDD</summary>
<br>

Nombre y apellido de los actores, ID de inventario, titulos de peliculas donde aparece el respectivo actor o actriz
<br>
<br>
![oldhdd](https://github.com/Calbacho/w3-database-project/blob/main/oldhdd.png)

</details>

<details>
<summary>RENTAL</summary>
<br>

ID de alquiler, fecha de alquiler, fecha de retorno, ID de inventario, ID de cliente, ID del staff
<br>
<br>

![rental](https://github.com/Calbacho/w3-database-project/blob/main/rental.png)

</details>

 ### Objetivo:
 
El objetivo se basó en  hacer un analisis exploratorio y posterior limpieza para relacionar las tablas de la manera ideal para el funcionamiento del video club.
 
 
 <a name="análisis"/>
 
## 🤓 Análisis general y limpieza

En primer lugar hemos realizado un ejercicio analítico de cada uno de los siete CSV que nos han proporcionado utilizando las técnicas más comunes como son `.head`,`.tail`,`.info`, `.shape`, `.columns` y `.value_counts`  para obtener información general de cada CSV. El objetivo de esta tarea consiste en verificar que las columnas estén limpias, tengan sentido, y encontrar inconsistencias. Durante este proceso, encontramos las siguientes incongruencias:

<details>
<summary>¿ACTRIZ DUPLICADA?</summary>
<br>

 ![susan](https://github.com/Calbacho/w3-database-project/blob/main/Susandavis.png)

<br>
<br>



</details>

<details>
<summary>¿RELEASE DATE INCORRECTO?</summary>
<br>

Notamos que la columna **release_year**, la fecha de estreno de las películas, indica **2006** para todas las pelis.
<br>
Pero en las fechas de los alquileres: 
```
year = []
for i in ren.rental_date:
    year.append(i[0:4])
set(year) 
```
**2005**
<br>
<br>
Al ser todos los alquileres previos a 2006, concluimos que la columna **release_year** está incorrectamente introducida y por tanto la vaciamos.


</details>
<details>
<summary>¿FALTA UN RENTAL ID?</summary>
<br>

![susan](https://github.com/Calbacho/w3-database-project/blob/main/rental_head.png)
<br>

Como se puede observar, la diferencia entre **id** y **rental_id** pasa de ser **+1** al principio a **+2** al final, por lo que se intuye que se han saltado un rental_id.
<br>
 
 Para obtener dicho **rental_id**:
```
print(list(ren.rental_id[ren.index==ren.rental_id -1])[-1])
```
 **320**
```
print(list(ren.rental_id[ren.index==ren.rental_id -2])[0])
```
 **322**
 <br>
 <br>
... por lo que sabemos que **falta el rental_id nº 321**

<br>
<br>



</details>


**¿Qué películas tenemos?**


 <a name="database"/>
 
## 🗂️ Database

Descripción general

<details>
<summary>FILMS</summary>
<br>


<br>
<br>



</details>

<details>
<summary>INVENTORY</summary>
<br>


<br>
<br>



</details>

<details>
<summary>RENTAL</summary>
<br>


<br>
<br>



</details>

<details>
<summary>CUSTOMER</summary>
<br>


<br>
<br>



</details>

<img src="https://github.com/Calbacho/w3-database-project/blob/main/EERD_inicial.png" width="550" height="400" />

<a name="transformación"/>

## 🧬 Transformación

<details>
<summary>INVENTORY_MASTER</summary>
<br>
 
```
SELECT inventory.inventory_id AS 'INVENTORY ID', film_id AS 'FILM ID', store_id AS 'STORE ID', 
		CASE
        WHEN rental_date IS NOT NULL AND return_date = '' AND rental.inventory_id IS NOT NULL THEN 'NOT AVAILABLE'
        ELSE 'AVAILABLE'
    END AS AVAILABILITY

FROM inventory

LEFT JOIN rental ON rental.inventory_id = inventory.inventory_id
; 
 ```
 
<details>
<summary>Si alquilamos la película cuyo id de inventario es 1...</summary>
<br>
 
```
 INSERT INTO rental (rental_id, rental_date, inventory_id, customer_id, return_date, staff_id)
 
 VALUES (1002, '2005-05-31 00:55:00', 1, 588, '', 2);
  ```


</details>
 
![inventory_master](https://github.com/Calbacho/w3-database-project/blob/main/inventory_master.png)

</details>

<details>
<summary>RENTAL_MASTER</summary>
<br>

```
SELECT rental_id AS RENTALS, rental_date AS 'RENTAL DATE', rental.inventory_id AS 'INVENTORY ID', customer_id AS 'CUSTOMER ID', 
	   return_date AS 'RETURN DATE', staff_id AS 'STAFF ID', title as TITLE, 
       (DATEDIFF(return_date, rental_date) + 1) AS DAYS,
       (rental_rate * (DATEDIFF(return_date, rental_date) + 1)) AS INCOME
       
FROM rental
LEFT JOIN inventory ON inventory.inventory_id = rental.inventory_id
LEFT JOIN films ON inventory.film_id = films.film_id
; 
 ```
![rental_master](https://github.com/Calbacho/w3-database-project/blob/main/rental_master.png)
 
</details>

<details>
<summary>CUSTOMER_MASTER</summary>
<br>
 
 ```
SELECT customer.customer_id AS 'CUSTOMER ID', name AS 'NAME', lastname AS 'LAST NAME', telephone AS TELEPHONE, 
	   mail AS EMAIL, round(sum((rental_rate * (DATEDIFF(return_date, rental_date) + 1))), 2) AS 'TOTAL SPENT',
       GROUP_CONCAT(' ',title) AS 'FILMS RENTED'
       
FROM rental

LEFT JOIN inventory ON inventory.inventory_id = rental.inventory_id
LEFT JOIN films ON inventory.film_id = films.film_id
LEFT JOIN customer ON customer.customer_id = rental.customer_id

GROUP BY customer.customer_id, name , lastname, telephone, mail
;
 ```


</details>


<a name="consultas"/>

## 📊 BONUS: Consultas

<details>
<summary>LOS CLIENTES QUE MÁS ALQUILAN</summary>
<br>

 ```
SELECT  rental.customer_id, count(rental.customer_id) as Rentals
FROM rental
 
LEFT JOIN customer ON rental.customer_id = customer.customer_id
 
GROUP BY rental.customer_id
 
ORDER BY Rentals desc
LIMIT 5
 ```

</details>

<details>
<summary>LOS CLIENTES QUE MÁS GASTAN</summary>
<br>

```
SELECT  `customer id`, round(sum(Income),2) as 'Total Spent'
FROM rental_master
 
GROUP BY `customer id`
 
ORDER BY 'Total Spent' desc
LIMIT 5 
 ```

<br>
<br>



</details>

<details>
<summary>LAS PELÍCULAS QUE MÁS SE ALQUILAN</summary>
<br>

```
SELECT  title, count(title) as Alquileres
FROM rental_master
 
GROUP BY title
 
ORDER BY Alquileres DESC
LIMIT 5
 ```

<br>
<br>



</details>
