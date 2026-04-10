# NotebookLM - Extensión para Gemini CLI 🚀

Esta es la extensión oficial para **Gemini CLI** que te permite interactuar con **Google NotebookLM**. Con ella, puedes gestionar tus pódcast, realizar investigaciones profundas y generar guías de estudio directamente desde tu terminal con un asistente inteligente que actúa como experto en la plataforma.

---

## 🛠️ Instalación (Paso a paso)

Para usar esta extensión, necesitas completar dos pasos: uno para el **motor** (que ejecuta las llamadas a Google) y otro para la **inteligencia** (la extensión de Gemini).

### 1. Instalar el motor (NotebookLM MCP)
Abre tu terminal y ejecuta uno de los siguientes comandos (se recomienda usar `uv`):

```bash
# Recomendado:
uv tool install notebooklm-mcp-cli

# O con pip:
pip install notebooklm-mcp-cli
```

### 2. Instalar la extensión en Gemini CLI
En tu terminal de Gemini, ejecuta:

```bash
gemini extension install https://github.com/jacob-bd/notebooklm-mcp-cli
```
*(Nota: Sustituye la URL por la de este repositorio si lo has bifurcado).*

---

## 🔑 Autenticación (¡Muy importante!)

NotebookLM requiere tus credenciales de Google. Para sincronizarlas la primera vez, ejecuta:

```bash
nlm login
```
Se abrirá una ventana de Chrome para que inicies sesión. Una vez hecho, tus cookies se guardarán de forma segura en tu PC y la extensión funcionará automáticamente.

---

## 🎯 ¿Qué puedes hacer?

Simplemente pídele a Gemini que use NotebookLM:

*   "Crea un cuaderno llamado 'Investigación IA' y añade este PDF."
*   "Hazme un pódcast tipo 'Deep Dive' de mis notas."
*   "Genera un cuestionario de estudio sobre este tema."
*   "Busca en mi Drive documentos sobre marketing y crea un resumen."

---

## ⚖️ Créditos y Licencia

Este proyecto es una extensión adaptada para **Gemini CLI** basada en el excelente trabajo de **Jacob Ben-David** y su proyecto original [notebooklm-mcp-cli](https://github.com/jacob-bd/notebooklm-mcp-cli).

*   **Autor original:** Jacob Ben-David.
*   **Adaptación:** Extensión nativa para Gemini CLI.
*   **Licencia:** [MIT](LICENSE) (Compatible y respetada según los términos del proyecto original).

El código fuente del motor de ejecución reside íntegramente en el repositorio original y es mantenido por su comunidad. Esta extensión actúa como una capa de interfaz inteligente (Skill) para mejorar la experiencia de usuario en Gemini CLI.
