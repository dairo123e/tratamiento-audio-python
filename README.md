# Tratamiento de audio en Python

Proyecto académico desarrollado para la experiencia de aprendizaje **Sonido**, perteneciente al CADI **Percepción Computacional** de la Universidad de Cundinamarca.

## Integrantes

- Dairo Enrique Contreras Quintana
- Stiven David Álvarez Olmos

## Gestora del conocimiento

Mónica María Fonseca Vigoya

## Descripción del proyecto

Este proyecto presenta el desarrollo de una solución práctica en Python para reducir el ruido de fondo y mejorar las condiciones de reproducción de una grabación de voz.

El procedimiento fue implementado en Google Colab y documenta las etapas de captura, caracterización, preprocesamiento, tratamiento, análisis y exportación de una señal de audio.

La grabación utilizada contenía ruido ambiental al comienzo y durante algunas pausas del discurso. Para abordar esta problemática se aplicaron diferentes técnicas de procesamiento digital de señales, procurando reducir las interferencias sin afectar la comprensión y naturalidad de la voz.

## Problemática abordada

Las grabaciones obtenidas mediante micrófonos convencionales pueden incorporar ruido producido por el ambiente, vibraciones, dispositivos cercanos o sonidos transitorios.

En el audio utilizado se identificó un ruido fuerte antes del comienzo de la voz y otras interferencias durante las pausas. Inicialmente se probó un perfil de ruido basado en el primer segundo de la grabación. Sin embargo, este segmento no representaba adecuadamente todos los ruidos presentes en el archivo.

Por esta razón, se ajustó el procedimiento mediante:

- Eliminación del ruido anterior al comienzo de la voz.
- Reducción no estacionaria del ruido.
- Aplicación de una puerta de ruido suave.
- Filtrado de componentes de baja frecuencia.
- Normalización de la amplitud de la señal.

## Objetivo general

Desarrollar y documentar una solución en Python para reducir el ruido de fondo y mejorar las condiciones de reproducción de una grabación de voz, conservando la información principal del mensaje.

## Procesamiento realizado

El tratamiento de la señal incluyó las siguientes etapas:

1. Carga del archivo de audio original.
2. Identificación de sus características técnicas.
3. Conversión de estéreo a mono.
4. Remuestreo de 48.000 Hz a 22.050 Hz.
5. Identificación de silencios y regiones de baja energía.
6. Eliminación del ruido fuerte anterior al habla.
7. Reducción no estacionaria del ruido de fondo.
8. Aplicación de una puerta de ruido durante las pausas.
9. Aplicación de un filtro Butterworth paso alto de 80 Hz.
10. Normalización de la amplitud máxima a 0,95.
11. Comparación mediante formas de onda y espectrogramas.
12. Cálculo de métricas antes y después del tratamiento.
13. Exportación y verificación del audio procesado.

## Características del audio original

| Característica | Resultado |
|---|---:|
| Nombre del archivo | Grabacion.wav |
| Formato | WAV |
| Tipo de señal | Estéreo |
| Número de canales | 2 |
| Muestras por canal | 1.439.744 |
| Frecuencia de muestreo | 48.000 Hz |
| Duración | 29,99 segundos |
| Tipo de dato | float32 |

## Configuración del tratamiento

### Reducción no estacionaria

La reducción de ruido se realizó considerando que las interferencias cambiaban durante la grabación.

Parámetros principales:

- Reducción proporcional: `0.80`
- Modo estacionario: `False`
- Constante temporal: `1.0` segundo
- Suavizado frecuencial: `300 Hz`
- Suavizado temporal: `80 ms`

### Puerta de ruido

Se aplicó una puerta de ruido suave para reducir las interferencias presentes durante las pausas.

- Umbral RMS: `0.00970509`
- Atenuación durante las pausas: `85 %`
- Amplitud conservada durante las pausas: `15 %`

### Filtro paso alto

Se utilizó un filtro digital con las siguientes características:

- Tipo: Butterworth paso alto
- Frecuencia de corte: `80 Hz`
- Orden del filtro: `4`
- Implementación: secciones de segundo orden
- Método utilizado: `sosfiltfilt`

### Normalización

La amplitud máxima antes de la normalización era de `0.379295`.

La señal fue normalizada hasta alcanzar una amplitud máxima de `0.950000`, conservando un margen de seguridad frente al límite digital de `1.0`.

## Resultados obtenidos

| Métrica | Audio original | Audio procesado |
|---|---:|---:|
| Duración | 29,99 s | 28,99 s |
| Frecuencia de muestreo | 22.050 Hz | 22.050 Hz |
| Energía RMS | 0,072460 | 0,081529 |
| Nivel RMS | -22,80 dBFS | -21,77 dBFS |
| Amplitud máxima | 0,694983 | 0,950000 |

El aumento de la energía RMS y del nivel RMS no representa necesariamente un incremento del ruido. Este cambio se relaciona principalmente con la normalización aplicada al final del tratamiento.

La comparación auditiva permitió identificar una reducción considerable de los ruidos de fondo, especialmente durante las pausas. La voz permaneció comprensible y el mensaje hablado se conservó completo.

Las formas de onda y los espectrogramas mostraron regiones de menor energía durante los silencios. Sin embargo, permaneció parcialmente una interferencia fuerte superpuesta con la voz al comienzo de la grabación. Esta interferencia no se eliminó completamente porque una reducción más agresiva podía afectar la inteligibilidad y naturalidad del mensaje.

## Resultado final exportado

El archivo procesado presenta las siguientes características:

- Nombre: `audio_procesado_Dairo_Contreras.wav`
- Formato: WAV
- Tipo de señal: mono
- Frecuencia de muestreo: 22.050 Hz
- Duración: 28,99 segundos
- Cantidad de muestras: 639.333
- Amplitud máxima verificada: 0,949982

El archivo exportado fue leído y reproducido nuevamente para comprobar su integridad y verificar que el procesamiento se conservara correctamente.



