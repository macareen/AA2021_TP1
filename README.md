<div>

<span class="c6 c32 c55">Trabajo práctico número 1 - Aprendizaje
Automático</span><span class="c6 c32">                                 
</span><span class="c46 c55 c6 c32">Grupo 12: Carrasco, Roel,
Sotelo</span>

</div>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 119.00px; height: 74.00px;">![](images/image14.png)</span>

<span class="c14 c12"></span>

<span class="c14 c12"></span>

<span class="c12 c14"></span>

<span class="c14 c12">UNIVERSIDAD DE BUENOS AIRES</span>

<span class="c14 c12">FACULTAD DE CS. EXACTAS Y NATURALES</span>

<span class="c12 c23"></span>

<span class="c12 c59">MAESTRÍA EN EXPLOTACIÓN DE DATOS Y DESCUBRIMIENTO
DE CONOCIMIENTO</span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c9"></span>

<span class="c12 c49">TRABAJO PRÁCTICO ENTREGABLE I  
Árboles de decisión</span>

### <span class="c12 c26"></span>

### <span class="c26 c12">Aprendizaje Automático </span>

<span class="c12">1er cuatrimestre de 2021</span>

<span class="c19"></span>

<span class="c6 c12 c29">Grupo 12</span>

<span class="c29 c6 c12">Integrantes:</span><span class="c29"> Lisandro
Carrasco</span><span class="c27 c29 c54">, Macarena Roel, Santiago
Sotelo</span>

-----

<span class="c3"></span>

### <span class="c27 c36">Resumen</span>

## <span class="c3">Poder clasificar el riesgo de sufrir un derrame cerebral de una persona a partir de información disponible y fácil de recolectar resulta de gran interés para la calidad de vida humana. </span>

## <span class="c5">En este trabajo, se analizan los datos de 5.110</span><span class="c3"> personas con resultados conocidos acerca de su padecimiento de un derrame cerebral o no, así como información sobre su edad, género, índice de masa corporal, estado civil, tipo de residencia y trabajo, y si tienen o no hipertensión, entre otras.</span>

## <span class="c5">A partir de aquello, se buscaron factores que podrían resultar de mayor interés a la hora de predecir un derrame cerebral. Para ello, s</span><span class="c5">e realizó un análisis exploratorio de los datos y se entrenaron varios árboles de clasificación con diferentes hiperparámetros y predictores, evaluando las diferencias en sus resultados.</span>

## <span class="c5">En función de las diferentes particiones hechas sobre la muestra, así como de los diferentes hiperparámetros utilizados, hemos notado cambios importantes en la performance de los modelos. Más allá de su variabilidad, valoramos haber logrado buenos resultados en métricas que eran de nuestro interés particular, principalmente </span><span class="c5 c6 c12">recall </span><span class="c5">y el </span><span class="c5 c6 c12">F2 score</span><span class="c5">.</span>

## <span class="c5">Como resultado, se obtuvo que las variables que mejor permiten discriminar entre quienes sufrieron derrames y quienes no fueron la edad, el índice de masa corporal y el nivel de glucosa en sangre. </span>

<span class="c3"></span>

## <span class="c36">Introducción</span>

## <span class="c5">Un derrame cerebrovascular puede ser causado cuando se rompe un vaso sanguíneo en o cerca del cerebro o cuando se interrumpe la irrigación de sangre y oxígeno al cerebro. Aunque se ha avanzado mucho en la detección y tratamiento de la enfermedad cerebrovascular, ésta sigue siendo una de las principales causas de muerte y discapacidad en muchos países del mundo (BBC News).  
Es por ello que resulta de gran interés encontrar métodos simples e interpretables para predecir el riesgo de padecer uno. </span>

## <span class="c5">El objetivo de este trabajo fue generar el mejor árbol de clasificación posible para identificar pacientes con riesgo de sufrir derrames cerebrales a partir de información sobre su estado de salud y estilo de vida.</span><span> </span><span class="c3">Para ello se comenzó por realizar un análisis y limpieza de los datos disponibles, buscando las posibles variables de mayor interés. Las mismas se encuentran descritas en las secciones “Datos” y “Metodologías”, discutiendo los resultados obtenidos en “Resultados” y finalizando el trabajo con algunas valoraciones en la sección “Conclusiones”.</span>

