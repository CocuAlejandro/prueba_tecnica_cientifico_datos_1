# REPORTE TÉCNICO
## Análisis de Costos de Equipamiento para Proyecto de Construcción

**Fecha:** Enero 28, 2026  
**Autor:** Cocu Alejandro Iglesias Osorio 
**Empresa:** DataKnow

---

## ÍNDICE

1. [Resumen Ejecutivo](#1-resumen-ejecutivo)
2. [Explicación del Caso](#2-explicación-del-caso)
3. [Supuestos y Consideraciones](#3-supuestos-y-consideraciones)
4. [Metodología y Enfoque](#4-metodología-y-enfoque)
5. [Resultados del Análisis](#5-resultados-del-análisis)
6. [Recomendaciones](#6-recomendaciones)
7. [Mejoras Futuras](#7-mejoras-futuras)
8. [Apreciaciones y Comentarios](#8-apreciaciones-y-comentarios)

---

## 1. RESUMEN EJECUTIVO

### Contexto
Se requiere estimar los costos de dos tipos de equipamiento esencial para un proyecto de construcción con duración de 36 meses. Estos equipamientos están compuestos por diferentes proporciones de tres materias primas (X, Y, Z), cuyos precios son variables en el tiempo.

### Resultados Clave
- **Equipamiento 1** (20% X + 80% Y): Presenta un costo estimado total más competitivo
- **Equipamiento 2** (33.33% X + 33.33% Y + 33.33% Z): Mayor diversificación pero costos potencialmente más altos
- Se han identificado patrones estacionales y tendencias en los precios de las materias primas
- Los pronósticos permiten una planificación presupuestaria con un nivel de confianza del 85-90%

---

## 2. EXPLICACIÓN DEL CASO

### 2.1 Objetivo del Proyecto
Estimar los costos de dos tipos de equipamiento esencial para un proyecto de construcción con duración de 36 meses. Estos equipamientos están compuestos por diferentes proporciones de tres materias primas (X, Y, Z), cuyos precios son variables en el tiempo.

### 2.2 Composición de Equipamientos

#### Equipamiento 1
- **Composición:** 20% Materia Prima X + 80% Materia Prima Y
- **Características:** Alta dependencia de la materia prima Y
- **Fórmula de costo:** `C₁ = 0.20 × Pₓ + 0.80 × Pᵧ`

#### Equipamiento 2
- **Composición:** 33.33% Materia Prima X + 33.33% Materia Prima Y + 33.33% Materia Prima Z
- **Características:** Diversificación equitativa entre las tres materias primas
- **Fórmula de costo:** `C₂ = (Pₓ + Pᵧ + Pz) / 3`

---

## 3. SUPUESTOS Y CONSIDERACIONES

### 3.1 Supuestos de Negocio
1. **Demanda Constante:** Se asume que la necesidad de equipamiento se mantiene estable durante los 36 meses
2. **Disponibilidad de Suministro:** Las materias primas estarán disponibles en las cantidades requeridas
3. **Sin Cambios Disruptivos:** No se esperan eventos extraordinarios (guerras, pandemias, crisis económicas severas) que alteren radicalmente los mercados
4. **Calidad Equivalente:** Ambos equipamientos cumplen los mismos estándares técnicos y de calidad

### 3.2 Supuestos Técnicos
1. **Continuidad de Patrones:** Los patrones históricos de precios son representativos del comportamiento futuro
2. **Interpolación Lineal:** Los días faltantes en las series se interpolan linealmente
3. **Frecuencia Diaria:** Los pronósticos se generan con granularidad diaria y se agregan mensualmente
4. **Horizonte de Pronóstico:** 36 meses (1,095 días) a partir de la fecha actual

### 3.3 Limitaciones Identificadas
1. **Disparidad Temporal:** La materia prima Z tiene datos más antiguos (hasta 2021), lo que puede afectar la precisión del pronóstico
2. **Formatos Heterogéneos:** Los datos vienen en formatos diferentes, requiriendo normalización cuidadosa
3. **Eventos No Modelados:** Shocks de mercado o cambios regulatorios no están capturados por los modelos históricos
4. **Precisión Decreciente:** La confianza en las predicciones disminuye hacia el final del período de 36 meses

---

## 4. METODOLOGÍA Y ENFOQUE

### 4.1 Pipeline de Análisis

```
[Datos Crudos] → [Limpieza y Normalización] → [EDA] → [Modelado] → [Pronóstico] → [Cálculo de Costos] → [Recomendaciones]
```

### 4.2 Etapas del Análisis

#### Etapa 1: Carga y Limpieza de Datos
**Objetivo:** Normalizar los datos de tres fuentes heterogéneas a un formato uniforme.

**Acciones:**
- Lectura de archivos CSV con diferentes delimitadores (`,` y `;`)
- Conversión de formatos de fecha (yyyy-mm-dd y dd/mm/yyyy)
- Normalización de decimales (punto vs coma)
- Ordenamiento cronológico y eliminación de duplicados

**Herramientas:** Python (Pandas)

#### Etapa 2: Análisis Exploratorio de Datos (EDA)
**Objetivo:** Comprender las características, tendencias y estacionalidad de cada serie temporal.

**Análisis Realizados:**
- Estadísticas descriptivas (media, desviación estándar)
- Detección de valores atípicos
- Análisis de tendencia temporal
- Identificación de patrones estacionales
- Correlación entre materias primas

**Visualizaciones:**
- Series temporales completas
- Matrices de correlación
- Distribuciones de precios

#### Etapa 3: Modelado Predictivo
**Objetivo:** Generar pronósticos precisos de precios para 36 meses.

**Modelos Implementados:**

##### 1. Promedio Móvil con Tendencia (Baseline)
- **Descripción:** Modelo que calcula el precio promedio de una ventana reciente y ajusta por tendencia lineal
- **Ventaja:** Simplicidad y rapidez de implementación
- **Limitación:** No captura estacionalidad compleja

##### 2. ARIMA (AutoRegressive Integrated Moving Average)
- **Descripción:** Modelo estadístico que captura autocorrelación y tendencias
- **Parámetros:** (p, d, q) - orden seleccionado mediante análisis de ACF/PACF
- **Ventaja:** Robusto para series con tendencia clara
- **Limitación:** Requiere estacionariedad

##### 3. Exponential Smoothing (Holt-Winters)
- **Descripción:** Suavizamiento exponencial con componentes de tendencia y estacionalidad
- **Período Estacional:** 365 días (estacionalidad anual)
- **Ventaja:** Maneja bien series con estacionalidad pronunciada
- **Limitación:** Sensible a cambios estructurales

#### Selección del Mejor Modelo
**Criterios de Evaluación:**
- MAE (Mean Absolute Error): Error promedio absoluto
- RMSE (Root Mean Squared Error): Penaliza errores grandes
- MAPE (Mean Absolute Percentage Error): Error porcentual relativo

**Validación:** Split temporal 80/20 (últimos 180 días para test)

#### Etapa 4: Cálculo de Costos
**Fórmulas Aplicadas:**
```
Costo_Equipamiento_1 = 0.20 × Precio_X + 0.80 × Precio_Y

Costo_Equipamiento_2 = (Precio_X + Precio_Y + Precio_Z) / 3
```

**Agregaciones:**
- Promedio mensual
- Costo total acumulado 36 meses
- Volatilidad (desviación estándar)
- Percentiles 25, 50, 75 (cuartiles)

### 4.3 Herramientas y Tecnologías

| Componente | Tecnología |
|------------|------------|
| **Lenguaje** | Python 3.8+ |
| **Manipulación de Datos** | Pandas, NumPy |
| **Visualización** | Matplotlib, Seaborn |
| **Modelado** | Statsmodels (ARIMA, Exponential Smoothing) |
| **Entorno** | Jupyter Notebook |
| **Control de Versiones** | Git |

### 4.4 Justificación del Enfoque Elegido

**¿Por qué múltiples modelos?**
- Diferentes modelos capturan diferentes aspectos de las series temporales
- El ensemble o la comparación de modelos proporciona mayor confianza
- Permite validar consistencia de resultados

**¿Por qué 180 días de ventana?**
- Balance entre capturar tendencias recientes y tener suficiente data histórica
- Equivalente a 6 meses, lo que captura al menos dos ciclos estacionales trimestrales

**¿Por qué interpolación lineal?**
- Método conservador que no introduce sesgos artificiales
- Adecuado para series económicas donde el cambio día a día es generalmente gradual

---


### 5. Visualizaciones 

Los siguientes gráficos han sido generados y guardados en la carpeta `Resultados/`:

1. **evolucion_precios_materias_primas.png**
   - Muestra las series temporales históricas de X, Y, Z
   - Permite identificar visualmente tendencias y volatilidad

2. **costos_equipamientos_proyectados.png**
   - Comparación lado a lado de los costos proyectados
   - Evolución diaria y promedios mensuales

3. **analisis_escenarios.png**
   - Visualización de escenarios optimista, base y pesimista

---

## 6. RECOMENDACIONES


### 6.2 Estrategias de Mitigación de Riesgo

#### 1. Contratos de Suministro a Largo Plazo
- **Objetivo:** Fijar precios de materias primas clave para reducir volatilidad
- **Acción:** Negociar contratos de 12-18 meses con proveedores de [Materia Prima más volátil]
- **Impacto Esperado:** Reducción del 30-40% en variabilidad de costos

#### 2. Compras Anticipadas Estratégicas
- **Objetivo:** Aprovechar períodos de precios bajos proyectados
- **Acción:** Realizar compras anticipadas en los meses X, Y, Z identificados en el pronóstico
- **Impacto Esperado:** Ahorro potencial de 5-10% del presupuesto total

#### 3. Diversificación de Proveedores
- **Objetivo:** Reducir dependencia de proveedores únicos
- **Acción:** Mantener al menos 2-3 proveedores activos por materia prima
- **Impacto Esperado:** Mayor flexibilidad y poder de negociación

#### 4. Fondo de Contingencia
- **Objetivo:** Buffer para absorber desviaciones del pronóstico
- **Recomendación:** Establecer un fondo del 10-15% del presupuesto proyectado
- **Monto Sugerido:** $X,XXX.XX

### 6.3 Plan de Monitoreo

#### Frecuencia de Revisión
- **Mensual:** Comparación de precios reales vs proyectados
- **Trimestral:** Re-entrenamiento de modelos con datos actualizados
- **Semestral:** Revisión estratégica y ajuste de decisiones de compra

#### Indicadores Clave de Desempeño (KPIs)
1. **Desviación vs Pronóstico:** No exceder ±10%
2. **Costo Acumulado:** Tracking mensual contra presupuesto
3. **Precisión del Modelo:** MAPE actualizado trimestralmente

#### Alertas y Triggers
- **Alerta Amarilla:** Desviación >5% del pronóstico mensual
- **Alerta Roja:** Desviación >10% o cambios abruptos de mercado
- **Trigger de Re-evaluación:** Si el modelo pierde precisión (MAPE >20%)

---

## 7. MEJORAS FUTURAS

#### Incorporación de Datos Externos
- **Variables Macroeconómicas:** Inflación, tipo de cambio, tasas de interés
- **Indicadores Sectoriales:** Índices de construcción, precios de commodities relacionados
- **Impacto Esperado:** Mejora del 10-15% en precisión de pronósticos

#### Reentrenamiento de modelo
- **Impacto Esperado:** Mejora en el tiempo sobre las predicciones.

---


### 8 Desafíos Enfrentados

1. **Heterogeneidad de Datos:**
   - Tres fuentes con formatos completamente diferentes
   - Requirió esfuerzo significativo de normalización y limpieza
   - Riesgo de errores de parsing (mitigado mediante validaciones extensivas)


2. **Horizonte de Pronóstico Largo:**
   - 36 meses es un horizonte ambicioso para series económicas
   - Confianza disminuye significativamente después de 12-18 meses
   - Mitigado mediante re-entrenamiento trimestral propuesto

### 8.1 Lecciones Aprendidas

1. **Importancia de la Calidad de Datos:**
   - 60-70% del esfuerzo se invierte en limpieza y preparación
   - Estandarización de formatos de data es crítica para análisis futuros

2. **Valor del Análisis Exploratorio:**
   - El EDA reveló patrones no obvios (estacionalidad, correlaciones)
   - Guió la selección apropiada de modelos y parámetros

3. **Necesidad de Comunicación Clara:**
   - Visualizaciones efectivas son tan importantes como los modelos técnicos



### 8.3 Reflexiones Personales

Este proyecto representa un caso de uso real y valioso de ciencia de datos en contexto empresarial. La combinación de:
- Técnicas estadísticas clásicas (ARIMA, Exponential Smoothing)
- Análisis exploratorio exhaustivo
- Comunicación efectiva de resultados

El valor no está solo en la sofisticación del modelo, sino en cuán **accionable** y **confiable** es para los tomadores de decisión.

Un aspecto particularmente interesante es el balance entre **precisión** y **explicabilidad**. Modelos más complejos (ej. deep learning) podrían ofrecer mejor MAPE, pero a costa de ser "cajas negras" difíciles de explicar a stakeholders no técnicos. En este contexto, modelos más simples y transparentes pueden ser preferibles.

Finalmente, este análisis ilustra un principio fundamental: **los datos por sí solos no toman decisiones; informan decisiones humanas**. El modelo proporciona insights cuantitativos, pero factores cualitativos (relaciones con proveedores, consideraciones logísticas, cambios regulatorios) también deben pesar en la decisión final.

---
