# Consultoría Retrasos y Cancelaciones de Vuelos

Analistas: Nova Gallardo y Lorna Remmele<br>
Septiembre 2024

## Enlaces

[Bitácora](https://docs.google.com/document/d/1J828SucRgOCuxv2QmOCihrxq2Bi-esE6-VxK_k5gfVY/edit?usp=sharing)<br>
[Dashboard]([https://www.google.com/url?q=https://lookerstudio.google.com/reporting/7893ce7d-40d0-4d16-ba5c-b9275a236f84/page/p_778ch8jqkd/edit&sa=D&source=docs&ust=1726039376046579&usg=AOvVaw2UbAPXp76nCRbfaiSDrke_](https://drive.google.com/file/d/1BQCOEkquTB-UqVQCvxon6f1ayAlaeEUu/view?usp=sharing)<br>
[Presentación](https://docs.google.com/presentation/d/12t9HLwdpcGI9iS5REN3a3Jl1W4Mq9BRH36wTNguW90U/edit#slide=id.p)<br>

## Contexto

Consultoría realizada en base a conjunto de datos extraído del Departamento de Transporte de EE.UU., [Oficina de Estadísticas de Transporte](https://www.transtats.bts.gov) y disponibles en Kaggle, con información sobre incidentes de vuelos de aerolíneas de enero de 2023. Las variables incluyen rutas de vuelo (origen y destino), duración y distancias, información técnica aeropuertos, aerolíneas, motivos/atribuciones de retrasos y cancelaciones, entre otros.

Se analizaron los datos sobre incidentes asociados a los vuelos, para hacer hallazgos de patrones y tendencias y así proporcionar información esclarecedora sobre qué factores inciden, dónde se concentran y ofrecer recomendaciones estratégicas.

## Herramientas utilizadas

BigQuery, Google Colab, Google Sheets, Looker Studio, Google Slides, Loom, Metodología Ágil Scrum y Slack. 

## Lenguajes utilizados

SQL y Pyhton.

## Metodología

- Preparación base de datos: Limpieza, creación de nuevas variables y unión de tablas.
- Técnicas de análisis utilizadas: Segmentación de aeropuertos, distancias, retrasos, entre otros. Medidas estadísticas como Correlación de Pearson y desviación estándar. Cálculo de riesgo relativo de variables para descubrir patrones y tendencias. Gráficas como scatter plots, histogramas y box plots.
- Responder preguntas: Entender los resultados del cálculo de riesgo relativo y las estadísticas para esclarecer las preguntas formuladas.
- Descubrimiento de información oculta en los datos: Explorar y analizar los datos para encontrar información adicional que pueda influir en la toma de decisiones y con ello desarrollar estrategias.

## Preguntas guía

Algunos de los planteamientos guía para el análisis fueron las siguientes:

- ¿Existen patrones frecuentes en relación a cancelaciones, retrasos y desvíos de vuelos? Por ejemplo, rutas, aeropuertos de origen o destino y horarios.
- ¿Cuál es el tiempo promedio de retraso?
- ¿Es posible identificar el principal motivo de retraso y cancelación?
- ¿Qué aerolíneas registran más incidentes de cada tipo?
- ¿Hay una relación entre la distancia de vuelo y la probabilidad de incidentes?
- ¿Los aeropuertos más grandes tienen más retrasos comparados con aeropuertos más pequeños?

## Composición dataset

Se trabajó en base a 3 tablas que contienen datos sobre vuelos efectuados en enero del 2023 por 15 aerolíneas distintas, dentro de territorio estadounidense. Las variables que componen el conjunto de datos original son las siguientes:

Tabla DOT_CODE_DICTIONARY
- CODE: identificador numérico del U.S. Department of Transportation (DOT) para aerolíneas.
- DESCRIPTION: descripción aerolínea.

Tabla AIRLINE_CODE_DICTIONARY:
- CODE: Código de operador único para agencias operadoras de aeronaves.
- DESCRIPTION: descripción de la agencia operadora de aeronaves.

Tabla FLIGHTS_202301
- FL_DATE: fecha de vuelo (yyyymmdd).
-AIRLINE_CODE: código de operador único.
- DOT_CODE: número de identificación asignado por el DOT de EE. UU. para identificar una aerolínea única.
- FL_NUMBER: número de vuelo.
- ORIGIN: aeropuerto de origen.
- ORIGIN_CITY: aeropuerto de origen, nombre de la ciudad.
- DEST: aeropuerto de destino.
- DEST_CITY: aeropuerto de destino, nombre de la ciudad.
- CRS_DEP_TIME: hora local de salida (hhmm) registrada CRS (Sistema de control de reservas).
- DEP_TIME: hora local de salida real (hhmm).
- DEP_DELAY: diferencia en minutos entre la hora de salida prevista y la real.
- TAXI_OUT: tiempo de taxi en la salida en minutos.
- WHEELS_OFF: hora exacta de despegue (hora local: hhmm).
- WHEELS_ON: hora exacta de aterrizaje (hora local: hhmm).
- TAXI_IN: tiempo de taxi en la llegada en minutos.
- CRS_ARR_TIME: hora local de llegada registrada en CRS (hhmm).
- ARR_TIME: hora local de llegada real (hhmm).
- ARR_DELAY: diferencia en minutos entre la hora de llegada prevista y la real.
- CANCELLED: indicador de vuelo cancelado.
- CANCELLATION_CODE: motivo de la cancelación.
- DIVERTED: indicador de vuelo desviado.
- CRS_ELAPSED_TIME: tiempo total de vuelo transcurrido en minutos registrado en CRS.
- ELAPSED_TIME: tiempo total de vuelo transcurrido en minutos real.
- AIR_TIME: tiempo de vuelo en el aire en minutos.
- DISTANCE: distancia entre aeropuertos (millas).
- DELAY_DUE_CARRIER: retraso del operador en minutos.
- DELAY_DUE_WEATHER: retraso meteorológico en minutos.
- DELAY_DUE_NAS: retraso del Sistema Aéreo Nacional en Minutos.
- DELAY_DUE_SECURITY: retraso de seguridad en minutos.
- DELAY_DUE_LATE_AIRCRAFT: retraso de aeronaves tardías en minutos.
- FL_YEAR: año en que se realizó el vuelo.
- FL_MONTH: mes en que se realizó el vuelo.
- FL_DAY: día en que se realizó el vuelo.


## 1. Procesamiento y preparación de datos

[Creación de nueva tabla](https://github.com/lornarr/proyecto-4-vuelos/blob/main/1.%20Procesamiento%20y%20preparaci%C3%B3n%20de%20datos/1.%20Creaci%C3%B3n%20nueva%20tabla.md)<br>
[Identificación y gestión de nulos y duplicados](https://github.com/lornarr/proyecto-4-vuelos/blob/main/1.%20Procesamiento%20y%20preparaci%C3%B3n%20de%20datos/2.%20Identificaci%C3%B3n%20y%20gesti%C3%B3n%20de%20nulos%20y%20duplicados.md)<br>
[Gestión de datos fuera del alcance del análisis y datos inconsistentes en variables categóricas](https://github.com/lornarr/proyecto-4-vuelos/blob/main/1.%20Procesamiento%20y%20preparaci%C3%B3n%20de%20datos/3.%20Gesti%C3%B3n%20datos%20fuera%20del%20alcance%20de%20an%C3%A1lisis%20e%20inconsistentes.md)<br>
[Unión tablas](https://github.com/lornarr/proyecto-4-vuelos/blob/main/1.%20Procesamiento%20y%20preparaci%C3%B3n%20de%20datos/4.%20Uni%C3%B3n%20tablas.md)<br>
[Creación de nuevas variables](https://github.com/lornarr/proyecto-4-vuelos/blob/main/1.%20Procesamiento%20y%20preparaci%C3%B3n%20de%20datos/5.%20Creaci%C3%B3n%20nuevas%20variables.md)<br>
[Identificación de nuevos datos atípicos y nulos](https://github.com/lornarr/proyecto-4-vuelos/blob/main/1.%20Procesamiento%20y%20preparaci%C3%B3n%20de%20datos/5.%20Identificaci%C3%B3n%20nuevos%20datos%20at%C3%ADpicos%20y%20nulos.md)<br>

## 2. Análisis Exploratorio de Datos

[Resumen estadísticas descriptivas variables](https://github.com/lornarr/proyecto-4-vuelos/blob/main/2.%20An%C3%A1lisis%20exploratorio%20de%20datos/1.%20Resumen%20estad%C3%ADsticas%20descriptivas%20variables.md)<br>
[Visualización de distribución de datos](https://github.com/lornarr/proyecto-4-vuelos/blob/main/2.%20An%C3%A1lisis%20exploratorio%20de%20datos/2.%20Visualizaci%C3%B3n%20distribuci%C3%B3n%20datos.md)

## 3. Aplicar técnicas de análisis

[Correlación de Pearson](https://github.com/lornarr/proyecto-4-vuelos/blob/main/3.%20Aplicaci%C3%B3n%20t%C3%A9cnicas%20de%20an%C3%A1lisis/1.%20Correlaci%C3%B3n%20de%20Pearson.md)<br>
[Cálculo de riesgo relativo](https://github.com/lornarr/proyecto-4-vuelos/blob/main/3.%20Aplicaci%C3%B3n%20t%C3%A9cnicas%20de%20an%C3%A1lisis/2.%20Riesgo%20relativo.md)<br>
[Respuesta a preguntas guía](https://github.com/lornarr/proyecto-4-vuelos/blob/main/3.%20Aplicaci%C3%B3n%20t%C3%A9cnicas%20de%20an%C3%A1lisis/3.%20Respuesta%20a%20preguntas%20gu%C3%ADa.md)

## Hallazgos

**Generales**

- La mayoría de los 3 tipos de incidentes se concentran en aeropuertos de origen y destino grandes, en viajes cortos de hasta hasta 1,500 km (aprox 930 millas) y de lunes a miércoles.

- Las aerolíneas que más incidentes acumulados registran (retrasos, cancelaciones y desvíos acumulados) son Southwest Airlines Co., American Airlines Inc., SkyWest Airlines Inc., Delta Air Lines Inc. y JetBlue Airways. La primera concentra 27,42% del total de incidentes del dataset. Sin embargo, se trata a la vez de las aerolíneas que más vuelos realizan, por lo cual es proporcional y lógico el porcentaje.

- Las aerolíneas que en general más altos riesgos relativos de incidentes poseen son SkyWest Airlines Inc., Frontier Airlines Inc., Southwest Airlines Co., Spirit Air Lines y Allegiant Air.

**Retrasos**

- El incidente más recurrente y significativo es el de vuelos retrasados, correspondiendo a un 21,7% del total de vuelos efectuados, aunque salen más vuelos antes de tiempo que retrasados. Las cancelaciones representan un 1,9%. Las desviaciones de vuelos representan el porcentaje más bajo, de un 0,2%.

- Para efectos de retrasos, cobra más relevancia la aerolínea u operadora, habiendo 6 con riesgo relativo de retrasos positivo.. En orden de mayor a menor, Frontier Airlines Inc. (1.73), Spirit Air Lines (1.37), JetBlue Airways (1.26), Allegiant Air (1.24), United Air Lines Inc. (1.07) y Southwest Airlines Co. (1.07).

- La mayoría de los retrasos se producen por motivos logísticos e internos. Delay_du_carrier (retraso de la aerolínea/operador) es la causa más significativa en relación a retrasos de partida (corr 0.69) y de llegada (corr 0.68). Le sigue delay_due_aicraft (retraso de aeronaves tardías) (corr 0.59 y 0.58). Ambos tipos de retraso están estrechamente relacionados entre sí en cuanto a causalidad.

- Los retrasos por motivos de seguridad son los menos recurrentes, apenas un 0.32% del total de vuelos. Spirit Air Lines es la aerolínea que más retrasos por NAS y por seguridad registra.

- La mayoría de los retrasos son cortos (15 a 30 minutos), aunque acumulativamente salen más vuelos adelantados que retrasados.El retraso promedio es de 69 minutos (largo).

- La franja horaria que más retrasos concentra es la mañana, de 06:00 a 12:00, seguida por poca diferencia por el horario de tarde, 16:00 a 20:00. El horario con menos retrasos asociados es la madrugada, de 00:00 a 06:00.

- En retrasos de vuelos destacan los días miércoles y lunes, así como la costa este tanto en origen como destino.

- El número de pistas de los aeropuertos no tiene una correlación positiva significativa con los retrasos de vuelo.

- Los aeropuertos con alto flujo de personas (large) y cantidad intermedia de pistas (4) son los que más retrasos registran.

**Cancelaciones**

- Para cancelaciones de vuelos, cobran más relevancia las rutas. Hay 5 rutas con riesgo relativo de 52.35: BWI - ABQ, CNY - SLC, DEN - GRB, FSD - SNA, GRB - DEN y SNA - FSD.

- El motivo de cancelación de vuelos más recurrente es por condiciones meteorológicas, por un amplio margen de diferencia (64,2%). Los retrasos por motivo de seguridad son la causa con menor incidencia, de apenas un 1,8%.

- La costa central tiene alta concentración de viajes cancelados, mayoritariamente por causas metereológicas en franja horaria nocturna, de 20:00 a 00:00 horas.

- Martes y miércoles son los días que más cancelaciones se registran.

- Los aeropuertos de origen con mayor riesgo de cancelación de vuelos son COD / Cody (17.45), ADK / Adak Island (13.09), VEL / Vernal (10.27), DVL / Devils Lake (9.35) y ASE / Aspen (8.91).

- Las aerolíneas con riesgo de cancelación positivo son, de mayor a menor, SkyWest Airlines Inc. (1.88), Frontier Airlines Inc. (1.76), Southwest Airlines Co. (1.74), Envoy Air (1.36) y Spirit Air Lines (1.22).

**Desvíos**

- Para desvíos, el factor más relevante es, por amplia diferencia, las rutas, seguido del aeropuerto de destino. Aquellas con mayor riesgo positivo alto son SAN - DSM (400.92), SAN - KOA (11.70), AMA - IAH, GRR - AH y SNA - MDW (las 3 con 100.23).

- Los destinos con mayor riesgo relativo de desvíos son PSG / Petersburg (33.51), ASE / Aspen (28.85), DVL / Devils Lake (21.51), YAK / Yakutat (20.07) y LBF / North Platte (19.36).

- Las aerolíneas con mayor riesgo relativo de desvíos son SkyWest Airlines Inc. (2.77), Alaska Airlines Inc. (2.11), PSA Airlines Inc. (1.06) y Allegiant Air. (1.02).

- La mayoría de los vuelos desviado tiene como origen y destino la costa central, y se realizan los días lunes y martes.

## Recomendaciones estratégicas

- Enfocarse en subsanar los retrasos, ya que están mayoritariamente asociados a factores internos controlables por la aerolínea y el aeropuerto. Las cancelaciones, por otro lado, dependen de factores externos no controlables, como el clima.

- Investigar qué motivos específicos de delay_due_late_aircraft y delay_due_carrier causan los retrasos.

- Investigar las causas de los desvíos.

- Se sugiere indagar respecto a las aerolíneas que más problemas asociados tienen: SkyWest Airlines Inc., Frontier Airlines Inc., Southwest Airlines Co., Spirit Air Lines y Allegiant Air.

- Investigar por qué Spirit Air Lines es la que más retrasos por NAS y por seguridad tiene y cuáles son los problemas asociados.

- Aumentar cantidad de pistas en aeropuertos grandes con menos de 4 pistas, ya que los incidentes suelen estar asociados a aeropuertos de mucho flujo.

- Considerando que las rutas cobran especial relevancia en cuanto a desvíos y cancelaciones, sobre todo en desvíos, indagar respecto a qué incidentes suelen presentar.

- Dado que el dataset es solo de enero 2023, se sugiere armar una muestra de datos más significativa, es decir, más prolongada en el tiempo (meses y años), que considere distintas estaciones del año y temporadas (alta y baja demanda).
