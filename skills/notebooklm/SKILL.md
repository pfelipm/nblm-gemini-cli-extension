---
name: notebooklm-expert
version: "0.5.19"
description: "Guía experta para la CLI de NotebookLM (`nlm`) y el servidor MCP. Usa esta habilidad para interactuar con NotebookLM programáticamente: crear/gestionar cuadernos, añadir fuentes (URLs, YouTube, texto, Google Drive), generar contenido (pódcast, informes, cuestionarios, flashcards, mapas mentales, diapositivas, infografías, vídeos, tablas de datos), realizar investigaciones, chatear con fuentes o automatizar flujos de trabajo. Se activa al mencionar \"nlm\", \"notebooklm\", \"generación de pódcast\", \"resumen de audio\" o cualquier tarea de automatización de NotebookLM."
---

# Experto en NotebookLM (CLI y MCP)

Esta habilidad proporciona una guía completa para usar NotebookLM a través de la CLI `nlm` y las herramientas MCP.

## Detección de Herramientas (CRÍTICO - Leer primero)

**SIEMPRE verifica qué herramientas están disponibles antes de proceder:**

1. **Busca herramientas MCP**: Herramientas que comiencen con `mcp__notebooklm-mcp__*` o `mcp_notebooklm_*`.
2. **Si AMBAS herramientas (MCP y CLI) están disponibles**: **PREGUNTA al usuario** cuál prefiere usar antes de continuar.
3. **Si solo hay herramientas MCP disponibles**: Úsalas directamente (consulta los docstrings para los parámetros).
4. **Si solo hay CLI disponible**: Usa comandos de la CLI `nlm` a través de Bash.

**Lógica de Decisión:**
```
has_mcp_tools = check_available_tools()  # Busca mcp__notebooklm-mcp__* o mcp_notebooklm_*
has_cli = check_bash_available()  # Puede ejecutar comandos nlm

if has_mcp_tools and has_cli:
    # PREGUNTAR AL USUARIO: "Puedo usar las herramientas MCP o la CLI nlm. ¿Cuál prefieres?"
    user_preference = ask_user()
else if has_mcp_tools:
    # Usar herramientas MCP directamente
    mcp__notebooklm-mcp__notebook_list()
else:
    # Usar CLI vía Bash
    bash("nlm notebook list")
```

Esta habilidad documenta AMBOS enfoques. Elige el adecuado según la disponibilidad de herramientas y la **preferencia del usuario**.

## Referencia Rápida

**Ejecuta `nlm --ai` para obtener documentación optimizada para IA** - proporciona una visión completa de todas las capacidades de la CLI.

```bash
nlm --help              # Listar todos los comandos
nlm <command> --help    # Ayuda para un comando específico
nlm --ai                # Documentación completa optimizada para IA (RECOMENDADO)
nlm --version           # Verificar versión instalada
```

## Reglas Críticas (Leer primero)

1. **Autenticarse siempre primero**: Ejecuta `nlm login` antes de cualquier operación.
2. **Las sesiones expiran en ~20 minutos**: Vuelve a ejecutar `nlm login` si los comandos empiezan a fallar.
3. **⚠️ SIEMPRE PREGUNTA ANTES DE ELIMINAR**: Antes de ejecutar CUALQUIER comando de eliminación, pide confirmación explícita al usuario. Las eliminaciones son **irreversibles**. Muestra qué se eliminará y advierte sobre la pérdida permanente de datos.
4. **`--confirm` es OBLIGATORIO**: Todos los comandos de generación y eliminación necesitan `--confirm` o `-y` (CLI) o `confirm=True` (MCP).
5. **La investigación requiere `--notebook-id`**: El flag es obligatorio, no posicional.
6. **Captura los IDs de la salida**: Los comandos de creación/inicio devuelven IDs necesarios para operaciones posteriores.
7. **Usa alias**: Simplifica los UUIDs largos con `nlm alias set <nombre> <uuid>`.
8. **Verifica alias antes de crear**: Ejecuta `nlm alias list` para evitar conflictos de nombres.
9. **NO inicies el REPL**: Nunca uses `nlm chat start` - abre una terminal interactiva que las herramientas de IA no pueden controlar. Usa `nlm notebook query` para preguntas y respuestas directas.
10. **Elige el formato de salida sabiamente**: La salida por defecto es compacta y eficiente en tokens. Usa `--quiet` para capturar IDs. Usa `--json` solo cuando necesites parsear campos específicos.
11. **Usa `--help` si tienes dudas**: `nlm <command> --help` para ver opciones y flags.

## Árbol de Decisión de Flujos de Trabajo

Usa esto para determinar la secuencia correcta de comandos:

