# Lección 03 — Patrones de Diseño para Agentes

Ya sabés construir un agente. Ahora viene algo más importante: **saber diseñarlo bien**.

Un agente mal diseñado funciona, pero da respuestas inconsistentes, es difícil de mantener y falla cuando los casos se complican. Un agente bien diseñado escala, es predecible y es fácil de mejorar.

En esta lección vas a aprender los **3 patrones de diseño** que usan los expertos.

---

## ¿Qué es un patrón de diseño?

Es una **solución probada** para un problema recurrente. No inventás la rueda cada vez — aplicás una receta que ya funcionó en miles de proyectos.

Pensalo como las recetas de cocina: podés inventar cómo hacer una pizza desde cero, o podés usar una receta que ya saben que funciona.

---

## Los 3 Patrones

### Patrón 1 — Instrucciones claras

El patrón más simple y el más impactante. La calidad del agente depende directamente de qué tan bien le explicás quién es y qué debe hacer.

**Malas instrucciones:**
```
Sos un asistente de viajes. Ayudá al usuario.
```

**Buenas instrucciones:**
```
Sos Alex, un concierge de viajes especializado en Latinoamérica.
Tu rol es:
1. Entender el presupuesto y preferencias del viajero
2. Verificar disponibilidad antes de recomendar
3. Dar sugerencias personalizadas con precios y época ideal
Siempre respondé en español, con tono cálido y profesional.
```

**¿Por qué funciona?** Las instrucciones claras definen:
- **Quién** es el agente (persona y tono)
- **Qué** debe hacer (responsabilidades paso a paso)
- **Cómo** debe comportarse (restricciones y estilo)

---

### Patrón 2 — Salida estructurada

Cuando el agente devuelve texto libre, es útil para conversación. Pero cuando necesitás procesar el resultado con código, necesitás **datos estructurados y predecibles**.

**Sin patrón** (texto libre):
```
"Te recomiendo Barcelona. Está disponible en mayo. El presupuesto es de unos 2000 dólares."
```

**Con patrón** (datos estructurados):
```python
{
  "destino": "Barcelona",
  "disponible": True,
  "mejor_epoca": "mayo-junio",
  "presupuesto_usd": 2000,
  "actividades": ["playa", "arquitectura", "gastronomía"]
}
```

El segundo formato podés guardarlo en una base de datos, mostrarlo en una UI o pasárselo a otro sistema sin tener que "parsear" texto a mano.

---

### Patrón 3 — Agente de responsabilidad única

Las tareas complejas se resuelven mejor con **múltiples agentes especializados**, cada uno haciendo una sola cosa bien.

**Sin patrón** (un agente hace todo):
```
Agente todo-en-uno → busca destinos + verifica vuelos + genera itinerario + calcula presupuesto
```
Resultado: respuestas inconsistentes, difícil de depurar, falla en casos complejos.

**Con patrón** (agentes especializados):
```
Agente Destinos → solo recomienda lugares
     ↓
Agente Logística → solo planifica vuelos e itinerario
     ↓
Agente Presupuesto → solo calcula costos
```
Resultado: cada agente es simple, testeable y mejorable por separado.

---

## Guía de diseño — principios clave

Más allá de los patrones, hay 3 principios que deben guiar cualquier agente que construyas:

| Principio | ¿Qué significa? | Ejemplo práctico |
|---|---|---|
| **Transparencia** | El usuario sabe que habla con una IA | "Soy un asistente de IA, puedo equivocarme" |
| **Control** | El usuario puede modificar y corregir | "Podés cambiar mis preferencias en cualquier momento" |
| **Consistencia** | El agente se comporta igual siempre | Mismo tono y formato en todas las respuestas |

---

## Abrí el notebook

En `code_samples/03-patrones-diseno.ipynb` vas a ver los 3 patrones implementados con Claude, con ejemplos que podés ejecutar directamente.

---

## Resumen

| Patrón | Problema que resuelve | Cuándo usarlo |
|---|---|---|
| Instrucciones claras | Respuestas inconsistentes | Siempre — es el punto de partida |
| Salida estructurada | Datos difíciles de procesar | Cuando el resultado va a otro sistema |
| Responsabilidad única | Agentes que hacen demasiado | Tareas complejas con múltiples pasos |

---

## Siguiente lección

En la [Lección 04](../04-herramientas-tool-use/README.md) profundizamos en las **herramientas (tools)** — cómo diseñarlas bien, combinarlas y manejar los casos donde pueden fallar.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
