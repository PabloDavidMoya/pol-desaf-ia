# Lección 08 — Sistemas Multi-Agente

Un solo agente puede hacer muchas cosas. Pero algunos problemas son demasiado complejos, demasiado grandes o requieren demasiada especialización para un único agente.

La solución: **múltiples agentes que trabajan juntos**.

---

## ¿Cuándo usar múltiples agentes?

| Situación | Ejemplo |
|---|---|
| **Tareas paralelas** | Investigar 5 temas al mismo tiempo |
| **Especialización** | Un agente para redactar, otro para revisar |
| **Escalabilidad** | Procesar 1000 consultas distribuyendo la carga |
| **Confiabilidad** | Si un agente falla, otro puede continuar |

---

## Los 3 patrones de flujo multi-agente

### Patrón 1 — Flujo Secuencial

Los agentes trabajan en cadena. El output de uno es el input del siguiente.

```
Agente A → Agente B → Agente C → Resultado final
```

**Cuándo usarlo:** cuando cada paso depende del anterior y el orden importa.

**Ejemplo:** Investigador → Redactor → Editor → Publicador

---

### Patrón 2 — Flujo Concurrente (Fan-Out)

Un agente distribuye trabajo a múltiples agentes que trabajan en paralelo.

```
         → Agente B ↘
Agente A → Agente C → Resultado combinado
         → Agente D ↗
```

**Cuándo usarlo:** cuando las subtareas son independientes entre sí y querés velocidad.

**Ejemplo:** Un dispatcher envía la misma consulta a 3 agentes especializados simultáneamente.

---

### Patrón 3 — Flujo Condicional

El flujo se bifurca según el resultado de un agente.

```
Agente A → Agente Revisor → ¿Aprobado? → Sí → Agente Publicador
                                        → No → Agente Corrector
```

**Cuándo usarlo:** cuando necesitás tomar decisiones basadas en el resultado intermedio.

**Ejemplo:** Un agente genera contenido, un revisor lo valida, y según el resultado va a publicación o a corrección.

---

## Comunicación entre agentes

Los agentes se "comunican" pasando mensajes — texto o JSON — de uno a otro. Hay tres formas:

| Forma | ¿Cómo funciona? | Ejemplo |
|---|---|---|
| **Directo** | A llama a B explícitamente | Agente ejecutor llama al especialista |
| **Orquestador** | Un agente central coordina a todos | Agente manager distribuye tareas |
| **Basado en eventos** | Los agentes reaccionan a eventos | Cuando falla X, se activa Y |

---

## El rol del Orquestador

En sistemas complejos, conviene tener un **agente orquestador** que:
1. Recibe la tarea del usuario
2. Decide qué agentes activar y en qué orden
3. Agrega los resultados
4. Devuelve la respuesta final

```
Usuario
   ↓
Orquestador
   ↓          ↓          ↓
Agente A   Agente B   Agente C
   ↓          ↓          ↓
        Orquestador (agrega)
              ↓
           Usuario
```

---

## Abrí el notebook

En `code_samples/08-multi-agente.ipynb` vas a implementar los 3 patrones con Claude:
1. **Secuencial:** pipeline de redacción (investigar → escribir → revisar)
2. **Concurrente:** múltiples agentes trabajando en paralelo con `asyncio`
3. **Condicional:** flujo con bifurcación según el resultado de revisión

---

## Resumen

| Patrón | Flujo | Ideal para |
|---|---|---|
| Secuencial | A → B → C | Pasos que dependen entre sí |
| Concurrente | A → B, C, D en paralelo | Subtareas independientes |
| Condicional | Bifurcación según resultado | Lógica de negocio compleja |

---

## Siguiente lección

En la [Lección 09](../09-metacognicion/README.md) vamos a ver la **metacognición** — cómo hacer que los agentes evalúen y mejoren sus propias respuestas.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
