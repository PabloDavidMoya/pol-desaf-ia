# Lección 09 — Metacognición

"Pensar sobre el propio pensamiento." Eso es la metacognición.

En los humanos es lo que nos permite darnos cuenta cuando cometemos un error y corregirlo. En los agentes de IA, es lo que les permite **evaluar sus propias respuestas, detectar fallas y adaptarse** sin que vos tengas que intervenir.

---

## ¿Por qué importa la metacognición en agentes?

Un agente sin metacognición hace lo que puede y devuelve una respuesta, aunque sea incorrecta o incompleta. Un agente con metacognición:

- **Se da cuenta** cuando una herramienta falla y busca alternativas
- **Evalúa** si su respuesta fue completa antes de devolverla
- **Aprende** de las interacciones anteriores para mejorar
- **Explica** su razonamiento de forma transparente

La diferencia entre un agente experimental y uno confiable para producción está en gran parte aquí.

---

## Los 3 mecanismos de metacognición

### 1. Recuperación ante errores (Fallback)

El agente intenta una herramienta, detecta que falló y automáticamente prueba una alternativa. No se rompe — se adapta.

```
Intenta herramienta principal
         ↓
    ¿Funcionó?
    SÍ → devuelve resultado
    NO → detecta el error → prueba herramienta de respaldo → informa al usuario
```

**Ejemplo:** Un agente busca vuelos en el sistema principal. Si falla con error 404, cambia al sistema de respaldo y le explica al usuario lo que pasó.

---

### 2. Auto-evaluación

Después de generar una respuesta, el agente la evalúa contra criterios predefinidos antes de entregarla al usuario.

```
Generar respuesta → Evaluar (¿es completa? ¿es precisa? ¿es útil?) → Ajustar si hace falta → Entregar
```

**Ejemplo:** Un agente escribe una recomendación, luego se pregunta "¿respondí todas las partes de la pregunta?" y si no, la completa.

---

### 3. Aprendizaje por feedback

El agente guarda un registro de qué funcionó y qué no, y usa esa información para tomar mejores decisiones en el futuro.

```
Interacción → Resultado → Feedback → Actualizar estrategia → Próxima interacción
```

**Ejemplo:** Si el usuario rechazó las últimas 3 recomendaciones de hotel económico, el agente ajusta su estrategia hacia opciones de mayor calidad.

---

## RAG Correctivo

Una aplicación práctica de metacognición: el **RAG correctivo**. En vez de confiar ciegamente en lo que recupera, el agente evalúa si la información es relevante y, si no lo es, vuelve a buscar con una consulta refinada.

```
Consulta del usuario
        ↓
Buscar en base de conocimiento
        ↓
¿La información es relevante?
   SÍ → responder
   NO → reformular la búsqueda → buscar de nuevo → responder
```

---

## El agente Maker-Evaluador

Un patrón poderoso: dos agentes trabajando juntos.

| Agente | Rol |
|---|---|
| **Maker** | Genera la respuesta |
| **Evaluador** | Puntúa la respuesta y sugiere mejoras |

El Evaluador actúa como el "crítico interno" del sistema, asegurando calidad antes de que la respuesta llegue al usuario.

---

## Abrí el notebook

En `code_samples/09-metacognicion.ipynb` vas a implementar:
1. Agente con recuperación ante errores (fallback automático)
2. Auto-evaluación de respuestas con puntaje
3. Sistema de aprendizaje por feedback
4. El patrón Maker-Evaluador completo

---

## Resumen

| Mecanismo | ¿Qué hace? | Beneficio |
|---|---|---|
| Fallback | Detecta errores y usa alternativas | Resiliencia ante fallas |
| Auto-evaluación | Evalúa la respuesta antes de entregarla | Calidad consistente |
| Feedback | Aprende de interacciones pasadas | Mejora con el tiempo |
| RAG Correctivo | Re-busca si la información no es relevante | Precisión mejorada |

---

## Siguiente lección

En la [Lección 10](../10-produccion/README.md) — la última — vemos cómo llevar tus agentes a **producción real**: observabilidad, evaluación continua y control de costos.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
