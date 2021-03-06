# Mutants API!

Esta API esta diseñada para clasificar un código ADN humano y uno mutante, además de generar estadísticas de los ADNs que va descubriendo.

El API se desarrolló en **NodeJS** version > 10.16.0 usando el framework **Express**, además está conectada a una base de datos NoSQL **MongoDB**, ejecutada como servicio en cloud desde **MongoDB Atlas**. 
  
A continuación se describen los métodos implementados:

**POST** /mutants
	Headers: `Content-type: application/json`
	Body: `{
    "dna": [
        "ATGCGA",
        "CAGTGC",
        "AGAAAA",
        "TTAGGT",
        "TCACTG",
        "CCCCTA"
    ]
}`
Responses:	
 - HTTP Code: **200** - OK (Es **Mutante**)
 - HTTP Code: **403** - Forbidden (Es **Humano**)
 - HTTP Code: **400** - Bad Request (No se envió una cadena de ADN **válida**)

**GET** /stats
Response:
 - HTTP Code: 200 - OK `{"count_mutant_dna":  40,"count_human_dna":  100,"ratio":  0.4}` 

## Configuración de Ambiente

 Crear archivo `.env` en la raíz del proyecto, guiarse del template `.env-example`. Allí se debe configurar el **DB_URL** que es el endpoint del cluster de **MongoDB Atlas**. Existen 3 bases de datos predefinidas (development, production y test), que la aplicación apuntará automáticamente según el modo de ejecución **NODE_ENV** (prod o dev) o durante los Test Automáticos. Por último configurar el **DB_USER** y **DB_PASS** (usuario y password de base de datos).

## Ejecución para Development

 1. Realizar la instalación de los módulos `npm install`.
 2. Ejecutar la aplicación `npm start`.
 3. Realizar los request al endpoint `localhost:3000`.

## Ejecución de Tests

Los **tests automáticos** se desarrollaron con las bibliotecas **Jest** y **Supertest** donde se realizaron diferentes test de los métodos expuestos en la **API**, logrando un **coverage** > 93%.

 Ejecutar el test `npm test`, la respuesta arroja en consola los resultados de los tests y del coverage. También en la **carpeta coverage** se pueden ver los resultados de los mismos.
