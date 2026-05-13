# Configurar Un LLM Local

> Ejecutá un modelo local para Librarian y tu LLM Wiki en Obsidian.

Esta guía muestra cómo configurar un endpoint local compatible con OpenAI usando Ollama. El objetivo es simple: mantener tus notas locales por defecto y darle a Librarian un modelo al que pueda llamar vía `http://127.0.0.1:11434/v1`.

> **Prefer to read in English?** → [README.md](./README.md)

## Por Qué Local

Los modelos locales son útiles para una base de conocimiento personal porque:

- Tus notas se quedan en tu máquina o red local.
- Podés experimentar sin mandar material privado a un proveedor cloud.
- Librarian puede usar la misma forma de API compatible con OpenAI.
- Tenés control sobre modelo, latencia y costo.

Local no significa privacidad perfecta en cualquier configuración. Si exponés Ollama en tu red, tratá ese endpoint como infraestructura sensible.

## Stack Recomendado

Usá Ollama primero. Es el runtime local más simple para este ecosistema.

Default recomendado:

```env
OLLAMA_BASE_URL=http://127.0.0.1:11434/v1
OLLAMA_MODEL=qwen3.5:4b
OLLAMA_FALLBACK_MODEL=llama3.1:8b
OLLAMA_TIMEOUT_MS=600000
```

Si `qwen3.5:4b` no está disponible en tu instalación de Ollama, usá un modelo que ya tengas, por ejemplo `llama3.1:8b`, `qwen2.5:7b` u otro modelo instruct.

## 1. Instalar Ollama

Descargá Ollama desde:

```text
https://ollama.com/download
```

Instalalo para tu sistema operativo y asegurate de que el comando `ollama` esté disponible en la terminal.

Verificá:

```bash
ollama --version
```

## 2. Descargar Un Modelo

Empezá con un modelo:

```bash
ollama pull qwen3.5:4b
```

Si ese modelo no está disponible, usá:

```bash
ollama pull llama3.1:8b
```

Podés listar modelos instalados con:

```bash
ollama list
```

## 3. Iniciar Ollama

Ollama normalmente corre como app de fondo después de instalarse. Si necesitás iniciarlo manualmente:

```bash
ollama serve
```

El endpoint default es:

```text
http://127.0.0.1:11434
```

Librarian usa el path compatible con OpenAI:

```text
http://127.0.0.1:11434/v1
```

## 4. Probar El Endpoint

Chequeá que la API compatible con OpenAI responda:

```bash
curl http://127.0.0.1:11434/v1/models
```

Deberías ver JSON con los modelos que Ollama conoce.

Después probá una respuesta de chat:

```bash
curl http://127.0.0.1:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen3.5:4b",
    "messages": [
      {"role": "user", "content": "Respondé hola en una oración."}
    ],
    "stream": false
  }'
```

Si descargaste `llama3.1:8b`, reemplazá el nombre del modelo.

## 5. Configurar Librarian

Librarian vive en un repositorio separado:

```bash
git clone git@github.com:Agents4Life/librarian.git
cd librarian
```

Después copiá el template de entorno:

```bash
cp .env.example .env
```

Configurá el modelo local:

```env
OLLAMA_BASE_URL=http://127.0.0.1:11434/v1
OLLAMA_MODEL=qwen3.5:4b
OLLAMA_FALLBACK_MODEL=llama3.1:8b
OLLAMA_TIMEOUT_MS=600000
LIBRARIAN_VAULT_PATH=/path/to/your/obsidian/vault
```

No configures una API key cloud salvo que quieras usar explícitamente un proveedor cloud.

## 6. Ejecutar Librarian

Desde el repo separado de Librarian:

```bash
npm install
npm run build
npm link
librarian "pregunta sobre mi wiki"
```

O abrí la TUI:

```bash
librarian
```

## Elegir Modelo

Para un agente de wiki personal, priorizá seguimiento de instrucciones y confiabilidad por sobre tamaño bruto.

| Máquina | Punto de partida | Notas |
|---------|------------------|-------|
| 8 GB RAM | modelo chico 3B-4B | Bueno para routing y resúmenes simples |
| 16 GB RAM | modelo 7B-8B | Mejor calidad, todavía práctico localmente |
| 32 GB+ RAM | modelo 14B+ | Mejor síntesis, más lento y pesado |

Si la latencia molesta, usá un modelo chico para routing y uno más grande solo para curaduría/síntesis más adelante.

## Seguridad

- Mantené `OLLAMA_BASE_URL` en `127.0.0.1` salvo que necesites acceso por red.
- No expongas Ollama directamente a internet.
- Si corrés Ollama en otra máquina, usá una red privada confiable.
- Tratá tu vault como datos privados.
- No commitees API keys cloud.

## Troubleshooting

### `curl /v1/models` falla

Asegurate de que Ollama esté corriendo:

```bash
ollama serve
```

### Modelo no encontrado

Descargá el modelo primero:

```bash
ollama pull llama3.1:8b
```

Después configurá `OLLAMA_MODEL=llama3.1:8b`.

### Librarian hace timeout

Usá un modelo más chico o aumentá:

```env
OLLAMA_TIMEOUT_MS=600000
```

### Ollama remoto no funciona

Preferí local primero. Si intencionalmente usás otra máquina, configurá:

```env
OLLAMA_BASE_URL=http://TU_IP_PRIVADA:11434/v1
```

Hacelo solo en una red privada confiable.

## Próximo Paso

Cuando el modelo local funcione, seguí con [Siguiente Nivel con IA](../second-brain/guides/es/07-next-level-with-ai.md) y configurá Librarian contra tu vault de Obsidian.
