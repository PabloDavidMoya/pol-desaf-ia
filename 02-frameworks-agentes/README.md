# Lección 02 — Frameworks para Agentes de IA

En la lección anterior construiste tu primer agente desde cero. Funcionó, pero el código era bastante manual — tuviste que escribir el bucle completo, manejar los mensajes y controlar cada paso.

En esta lección vamos a ver **cómo los frameworks simplifican todo eso** y cuándo conviene usarlos.

---

## ¿Qué es un framework de agentes?

Un **framework** es como un conjunto de herramientas prearmadas que te ahorran escribir código repetitivo.

Imaginá que construir un agente sin framework es como armar un mueble desde la madera cruda. Un framework es como comprar el mueble en IKEA: todavía lo armás vos, pero ya viene cortado y con instrucciones.

**Sin framework** (lo que hiciste en la lección 01):
- Escribís el bucle agente manualmente
- Gestionás los mensajes vos mismo
- Manejás el historial de conversación a mano

**Con framework:**
- El bucle ya está resuelto
- La memoria/historial se maneja solo
- Podés agregar herramientas fácilmente

---

## Los tres enfoques que vamos a ver

| Enfoque | ¿Cuándo usarlo? | Complejidad |
|---|---|---|
| **SDK directo de Claude** | Proyectos simples, aprender | Básica |
| **Clase Agente personalizada** | Proyectos propios, control total | Media |
| **LangChain + Claude** | Proyectos grandes, muchas integraciones | Media-Alta |

---

## Enfoque 1 — SDK Directo (repaso de lección 01)

Ya lo conocés. Es el enfoque más explícito: vos controlás todo.

**Ideal cuando:** estás aprendiendo o el agente es simple.

**Limitación:** si el agente crece, el código se vuelve difícil de mantener.

---

## Enfoque 2 — Clase Agente Personalizada

La solución de punto medio: crear tu propia clase `Agente` que encapsula el bucle y la memoria. Esto te da control total pero con código más limpio y reutilizable.

Este es el enfoque que más usarás en proyectos propios.

Mirá el notebook `code_samples/02-clase-agente.ipynb` para ver cómo se construye.

---

## Enfoque 3 — LangChain con Claude

[LangChain](https://python.langchain.com/) es uno de los frameworks más populares del ecosistema de IA. Tiene integraciones con cientos de herramientas, bases de datos y servicios.

**Ideal cuando:**
- Necesitás conectar el agente con muchas fuentes de datos
- Querés usar herramientas prefabricadas (búsqueda web, bases de datos, etc.)
- El proyecto es grande y trabajan varias personas

**Limitación:** más complejo de aprender, menos control fino sobre el comportamiento del agente.

Mirá el notebook `code_samples/02-langchain-claude.ipynb` para ver un ejemplo.

---

## ¿Cuál elegir?

```
¿Estás aprendiendo o el agente es simple?
    → SDK directo de Claude

¿Querés control total con código limpio?
    → Clase Agente personalizada

¿Necesitás muchas integraciones o el proyecto es grande?
    → LangChain + Claude
```

Para el 80% de los proyectos que vas a hacer, **la Clase Agente personalizada** es la mejor opción. Es lo que usaremos en el resto del curso.

---

## Conceptos clave de esta lección

- **Framework:** conjunto de herramientas prearmadas para simplificar el desarrollo
- **Sesión / Memoria:** historial de conversación que el agente recuerda entre mensajes
- **Multi-turno:** conversación donde el agente recuerda lo que se habló antes
- **Encapsulación:** agrupar el código relacionado en una clase para reutilizarlo

---

## Resumen

| Concepto | Descripción |
|---|---|
| SDK directo | Control total, más código manual |
| Clase personalizada | Balance ideal para proyectos propios |
| LangChain | Ecosistema amplio, más abstracción |
| Sesión | Memoria de conversación del agente |

---

## Siguiente lección

En la [Lección 03](../03-patrones-diseno/README.md) vamos a ver los **patrones de diseño** más usados en sistemas de agentes — las recetas probadas para resolver problemas comunes.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
