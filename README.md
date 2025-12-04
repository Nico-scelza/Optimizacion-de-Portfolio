# 📈 Optimización Quantamental: CAPM, Shrinkage & CVaR

Este repositorio contiene un motor de **Ingeniería Financiera** diseñado para la gestión profesional de portafolios de inversión. Combina el análisis fundamental (Upside manual) con modelos cuantitativos robustos para la estimación y desglose del riesgo.

A diferencia de los optimizadores básicos, este modelo incorpora **Ledoit-Wolf Shrinkage** para limpiar el ruido estadístico, **CVaR** para proteger contra eventos extremos y una **Suite de Visualización Avanzada** para entender la "fisiología" del riesgo en la cartera.

---

## ⚠️ IMPORTANTE: Instrucciones de Ejecución
El código está estructurado en módulos lógicos que dependen entre sí. Para asegurar el correcto funcionamiento de las variables y gráficos:
1. **NO uses "Run All" (Ejecutar Todo).**
2. Ejecutá las celdas **una por una en orden secuencial** (de arriba hacia abajo).
3. Es fundamental ejecutar el botón **"Ejecutar Optimización"** (en la sección de Frontera Eficiente) *antes* de intentar visualizar los gráficos de análisis avanzado (Heatmap, Underwater Plot, Riesgo Marginal).

---

## 🚀 Características Principales

El notebook (`Optimización de Portfolio.ipynb`) ejecuta un flujo de trabajo institucional:

* **Enfoque Híbrido (Quantamental):** Permite al usuario definir sus propios retornos esperados (Upside) o confiar en el equilibrio del mercado (CAPM).
* **Horizonte Temporal Robusto:** Analiza **10 años de historia** de mercado para capturar ciclos económicos completos, incluyendo crisis (COVID-19, subas de tasas, etc.), evitando el sesgo de recencia.
* **Estadística Robusta:** Reemplaza la covarianza histórica simple por la estimación de **Ledoit-Wolf**, reduciendo errores de estimación.
* **Gestión de Riesgo de Cola:** Optimiza por **CVaR al 95%** (pérdida esperada en escenarios de crisis), ideal para evitar "cisnes negros".
* **Ajuste Argentina:** Incorpora automáticamente el **Riesgo País** (vía scraping) al modelo CAPM para activos locales.

---

## 🔬 Suite de Análisis Visual (NUEVO)
El modelo no solo entrega un número final, sino que ofrece herramientas de diagnóstico profundo:

### 1. Heatmap de Correlaciones
Un mapa de calor interactivo para verificar la diversificación real. Permite detectar si los activos elegidos están "repetidos" (alta correlación) o si realmente ofrecen cobertura entre sí.

### 2. Underwater Plot (Análisis de Drawdown)
Visualiza el "dolor" histórico. Muestra la profundidad de las caídas desde los máximos históricos de cada activo y compara cómo un **Portfolio Equiponderado** hubiese suavizado esas pérdidas en momentos de estrés.

### 3. Contribución Marginal al Riesgo (MCR)
Desglosa qué porcentaje del riesgo total de la cartera proviene de cada activo. Permite identificar activos "tóxicos" que, aunque tengan poco peso en capital, aportan una cantidad desproporcionada de volatilidad.

---

## 📊 Modelado de Retornos (La Visión)

El modelo permite contrastar dos fuentes de retorno para cada activo:

**1. Tasa Teórica (CAPM Ajustado)**
Calcula el retorno de equilibrio exigido por el mercado:  
`E(R) = Rf + β(Rm - Rf) + Spread Riesgo País`
*(El Spread de Riesgo País se aplica automáticamente a activos argentinos).*

**2. Visión del Inversor (Upside)**
Permite ingresar manualmente un **Upside estimado a 5 años**. Si el usuario tiene una tesis de inversión fuerte (ej. "Esta acción va a subir 40%"), el modelo prioriza este input sobre el CAPM.

---

## 🛡️ Modelado de Riesgo (La Ingeniería)

Aquí es donde el modelo se diferencia de las herramientas académicas básicas:

### 📉 Matriz de Covarianza "Shrinkage" (Ledoit-Wolf)
Las matrices de covarianza históricas suelen tener mucho "ruido". Este modelo aplica una técnica de contracción (Shrinkage) para generar portafolios más estables en el tiempo y reducir la sobre-concentración errónea.

### 🌪️ Conditional Value at Risk (CVaR 95%)
Mientras que la Varianza mide volatilidad general, el CVaR responde: *"En el peor 5% de los casos, ¿cuánto espero perder?"*. El optimizador busca minimizar estas pérdidas catastróficas.

---

## ⚙️ Escenarios de Optimización

El algoritmo resuelve numéricamente tres problemas de optimización distintos:

1.  **⭐ Máximo Sharpe:** La mejor relación Retorno/Riesgo.
2.  **💎 Mínima Varianza:** El portafolio con menor volatilidad global.
3.  **🛡️ Mínimo CVaR:** El portafolio más defensivo ante eventos de cola.

---

## 🧰 Guía de Uso

1.  **Ejecutar:** Abrí el notebook y corré la primera celda de configuración.
2.  **Cargar Activos:** Ingresá los tickers de tu interés (ej: `AAPL`, `GGAL`, `KO`).
3.  **Definir Visión:** En el panel interactivo, ingresá el **Upside %** si tenés una proyección propia. Dejá en `0` para usar CAPM.
4.  **Optimizar:** Hacé clic en **"Ejecutar Optimización"**.
5.  **Diagnosticar:** Ejecutá las celdas siguientes para ver el **Heatmap**, el **Underwater Plot** y el análisis de **Contribución de Riesgo**.

---

## 📝 Requisitos Técnicos

* Python 3.x
* **Pandas & NumPy** (Manipulación de datos)
* **SciPy** (Motor de optimización `minimize`)
* **Scikit-Learn** (Cálculo de Covarianza Ledoit-Wolf)
* **Plotly** (Visualizaciones interactivas avanzadas)
* **YFinance** (Descarga de datos de mercado - 10 años)
* **BeautifulSoup** (Scraping de tasas y riesgo país)
