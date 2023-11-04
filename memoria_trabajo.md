

## Dataset

CrabAgePrediction.csv de Kaggle.
Se sube Google Sheets de nuestro grupo.

https://docs.google.com/spreadsheets/d/e/2PACX-1vR42Z5BNxHUNED18y3hyppc9T5g-X1oDi9I6b2X8HRy3eB-jpXo7a3XIVWdwWOyEeodwXM5c0YPUYCQ/pub?output=csv


### Descripción

Columnas:

|Sex|Length|Diameter|Height|Weight|Shucked Weight|Viscera Weight|Shell Weight|Age|
|---|---|---|---|---|---|---|---|---|
|F|1,4375|1,175|0,4125|24,6357155|12,3320325|5,5848515|6,747181|9|

La idea es, más que realizar una regresión lineal para predecir la variable objetivo, es poder intentar explicar con las variables tomadas como predictoras, la edad de los crustáceos. 


## Hipótesis

$H_0$: con las columnas seleccionadas del dataset, se puede explicar la edad de los cangrejos;
$H_1$: los datos provistos en el dataset no son suficientes como para poder predecir o explicar la edad para un nuevo conjunto de datos


## Preguntas

- ¿Qué relación hay entre length, diameter, height y weight?
- ¿Qué sería la 'I' en el sexo?
	I es de indeterminado

- ¿Qué nivel de correlación hay entre la variable predicha y las demás?


## Objetivo del estudio

La idea del presente estudio es, mediante las variables con las que ya cuenta el dataset, o en todo caso el agregado de alguna más relevante, analizar la posibilidad de explicar la edad del cangrejo mediante mediciones externas, que puedan realizarse ya sea por inspección humana, o con la asistencia de una computadora. Esto permitiría elaborar un sistema automático de medición de cangrejos vivos, que puedan estudiarse y devolverse a su habitat.
En el dataset original, se pueden ver variables como "Shucked Weight",  "Viscera Weight" y "Shell Weight", por ende no se estaría trabajando con especímenes vivos, ya que esto implicaría la disección del animal y la intervención humana en el proceso.
De todas maneras, se intentará ir por el primer enfoque, evaluando los resultados, y luego incluyendo las últimas variables mencionadas, para comparar los datos obtenidos.
## ¿Cómo se determina normalmente la edad de un cangrejo?

Se revisa bibliografía para poder entender más sobre el proceso de estimación de la edad de los crustáceos. Esto arrojaría información no solo sobre métodos, si no para buscar alternativas, o bien información para complementar el proceso de selección de atributos para el modelo.
En general, la metodología utilizada implica métodos destructivos, es decir, requieren un espécimen sin vida del crustáceo, ya que se consideran variables correspondientes a la fisiología del mismo, y que requieren procesos histológicos.

#### Métodos destructivos

Mediante la _lipofuscina_, un pigmento de desgaste que se encuentra con frecuencia en tejidos del corazón, hígado y cerebro, se pueden analizar los niveles en relación con la edad del crustáceo, como se indica en el caso del estudio [PRELIMINARY IDENTIFICATION AND QUANTIFICATION OF THE AGE-PIGMENT LIPOFUSCIN IN THE BRAIN OF Farfantepenaeus paulensis (CRUSTACEA: DECAPODA)]()

