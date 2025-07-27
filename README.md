# legal\_data\_mining

Lab notebook reproducible para minería jurídica de fichas de jurisprudencia (resúmenes de sentencias).\
Ejemplo aplicado: protección de datos (GDPR) vinculada con la Ley Chilena 21.719.

**Funcionalidades principales:**

- Ingesta y limpieza de datos (Pandas)
- Embeddings semánticos (OpenAI)
- Clustering de casos similares (K‑Means)
- Extracción de términos clave (TF‑IDF)
- Visualización PCA/SVD
- Mapeo a principios, derechos y obligaciones (RGPD / Ley 21.719)
- Salidas estructuradas (Parquet/JSON/PNG/MD)

---

## Flujo de trabajo (8 notebooks)

| Etapa | Notebook / Script        | Objetivo resumido                                                                    | Salida principal                                                |
| ----- | ------------------------ | ------------------------------------------------------------------------------------ | --------------------------------------------------------------- |
| 0     | `00_config.ipynb`        | Configurar entorno (dependencias, OpenAI Key, rutas, sanity‑check de embeddings)     | `outputs/config.json`, `outputs/embedding_prueba.npy`           |
| 1     | `01_ingesta.ipynb`       | Leer CSV (`gdpr_fines.csv`), estandarizar columnas y limpiar duplicados/nulos        | `outputs/gdpr_clean.parquet`                                    |
| 2     | `02_limpieza.ipynb`      | Normalizar texto (HTML, URLs), crear `summary_clean` y stopwords de dominio          | `outputs/gdpr_norm.parquet`                                     |
| 3     | `03_embeddings.ipynb`    | Generar embeddings con OpenAI API (`text-embedding-3-small`) en lotes                | `outputs/embeddings.npy`, `outputs/df_emb.parquet`              |
| 4     | `04_clustering.ipynb`    | Evaluar K (Silhouette 4–16), entrenar K‑Means, asignar clusters                      | `outputs/df_clustered.parquet`, `outputs/silhouette.json`       |
| 5     | `05_tfidf.ipynb`         | Extraer tópicos por cluster con TF‑IDF y ejemplos representativos                    | `outputs/cluster_keywords.json`, `outputs/cluster_examples.csv` |
| 6     | `06_visualizacion.ipynb` | Reducir embeddings a 2D (PCA/SVD) y graficar clusters                                | `outputs/pca_clusters.png`, `outputs/clusters_2d.csv`           |
| 7     | `07_mapping_21719.ipynb` | Mapear clusters a principios, derechos, obligaciones y artículos (RGPD / Ley 21.719) | `outputs/cluster_cards.json`, `outputs/cluster_cards.md`        |

---

## Requisitos

- Python ≥ 3.10
- OpenAI API Key
- Dependencias en `requirements.txt`

---

## Ejecución

### Google Colab

1. Abre el notebook deseado en Colab (badge en cada `.ipynb`).
2. Define tu clave de OpenAI:
   ```python
   import os
   os.environ["OPENAI_API_KEY"] = "sk-xxxxxxxxxxxxxxxx"
   ```
3. Ejecuta las celdas en orden: 00 → 01 → 02 → 03 → 04 → 05 → 06 → 07.

### Local

```bash
git clone https://github.com/mtsvk/legal_data_mining.git
cd legal_data_mining
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
export OPENAI_API_KEY="sk-xxxxxxxxxxxxxxxx"
jupyter lab
```

---

## Estructura de carpetas

```text
legal_data_mining/
├─ data/            # CSV de entrada: gdpr_fines.csv
├─ notebooks/       # 00_… – 07_… ipynb o scripts .py
├─ outputs/         # Parquet / JSON / PNG / MD generados
├─ requirements.txt
└─ README.md
```

---

## Licencia

- Código fuente: MIT
- Documentación y notebooks: CC BY 4.0

---

## Cita sugerida

Vukusic, Matías (2025). *Minería de fichas de jurisprudencia*. GitHub repository.\
[https://github.com/mtsvk/legal\_data\_mining](https://github.com/mtsvk/legal_data_mining)

---