```
El usuario quiere...
│
├─► Trabajar con NotebookLM por primera vez
│   └─► nlm login → nlm notebook create "Título"
│
├─► Añadir contenido a un cuaderno
│   ├─► Desde una URL/web → nlm source add <nb-id> --url "https://..."
│   ├─► Desde YouTube → nlm source add <nb-id> --url "https://youtube.com/..."
│   ├─► Desde texto pegado → nlm source add <nb-id> --text "contenido" --title "Título"
│   ├─► Desde Google Drive → nlm source add <nb-id> --drive <doc-id> --type doc
│   └─► Descubrir nuevas fuentes → nlm research start "consulta" --notebook-id <nb-id>
│
├─► Generar contenido desde las fuentes
│   ├─► Pódcast/Audio → nlm audio create <nb-id> --confirm
│   ├─► Resumen escrito → nlm report create <nb-id> --confirm
│   ├─► Materiales de estudio → nlm quiz/flashcards create <nb-id> --confirm
│   ├─► Contenido visual → nlm mindmap/slides/infographic create <nb-id> --confirm
│   ├─► Vídeo → nlm video create <nb-id> --confirm
│   └─► Extraer datos → nlm data-table create <nb-id> "descripción" --confirm
│
├─► Hacer preguntas sobre las fuentes
│   └─► nlm notebook query <nb-id> "pregunta"
│       (Usa --conversation-id para seguimientos)
│       ⚠️ NO uses `nlm chat start` - es solo para humanos
│
├─► Verificar estado de generación
│   └─► nlm studio status <nb-id>
│
└─► Gestionar/Limpiar
    ├─► Listar cuadernos → nlm notebook list
    ├─► Listar fuentes → nlm source list <nb-id>
    ├─► Eliminar fuente → nlm source delete <source-id> --confirm
    └─► Eliminar cuaderno → nlm notebook delete <nb-id> --confirm
```

## Categorías de Comandos

### 1. Autenticación

#### Autenticación MCP

Si usas herramientas MCP y encuentras errores de autenticación:

```bash
# Ejecuta la autenticación CLI (funciona para CLI y MCP)
nlm login

# Luego recarga los tokens en MCP
mcp__notebooklm-mcp__refresh_auth()
```

O guarda las cookies manualmente vía MCP (contingencia):
```python
# Extrae las cookies de Chrome DevTools y guarda
mcp__notebooklm-mcp__save_auth_tokens(cookies="<cookie_header>")
```

#### Autenticación CLI

```bash
nlm login                           # Lanza el navegador, extrae cookies (método principal)
nlm login --check                   # Validar sesión actual
nlm login --profile work            # Usar perfil con nombre para múltiples cuentas
nlm login --provider openclaw --cdp-url http://127.0.0.1:18800  # Proveedor CDP externo
nlm login switch <perfil>           # Cambiar el perfil por defecto
nlm login profile list              # Listar todos los perfiles con emails
nlm login profile delete <nombre>   # Eliminar un perfil
nlm login profile rename <viejo> <nuevo> # Renombrar un perfil
```

**Soporte Multi-Perfil**: Cada perfil tiene su propia sesión de navegador aislada.

**Vida de la sesión**: ~20 minutos. Re-autentícate cuando fallen los comandos.

### 2. Gestión de Cuadernos

#### Herramientas MCP
Usa herramientas: `notebook_list`, `notebook_create`, `notebook_get`, `notebook_describe`, `notebook_query`, `notebook_rename`, `notebook_delete`. Todas aceptan `notebook_id`. Eliminar requiere `confirm=True`.

#### Comandos CLI
```bash
nlm notebook list                      # Listar todos los cuadernos
nlm notebook list --json               # Salida JSON
nlm notebook list --quiet              # Solo IDs
nlm notebook create "Título"           # Crear cuaderno, devuelve ID
nlm notebook get <id>                  # Detalles del cuaderno
nlm notebook describe <id>             # Resumen IA + temas sugeridos
nlm notebook query <id> "pregunta"     # Q&A directo con fuentes
nlm notebook rename <id> "Nuevo Título" # Renombrar cuaderno
nlm notebook delete <id> --confirm     # Eliminación PERMANENTE
```

### 3. Gestión de Fuentes

#### Herramientas MCP
Usa `source_add` con estos valores de `source_type`:
- `url` - Web o YouTube (`url`)
- `text` - Contenido pegado (`text` + `title`)
- `file` - Subida de archivo local (`file_path`)
- `drive` - Google Drive doc (`document_id` + `doc_type`)

Otras: `source_list_drive`, `source_describe`, `source_get_content`, `source_rename`, `source_sync_drive` (requiere `confirm=True`), `source_delete` (requiere `confirm=True`).

#### Comandos CLI
```bash
# Añadir fuentes
nlm source add <nb-id> --url "https://..."           # Página web
nlm source add <nb-id> --url "https://youtube.com/..." # Vídeo de YouTube
nlm source add <nb-id> --text "contenido" --title "X"  # Texto pegado
nlm source add <nb-id> --drive <doc-id>              # Drive doc (auto-detectar tipo)
nlm source add <nb-id> --drive <doc-id> --type slides # Tipo explícito

# Listar y ver
nlm source list <nb-id>                # Tabla de fuentes
nlm source list <nb-id> --drive        # Fuentes de Drive con estado de frescura
nlm source get <source-id>             # Metadatos de la fuente
nlm source describe <source-id>        # Resumen IA + palabras clave
nlm source content <source-id>         # Contenido de texto crudo

# Sincronización de Drive
nlm source stale <nb-id>               # Listar fuentes de Drive desactualizadas
nlm source sync <nb-id> --confirm      # Sincronizar todas las desactualizadas

# Deletción
nlm source delete <source-id> --confirm
```