<span class="c3"></span>

## <span class="c27 c36">Datos</span>

<span class="c5">Una breve descripción de las variables en cuestión y
sus diferentes valores. </span>

  - <span class="c5 c16 c12">id.</span><span class="c27 c5 c16"> identificatoria
    de cada paciente. Si bien utiliza números, no deja de ser una
    variable nominal.</span>
  - <span class="c5 c16 c12">gender</span><span class="c27 c5 c16">.
    Categórica, describe el género de la persona observada de manera
    binaria (hombre o mujer). También considera un caso no binario en la
    categoría 'otros'.</span>
  - <span class="c5 c16 c12">age</span><span class="c5 c16 c27">.
    Numérica y continua. Si bien la mayoría de sus valores están
    discretizados por la edad en años, esto solo se cumple en los
    mayores de 2 años. En tanto a los menores de 2 años se los registra
    con mayor detalle, lo que hace que la variable sea continua.</span>
  - <span class="c5 c16 c12">hypertension</span><span class="c27 c5 c16">.
    Es una variable binaria que evalúa si una persona tiene o no
    hipertensión. </span>
  - <span class="c5 c16 c12">heart\_disease</span><span class="c27 c5 c16">.
    Igual que la hipertensión, es una categórica dicotómica que evalúa
    si la persona tiene o tuvo alguna enfermedad cardíaca.</span>
  - <span class="c5 c16 c12">ever\_married</span><span class="c5 c16">.
    También es binaria, más allá de que el lugar de unos y ceros use
    'sí' y 'no'. Detalla si la persona está o estuvo alguna vez
    casada.</span>

<!-- end list -->

  - <span class="c5 c16 c12">work\_type</span><span class="c27 c5 c16">.
    Variable categórica, no binaria, que clasifica el tipo de empleo de
    las personas observadas, y los etiqueta según si son empleados del
    sector privado, del sector público, si son cuentapropistas, si nunca
    trabajaron o si son niños.</span>
  - <span class="c5 c16 c12">Residence\_type</span><span class="c27 c5 c16"> divide
    a las personas entre habitantes de zonas urbanas o rurales.</span>
  - <span class="c5 c16 c12">abg\_glucose\_level</span><span class="c5 c16">.
    Numérica continua, registra el nivel de
    glucosa</span><span class="c5 c16"> en
    sangre</span><span class="c27 c5 c16"> de las personas
    observadas.</span>
  - <span class="c5 c16 c12">bmi</span><span class="c5 c16">. Se trata
    del índice de masa corporal de las personas. Es la única variable
    con valores faltantes y no se puede imputar a partir de otras, pues
    requiere de variables tales como peso y altura, que no se encuentran
    disponibles. A su vez, presenta valores poco comunes por lo visto en
    la literatura médica.</span>
  - <span class="c5 c16 c12">smoking\_status</span><span class="c27 c5 c16">.
    Clasifica de manera categórica entre actuales fumadores, ex
    fumadores o personas que nunca fumaron. Si bien no hay "formalmente"
    valores faltantes, hay una importante cantidad de registros -1544-
    que tienen registrado el valor "desconocido".</span>
  - <span class="c5 c16 c12">stroke</span><span class="c5 c16">. La
    variable objetivo. Apunta si la persona
    </span><span class="c5 c16">sufrió</span><span class="c27 c5 c16"> o
    no un accidente cerebrovascular.</span>

<span class="c5 c16">La cuestión de los valores faltantes merece una
doble consideración. Por un lado, como ya se ha dicho, la única variable
que no tiene un valor asignado en una o varias filas, es decir, que
registra valores faltantes, es
</span><span class="c5 c16 c12">bmi</span><span class="c5 c16">.  Sin
embargo, la variable
</span><span class="c5 c16 c12">smoking\_Status</span><span class="c5 c16"> registra
más de un cuarto de las observaciones bajo la categoría
</span><span class="c5 c6 c16">unknown</span><span class="c27 c5 c16">.
Esto implica que si bien tiene una asignación sobre un valor, es decir
que se puede contar como un valor "presente", en verdad no aporta
ninguna información sobre si esas personas son o han sido en algún
momento fumadoras.</span>

