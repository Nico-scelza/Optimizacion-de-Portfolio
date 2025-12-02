# 📈 Optimización de Portafolio: CAPM y Upside

Este repositorio contiene un **modelo completo** para calcular retornos esperados de activos, construir una matriz de riesgo y ejecutar una optimización de portafolio, utilizando metodologías robustas como **CAPM** (ajustado por riesgo país para activos argentinos) y **Upside**.

La idea principal es tener un flujo limpio y metodológico. Obtener datos, elegir metodología de retorno, estimar riesgo y finalmente optimizar.

---

## 🚀 ¿Qué hace este proyecto?

El *notebook* (`Optimización de Portfolio.ipynb`) permite gestionar el flujo completo de la optimización:

* **Calcular retornos esperados** usando dos métodos distintos. **Upside** basado en precios objetivos o **CAPM** basado en riesgo sistemático.
* **Ajustar automáticamente el CAPM** para empresas argentinas agregando **riesgo país** al rendimiento esperado.
* **Construir matrices de covarianza** a partir de retornos históricos.
* **Ejecutar una optimización tipo Markowitz** buscando la mejor combinación riesgo-retorno.
* **Graficar la frontera eficiente** con puntos clave.
* **Mostrar pesos óptimos** y métricas del portafolio, como el **Sharpe Ratio**.

En resumen, te permite desde cero: Cargar activos, elegir método de retorno y Optimizar.

---

## 📊 Cálculo de Retornos Esperados

Tenés dos métodos a disposición. Podés elegir cuál usar según tu análisis.

### 🔵 1. Método Upside

El retorno esperado se calcula de forma sencilla, asumiendo que el precio del activo se moverá hacia un **Target Price** (Precio Objetivo) en un horizonte dado.

$$\text{Upside} = \frac{\text{Target Price} - \text{Current Price}}{\text{Current Price}}$$

Es útil cuando trabajás con acciones donde tenés un precio objetivo confiable, como reportes de analistas o valuaciones propias.

### 🔴 2. Modelo CAPM (Capital Asset Pricing Model)

El modelo CAPM calcula el rendimiento esperado en función de la tasa libre de riesgo y el riesgo sistemático del activo ($\beta$).

$$\text{Return} = R_f + \beta \times (R_m - R_f)$$

Donde:

* $R_f$ es la **tasa libre de riesgo**.
* $R_m$ es el **rendimiento esperado del mercado**.
* $\beta$ mide la **sensibilidad del activo** a los movimientos del mercado.

### 🇦🇷 Ajuste especial para empresas argentinas

Si el activo corresponde a una compañía argentina, se añade el **Riesgo País** al retorno esperado. Esto refleja el mayor riesgo soberano inherente a la inversión en Argentina.

La fórmula queda así:

$$\text{Return}_{\text{AR}} = R_f + \text{Riesgo\_País} + \beta \times (R_m - R_f)$$

Ese ajuste se aplica automáticamente según el *ticker*/país que indiques en los datos de entrada.

---

## 🧮 Construcción de la Matriz de Riesgo

El *notebook*:

* Descarga o procesa datos históricos de precios.
* Calcula rendimientos logarítmicos o simples.
* Estima la **matriz de covarianza** ($\Sigma$) de los retornos.
* Usa esa matriz como insumo principal del optimizador.

---

## ⚙️ Optimización del Portafolio

Se resuelve un problema clásico de la **Teoría Moderna de Portafolio (Markowitz)**, encontrando la asignación de pesos óptimos que mejor balancea riesgo y retorno.

El problema de optimización puede formularse como:

$$\text{Minimizar: } \quad w^{\text{T}} \Sigma w$$

$$ \text{Sujeto a: } \quad w^{\text{T}} \mu = \text{retorno objetivo (o maximizar Sharpe)}$$
$$\qquad \qquad \sum w = 1$$
$$\qquad \qquad w \geq 0 \quad \text{(si no se permiten ventas en corto)}$$

Donde:

* $\Sigma$ es la **matriz de covarianza**.
* $\mu$ son los **retornos esperados**.
* $w$ son los **pesos** (la combinación que buscamos).

Los resultados de la optimización incluyen:

* **Pesos óptimos**.
* **Sharpe ratio** para cada portafolio.
* Gráfico de la **frontera eficiente**.
* Identificación del **Portafolio con máximo Sharpe**.
* Identificación del **Portafolio de mínima varianza**.

---

## 🧰 Cómo usarlo

1.  **Abrí el notebook** `Optimización de Portfolio.ipynb` (recomiendo hacerlo con un IDE para la correcta visualización del gráfico).
2.  **Cargá tu lista de *tickers*** y los datos históricos (o usa la función de descarga).
3.  **Elegí el método de retorno** que querés usar, ingresando `"upside"` o `"capm"`.
4.  Si usás CAPM y el activo es argentino, el *script* suma riesgo país automáticamente.
5.  **Ejecutá la optimización** y revisá los resultados y gráficos generados.

---

## 📝 Requisitos

Este proyecto requiere las siguientes librerías de Python 3.x:

* **Python 3.x**
* **pandas**
* **numpy**
* **yfinance** (si descargás datos online)
* **matplotlib** / **seaborn**
* **scipy** (para la optimización)

---

## 💬 Notas Finales

Este proyecto busca dar una base simple pero sólida para optimización real. Sirve tanto para análisis académico como para armar portafolios reales basados en expectativas propias de retorno.

Si querés ampliar esto, agregar métricas, VaR, CVaR, o un optimizador con restricciones avanzadas, se puede sumar cuando quieras.
