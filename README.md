# 📈 Optimización Quantamental: CAPM, Shrinkage & CVaR

Este repositorio contiene un motor de **Ingeniería Financiera** diseñado para la gestión de portafolios de inversión. Combina el análisis fundamental (Upside manual) con modelos cuantitativos robustos para la estimación de riesgo.

A diferencia de los optimizadores básicos de Markowitz, este modelo incorpora **Ledoit-Wolf Shrinkage** para limpiar el ruido estadístico de la matriz de covarianza y **CVaR (Conditional Value at Risk)** para proteger la cartera contra eventos extremos del mercado ("cisnes negros" o colas gordas).

---

## 🚀 Características Principales

El *notebook* (`Optimización de Portfolio.ipynb`) ejecuta un flujo de trabajo profesional:

* **Enfoque Híbrido (Quantamental):** Permite al usuario definir sus propios retornos esperados (*Upside*) o confiar en el equilibrio del mercado (*CAPM*).
* **Estadística Robusta:** Reemplaza la covarianza histórica simple por la estimación de **Ledoit-Wolf**, reduciendo errores de estimación y evitando soluciones de esquina inestables.
* **Gestión de Riesgo de Cola:** Optimiza no solo por Varianza (volatilidad normal), sino también por **CVaR al 95%** (pérdida esperada en escenarios de crisis).
* **Ajuste Argentina:** Incorpora automáticamente el **Riesgo País** al modelo CAPM para activos locales.
* **Comparativa Transparente:** Genera una tabla final que confronta la "Teoría" (Tasa CAPM) contra la "Visión del Inversor" (Retorno Final).

---

## 📊 Modelado de Retornos (La Visión)

El modelo permite contrastar dos fuentes de retorno para cada activo:

### 1. Tasa Teórica (CAPM Ajustado)
Calcula el retorno de equilibrio exigido por el mercado:
$$E(R) = R_f + \beta (R_m - R_f) + \text{Spread Riesgo País}$$
* *Nota:* El Spread de Riesgo País se aplica automáticamente a activos argentinos (basado en datos de Ámbito/Rava).

### 2. Visión del Inversor (Upside)
Permite ingresar manualmente un **Target Price** o Upside estimado a 5 años. Si el usuario tiene una tesis de inversión fuerte (ej. "Esta acción va a subir 40%"), el modelo prioriza este *input* sobre el CAPM.

---

## 🛡️ Modelado de Riesgo (La Ingeniería)

Aquí es donde el modelo se diferencia de las herramientas académicas básicas:

### 📉 Matriz de Covarianza "Shrinkage" (Ledoit-Wolf)
Las matrices de covarianza históricas suelen tener mucho "ruido" estadístico. Este modelo aplica una técnica de contracción (*Shrinkage*) hacia una matriz objetivo estructurada.
* **Beneficio:** Genera portafolios más estables en el tiempo y reduce la sobre-concentración errónea en activos volátiles.

### 🌪️ Conditional Value at Risk (CVaR 95%)
Mientras que la Varianza mide cuánto se mueve el precio (hacia arriba o abajo), el CVaR responde: **"En el peor 5% de los casos, ¿cuánto espero perder?"**.
* El optimizador calcula un portafolio específico (`Mínimo CVaR`) diseñado para minimizar estas pérdidas catastróficas, ideal para inversores aversos a crisis.

---

## ⚙️ Escenarios de Optimización

El algoritmo resuelve numéricamente tres problemas de optimización distintos y los grafica en la Frontera Eficiente:

1.  **⭐ Máximo Sharpe:** La mejor relación Retorno/Riesgo (Volatilidad).
2.  **💎 Mínima Varianza:** El portafolio con menor volatilidad global (usando Ledoit-Wolf).
3.  **🛡️ Mínimo CVaR:** El portafolio más defensivo ante eventos de cola (Fat Tails).

---

## 🧰 Guía de Uso

1.  **Ejecutar:** Abrí el notebook `Optimización de Portfolio.ipynb`.
2.  **Configurar:** Ingresá los *tickers* de tu interés (ej: `AAPL`, `GGAL`, `KO`).
3.  **Definir Visión:** Se abrirá un panel interactivo.
    * Ingresá el **Upside %** si tenés una proyección propia.
    * Dejá en `0` para que el modelo use el **CAPM** automáticamente.
4.  **Analizar:**
    * Revisá el gráfico de la Frontera Eficiente.
    * Analizá la tabla final para ver cómo el modelo asignó los pesos (Markowitz vs CVaR) y compará tu retorno esperado final contra el teórico.

---

## 📝 Requisitos Técnicos

* **Python 3.x**
* **Pandas & NumPy** (Manipulación de datos)
* **SciPy** (Motor de optimización `minimize`)
* **Scikit-Learn** (Cálculo de Covarianza Ledoit-Wolf)
* **Plotly** (Visualizaciones interactivas)
* **YFinance** (Descarga de datos de mercado)
* **BeautifulSoup** (Scraping de tasas y riesgo país)

---

## 💬 Nota del Autor

Este proyecto busca cerrar la brecha entre la teoría académica y la práctica profesional. Al incorporar **Shrinkage** y **CVaR**, pasamos de jugar con números a gestionar riesgos reales, aceptando que los mercados financieros no siempre siguen una distribución normal perfecta.