<span class="c3">En el caso de la variable bmi, debió considerarse que
no todos los valores observados eran valores comunes o posibles. Según
lo establecido por el NIH (National Heart, Lung and Blood Institute), la
tabla de índice de masa corporal comprende los valores entre 19 y 57;
sin embargo, la tabla no contempla a los niños (que sí están presentes
en el set de datos). Por otro lado, al realizar un boxplot, se pudo ver
que este método hace pensar que los valores mayores a 45 son outliers.
Esto se trataría de un caso de outlier de contexto: un caso que
normalmente no es extraño, pero en esta muestra puntual sí resulta
serlo. Ante estas dos consideraciones, se siguieron los valores de NIH,
por lo que se decidió eliminar las observaciones con valores menores a
10 (ninguna observación) y mayores a 57 (70 observaciones, de las cuales
sólo 1 había presentado derrames).  
</span>

<span class="c36">Metodología</span><span class="c3"> </span>

<span class="c5">Se comenzó por realizar un análisis exploratorio de las
variables y estudiar posibles correlaciones con la variable de interés
</span><span class="c5 c6 c12">stroke</span><span class="c5">. El número
total de casos que efectivamente había presentado un derrame era
bastante reducido (un total de 249, que representan un 4,87% de la
muestra) </span><span class="c5">y
</span><span class="c5">dificultaron</span><span class="c5"> la
observación de patrones que los
</span><span class="c5">relacionaran</span><span class="c5">, por lo que
se recurrió a generar tablas de doble entrada y gráficos de barras que
permitieran observar gráficamente el porcentaje de cada respuesta para
las distintas variables consideradas</span><span class="c5">.  </span>

<span class="c5">Para adecuar las variables categóricas a los
requerimientos de los árboles de clasificación, se generaron
</span><span class="c5 c6 c12">dummies </span><span class="c5">para
todas las variables categóricas con más de dos niveles (género, tipo de
trabajo, y si son o no fumadores) y se codificaron las binarias con
</span><span class="c5 c6 c12">label encoder</span><span class="c5"> (si
alguna vez se habían casado y tipo de residencia). En tanto para tratar
con los valores faltantes de la variable
</span><span class="c5 c6 c12">bmi</span><span class="c5"> se
consideraron diferentes estrategias: eliminar los 201 casos faltantes,
entrenar un modelo KNN para imputarlas o realizar imputaciones por la
media agrupadas. Se optó por la última opción, agrupando por género y
cuartiles de edad para evitar aumentar el sesgo de la muestra. En el
caso de
</span><span class="c5 c6">smoking\_status</span><span class="c3">, dado
el peso que tienen los desconocidos para el total del dataset, se
decidió mantenerlos todos. </span>

<span class="c5">Más allá de las consideraciones hechas respecto de la
mayor correlación de variables tales como edad, nivel de glucosa o el
índice de masa corporal, se decidió entrenar los árboles con todas las
variables disponibles. Sobre el final del trabajo, recurrimos
</span><span class="c5">a RFE</span><span class="c5"> para reducir las
dimensiones utilizadas en función de la importancia presentada por cada
una en árboles anteriore</span><span class="c5">s. </span>

<span class="c5">Como se mencionó previamente, el conjunto de datos se
encontraba fuertemente desbalanceado, con muchos más casos negativos que
positivos. Ante esto, se utilizaron dos estrategias para reducir su
impacto: por un lado, las divisiones de muestras consideraron el
parámetro
</span><span class="c5 c6 c12">stratify</span><span class="c5">, para
asegurar que los conjuntos a utilizar
</span><span class="c5">contuvieran</span><span class="c5"> datos de
strokes positivos; por otro lado, cada árbol utilizó el hiperparámetro
</span><span class="c5 c6 c12">class\_weight</span><span class="c5 c6 c12"> </span><span class="c5">con
el argumento
‘</span><span class="c5 c6 c12">balanced</span><span class="c5">’</span><span class="c5 c6 c12">,
</span><span class="c3">que agrega un peso para medir la impureza en
función de cuán desbalanceados están los datos. </span>

