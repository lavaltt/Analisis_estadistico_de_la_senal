# Análisis estadístico de la señal
## Descripción
Este proyecto realiza un análisis estadístico de una señal biomédica (ECG) obtenida de PhysioNet. Incluye visualización de la señal, cálculos estadísticos, generación de histogramas, y la introducción de diferentes tipos de ruido (gaussiano, impulso y artefacto) con normalización en dos escenarios distintos (SNR positivo y negativo).
### Detalles de la señal
La señal utilizada en este proyecto proviene de PhysioNet y está almacenada en un archivo con extensión .dat y .hea. En este proyecto, se elige una señal multicanal, que refleja los efectos de ciertos farmácos como dofetilida, moxifloxacino, mexiletina y otros, en un ECG. Dichos medicamentos actuan en la prolongación del intervalo QT.
Teniendo en cuenta las características de la señal,se toma específicamente el canal 12 para su análisis. Se realizan diversos cálculos y gráficos para proporcionar una comprensión integral de la señal y los efectos del ruido en ella.

## Instrucciones para el uso del código
### Prerrequisitos
Antes de ejecutar el código, asegúrate de tener instaladas las siguientes bibliotecas de Python:
1. wfdb
2. matplotlib
3. numpy
4. statistics
   
Pueden instalarse haciendo uso del comando 'pip install', seguido del nombre de la libreria, en la consola del compilador.

### Ejecución del Código
#### Carga de la Señal

Asegúrate de que los archivos .dat y .hea de la señal estén en la misma carpeta que el proyecto de Python. El código carga la señal utilizando la biblioteca wfdb.

#### Menú Principal

Al ejecutar el código, se presenta un menú con varias opciones:

Opción 1: Visualizar los datos y gráficos de la señal original.
Opción 2: Calcular y mostrar estadísticas descriptivas (media, desviación estándar y coeficiente de variación) usando fórmulas programadas y funciones de la biblioteca statistics.
Opción 3: Generar y mostrar un histograma de la señal utilizando funciones de Python y programando las fórmulas manualmente.
Opción 4: Contaminar la señal con ruido gaussiano y visualizar los resultados para dos casos de normalización (SNR positivo y negativo).
Opción 5: Contaminar la señal con ruido impulso y visualizar los resultados para dos casos de normalización (SNR positivo y negativo).
Opción 6: Contaminar la señal con ruido artefacto y visualizar los resultados para dos casos de normalización (SNR positivo y negativo).

#### Seleccionar una Opción

Ingresa el número de la opción deseada y sigue las instrucciones adicionales que se presenten en pantalla. Por ejemplo, algunas opciones requieren que elijas entre cálculos manuales o automáticos, o entre diferentes casos de normalización.

## Cálculos estadísticos
Para los cálculos por medio de bibliotecas de python, simplemente se utilizan las funciones predeterminadas que hacen internamente el cálculo. 

```python
media = stt.mean(a)
```
a es el canal elegido de la señal multicanal descrita anteriomente. 
Se logró determinar que ambos métodos (funciones de python y programando fórmulas) proporcionan los mismos resultados. 

### Cálculo programando fórmulas
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

## Relación señal-ruido(SNR)
El SNR (Signal-to-Noise Ratio) es una medida que compara el nivel de una señal deseada con el nivel del ruido de fondo. Se expresa en decibelios (dB) y se calcula como:

*SNR=10⋅log_10(Pruido/Psenal)

La P hace referencia a la potencia que se obteien de la siguiente manera: 

### Interpretación
-SNR Positivo: Indica que la potencia de la señal es mayor que la del ruido, lo que significa que la señal es claramente distinguible del ruido.

-SNR Negativo: Indica que la potencia del ruido es mayor que la de la señal, haciendo más difícil distinguir la señal del ruido.

Por ejemplo, para la contaminación con ruido Gaussiano, se realizaron dos normalizaciones tras la generación del ruido, esto con el fin de manipular el ruido para realizar un análisis más óptimo del SNR. 
La normalización se realiza a partir de una regla de 3, con la amplitud del ruido generado y la amplitud en que deseamos dejarlo, de la siguiente manera:
```python
ruidoGN = (ruido_gaussiano*0.3)/4
```
Es decir, el ruido generado tiene una amplitud de 4 y se disminuyó a 0.3.
Para este caso, se obtuvo una SNR = 11.04 dB. Esto quiere decir que la señal es mucho mayor que el ruido y puede observar sin mayor dificultad, la gráfica de la señal con el ruido nos permite corroborarlo. 

Por el lado contrario, al realizar una segunda normalización, dejando el ruido con una amplitud de 1.5, se cálculo un SNR = -2.9. Indicando que el ruido es mayor y no permite visualizar la señal correctamente. La señal se observa a continuación. 


