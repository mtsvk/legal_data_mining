# legal_data_mining

Flujo de minería de datos jurídicos para “fichas de jurisprudencia” (resúmenes de sanciones), aplicado como ejemplo a sanciones del GDPR extraídas de [enforcementtracker.com](https://enforcementtracker.com) (CMS Law.Tax, CC BY‑NC‑SA 4.0). Reproducible en Google Colab y también ejecutable localmente como script Python.

---

## 📂 Estructura del repositorio

```
/
├── .gitignore
├── LICENSE
├── README.md
├── requirements.txt
├── pipeline_legal_data_mining_20250725.ipynb
├── pipeline_legal_data_mining_20250725.py
└── outputs/                       ← Generado tras ejecutar la pipeline, disponibles en https://github.com/mtsvk/legal_data_mining/blob/main/outputs.zip
    ├── config.json
    ├── gdpr_clean.parquet
    ├── gdpr_norm.parquet
    ├── embedding_prueba.npy
    ├── embeddings.npy
    ├── df_emb.parquet
    ├── df_clustered.parquet
    ├── silhouette.json
    ├── kmeans.joblib
    ├── cluster_profile.json
    ├── clusters_2d.png
    ├── clusters_2d.csv
    └── general_insights.md
```

---

## 🎯 Objetivo

- **Analizar** cientos de resúmenes de sanciones GDPR.
- **Limpiar** y **normalizar** el texto.
- **Generar embeddings** semánticos con OpenAI.
- **Agrupar** documentos similares con **K‑Means**.
- **Perfilar** clusters y **visualizar** en 2D.
- **Generar insights** automáticos con un LLM (OpenAI).

Este pipeline es totalmente **reproducible** y fácilmente **adaptable** a otros datasets jurídicos o administrativos.

---

## 📋 Requisitos

- Python ≥ 3.8  
- Una **clave de API de OpenAI** (se usa para embeddings e insights)
- Internet (si ejecutas el notebook en Colab o deseas llamar a la API)
- Las siguientes librerías (listadas en `requirements.txt`):
  ```
  openai
  python-dotenv
  tqdm
  matplotlib
  scikit-learn
  joblib
  pandas
  numpy
  ```

---

## 🚀 Instalación

1. **Clonar este repositorio**  
   ```bash
   git clone https://github.com/mtsvk/legal_data_mining.git
   cd legal_data_mining
   ```

2. **Crear un entorno virtual** (opcional pero recomendado)  
   ```bash
   python -m venv .venv
   source .venv/bin/activate      # Linux/macOS
   .venv\Scripts\activate       # Windows
   ```

3. **Instalar dependencias**  
   ```bash
   pip install -r requirements.txt
   ```

4. **Configurar la API Key**  
   Define tu `OPENAI_API_KEY` en el entorno o crea un archivo `.env` con:
   ```
   OPENAI_API_KEY=tu_clave_aquí
   ```

---

## 🧩 Uso

### 1. Notebook en Google Colab

1. Abre `pipeline_legal_data_mining_20250725.ipynb` en Colab.
2. Monta tu Google Drive (opcional) o sube tu CSV (`gdpr_fines.csv`).
3. Ejecuta celda a celda. El directorio `outputs/` se irá llenando automáticamente.

### 2. Ejecutar como script Python

```bash
python pipeline_legal_data_mining_20250725.py   --input_csv path/to/gdpr_fines.csv   --output_dir outputs/
```

El script está diseñado para correr todo el pipeline de un tirón, produciendo idénticos artefactos en `outputs/`.

---

## 🔄 Descripción de los pasos (Scripts)

- **Script 0 – Configuración inicial**  
  Instala dependencias, fija semilla, crea `config.json` y hace un sanity‐check de embeddings.

- **Script 1 – Ingesta y limpieza básica**  
  Lee CSV, renombra columnas, elimina duplicados y genera `gdpr_clean.parquet`.

- **Script 2 – Limpieza avanzada y stopwords**  
  Quita HTML/URLs, normaliza texto, aplica stopwords generales y de dominio, guarda `gdpr_norm.parquet`.

- **Script 3 – Embeddings OpenAI**  
  Sanitiza textos, llama a la API de OpenAI en batches, guarda `embeddings.npy` y `df_emb.parquet`.

- **Script 4 – Clustering K‑Means**  
  Evalúa silhouette para K=4…16, selecciona K óptimo, entrena modelo, guarda `kmeans.joblib`, clusters y scores.

- **Script 5 – Perfilado de clusters**  
  Tokeniza resúmenes, extrae top‑terms y ejemplos, guarda `cluster_profile.json`.

- **Script 6 – Visualización 2D**  
  Proyecta embeddings a 2D con TruncatedSVD, grafica clusters, guarda PNG y CSV de coordenadas.

- **Script 7 – Insights automáticos**  
  Construye prompt con scores y perfiles, llama a GPT-3.5/4, genera informe en Markdown (`general_insights.md`).

---

## ⚙️ Adaptación a otros proyectos

1. Cambia el CSV de entrada (`--input_csv` o `cfg["dataset_csv"]`).
2. Ajusta el mapeo de columnas en el Script 1.
3. Modifica stopwords o parámetros de `TfidfVectorizer` en el Script 2.
4. Experimenta con otros algoritmos de clustering o proyecciones (PCA, UMAP).

---

## 📄 Licencia

Este proyecto está bajo la licencia **MIT**.  
Los datos de enforcementtracker.com están bajo **CC BY‑NC‑SA 4.0**.

---

¡Contribuciones y sugerencias bienvenidas! 🚀  