<span class="c5">Como métrica principal se utilizó
</span><span class="c5 c12">Fβ-Score </span><span class="c5">con un
 valor de 2 para β, buscando darle un mayor peso al
</span><span class="c5 c12">recall</span><span class="c5">, pero sin
dejar de lado</span><span class="c3"> la accuracy. En este sentido,
también se le prestó una importante atención a la medida de recall,
entiendo la importancia de la sensibilidad de detectar casos que pueden
ser cuestiones de vida o muerte.</span>

<span class="c5">En cuanto a los modelos, se han entrenado árboles con
varias profundidades (evitando superar una profundidad de 10 para no
caer en grandes sobreajustes), diferentes estrategias de muestreo y de
poda, utilizando divisiones de sets de validación con varias semillas o
con </span><span class="c5 c12">StratifiedKFold
</span><span class="c5">de
</span><span class="c5 c12">GridSearchCV</span><span class="c3">, así
como diferentes niveles de α para la post poda. Tanto los árboles
entrenados sin poda con GridSearchCV así como los árboles podados, se
evaluaron en los sets de validación y de prueba, graficando sus
resultados con boxplots y matrices de confusión.</span>

<span class="c3"></span>

<span class="c36">Resultados</span><span class="c5"> </span>

<span class="c5">Si bien el desbalance y la poca presencia de casos con
strokes
</span><span class="c5">dificultó</span><span class="c5"> establecer
correlaciones, así como la presencia de múltiples variables categóricas
redujo la dimensión del correlograma, destacamos que la variable que más
correlación presenta con la posibilidad o no de sufrir una lesión es la
edad. Si bien presenta una baja correlación lineal (0,245),
</span><span class="c5">la misma no parece ser la adecuada en este
caso,</span><span class="c5"> ya que es la variable más importante
(posteriormente, se ha visto como principal discriminante en los
árboles). El nivel de glucosa en sangre ha resultado ser la segunda
variable más correlacionada. (Anexo I)  
También se realizaron gráficos comparativos entre las variables
categóricas y los casos de strokes, donde se comparó la proporción de
cada clase que había sufrido o no un accidente. La distribución de
hombres y mujeres que presentaron strokes fue prácticamente idéntica a
la que no, así como tampoco se presentaron grandes diferencias según los
lugares de residencias.  
Por otro lado, sí hubo importantes desproporciones en las variables de
hipertensión y enfermedades cardíacas; siendo las personas que padecían
estas enfermedades más propensas a sufrir una lesión; mientras que las
personas que están o estuvieron casadas presentaron menos casos. (Anexo
II)  
Dos datos muy llamativos se han presentado en las variables de
</span><span class="c5 c12">fumadores </span><span class="c5">y de
</span><span class="c5 c12">tipos de trabajos</span><span class="c5">:
la proporción de los ex fumadores que presentaron casos es bastante más
elevada que la de los que no presentaron, esta diferencia intraclase es
aún más amplia que la que presentaron los fumadores. En un segundo
punto, también se aprecia una diferencia notable en la ocurrencia de
casos según el tipo de empleos, siendo la proporción de empleados en el
sector público y privado muy similar ante los strokes, pero con los
cuentapropistas mucho más afectados que en los otros
caso</span><span class="c5">s (Figura 1).</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 230.82px; height: 220.00px;">![](images/image11.png)</span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 227.50px; height: 220.39px;">![](images/image15.png)</span>

<span class="c5 c6">Figura
1</span><span class="c5 c6">:</span><span class="c5 c12"> </span><span class="c5 c6">gráficos
de barras porcentuales de las variables tipo de trabajo y fumadores,
divididas según derrame o no y coloreadas según los valores que
tomaron.</span>

<span class="c3"></span>

<span class="c3"></span>

<span class="c3"></span>

<span class="c5">Se han entrenado 3 árboles, uno con 50 conjuntos de
validación generados por 50 semillas distintas; otro utilizando Cross
Validation con 50 folds que
</span><span class="c5">respetaran</span><span class="c3"> las
proporciones de casos objetivos y, finalmente, un árbol con diferentes
niveles de α.</span>