### 4. Investigación (Descubrimiento de Fuentes)

#### Herramientas MCP
Usa `research_start` con:
- `source`: `web` o `drive`
- `mode`: `fast` (~30s) o `deep` (~5min, solo web)

Flujo: `research_start` → poll `research_status` → `research_import`.

#### Comandos CLI
```bash
# Iniciar investigación (--notebook-id es OBLIGATORIO)
nlm research start "consulta" --notebook-id <id>              # Web rápida (~30s)
nlm research start "consulta" --notebook-id <id> --mode deep  # Web profunda (~5min)
nlm research start "consulta" --notebook-id <id> --source drive  # Búsqueda en Drive

# Verificar progreso
nlm research status <nb-id>                   # Poll hasta terminar
nlm research import <nb-id> <task-id>         # Importar todos los hallazgos
```

### 5. Generación de Contenido (Studio)

#### Herramientas MCP (Creación Unificada)
Usa `studio_create` con `artifact_type`. Todos requieren `confirm=True`.

| artifact_type | Opciones Clave |
|--------------|-------------|
| `audio` | `audio_format`: deep_dive/brief/critique/debate, `audio_length`: short/default/long |
| `video` | `video_format`: explainer/brief, `visual_style`: classic/whiteboard/anime... |
| `report` | `report_format`: Briefing Doc/Study Guide/Blog Post/Create Your Own, `custom_prompt` |
| `quiz` | `question_count`, `difficulty`: easy/medium/hard |
| `mind_map` | `title` |
| `slide_deck` | `slide_format`: detailed_deck/presenter_slides |
| `infographic` | `orientation`: landscape/portrait/square, `style`: professional/anime... |
| `data_table` | `description` (OBLIGATORIO) |

#### Comandos CLI
```bash
# Audio (Pódcast)
nlm audio create <id> --confirm
nlm audio create <id> --format deep_dive --confirm

# Informe (Report)
nlm report create <id> --confirm
nlm report create <id> --format "Study Guide" --confirm

# Cuestionario (Quiz)
nlm quiz create <id> --count 5 --difficulty 3 --confirm

# Diapositivas (Slides)
nlm slides create <id> --confirm
nlm slides revise <artifact-id> --slide '1 Haz el título más grande' --confirm
```

### 6. Gestión de Artefactos (Studio)

#### Herramientas MCP
Usa `studio_status` para progreso. `download_artifact` para obtener el archivo. `export_artifact` para Google Docs/Sheets. `studio_delete` (requiere `confirm=True`).

#### Comandos CLI
```bash
# Verificar estado
nlm studio status <nb-id>                          # Listar todos los artefactos

# Descargar artefactos
nlm download audio <nb-id> --output podcast.mp3
nlm download video <nb-id> --output video.mp4
nlm download report <nb-id> --output report.md
nlm download slide-deck <nb-id> --output slides.pdf
```

### 7. Configuración de Chat y Notas

#### Herramientas MCP
`chat_configure` con `goal`. `note` con `action`: create/list/update/delete.

#### Comandos CLI
```bash
# Configurar comportamiento del chat
nlm chat configure <id> --goal learning_guide
nlm chat configure <id> --response-length longer

# Gestión de notas
nlm note create <nb-id> "Contenido" --title "Título"
nlm note list <nb-id>
```

### 12. Operaciones por Lote (Batch)

#### Herramientas MCP
Usa `batch` con `action`. Selecciona cuadernos por `notebook_names`, `tags` o `all=True`.

```python
batch(action="query", query="¿Cuáles son los hallazgos?", notebook_names="Investigación IA")
batch(action="studio", artifact_type="audio", tags="research", confirm=True)
```

#### Comandos CLI
```bash
nlm batch query "Resumen" --tags "ai,research"
nlm batch studio --type audio --tags "research" --confirm
```

### 13. Consulta entre Cuadernos (Cross-Notebook)

#### Herramientas MCP
```python
cross_notebook_query(query="Compara enfoques", tags="ai,research")
```

#### Comandos CLI
```bash
nlm cross query "Compara enfoques" --tags "ai,research"
```

## Patrones Comunes

### Patrón 1: Investigación → Pódcast
```bash
nlm notebook create "IA 2026"
nlm alias set ai <id>
nlm research start "tendencias IA" --notebook-id ai --mode deep
# Esperar...
nlm research import ai <task-id>
nlm audio create ai --format deep_dive --confirm
nlm studio status ai
```

## Solución de Errores

| Error | Causa | Solución |
|-------|-------|----------|
| "Cookies have expired" | Sesión expirada | `nlm login` |
| "Notebook not found" | ID inválido | `nlm notebook list` |
| "Rate limit exceeded" | Demasiadas peticiones | Espera 30s y reintenta |

---
**Nota final**: Siempre cita fuentes y entrega enlaces de descarga claros. Respeta la privacidad del usuario y no realices eliminaciones sin confirmación.