En la nota [## How Old is That Crab?](https://adfg.alaska.gov/index.cfm?adfg=wildlifenews.view_article&articles_id=845), se indica como se puede obtener la edad y un indicativo del crecimiento del  _snow crab_ mediante las bandas de crecimiento del estómago de los cangrejos.
Esto se ecplica con más detalle en [PRELIMINARY INVESTIGATION OF DIRECT AGE DETERMINATION USING BAND COUNTS IN THE GASTRIC MILL OF THE BLUE SWIMMER CRAB (PORTUNUS PELAGICUS LINNAEUS, 1758) IN TWO SALT-WATER LAKES IN THE EASTERN MEDITERRANEAN](https://www.researchgate.net/publication/284173779_PRELIMINARY_INVESTIGATION_OF_DIRECT_AGE_DETERMINATION_USING_BAND_COUNTS_IN_THE_GASTRIC_MILL_OF_THE_BLUE_SWIMMER_CRAB_PORTUNUS_PELAGICUS_LINNAEUS_1758_IN_TWO_SALT-WATER_LAKES_IN_THE_EASTERN_MEDITERRANE). y también se puede ver en  [# Feasibility of using Growth Band Counts in Age Determination of Four Crustacean Species in the Northern Atlantic](https://academic.oup.com/jcb/article/35/4/499/2547802?login=false),
Para estos casos se analiza el _gastric mill_, un órgano del tracto digestivo de varios animales como los cangrejos, para la determinación de la edad de forma directa, dado que al parecer  se puede conocer la edad del crustáceo por el conteo de las bandas de crecimiento, resultado de que el espécimen va mudando su cuerpo con el tiempo.


#### Métodos no destructivos

Para poder recolectar cangrejos, se deben tener en cuenta varios factores, y esto depende también de la especie. Por ejemplo, para el caso del cangrejo rey, la captura varía entre aquellos especímenes de entre 5 y 7 años de edad [Ablison](https://www.ablison.com/es/%C2%BFQu%C3%A9-edad-tienen-los-cangrejos-rey-cuando-se-cosechan%3F/?expand_article=1)

En el estudio [# Towards Age Determination of Southern King Crab (Lithodes santolla) Off Southern Chile Using Flexible Mixture Modeling](https://www.mdpi.com/2077-1312/6/4/157), se plantea un enfoque interesante para conocer la edad de la _centolla_ (al sur del continente americano), usando _length frecuency data (LDF o LFQ)_

Para ampliar revisar en:

https://www.st.nmfs.noaa.gov/st1/recreational/pubs/data_users/chap_5.pdf

https://academic.oup.com/icesjms/article/61/2/218/620849

https://www.sciencedirect.com/science/article/abs/pii/S016578362030093X

https://www.sciencedirect.com/science/article/abs/pii/0165783691900136


(FMN) distributions for each LFD. (finite mixture normal) << asume normalidad



En el estudio anterior también se plantea la separación en grupos por rango etario, algo que también sería de utilidad considerar, puesto que podría realizarse una clasificación para predecir en que grupo estaría el espécimen, dando un resultado directo a la hora de decidir si está apto para el cultivo.



## Modelo regresión

La aplicación del modelo de regresión lineal (múltiple en este caso), no arroja un valor realmente satisfactorio. Varios de los atributos que serían predictores, tienen una alta correlación, y esto sería contraproducente al efectuar dicho modelo. Finalmente, las variables que pueden explicar la edad del cangrejo, son pocas, y no aportan demasiado al modelo para minimizar el error.
Se considera la aplicación entonces, de otro modelo de regresión, para evitar el problema de la multicolinealidad que se tiene coon la regresión lineal, pero de todas maneras la alta correlación entre "weight" y varias de las demás variables, se interpreta como un problema que puede llevar a un overfitting.
Quizás el uso de otro modelo más complejo, como regresión con KNN o RandomForest se justifique si hubiera más columnas que aporten valor.



## Modelo de clasificación


Analizando el set de datos, se investiga la procedencia del mismo.

https://www.kaggle.com/datasets/sidhus/crab-age-prediction

Según la fuente oficial, se mencionan cangrejos del área de Boston, pero no se indica su especie ni su procedencia. Este es un dato realmente importante, debido a que entre las diversas especies de cangrejos que existen, o incluso de las que se pueden pescar o cosechar en la zona de Boston, hay una marcada variabilidad en cuanto a al espectativa de vida, el tamaño y la madurez sexual del espécimen (entre otras).

So consulta entonces en diferente bibliografía, para contar con más detalles.
Según información de publicaciones e información del estado de Massachusetts (donde se encuentra Boston), las especies nativas (ya sea en estuarios o del mar directamente) o invasivas, tienen medidas que no se corresponden con las que están en el dataset.
Para ello se compararon las medias, y valores máximos de los diferentes atributos.
La publicación [Profile: Crabs](https://climateactiontool.org/content/profile-crabs)sirvió de referencia para esto.

De lo antes mencionado, solamente con lo que se pueda obtener de los datos provistos, se realizan algunas interpretaciones:

- la proveniencia de los crustáceos es incorrecta:
	- el cangrejo _Paralithodes camtschaticus_ o __Red King Crab__ (Alaska) puede tener más de 24 libras ([Red King Crab](https://www.fisheries.noaa.gov/species/red-king-crab/overview)), y su edad puede llegar a ser mayor a 20 años ([Red King Crab - Alaska](https://www.adfg.alaska.gov/index.cfm?adfg=redkingcrab.main)) , con un rango esperado de entre 15 y 20. lo que se adapta a la realidad de los valores del set de datos. Sin embargo, la distribución geográfica no se corresponde con el área costera de Boston, ya que se encuentran mayormente en las aguas frías de Alaska, en el Océano Pacífico Norte (además de otras regiones, fuera de Estados Unidos), y además, el peso medio del set de datos está muy por debajo de la media de peso de estos crustáceos;
	- se trata en realidad del _Chionoecetes opilio_ o __Snow Crab__ . Su habitat también abarca el Océano Atlántico, pero abarca desde el estado de Maine hasta Groenlandia. Alcanzan la madurez entre los 4 y los 10 años y en general son similares a la especie anterior, si embargo, son más pequeños en peso y tamaño, por lo que no son candidatos que se ajusten bien al dataset;

- el dataset hacer referencia al "horsehore crab":
	- en la nota de [Horseshoe Crab](https://biologydictionary.net/horseshoe-crab/), se mencionan los datos en cuanto longitud y peso, que se acercan más a los indicado en el conjunto de datos. Además, habitan las costas de América Central y América del Norte, además del Sudeste de Asia. Sin embargo, en realidad este espécimen no es un cangrejo (es de otra familia), y su consumo no es habitual como los otros casos;
	

¿Porqué identificar la especie? Porque de esta forma, se podría realizar una clasificación correcta en dos grupos: jóvenes y adultos, de forma que se pueda predecir aquellos aptos para "cosecha".
Debido entonces, a la falta de información, se toma como referencia al __red king crab__, interpretando que los datos tampoco están correctos en el dataset (longitud y diámetro no se corresponden con peso)  y la procedencia es errónea, y se realiza una separación en dos clases:
- jóvenes: < 10 años 
- adultos: > 10 años






<hr>

## Enlaces de interés

https://rpubs.com/sarvinnah/1055418

https://github.com/amyrmahdy/Predicting-Crab-Age-Using-Machine-Learning/blob/master/crab-age.ipynb

https://github.com/Aravinth-Megnath/Crab_age/blob/crab1/crab_age_prediction.ipynb


https://christopherdavisuci.github.io/UCI-Math-10-S23/Proj/StudentProjects/KaijieZhang.html



https://cienciadedatos.net/documentos/py10-regresion-lineal-python



## Pasos a seguir


- Hacer regresión lineal. Justificar supuestos y elección de características
- Realizar una clasificación por categoría:

- joves 

https://findelmundo.tur.ar/es/gastronomia/productos/centolla/3605






