<span class="c5">En términos generales, se obtuvieron buenos resultados
en una de las métricas más importantes,
</span><span class="c5 c12">recall</span><span class="c3">, tanto sobre
el set de validación como el de prueba. Sin embargo, la performance
asociada al score F2 ha sido considerablemente menor, dado que el
accuracy de los tres modelos fue considerablemente bajo. Por otro lado,
también se observó una diferencia de rendimiento cuando los modelos se
evaluaban sobre los sets de validación o los de testeos, siendo en el
segundo caso algo menor y dando un indicio de sobreajuste a los datos de
entrenamiento. </span>

<span class="c5">En términos puntuales, el árbol entrenado con
validación cruzada ha presentado mejores resultados que el árbol
entrenado con 50 conjuntos de validación definidos por semillas
distintas. Si bien ambos presentaron medianas de 0,34 en lo que respecta
a la métrica de F2, el árbol entrenado con CV alcanzó mejores resultados
máximos, con scores de hasta 0.71, mientras que el primero no superó el
0,5. </span><span class="c5">Los boxplots de ambos árboles se encuentran
en el anexo (Anexo III).</span><span class="c5">  
El árbol que mejores resultados presentó bajo la estrategia de Grid
Search, contó con una profundidad de 4, un
</span><span class="c5 c6">alpha </span><span class="c3">de 0,  una
cantidad de hojas mínima de 1 y utilizó el criterio de entropía. Las
variables que han resultado de mayor importancia para generar sus
divisiones han sido la variable de edad (por mucho, la más importante y
presente en los primeros tres nodos), el nivel de glucosa en sangre y el
índice de masa corporal. Puede verse el árbol entero en el anexo (Anexo
IV).</span>

<span class="c5">Los </span><span class="c5 c12">mejores resultados
totales los ha presentado el árbol podado</span><span class="c5">, tanto
sobre validación como sobre testeo. Se atribuye esta mejora considerable
a la reducción del sobreajuste de los modelos anteriores al set de
entrenamiento. El árbol podado fue entrenado con una estrategia de
Random Search y presentó una profundidad máxima de 2, un α de 0,1315 y
utilizó el criterio de entropía.  
Evaluando </span><span class="c5 c12">sobre el set de testeo, presentó
un nivel de recall de 0,92</span><span class="c5">, siendo muy superador
del árbol sin poda, que alcanzó un 0,68. De los 50 casos que se le
presentaron y que efectivamente habían sufrido accidentes, el árbol
podado pudo identificar a 46, mientras que el árbol sin poda solo
detectó 36 de los casos. Las matrices de confusión pueden verse en el
</span><span class="c5">anexo (Anexo V).</span>

<span class="c5">Para evaluar el efecto de los diferentes niveles de
poda, se realizó un gráfico comparativo entre los resultados generados
por múltiples valores de este hiperparámetro. Si bien está planteado
sobre el accuracy y no sobre nuestras métricas principales, puede
evaluarse claramente como </span><span class="c5 c12">un mayor nivel de
α mejora la métrica sobre el set de testeo y la reduce sobre el de
entrenamiento y el de validación</span><span class="c5">, hasta llegar a
un punto en que se encuentran y este efecto se estabiliza. Puede verse
este gráfico en el anexo (Anexo VI).</span><span class="c15 c5"> </span>

<span class="c5">Finalmente, se analizó la importancia que aportó cada
variable al árbol entrenado con validación cruzada. Como podía
visualizarse en las divisiones del árbol, la edad ha sido el descriptor
de mayor importancia, seguida por el nivel de glucosa y el índice de
masa corporal; en tanto el árbol no ha considerado ninguna otra variable
como importante y estas tres concentraron toda la importancia, con
niveles de 0,7877, 0,16422 y 0,04801, respectivamente. Luego de revisar
estos valores, se volvió a entrenar el árbol haciendo uso de la técnica
de eliminación recursiva, utilizando la herramienta
</span><span class="c5 c6 c12">RFE </span><span class="c3"> de scikit
learn. Tanto al reducir las variables a 3 como a 4, los resultados de
las métricas se han mantenido inalterables, tanto evaluando sobre el
test de validación como el de prueba, mostrando así la importancia
excluyente de la edad, el nivel de glucosa y el bmi como descriptores.
</span>

