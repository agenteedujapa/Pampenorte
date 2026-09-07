# Pampenorte — Workflows n8n

Control de versiones de los flujos de n8n del proyecto Pampenorte (agente de IA + paneles internos), exportados desde la instancia `pampenorte.freeddns.org`.

## Estructura

```
cordoba/
  chatbox-agente-1-v2.json       Chatbot/agente de IA de Córdoba (RAG sobre base de conocimiento + acciones)
  panel-vendedor-cordoba.json    Panel interno del vendedor (dashboard)
  indexador-agente-1.json        Indexa la carpeta de Drive "Pampenorte Cba" a Supabase (tabla documents)

tucuman/
  chatbox-agente-tuc-v2.json     Chatbot de Tucumán v2 (copia adaptada del agente de Córdoba)
  chatbox-agente-tuc-v3.json     Chatbot de Tucumán v3 — agrega menú de inicio, manejo de horario, foto/audio y mayorista
  panel-vendedor-tucuman.json    Panel interno del vendedor de Tucumán (copia adaptada del de Córdoba)
  indexador-agente-tucuman.json  Indexa la carpeta de Drive "Pampenorte Tuc" a Supabase (tabla documents_tucuman)

shared/
  panel-auth.json                Login / logout / validación de sesión, usado por ambos paneles (Córdoba y Tucumán)
```

## Notas

- Cada archivo es un export de workflow en formato nativo de n8n (`name`, `nodes`, `connections`, `settings`, `tags`), importable directamente desde la UI (Import from File) o vía API/CLI.
- Las credenciales de n8n (Supabase, Google Drive, Whapi, etc.) **no** viajan en estos archivos — hay que volver a asignarlas al importar en otra instancia.
- `chatbox-agente-tuc-v2.json` y `chatbox-agente-tuc-v3.json` son snapshots de dos workflows distintos en n8n (v3 es un clon de v2 al que se le aplicaron cambios), no distintas versiones de un mismo archivo — por eso ambos quedan versionados por separado.
- El campo `active` refleja el estado en n8n al momento del export, no si el workflow "debería" estar activo.

## Próximos pasos

Por ahora el versionado es manual: exportar desde n8n y hacer commit a mano. El plan es migrar a un proceso automatizado (script o GitHub Action) que detecte cambios y haga commit solo, sin intervención manual.
