# Taller RAG con LangChain, OpenAI y Pinecone

Proyecto académico con dos implementaciones de Retrieval-Augmented Generation (RAG) en un único Jupyter Notebook.

## Arquitectura

```text
Base de conocimiento (TXT)
    ↓ segmentación (LangChain)
Embeddings (OpenAI)
    ↓
[Parte 1: InMemoryVectorStore] o [Parte 2: Pinecone]
    ↑ búsqueda semántica de la pregunta
Fragmentos relevantes → Prompt contextual → ChatOpenAI → Respuesta y fuentes
```

## Estructura

- `notebooks/RAG_LangChain_Pinecone.ipynb`: código explicado, pruebas y comparación.
- `data/knowledge_base.txt`: corpus de ejemplo Campus Café.
- `.env.example`: nombres de variables necesarias (sin credenciales reales).
- `requirements.txt`: dependencias Python.

## Requisitos

Python 3.11 recomendado, acceso a Internet, clave de API OpenAI con facturación/créditos y clave Pinecone con permisos para crear índices. Estos servicios pueden generar cargos.

## Instalación (Windows PowerShell)

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
Copy-Item .env.example .env
notepad .env
jupyter lab
```

En `.env`, reemplazar los valores de `OPENAI_API_KEY` y `PINECONE_API_KEY`. No subir `.env` a GitHub. Abrir `notebooks/RAG_LangChain_Pinecone.ipynb` y ejecutar las celdas en orden, usando el kernel del entorno virtual.

Si PowerShell bloquea la activación, ejecutar `Set-ExecutionPolicy -Scope Process Bypass` solo en esa sesión o invocar directamente `.\.venv\Scripts\python.exe`.

## Comparación

La Parte 1 almacena vectores en memoria y se reconstruye al reiniciar. La Parte 2 utiliza un índice persistente Pinecone con namespace separado por ejecución. El notebook imprime respuestas, fragmentos y latencias; las cifras dependen de la red y servicios externos.

## Seguridad y limitaciones

- No subir credenciales, tokens ni `.env`.
- El corpus es ilustrativo y no contiene información sensible.
- Los modelos pueden producir errores; las respuestas deben verificarse con las fuentes.
- No se incluyen resultados inventados: es necesario ejecutar el notebook con claves reales para obtener evidencia de ambas integraciones.
- Se utiliza por defecto `text-embedding-3-small` (1536 dimensiones). Si se cambia el modelo, revisar compatibilidad con el índice.

## Publicación en GitHub

```powershell
git init
git add .
git commit -m "Implementar taller RAG LangChain OpenAI Pinecone"
git branch -M main
git remote add origin https://github.com/USUARIO/NOMBRE-REPOSITORIO.git
git push -u origin main
```

Crear antes un repositorio vacío en GitHub y reemplazar la URL. Verificar con `git status` que `.env` no esté incluido.