<span class="c15 c5"></span>

<span class="c36">Conclusión</span>

<span class="c5">En este trabajo, se realizó un proceso desde el
análisis de los datos “crudos” hasta la creación de un árbol de
decisión con validación y poda, pasando por el preprocesamiento y el
análisis de posibles correlaciones. En el camino, debieron
</span><span class="c5">tomarse
diversas</span><span class="c3"> decisiones que fueron afectando el
posible resultado a obtener, como el método de imputación de datos
faltantes, las métricas a priorizar, y el tratamiento de variables
categóricas, así como la selección de features a utilizar para la
creación de los árboles y la selección de hiperparámetros.</span>

<span class="c3">El principal limitante del trabajo ha sido la baja
proporción de casos positivos en el dataset original. Esto dificultó
seriamente la eficiencia de los modelos y, si bien se utilizaron
diferentes estrategias para un correcto balanceo en los conjuntos de
datos y en los pesos del modelo, esta cuestión pudo apreciarse en
algunos niveles bajos en las métricas evaluadas. </span>

<span class="c5">Aún así, resaltamos que fue posible identificar las
variables que mejor
</span><span class="c5">permitieron</span><span class="c5"> predecir el
riesgo de derrame: edad, índice de masa corporal y glucosa en sangre.
Pero, principalmente, destacamos haber logrado
un</span><span class="c5 c12"> alto nivel de
sensibilidad</span><span class="c3"> para detectar potenciales casos de
strokes, gracias al aporte de la estrategia de poda, incluso en los
datos de testeo.</span>

<span class="c5">A pesar de contar con espacio para mejoras,
consideramos que este método permite un buen primer análisis del riesgo
de derrame cerebral que corre una persona, además de proveer una idea
general de qué factores podrían cambiarse para reducir el mismo.</span>

-----

### <span class="c27 c36">Anexos</span>

#### <span class="c13">Anexo I</span>

<span id="t.9410fae68fe4187b396432f1ada25b359850f069"></span><span id="t.0"></span>

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><h3 id="h.dgw2wnirdtvk" class="c4"><span class="c8">stroke</span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-1" class="c4"><span class="c8">No Stroke     </span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-2" class="c4"><span class="c8">Stroke</span></h3></td>
</tr>
<tr class="even">
<td><h3 id="h.dgw2wnirdtvk-3" class="c4"><span class="c8">Promedio BMI</span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-4" class="c4"><span class="c24 c16">28.527915  </span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-5" class="c4"><span class="c24 c16">30.471292</span></h3></td>
</tr>
<tr class="odd">
<td><h3 id="h.dgw2wnirdtvk-6" class="c4"><span class="c8">Promedio Edad</span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-7" class="c4"><span class="c24 c16">41.760451  </span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-8" class="c4"><span class="c24 c16">67.712919</span></h3></td>
</tr>
<tr class="even">
<td><h3 id="h.dgw2wnirdtvk-9" class="c4"><span class="c8">Promedio Glucosa en sangre</span></h3></td>
<td><h3 id="h.dgw2wnirdtvk-10" class="c4"><span class="c16 c24">104.003736 </span></h3></td>
<td><h3 id="h.rqq425qnuu32" class="c4"><span class="c16 c44 c53">134.571388</span></h3></td>
</tr>
</tbody>
</table>

<span class="c5 c6">   </span><span class="c0">Tabla 1: medias de las
variables numéricas para cada grupo</span>

<span class="c0"></span>

<span class="c0"></span>

<span class="c0"></span>

### <span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 557.60px; height: 497.69px;">![](images/image5.png)</span>

<span class="c5 c6">Figura 2: histogramas y distribución de puntos para
las variables numéricas, coloreadas según la presencia de
derrame.</span>

<span class="c19"></span>

<span class="c19"></span>

