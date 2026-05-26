# Lección 05 — Memoria y RAG Agéntico

Hasta ahora tus agentes saben lo que vos les decís y lo que tienen en su system prompt. Pero ¿qué pasa cuando necesitan consultar **tu propia información**? ¿Documentos, bases de conocimiento, datos de tu negocio?

Eso es exactamente lo que resuelve el **RAG Agéntico**.

---

## ¿Qué es RAG?

**RAG** significa *Retrieval-Augmented Generation* — generación aumentada por recuperación.

En términos simples: en vez de que Claude "adivine" la respuesta, primero **busca información relevante** en tu base de datos y después responde basándose en esos datos reales.

```
Sin RAG:
Usuario → Claude → responde con lo que "sabe" (puede alucinar)

Con RAG:
Usuario → Claude → busca en tu base de datos → responde con información real
```

---

## RAG tradicional vs. RAG Agéntico

| | RAG Tradicional | RAG Agéntico |
|---|---|---|
| **Cómo busca** | Siempre el mismo pipeline fijo | El agente decide cuándo y cómo buscar |
| **Cuántas búsquedas** | Una sola por pregunta | Puede hacer múltiples búsquedas iterativas |
| **Si no encuentra** | Devuelve lo más cercano | Reformula la búsqueda y reintenta |
| **Autonomía** | Ninguna | Alta |

**La diferencia clave:** en RAG agéntico, Claude decide autónomamente si necesita más información, cuántas veces buscar y qué buscar en cada iteración.

---

## El patrón Maker-Checker

Una técnica potente del RAG agéntico: usar **dos agentes** para verificar la calidad de las respuestas.

```
Pregunta del usuario
        ↓
  [Maker] Busca y responde
        ↓
  [Checker] Verifica la respuesta buscando nuevamente
        ↓
  Respuesta verificada y más precisa
```

Es como tener un escritor y un editor trabajando juntos.

---

## Tipos de memoria en agentes

Los agentes pueden tener diferentes tipos de memoria:

| Tipo | ¿Qué guarda? | Duración |
|---|---|---|
| **Memoria de conversación** | El historial del chat | Solo la sesión actual |
| **Base de conocimiento** | Documentos, FAQs, datos de negocio | Permanente |
| **Memoria de usuario** | Preferencias y contexto de cada usuario | Configurable |
| **Memoria episódica** | Experiencias y decisiones pasadas | Persistente entre sesiones |

En esta lección nos enfocamos en la **base de conocimiento** — la más común y útil para proyectos reales.

---

## Casos de uso prácticos

- **Soporte al cliente:** el agente consulta tu documentación antes de responder
- **Asistente de ventas:** el agente conoce tu catálogo de productos actualizado
- **Tutor de cursos:** el agente consulta el material del curso para responder preguntas
- **Agente legal:** el agente busca en leyes y regulaciones específicas

---

## Abrí el notebook

En `code_samples/05-memoria-rag.ipynb` vas a construir:
1. Una base de conocimiento propia (simulando documentos reales)
2. Un agente RAG que busca antes de responder
3. El patrón Maker-Checker con dos agentes que se verifican mutuamente

---

## Resumen

| Concepto | Descripción |
|---|---|
| RAG | Buscar información antes de responder |
| RAG Agéntico | El agente decide cuándo y cómo buscar |
| Base de conocimiento | Tu información como herramienta del agente |
| Maker-Checker | Doble verificación con dos agentes |

---

## Siguiente lección

En la [Lección 06](../06-agentes-confiables/README.md) vamos a ver cómo construir agentes **seguros y confiables** — cómo protegerlos de ataques, cómo diseñar buenos system prompts y cómo mantener al humano en control.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
