# Análisis de Costos de Equipamiento - Proyecto de Construcción - Prueba tecnica Cientifico de Datos

## Descripción

Este proyecto realiza un análisis predictivo de costos para dos tipos de equipamiento esencial en un proyecto de construcción de 36 meses. Utiliza técnicas de series temporales para pronosticar precios de materias primas y estimar costos totales.

## Objetivo

Estimar los costos de dos tipos de equipamiento esencial para un proyecto de construcción con duración de 36 meses. Estos equipamientos están compuestos por diferentes proporciones de tres materias primas (X, Y, Z), cuyos precios son variables en el tiempo.

## Estructura del Proyecto

```
Prueba tecnica 1/
│
├── Datos/
│   ├── X.csv                          # Precios históricos materia prima X
│   ├── Y.csv                          # Precios históricos materia prima Y
│   └── Z.csv                          # Precios históricos materia prima Z
│
├── Resultados/
│
├── Caso/
│   └── Caso consultoria 1.pdf         # Documento con el caso de negocio
│
├── analisis_costos_equipamiento.ipynb  # Jupyter Notebook principal
├── REPORTE_TECNICO.md                   # Reporte técnico
├── requirements.txt                     # Dependencias Python
└── README.md                            # Este archivo
```

## Instalación y Uso

### Requisitos Previos
- Python 3.8 o superior
- pip (gestor de paquetes de Python)

### Paso 1: Instalar Dependencias

```bash
pip install -r requirements.txt
```

### Paso 2: Ejecutar el Análisis

```bash
jupyter notebook analisis_costos_equipamiento.ipynb
```


### Paso 3: Revisar Resultados

Los resultados se generarán automáticamente en la carpeta `Resultados/`:
- Gráficos (PNG)
- Tablas de pronósticos (CSV)

## Metodología

### 1. **Carga y Limpieza de Datos**
- Normalización de formatos heterogéneos
- Manejo de separadores y decimales diferentes
- Interpolación de datos faltantes

### 2. **Análisis Exploratorio (EDA)**
- Estadísticas descriptivas
- Visualización de series temporales
- Detección de tendencias y estacionalidad

### 3. **Modelado Predictivo**
Modelos implementados:
- **ARIMA**: Modelo autorregresivo integrado de media móvil
- **Exponential Smoothing**: Suavizamiento exponencial con componentes de tendencia y estacionalidad
- **Moving Average**: Promedio móvil con tendencia (baseline)

### 4. **Cálculo de Costos**
- **Equipamiento 1**: 20% X + 80% Y
- **Equipamiento 2**: 33.33% X + 33.33% Y + 33.33% Z

### 5. **Análisis de Escenarios**
- Escenario Optimista (precios bajos)
- Escenario Base (pronóstico esperado)
- Escenario Pesimista (precios altos)

## Resultados Clave

*Los resultados específicos se generan tras ejecutar el código. Consultar `REPORTE_TECNICO.md` para análisis detallado.*

## Tecnologías Utilizadas

- **Python 3.8+**
- **Pandas & NumPy**: Manipulación de datos
- **Matplotlib & Seaborn**: Visualización
- **Statsmodels**: Modelos de series temporales (ARIMA, Exponential Smoothing)
- **Jupyter**: Entorno interactivo de desarrollo

## Documentación

Para un análisis completo y detallado, consultar:
- **[REPORTE_TECNICO.md](REPORTE_TECNICO.md)**: Reporte técnico con:
  - Supuestos y limitaciones
  - Metodología paso a paso
  - Resultados cuantitativos
  - Recomendaciones estratégicas
  - Mejoras futuras


## Contacto

**Autor:** Cocu Alejandro Iglesias Osorio
**Fecha:** Enero 2026  
**Organización:** DataKnow

---