#### <span class="c13">Anexo II</span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 192.00px; height: 185.28px;">![](images/image10.png)</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 192.00px; height: 185.98px;">![](images/image8.png)</span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 192.00px; height: 185.98px;">![](images/image7.png)</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 192.00px; height: 185.98px;">![](images/image4.png)</span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 192.00px; height: 185.98px;">![](images/image6.png)</span>

<span class="c5 c6">Figuras 3 a 7: gráficos de barras porcentuales de
las variables categóricas, divididas según derrame o no y coloreadas
según los valores de la variable categórica: género, hipertensión si
alguna vez se casaron, tipo de residencia y enfermedad cardíaca</span>

<span class="c19"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13">Anexo III</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 273.00px; height: 188.30px;">![](images/image13.png)</span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 272.64px; height: 191.82px;">![](images/image3.png)</span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c5 c6">Figuras 8 y 9: Boxplots del árbol de semillas
(izquierda), y árbol de validación cruzada (derecha)</span>

<span class="c13"></span>

<span class="c15 c29"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13"></span>

<span class="c13">Anexo IV</span>

<span class="c19"></span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 601.70px; height: 292.00px;">![](images/image9.png)</span>

<span class="c5 c6">Figura 10: Árbol con mejores resultados</span>

<span class="c19"></span>

<span class="c19"></span>

<span class="c19"></span>

<span class="c29 c32">Anexo V</span>

### <span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 296.63px; height: 210.03px;">![](images/image12.png)</span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 292.52px; height: 208.50px;">![](images/image1.png)</span>

### <span class="c5 c6 c54">Figuras 11 y 12:</span>

<span class="c0">Izquierda:  
Árbol sin podar sobre test  
Recall del árbol sin podar: 0.68  
F2 del árbol sin podar: 0.37527593818984545  
Accuracy del árbol sin podar: 0.769155206286837</span>

<span class="c0"></span>

<span class="c0">Derecha:  
Árbol podado sobre test  
Recall del árbol podado: 0.92  
F2 del árbol podado: 0.35384615384615387  
Accuracy del árbol podado: 0.5992141453831041</span>

<span class="c19"></span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 373.50px; height: 247.84px;">![](images/image2.png)</span>

<span class="c5 c6">Figura 13: Accuracy vs alpha en conjuntos de
entrenamiento y validación</span>

### <span class="c27 c36"></span>

### <span class="c27 c36"></span>

### <span class="c27 c36"></span>

### <span class="c27 c36">Bibliografía</span>

<span class="c5">BBC News. (2012, 05 09). </span><span class="c5 c6">Un
dibujo puede mostrar el riesgo de un derrame
cerebral</span><span class="c3">. BBC News Mundo. Retrieved 05 22, 2021,
from
https://www.bbc.com/mundo/noticias/2012/05/120509\_prueba\_dibujo\_derrame\_cerebral\_men</span>

<span class="c5">NIH (National Heart, Lung and Blood Institute). (2021).
</span><span class="c5 c6">Body Mass Index
Table</span><span class="c3">. NIH Body Mass Table. Retrieved 05 15,
2021, from
https://www.nhlbi.nih.gov/health/educational/lose\_wt/BMI/bmi\_tbl.htm</span>

<span class="c5">sklearn documentation.
</span><span class="c5 c6">sklearn Decision Tree
Classifier</span><span class="c3">. scikit learn.
https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html</span>

<span class="c5">sklearn documentation.
</span><span class="c5 c6">sklearn metrics fbeta
score</span><span class="c3">. Scikit Learn.
https://scikit-learn.org/stable/modules/generated/sklearn.metrics.fbeta\_score.html</span>

<span class="c5">sklearn documentation.
</span><span class="c5 c6">Sklearn Post Cost Complexity
Pruning</span><span class="c3">. scikit learn.
https://scikit-learn.org/stable/auto\_examples/tree/plot\_cost\_complexity\_pruning.htm</span>

<span class="c5">sklearn documentation.
</span><span class="c5 c6">Sklearn RFE</span><span class="c3">. scikit
learn.
https://scikit-learn.org/stable/modules/generated/sklearn.feature\_selection.RFE.html</span>

<span class="c3"></span>

<span class="c19"></span>

<div>

<span class="c19"></span>

</div>
