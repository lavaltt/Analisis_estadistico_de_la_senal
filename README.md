# Análisis estadístico de la señal
## Descripción
Este proyecto realiza un análisis estadístico de una señal biomédica (ECG) obtenida de PhysioNet.[^1^].
Incluye visualización de la señal, cálculos estadísticos, generación de histogramas, y la introducción de diferentes tipos de ruido (gaussiano, impulso y artefacto) con normalización en dos escenarios distintos (SNR positivo y negativo).
### Detalles de la señal
La señal utilizada en este proyecto proviene de PhysioNet y está almacenada en un archivo con extensión .dat y .hea. En este caso, se elige una señal multicanal, que refleja los efectos de ciertos farmácos como dofetilida, moxifloxacino, mexiletina y otros, en un ECG. Dichos medicamentos actuan en la prolongación del intervalo QT.
Teniendo en cuenta las características de la señal,se toma específicamente el canal 12 para su análisis. Se realizan diversos cálculos y gráficos para proporcionar una comprensión integral de la señal y los efectos del ruido en ella.

![Señal ECG](https://github.com/lavaltt/An-lisis-estad-stico-de-la-se-al/blob/main/se%C3%B1al%20ecg.png?raw=true)

*Señal ECG elegida para realizar su análisis.(Gráfica realizada en el código).*
#### Descarga de una señal desde PhysioNet

1. Acceder a PhysioNet:
* Ir al sitio web de PhysioNet.[^1^]
  
2. Seleccionar la Base de Datos:
* Presionar el botón data del menú principal y navegar a través de las bases de datos disponibles. Seleccionar una que sea adecuada para el análisis deseado.
(Por ejemplo, la que fue elegida para este proyecto es ECG Effects of Dofetilide, Moxifloxacin, Dofetilide+Mexiletine, Dofetilide+Lidocaine and Moxifloxacin+Diltiazem).
  
3. Descargar los Archivos:
* Descargar los archivos .dat y .hea correspondientes a la señal de interés.
  
4. Guardar los Archivos:
* Guardar los archivos descargados en el mismo directorio donde se encuentra el proyecto de python.

## Instrucciones para el uso del código
El archivo Lab1.zip, contiene el código generado en python y la señal elegida en las extensiones requeridas. 
Recuerde guardar en esta carpeta su nueva señal, si desea probar con otra diferente. 

### Prerrequisitos
Antes de ejecutar el código, asegúrese de tener instaladas las siguientes bibliotecas de Python:
1. wfdb
2. matplotlib
3. numpy
4. statistics
   
*Nota: Las librerias pueden instalarse haciendo uso del comando 'pip install', seguido del nombre de la libreria, en la consola del compilador.*

### Ejecución del Código
#### Carga de la Señal

Verifique que los archivos .dat y .hea de la señal estén en la misma carpeta que el proyecto de Python. El código carga la señal utilizando la biblioteca wfdb.

#### Menú Principal

Al ejecutar el código, se presenta un menú con varias opciones:

* Opción 1: Visualizar los datos y gráficos de la señal original.
* Opción 2: Calcular y mostrar estadísticas descriptivas (media, desviación estándar y coeficiente de variación) usando fórmulas programadas y funciones de la biblioteca statistics.
* Opción 3: Generar y mostrar un histograma de la señal utilizando funciones de Python y programando las fórmulas manualmente.
* Opción 4: Contaminar la señal con ruido gaussiano y visualizar los resultados para dos casos de normalización (SNR positivo y negativo).
* Opción 5: Contaminar la señal con ruido impulso y visualizar los resultados para dos casos de normalización (SNR positivo y negativo).
* Opción 6: Contaminar la señal con ruido artefacto y visualizar los resultados para dos casos de normalización (SNR positivo y negativo).

#### Seleccionar una Opción

Ingrese el número de la opción deseada y siga las instrucciones adicionales que se presenten en la consola. Por ejemplo, algunas opciones requieren que elija entre cálculos manuales o automáticos, o entre diferentes casos de normalización.

## Cálculos estadísticos
Para los cálculos por medio de bibliotecas de python, simplemente se utilizan las funciones predeterminadas que hacen internamente el cálculo. 

```python
media = stt.mean(a)
```
'a' es el canal elegido de la señal multicanal descrita anteriomente. 
Se logró determinar que ambos métodos (funciones de python y programando fórmulas) proporcionan los mismos resultados. 

### Cálculo programando fórmulas
Para esta sección se tuvieron en cuenta las fórmulas matemáticas para el cálculo de estos parámetros, como se indica en [^4^] .
#### Media
Sumar todos los valores de la señal y dividir por el número total de muestras.

```python
sumatoria = sum(a)
media_0 = sumatoria / datos
```
#### Desviación estándar
Calcular la suma de las diferencias al cuadrado entre cada valor y la media, dividir por el número de muestras menos uno, y tomar la raíz cuadrada del resultado.

```python
sumaD = sum((x - media_0) ** 2 for x in a)
v = sumaD / (datos - 1)
desviacion_0 = math.sqrt(v)
```
#### Coeficiente de variación
Dividir la desviación estándar entre la media.

```python
coeficiente_0 = desviacion_0 / media_0
```
## Histograma y función de probabilidad
El histograma es una representación gráfica de la distribución de un conjunto de datos. Se utiliza para visualizar la frecuencia con la que ocurren diferentes valores en un conjunto de datos. Los histogramas son útiles para entender la forma, dispersión y tendencias de los datos. [^3^] . 

En este proyecto, se realizó el histograma de dos maneras, así como los cálculos estadísticos. La primera, por medio de las librerias de python que continene funciones para realizar este diagrama; y la segunda, de manera más larga, programando por pasos las fórmulas. 

![Histograma](https://github.com/lavaltt/An-lisis-estad-stico-de-la-se-al/blob/main/histograma%20programado.png?raw=true)

*Histograma realizado por medio de bibliotecas de python.*

### Función de probabilidad
La función de probabilidad o función de densidad de probabilidad (PDF) para variables continuas, describe cómo se distribuyen los valores de una variable aleatoria. Es fundamental para entender la naturaleza de los datos y hacer inferencias estadísticas. Se utiliza en modelado de datos, predicción, pruebas de hipótesis, análisis de riesgos y generación de datos sintéticos. La función de probabilidad permite cuantificar la probabilidad de diferentes eventos dentro del rango de los datos observados.[^5^].

![Histograma con función de probabilidad](https://github.com/lavaltt/Analisis_estadistico_de_la_senal/blob/main/histogramafp.jpeg?raw=true)

*Histograma realizado en python con la función de probabilidad.*

En la gráfica generada, la función de probabilidad muestra que la mayoría de los datos se concentran en valores bajos cerca de cero y disminuyen exponencialmente hacia valores más altos, indicando una distribución sesgada a la derecha. La línea azul de la función de probabilidad sigue de cerca la forma del histograma, comenzando alta y disminuyendo gradualmente. Esto refleja que los valores bajos son mucho más comunes, mientras que los valores altos son raros. La normalización de la función de probabilidad asegura que el área total bajo la curva sea igual a uno, permitiendo una interpretación precisa de las probabilidades relativas de diferentes rangos de valores en el conjunto de datos.

## Relación señal-ruido(SNR)
El SNR (Signal-to-Noise Ratio) es una medida que compara el nivel de una señal deseada con el nivel del ruido de fondo.[^2^] .Se expresa en decibelios (dB) y se calcula como:

* SNR=10⋅log_10(Pruido/Psenal)

La P hace referencia a la potencia que se obteien de la siguiente manera: 

* P=(∑|X₁|^2 )/N

### Interpretación
* SNR Positivo: Indica que la potencia de la señal es mayor que la del ruido, lo que significa que la señal es claramente distinguible del ruido.

* SNR Negativo: Indica que la potencia del ruido es mayor que la de la señal, haciendo más difícil distinguir la señal del ruido.

Por ejemplo, para la contaminación con ruido Gaussiano, se realizaron dos normalizaciones tras la generación del ruido, esto con el fin de manipular el ruido para realizar un análisis más óptimo del SNR. 
La normalización se realiza a partir de una regla de 3, con la amplitud del ruido generado y la amplitud en que deseamos dejarlo, de la siguiente manera:
```python
ruidoGN = (ruido_gaussiano*0.3)/4
```
Es decir, el ruido generado tiene una amplitud de 4 y se disminuyó a 0.3.
Para este caso, se obtuvo una SNR = 11.04 dB. Esto quiere decir que la señal es mucho mayor que el ruido y se puede distinguir sin mayor dificultad, la gráfica de la señal con el ruido nos permite corroborarlo. 

![Normalización 1, ruido Gaussiano](https://github.com/lavaltt/An-lisis-estad-stico-de-la-se-al/blob/main/RGcaso1.png?raw=true)

*Gráfica de la señal con la normalización del ruido Gaussiano para un SNR positivo.*

Por el lado contrario, al realizar una segunda normalización, dejando el ruido con una amplitud de 1.5, se cálculo un SNR = -2.9. Indicando que el ruido es mayor y no permite visualizar la señal correctamente. La señal se observa a continuación. 

![Normalización 2, ruido Gaussiano](https://github.com/lavaltt/An-lisis-estad-stico-de-la-se-al/blob/main/RGcaso2.png?raw=true)

*Gráfica de la señal con la normalización del ruido Gaussiano para un SNR negativo.*

[^1^]: https://physionet.org/
[^2^]:Qué es Señal-Ruido. Diccionario Médico. Clínica U. Navarra. (s/f). https://www.cun.es. Recuperado de https://www.cun.es/diccionario-medico/terminos/senal-ruido.
[^3^]: Roberto Behar Gutiérrez, P. G. i. C. (2013). El histograma como un instrumento para la comprensión de las funciones de densidad de probabilidad. Probabilidad Condicionada: Revista de didáctica de la Estadística, ISSN-e 2255-5854, No. 2, 2013, ágs. 229-235.
[^4^]: Hernández, G. J. P. (2016). ELEMENTOS BÁSICOS DE ESTADÍSTICA DESCRIPTIVA PARA EL ANÁLISIS DE DATOS. Fondo Editorial Luis Amigó.
[^5^]:Probability and Statistics for Engineers and Scientists por Ronald E. Walpole, Raymond H. Myers, Sharon L. Myers, y Keying Ye.



