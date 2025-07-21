# 🤖 legal_data_mining

Lab notebook reproducible para minería jurídica de **fichas de jurisprudencia** (resúmenes de sentencias).  
Ejemplo aplicado: protección de datos (GDPR) vinculada con la **Ley Chilena 21.719**.

Funcionalidades principales:
- Embeddings semánticos (OpenAI)
- Clustering de casos similares
- Extracción de términos clave (TF‑IDF)
- Visualización PCA
- Mapeo automático a principios / derechos de la Ley 21.719
- Salidas estructuradas (Parquet / JSONL / imágenes) + API de ejemplo

---

## 🧩 Flujo de trabajo (8 notebooks)

| Etapa | Notebook / Script            | Objetivo resumido                                      | Salida principal |
|-------|------------------------------|---------------------------------------------------------|------------------|
| 0     | `00_config.ipynb`            | Configurar entorno (dependencias, claves, rutas)       | Variables en memoria |
| 1     | `01_ingesta.ipynb`           | Leer CSV y depurar duplicados/nulos                    | `outputs/df_clean.parquet` |
| 2     | `02_limpieza.ipynb`          | Normalizar texto + stopwords rudimentarias             | `outputs/df_tokens.parquet` |
| 3     | `03_embeddings.ipynb`        | Generar embeddings OpenAI (1536 dims)                  | `outputs/embeddings.npy` |
| 4     | `04_clustering.ipynb`        | Seleccionar *k* (Silhouette) y asignar clusters        | `outputs/df_clustered.parquet`, `cluster_silhouette.png` |
| 5     | `05_tfidf.ipynb`             | Términos diferenciales por cluster (TF‑IDF)            | `outputs/cluster_keywords.json` |
| 6     | `06_visualizacion.ipynb`     | Proyección PCA 2D y gráfico de clusters                | `outputs/pca_clusters.png` |
| 7     | `07_mapping_21719.ipynb`     | Mapeo Ley 21.719 + API demo                            | `outputs/resultados.jsonl` |

**Google Colab:**:

[![Próximamente](https://img.shields.io/badge/open%20in%20colab-próximamente-lightgrey)](#)

---

## 📦 Requisitos

- Python ≥ 3.10  
- OpenAI API Key  
- Dependencias en `requirements.txt`  

---

## 🚀 Ejecución (local y Colab)

### Google Colab
1. Abre el notebook deseado (badge).
2. Define tu clave de OpenAI en la primera celda:
   ```python
   import os
   os.environ["OPENAI_API_KEY"] = "sk-xxxxxxxxxxxxxxxx"
   ```
3. Ejecuta los notebooks en orden 0 → 7.

### Local

```bash
git clone https://github.com/mtsvk/legal_data_mining.git
cd legal_data_mining

python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

pip install -r requirements.txt
export OPENAI_API_KEY="sk-xxxxxxxxxxxxxxxx"  # o usar archivo .env

jupyter lab
```

Archivo `.env` opcional:

```env
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
```

---

## 📂 Estructura de carpetas

```
legal_data_mining/
├─ data/            # Datos de entrada
├─ notebooks/       # Notebooks ejecutables
├─ outputs/         # Parquet / JSONL / imágenes
├─ requirements.txt
└─ README.md
```

---

## 📜 Licencia

- Código fuente: MIT  
- Documentación y notebooks: CC BY 4.0  

---

## ✍️ Cita sugerida

Vukusic, Matías (2025). *Metodología reproducible para minería de fichas de jurisprudencia*. GitHub repository.  
https://github.com/mtsvk/legal_data_mining

---

## 🤝 Contacto

¿Comentarios o sugerencias? Abre un [Issue](https://github.com/mtsvk/legal_data_mining/issues) o escribe a `matias@vukusic.cl`.
