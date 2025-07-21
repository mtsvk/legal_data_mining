# 🤖 legal_data_mining

Lab notebook reproducible para minería jurídica de **fichas de jurisprudencia**: metodología generalizable para limpieza, embeddings, clustering y mapeo normativo.  

> **Ejemplo aplicado:** fichas relativas a protección de datos (GDPR), vinculadas con la **Ley Chilena 21.719**.

Este pipeline funciona con **cualquier** colección de fichas de jurisprudencia y, a modo de ejemplo, ofrece:

- **Representación semántica** (embeddings)  
- **Agrupación de casos similares** (clustering)  
- **Detección automatizada** de principios y derechos vulnerados  
- **Salida estructurada** en JSON  

---

## 🧩 Estructura del flujo

| Etapa                   | Script / Notebook        | Salida clave               |
|-------------------------|--------------------------|----------------------------|
| 0. Configuración global | `config.py`              | Parámetros, rutas, claves  |
| 1. Ingesta              | `01_ingesta.ipynb`       | `df_clean.parquet`         |
| 2. Limpieza textual     | `02_limpieza.ipynb`      | `df_tokens.parquet`        |
| 3. Embeddings           | `03_embeddings.ipynb`    | `embeddings.npy`           |
| 4. Clustering           | `04_clustering.ipynb`    | `cluster_plot.png`         |
| 5. Mapeo Ley 21.719     | `05_mapping_21719.ipynb` | `resultados.jsonl`         |

---

## 📦 Requisitos

- Python ≥ 3.10  
- OpenAI API Key (para embeddings)  
- Paquetes en `requirements.txt`  

---

## 🚀 Ejecución local

1. **Clona este repositorio**:

   ```bash
   git clone https://github.com/mtsvk/legal_data_mining.git
   cd legal_data_mining
   ```

2. **Crea y activa un entorno virtual**:

   ```bash
   python -m venv .venv
   source .venv/bin/activate       # En Windows: .venv\Scripts\activate
   ```

3. **Instala las dependencias**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Lanza JupyterLab** y ejecuta los notebooks en orden (o ábrelos en Google Colab):

   ```bash
   jupyter lab
   ```

---

## ☁️ Ejecución en Colab

Puedes ejecutar y editar cada script directamente en Google Colab. Haz clic en el badge correspondiente para abrirlo:

| Etapa                   | Script                | Open in Colab                                                                                                      |
|-------------------------|-----------------------|--------------------------------------------------------------------------------------------------------------------|
| 0. Configuración global | `00_config.py`        | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu_usuario/legal_data_mining/blob/main/scripts/00_config.py) |
| 1. Ingesta              | `01_ingesta.py`       | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu_usuario/legal_data_mining/blob/main/scripts/01_ingesta.py) |
| 2. Limpieza textual     | `02_limpieza.py`      | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu_usuario/legal_data_mining/blob/main/scripts/02_limpieza.py) |
| 3. Embeddings           | `03_embeddings.py`    | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu_usuario/legal_data_mining/blob/main/scripts/03_embeddings.py) |
| 4. Clustering           | `04_clustering.py`    | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu_usuario/legal_data_mining/blob/main/scripts/04_clustering.py) |
| 5. Mapeo Ley 21.719     | `05_mapping_21719.py` | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu_usuario/legal_data_mining/blob/main/scripts/05_mapping_21719.py) |

> **Nota:** Al guardar cambios en Colab, usa **File → Save a copy in GitHub** y selecciona `scripts/<nombre_script>.py` en tu repositorio para mantener tu historial actualizado.

---

## 🔐 Variables sensibles

Este proyecto requiere una clave de API de OpenAI. Puedes definirla en tu entorno:

```bash
export OPENAI_API_KEY="sk-xxxxxxxxxxxxxxxx"
```

O crear un archivo `.env` en la raíz:

```env
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
```

---

## 📂 Estructura de carpetas

```
legal_data_mining/
├─ data/                  # Datos de entrada
├─ outputs/               # Resultados (Parquet, JSONL, imágenes)
├─ notebooks/             # Notebooks ejecutables
├─ config.py              # Parámetros globales
├─ requirements.txt
└─ README.md
```

---

## 📜 Licencia

- **Código fuente**: Licencia MIT  
- **Documentación y notebooks**: CC BY 4.0  
  Eres libre de usar, adaptar y redistribuir este trabajo con atribución adecuada.

---

## ✍️ Cita sugerida

Si reutilizas esta metodología en investigación académica o técnica, considera citarla así:

> Vukusic, Matías (2025). **Metodología reproducible para minería de fichas de jurisprudencia**. GitHub repository.  
> Disponible en: https://github.com/mtsvk/legal_data_mining

---

## 🤝 Contacto

¿Comentarios, errores, propuestas? Abre un [Issue](https://github.com/mtsvk/legal_data_mining/issues) o escríbeme a `matias@vukusic.cl`.
