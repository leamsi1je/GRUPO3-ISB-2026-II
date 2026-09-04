# Resumen de Laboratorios — Señales Biomédicas
**Universidad Peruana Cayetano Heredia — Ingeniería Biomédica**

---

## Lab 1 — Introducción con PhysioNet

**Objetivo general:** dar el primer contacto con datos fisiológicos reales, usando la librería `wfdb` para acceder a PhysioNet.

**Contenido y flujo de trabajo:**
- Concepto `DATABASE` (ej. `mitdb`, MIT-BIH Arrhythmia Database) vs. `RECORD` (registro específico, ej. `"100"`).
- Carga de un registro ECG con `wfdb.rdrecord(RECORD, pn_dir=DATABASE)`.
- Exploración de metadatos: `fs` (frecuencia de muestreo), `sig_len`, `n_sig`, `sig_name`, `units`.
- Selección de canal (`record.p_signal[:, CHANNEL]`) y construcción del eje temporal `t[n] = n/fs`.
- Cuatro visualizaciones principales:
  1. ECG completo (todo el registro).
  2. Segmento ECG de `DURATION` segundos.
  3. Histograma de amplitudes.
  4. Representación discreta `x[n]` (muestras individuales con marcadores).
- Estadística básica (media, desviación estándar, mínimo, máximo, rango).
- Conversión del segmento ECG a formato `.wav` (eliminar componente DC → normalizar → convertir a `int16` → guardar) y reproducción/descarga del audio.
- Ejercicios propuestos: cambiar de `RECORD`, cambiar de `CHANNEL`, cambiar `DURATION`, y un "reto final" con un registro distinto (103), incluyendo interpretación de resultados.

**Conceptos clave trabajados:** muestreo (`fs`, `Ts = 1/fs`), estructura de un registro fisiológico, diferencia entre señal biomédica y señal de audio, morfología ECG (ondas P, QRS, T).

---

## Lab 2 — Análisis de señales biomédicas con PhysioNet (dominio tiempo/frecuencia)

**Objetivo general:** analizar tres registros ECG de la base **NSRDB** (ritmo sinusal normal) en los dominios temporal, frecuencial y tiempo-frecuencia.

**Contenido y flujo de trabajo:**
- Parámetros: base `nsrdb`, registros `16265`, `16272`, `16420`; 3600 muestras (10 s) por registro, canal 0.
- Carga robusta de los tres registros (con reintentos) y de sus anotaciones (`wfdb.rdann`, extensión `atr`).
- Exploración de metadatos por registro (fs, número de muestras, canales, unidades).
- Extracción de señales y construcción de ejes temporales para los tres registros.
- Gráficas de amplitud vs. tiempo (dominio temporal) para comparar morfología entre registros.
- **FFT (Transformada Rápida de Fourier):**
  - Cálculo del espectro con y sin componente DC (`x[n] - media`).
  - Comparación visual de ambos espectros.
  - Identificación de la frecuencia dominante (ignorando 0 Hz).
- **STFT (Short-Time Fourier Transform):**
  - Cálculo con `scipy.signal.stft`, usando ventanas distintas por registro (256 muestras para 16265 y 16420; 32 muestras para 16272).
  - Visualización como espectrograma (`pcolormesh`).
- Tabla comparativa final de los tres registros (fs, muestras, canales, amplitud, componente DC).
- Ejercicios propuestos: analizar otro segmento temporal del registro (ej. segundos 10–20), preguntas conceptuales, y un "reto final" con análisis completo de un registro elegido.

**Conceptos clave trabajados:** dominio temporal vs. frecuencial, FFT de una sola cara (`rfft`), efecto de eliminar la componente DC, resolución tiempo-frecuencia (STFT), trade-off entre resolución temporal y frecuencial según el tamaño de ventana (`nperseg`).

---

## Lab 3 — Filtros FIR, IIR y Transformada Z

**Objetivo general:** desarrollar criterio para inspeccionar, caracterizar, filtrar y validar una señal biomédica (no solo aplicar funciones de Python).

