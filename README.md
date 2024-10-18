# Limpieza y consolidado de dos datasets

# Índice

1. [Configuración del proyecto y ejecución](#configuración-del-proyecto-y-ejecución)
2. [Limpieza de datos](#limpieza-de-datos)
3. [EDA (Análisis exploratorio de datos)](#eda-análisis-exploratorio-de-datos)
1. [Consolidado de los datasets](#consolidado-de-los-datasets)

## Configuración del proyecto y ejecución

Comenzamos creando un entorno virtual de trabajo utilizando los siguientes comandos:

- py -m venv venv | Otras opciones en lugar de py pueden ser python o python3.

Activamos el entorno con uno de estos tres comandos:

- source venv/Scripts/activate

Por último instalamos las librerías necesarias para el proyecto usando los comandos:
- pip install pandas
- pip install matplotlib
- pip install seaborn

## Limpieza de datos

1) Cargamos los dos datasets: 

- booking.csv
- propiedades.csv

2) Inspeccionamos la estructura general de los datasets, número de variables y filas, tipos de datos y hacemos resúmenes estadísticos de las variables numéricas para encontrar posibles discrepancias que más adelante verificaremos.

3) Revisamos valores nulos y duplicados. 

4) Estandarizamos el tipo de dato de las variables que contenían fechas a datetime. Las variables estandarizadas fueron: BookingCreatedDate, ArrivalDate, DepartureDate, ReadyDate.

5) Tratamiento de valores nulos en las columnas: Channel, RoomRate, Revenue, ADR, TouristTx.

- En Channel reemplzamos los valores faltantes con el valor categórico "Unknown".
- En el caso de las columnas numéricas RoomRate, Revenue y ADR imputamos los valores faltantes con la media de cada variable. 
- En la variable TouristTax sustituimos los nulos con el valor 0.

6) Verificamos la coherencia de la columna Persons en tanto que debe ser la suma de los valores presentes en las columnas Adults, Children e Infants. No se encontró inconsistencias. 

7) En la columna PropertyType encontramos el valor 'Apa' y el valor 'Apartment'. Como hacen referencia al mismo valor optamos por sustituir los valores 'Apa' por 'Apartment'. 

## EDA (Análisis exploratorio de datos)

1) El resumen estadístico inicial nos llevo a buscar y detectar outliers en las siguientes columnas: RoomRate, NumNights, CleaningFee, Revenue, ADR, TouristTax, TotalPaid.  
2) Para la detección de outliers primero graficamos boxplots de cada una de las variables de nuestro interés. 
3) Posteriormente procedimos a eliminar esos valores atípicos para lo cual se determinaron los límites inferior (lower_bound) y superior (upper_bound) basados en los percentiles 1% y 99%. Estos percentiles definen un rango que excluye los valores más extremos, tanto los más bajos como los más altos, asegurando que solo se consideren los valores de las variables analizadas que están dentro del 98% central de los datos.
4) Por otra parte, en las variables Capacity, Square y NumBedrooms buscamos valores que no tuvieran sentido filtrando el dataset para aquellos valores exclusivamente mayores a 0.


## Consolidado de los datasets

Finalmente unimos los dos datasets limpios usando como primary key la columna PropertyId. 