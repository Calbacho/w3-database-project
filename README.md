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


<br>
<br>



</details>
<details>
<summary>¿FALTA UN RENTAL ID?</summary>
<br>


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

**PANTALLAZO**


<a name="transformación"/>

## 🧬 Transformación

<details>
<summary>INVENTORY_MASTER</summary>
<br>


<br>
<br>



</details>

<details>
<summary>RENTAL_MASTER</summary>
<br>


<br>
<br>



</details>

<details>
<summary>CUSTOMER_MASTER</summary>
<br>


<br>
<br>



</details>


<a name="consultas"/>

## 📊 BONUS: Consultas

- Top 3 clientes
- Top 3 películas alquiladas
- Algo con el tiempo que tardan en devolver las pelis
