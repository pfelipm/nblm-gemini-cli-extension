# NotebookLM expert - extensión para Gemini CLI 🚀

**Nota:** *Esta es una extensión de la comunidad. No es una extensión oficial de Google ni del equipo de NotebookLM.*

Esta extensión para **Gemini CLI** es un **empaquetado (wrapper)** nativo para el excelente motor de **NotebookLM MCP** desarrollado por [Jacob Ben-David](https://github.com/jacob-bd/notebooklm-mcp-cli).

---

## 🧐 ¿Por qué existe esta extensión?

Este proyecto ha sido construido principalmente como un **ejercicio de aprendizaje** por [pfelipm](https://github.com/pfelipm) para familiarizarse con la estructura, las habilidades (skills) y la integración de servidores MCP dentro del ecosistema de **Gemini CLI**.

Aunque el proyecto original de Jacob ya permite la conexión con Gemini CLI mediante comandos manuales, esta extensión ofrece una experiencia **"Plug-and-play"**:
1.  **Instalación simplificada:** configura el servidor MCP, carga la habilidad experta (skill) y el contexto (`GEMINI.md`) en un solo paso con `gemini extension install`.
2.  **Configuración predefinida:** activa automáticamente el soporte para el idioma español (`es`) para mejorar la generación de contenidos y la interacción.
3.  **Habilidad nativa:** utiliza la guía experta original de Jacob (en inglés para máxima precisión técnica) para que Gemini actúe como un experto avanzado en la plataforma.

---

## 🛠️ Instalación (paso a paso)

### 1. Instalar el motor (NotebookLM MCP)
Esta extensión depende del paquete de Python original. Instálalo globalmente (se recomienda `uv`):

```bash
# Recomendado:
uv tool install notebooklm-mcp-cli

# O con pip:
pip install notebooklm-mcp-cli
```

### 2. Instalar la extensión en Gemini CLI
En tu terminal de Gemini, ejecuta:

```bash
gemini extension install https://github.com/pfelipm/nblm-gemini-cli-extension
```

---

## 🔑 Autenticación (paso obligatorio)

NotebookLM requiere tus credenciales de Google. Para sincronizarlas la primera vez, ejecuta en tu terminal:

```bash
nlm login
```
Sigue los pasos en el navegador para iniciar sesión. Una vez hecho, Gemini podrá realizar las operaciones en tu nombre.

---

## 🎯 Ejemplos de uso

*   "Crea un cuaderno llamado 'Investigación IA' y añade este PDF."
*   "Genera un pódcast de tipo 'Deep dive' basado en mis fuentes."
*   "¿Cuáles son los puntos clave de este cuaderno? Cita las fuentes."
*   "Crea una guía de estudio (report) y dame el enlace de descarga."

---

## ⚖️ Créditos y licencia

Este proyecto es una adaptación educativa basada íntegramente en el motor y la documentación técnica de **Jacob Ben-David** ([notebooklm-mcp-cli](https://github.com/jacob-bd/notebooklm-mcp-cli)).

*   **Motor, skills y contexto original:** Jacob Ben-David.
*   **Empaquetado y adaptación Gemini CLI:** [pfelipm](https://github.com/pfelipm).
*   **Licencia:** [MIT](LICENSE).

Esta extensión respeta íntegramente la licencia original y actúa como una capa de conveniencia para la comunidad de Gemini CLI.
