# Sistema de Recomendación Multimodal para Juegos de Mesa

Este repositorio contiene el código fuente y recursos del proyecto de investigación **"Sistema de Recomendación Multimodal aplicado a Juegos de Mesa"**, desarrollado por Cristóbal Merino, Diego Sfeir y Pedro Irarrázaval.

El proyecto aborda el desafío de recomendar juegos de mesa en un entorno de "cola larga" (long-tail) y alta dispersión de datos (sparsity), utilizando el dataset de BoardGameGeek (BGG).

## Descripción y Metodología

El estudio explora la tensión entre la exactitud del ranking y la capacidad de descubrimiento (novedad). Se implementan y comparan modelos desde heurísticas simples hasta arquitecturas de aprendizaje profundo (DeepFM) y enfoques híbridos, integrando información semántica (mecánicas y temáticas).

### Protocolo de Evaluación

Se utiliza un esquema de validación **Hold-Out Estratificado por Usuario** (80/20), asegurando que todos los usuarios estén representados. Para la evaluación de ranking, se emplea **Negative Sampling** (1 ítem positivo vs 100 negativos) para calcular métricas Top-K de manera eficiente.

### Modelos Implementados

El código (`main.ipynb`) implementa los siguientes modelos:

1.  **Líneas Base (Baselines)**:
    - **Most Popular**: Ranking basado en frecuencia de interacciones. Domina en métricas de exactitud (nDCG > 0.7) pero carece de diversidad.
    - **Random**: Cota inferior aleatoria.
    - **Content-Based (CB)**: Recuperación vectorial usando TF-IDF sobre descripciones, mecánicas y temáticas.
2.  **Filtrado Colaborativo Latente**:
    - **SVD**: Factorización de matrices optimizada (K=50).
3.  **Modelos Avanzados e Híbridos**:
    - **SVD + Popularidad (SVD+Pop)**: **[Modelo Propuesto]** Ensamble lineal que balancea la personalización con la tendencia global. Identificado en el paper como el equilibrio óptimo entre precisión y novedad.
    - **DeepFM**: Deep Factorization Machine implementada en PyTorch. Captura interacciones de alto y bajo orden.
    - **DeepFM + Features**: Variante que inyecta contenido (features densos de ítems) en el espacio latente para mitigar el problema de *cold-start*.

## Contenidos del Repositorio

- **`main.ipynb`**: Notebook principal con el pipeline completo: carga de datos, preprocesamiento, implementación de modelos, entrenamiento y generación de métricas.
- **`metrics/`**: Resultados de la evaluación en formato JSON (Precision, Recall, nDCG, ILD, Novelty, Theme Concentration).
- **`figs/`**: Visualizaciones generadas (distribuciones, espacios latentes, comparaciones).
- **`csv/`**: Dataset utilizado (BGG Data).
- **`bgg_data_documentation.txt`**: Diccionario de datos.
- **`requirements.txt`**: Librerías necesarias.

## Ejecución del Código

Para reproducir los experimentos y generar las métricas/gráficos:

1.  Instale las dependencias:
    ```bash
    pip install -r requirements.txt
    ```
2.  Ejecute el notebook completo:
    Puede abrir `main.ipynb` en Jupyter/VSCode y ejecutar todas las celdas, o usar la línea de comandos:
    ```bash
    jupyter nbconvert --to notebook --execute --inplace main.ipynb
    ```

**Nota**: El notebook guardará automáticamente las métricas generadas en la carpeta `metrics/` y las figuras en `figs/`.
