# NotebookLM Expert - Extensión para Gemini CLI 🚀

**Nota:** *Esta es una extensión de la comunidad. No es una extensión oficial de Google ni del equipo de NotebookLM.*

Esta extensión para **Gemini CLI** actúa como una capa de inteligencia (Expert Skill) sobre el motor de **NotebookLM MCP**. Te permite gestionar tus cuadernos, realizar investigaciones profundas y generar contenido multimedia (pódcast, vídeos, guías) con un asistente que comprende los flujos de trabajo específicos de la plataforma.

---

## 🧐 ¿Por qué usar esta extensión?

El proyecto original de **Jacob Ben-David** ya incluye un comando (`nlm setup add gemini`) que conecta el servidor MCP con Gemini CLI. Sin embargo, esta extensión aporta tres pilares fundamentales que no se obtienen con la configuración básica:

1.  **Expert Skill (Habilidad Especializada):** Incluye un archivo `SKILL.md` que instruye al modelo de lenguaje sobre *cómo* razonar con las herramientas de NotebookLM. El asistente sabrá que para darte un enlace de pódcast debe primero verificar el estado de generación y luego usar la herramienta de descarga, en lugar de simplemente fallar.
2.  **Contexto Enriquecido:** Proporciona un archivo de contexto que resume todas las capacidades del sistema, permitiendo que Gemini entienda mejor qué puede y qué no puede hacer sin tener que adivinar.
3.  **Configuración Predefinida:** Configura automáticamente variables de entorno críticas (como el idioma español `es`) para asegurar que la experiencia sea coherente desde el primer minuto.

---

## 🛠️ Instalación (Paso a paso)

### 1. Instalar el motor (NotebookLM MCP)
Abre tu terminal y instala el paquete de Python (se recomienda usar `uv`):

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

## 🔑 Autenticación (¡Muy importante!)

Para que la extensión funcione, debes sincronizar tus credenciales de Google una sola vez ejecutando:

```bash
nlm login
```
Esto abrirá tu navegador para realizar el login. Una vez hecho, tus cookies se guardarán de forma segura y Gemini podrá realizar las operaciones en tu nombre.

---

## 🎯 Ejemplos de uso

*   "Investiga sobre la fusión nuclear y crea un nuevo cuaderno con lo que encuentres."
*   "Genera un pódcast de tipo 'Deep Dive' basado en mis fuentes."
*   "¿Cuáles son los puntos clave de este cuaderno? Cita las fuentes."
*   "Crea una guía de estudio (report) y dame el enlace de descarga."

---

## ⚖️ Créditos y Licencia

Este proyecto es una adaptación para **Gemini CLI** basada en el motor de **Jacob Ben-David** ([notebooklm-mcp-cli](https://github.com/jacob-bd/notebooklm-mcp-cli)).

*   **Motor original:** Jacob Ben-David.
*   **Adaptación de la Extensión:** [pfelipm](https://github.com/pfelipm).
*   **Licencia:** [MIT](LICENSE).

Esta extensión respeta íntegramente la licencia original y actúa como un puente de inteligencia para mejorar la experiencia de usuario en Gemini CLI.