**Flujo de trabajo declarado:** señal → inspección → caracterización → análisis temporal → análisis frecuencial → identificación del ruido → selección del filtro → diseño → aplicación → validación → interpretación fisiológica.

**Contenido:**
- Generación de un ECG sintético reproducible con `neurokit2` (`nk.ecg_simulate`, duración 10 s, `fs = 250 Hz`, FC = 70 bpm).

**Ejercicio 1 — Análisis y caracterización:**
- Inspección de un archivo WAV (o la señal sintética como respaldo): fs, número de muestras, shape, dtype, duración.
- Análisis temporal y FFT (magnitud normalizada por N).
- Identificación de componentes dominantes y su relación con la frecuencia cardíaca (70 bpm ≈ 1.17 Hz).

**Ejercicio 2 — Diseño y comparación de filtros FIR e IIR:**
- **FIR:** `signal.firwin` (pasa-bajos, ej. `numtaps=101`, `cutoff=40 Hz`).
- **IIR:** `signal.butter` en forma SOS (ej. orden 4, `cutoff=40 Hz`), aplicado con `sosfiltfilt` para evitar distorsión de fase.
- Aplicación de ambos filtros (`filtfilt` para FIR, `sosfiltfilt` para IIR) y comparación visual con la señal original.
- Respuesta en frecuencia con `freqz` (FIR) y `sosfreqz` (IIR), en dB.
- Tabla comparativa conceptual FIR vs. IIR (realimentación, estabilidad, fase lineal, orden, costo computacional).

**Ejercicio 3 — Señal contaminada:**
- Construcción de `x[n] = ECG[n] + A·sin(2π·f_noise·t)` (ej. `A=0.20`, `f_noise=35 Hz`).
- FFT para localizar la interferencia (pico entre 25–45 Hz).
- Diseño de un filtro pasa-bajos Butterworth (`cutoff=25 Hz`, orden 4, SOS) para recuperar la señal.
- **Validación cuantitativa:** MSE, RMSE y SNR (antes/después del filtrado).
- **Validación biomédica (cualitativa):** conservación del QRS, la frecuencia cardíaca aproximada y la morfología general.

**Análisis de errores de diseño:** demostración de al menos dos fallos típicos —p. ej. frecuencia de corte demasiado baja (distorsiona/aplana el QRS) y filtrado sin compensar fase (`sosfilt` vs. `sosfiltfilt`, que introduce desplazamiento de fase).

**Cierre:** preguntas integradoras sobre por qué no conviene eliminar todas las frecuencias altas, cómo se determina la frecuencia de corte, relación entre fs y frecuencia máxima observable (Nyquist), y diferencias fundamentales entre FIR e IIR. Incluye rúbrica de evaluación (20 puntos: análisis, diseño de filtro, implementación, validación, interpretación).

**Conceptos clave trabajados:** relación Fourier–Transformada Z, diseño de filtros FIR/IIR, filtrado sin distorsión de fase (`filtfilt`/`sosfiltfilt`), métricas de validación (MSE, RMSE, SNR), criterio de selección de frecuencia de corte a partir del contenido espectral real de la señal.

---

## Progresión general de los tres laboratorios

| Lab | Enfoque principal | Herramientas clave | Salida esperada |
|---|---|---|---|
| 1 | Acceso y exploración básica de una señal ECG real | `wfdb`, `matplotlib`, `scipy.io.wavfile` | Gráficas, histograma, estadísticas, archivo WAV |
| 2 | Comparación de señales en dominio tiempo/frecuencia | `wfdb`, `numpy.fft`, `scipy.signal.stft` | Espectros FFT, espectrogramas STFT, tabla comparativa |
| 3 | Diseño y validación de filtros digitales | `neurokit2`, `scipy.signal` (FIR/IIR), métricas MSE/RMSE/SNR | Filtros diseñados y justificados, señal recuperada, validación cuantitativa y biomédica |

En conjunto, la secuencia va de **explorar** una señal biomédica real (Lab 1), a **caracterizarla en distintos dominios** (Lab 2), hasta **procesarla activamente mediante filtros** con criterio técnico y validación (Lab 3).
