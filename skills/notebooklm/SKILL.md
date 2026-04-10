## **name: notebooklm-expert description: Guía experta para NotebookLM (CLI y MCP). Permite gestionar cuadernos, fuentes (URLs, YouTube, Drive), generar pódcast, vídeos, cuestionarios, realizar investigaciones y automatizar flujos de trabajo.**

# **Experto en NotebookLM (CLI y MCP)**

Esta habilidad proporciona una guía completa para usar NotebookLM a través de la CLI `nlm` y las herramientas MCP.

## **Detección de Herramientas (CRÍTICO - Leer primero)**

**SIEMPRE verifica qué herramientas están disponibles antes de proceder:**

1. **Herramientas MCP**: Busca herramientas que comiencen con `mcp__notebooklm-mcp__*` o `mcp_notebooklm_*`.
2. **Si AMBAS (MCP y CLI) están disponibles**: **PREGUNTA al usuario** cuál prefiere usar.
3. **Si solo hay MCP**: Úsalas directamente (consulta los parámetros en la documentación de la herramienta).
4. **Si solo hay CLI**: Usa comandos de Bash con `nlm`.

---

## **Reglas Críticas de Funcionamiento**

1. **Autenticación obligatoria**: El usuario DEBE ejecutar `nlm login` antes de cualquier operación.
2. **Sesiones temporales**: Las sesiones expiran. Si los comandos fallan, sugiere `nlm login`.
3. **Confirmación de eliminación**: **SIEMPRE PIDE CONFIRMACIÓN** antes de ejecutar cualquier comando de eliminación (`delete`). Las eliminaciones son irreversibles.
4. **Flag `--confirm`**: Todos los comandos de generación o eliminación requieren `--confirm` (CLI) o `confirm=True` (MCP).
5. **IDs de recursos**: Los comandos de creación devuelven IDs necesarios para pasos posteriores. Captúralos siempre.
6. **No usar `nlm chat start`**: Los agentes de IA NO deben usar este comando porque abre una terminal interactiva (REPL). Usa `notebook_query` en su lugar.

---

## **Glosario de Herramientas y Comandos**

### **1. Gestión de Cuadernos (Notebooks)**
*   **Listar**: `notebook_list` / `nlm notebook list`
*   **Crear**: `notebook_create(title)` / `nlm notebook create "Título"`
*   **Consultar (Q&A)**: `notebook_query(id, query)` / `nlm notebook query <id> "pregunta"`
*   **Eliminar**: `notebook_delete(id, confirm=True)` / `nlm notebook delete <id> --confirm`

### **2. Gestión de Fuentes (Sources)**
*   **Añadir URL/YouTube**: `source_add(id, url="...")` / `nlm source add <id> --url "..."`
*   **Añadir Texto**: `source_add(id, text="...", title="...")` / `nlm source add <id> --text "..." --title "..."`
*   **Añadir Google Drive**: `source_add(id, drive="doc_id", type="doc")` / `nlm source add <id> --drive <id>` (Tipos: `doc`, `slides`, `sheets`, `pdf`).
*   **Sincronizar Drive**: `source_sync_drive(id, confirm=True)` / `nlm source sync <id> --confirm` (Actualiza fuentes de Drive editadas).

### **3. Investigación (Research)**
Permite encontrar nuevas fuentes en la web o Drive.
*   **Iniciar**: `research_start(topic, mode="fast/deep", source="web/drive")`
*   **Estado**: `research_status(id)` (Poll hasta que termine).
*   **Importar**: `research_import(id, task_id)` (Añade los hallazgos al cuaderno).

### **4. Generación de Contenido (Studio)**
*   **Crear Artefacto**: `studio_create(id, artifact_type, ...)`
    *   `audio`: Pódcast/Deep Dive. Formatos: `deep_dive`, `brief`, `critique`, `debate`.
    *   `video`: Vídeo explicativo. Estilos: `classic`, `whiteboard`, `anime`, `watercolor`.
    *   `report`: Guía de estudio, Briefing Doc, Blog Post.
    *   `quiz`: Cuestionario. Parámetros: `question_count`, `difficulty` (1-5).
    *   `slides`: Presentación de diapositivas.
    *   `infographic`: Infografía. Estilos: `professional`, `bento_grid`, `clay`.
*   **Estado de generación**: `studio_status(id, artifact_id)`. **No des el link hasta que el estado sea `SUCCESS` o `completed`.**
*   **Descargar**: `download_artifact(id, artifact_id)`.

### **5. Operaciones por Lote y Cross-Notebook**
*   **Batch**: `batch(action="query/create/audio", tags="...", query="...")`. Ejecuta acciones en varios cuadernos a la vez.
*   **Cross-Query**: `cross_notebook_query(query, tags="...")`. Consulta múltiples cuadernos y agrega las respuestas con citas.

---

## **Flujos de Trabajo Recomendados**

### **Flujo A: De la Investigación al Pódcast**
1. Crear cuaderno: `notebook_create("Tema")`.
2. Investigar: `research_start("Tema", mode="deep")`.
3. Importar fuentes tras finalizar la investigación.
4. Generar audio: `studio_create(id, artifact_type="audio", format="deep_dive")`.
5. Esperar a `SUCCESS` en `studio_status` y entregar link de `download_artifact`.

### **Flujo B: Preparación de Examen**
1. Añadir apuntes/PDFs: `source_add`.
2. Generar guía: `studio_create(id, artifact_type="report", format="Study Guide")`.
3. Generar cuestionario: `studio_create(id, artifact_type="quiz", question_count=10)`.
4. Generar flashcards: `studio_create(id, artifact_type="flashcards")`.

---

## **🔑 Solución de Problemas (Autenticación)**

Si recibes un error de "Unauthorized" o "Cookies expired":
1. Informa al usuario: "Tu sesión de NotebookLM ha expirado o no has iniciado sesión."
2. Instrucción clara: "Por favor, ejecuta `nlm login` en tu terminal para sincronizar tus credenciales de Google."
3. Si el usuario ya lo hizo y sigue fallando, sugiere `nlm login --check`.

Siempre cita tus fuentes cuando respondas preguntas basadas en los cuadernos del usuario. Proporciona los enlaces de descarga de forma clara al final de tus respuestas.
