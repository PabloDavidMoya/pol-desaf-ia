# Lección 10 — Agentes en Producción

Llegaste a la última lección. Sabés construir agentes, darles herramientas, hacerlos planificar, trabajar en equipo y evaluarse a sí mismos.

Ahora queda el paso final: **llevar eso a producción**. Y acá es donde muchos proyectos fallan — no porque el agente no funcione, sino porque no está preparado para usuarios reales, escala real y costos reales.

---

## Los 3 pilares de producción

### Pilar 1 — Observabilidad

> "No podés mejorar lo que no podés ver."

En producción, necesitás saber qué está haciendo tu agente en todo momento:

- ¿Cuánto tarda cada consulta?
- ¿Qué herramientas está llamando y con qué frecuencia?
- ¿Dónde están fallando las respuestas?
- ¿Cuánto está costando cada interacción?

**Sin observabilidad:** el agente es una caja negra. Cuando falla, no sabés por qué.
**Con observabilidad:** el agente es una caja de vidrio. Cada paso es visible y medible.

**Métricas clave a monitorear:**

| Métrica | ¿Qué mide? |
|---|---|
| Latencia | Tiempo de respuesta — afecta la experiencia del usuario |
| Costo por consulta | Tokens usados × precio del modelo |
| Tasa de error | % de respuestas que fallan o son incorrectas |
| Uso de herramientas | Qué tools se llaman y cuántas veces |
| Feedback del usuario | Ratings, thumbs up/down, rephrasing |

---

### Pilar 2 — Evaluación continua

Producción no es un estado estático. Los modelos cambian, los datos cambian, los usuarios cambian. Necesitás evaluar continuamente que tu agente sigue funcionando bien.

**Evaluación offline:** antes de lanzar un cambio, probás contra un set de casos de prueba conocidos. Es rápido y reproducible. Ideal para CI/CD.

**Evaluación online:** monitoreás las interacciones reales en producción. Capturás casos inesperados que no tenías en tus tests.

**El ciclo recomendado:**
```
Tests offline → Deploy → Monitor en producción → Detectar fallos
      ↑                                                  ↓
      ← ← ← ← ← Agregar al dataset de tests ← ← ← ← ← ←
```

---

### Pilar 3 — Control de costos

Cada llamada a Claude tiene un costo en tokens. A escala, esto puede ser significativo.

**Estrategias para reducir costos sin sacrificar calidad:**

| Estrategia | Ahorro estimado | Complejidad |
|---|---|---|
| **System prompts concisos** | 10-30% | Baja |
| **Usar modelos más pequeños** para tareas simples | 50-80% | Media |
| **Caché de respuestas** frecuentes | 40-70% | Media |
| **Router de complejidad** | 30-60% | Alta |
| **Limitar `max_tokens`** | 10-25% | Baja |

**El router de complejidad** es especialmente poderoso: un modelo pequeño y barato analiza cada consulta y decide si la puede responder él mismo o si necesita escalar al modelo más potente.

```
Consulta del usuario
        ↓
Router (modelo pequeño, barato)
        ↓
¿Es compleja?
   NO → Responde el modelo pequeño (barato)
   SÍ → Escala al modelo grande (potente)
```

---

## Problemas comunes en producción

| Problema | Síntoma | Solución |
|---|---|---|
| Respuestas inconsistentes | El agente da respuestas diferentes a la misma pregunta | Refinar el system prompt, bajar temperatura |
| Bucles infinitos | El agente sigue llamando herramientas sin terminar | Agregar límite de iteraciones |
| Herramientas mal llamadas | Parámetros incorrectos o herramientas innecesarias | Mejorar las descripciones de las tools |
| Costo descontrolado | Facturas altas inesperadamente | Implementar logging de tokens y alertas |
| Deriva del modelo | Con el tiempo el agente responde diferente | Evaluación continua con dataset fijo |

---

## Checklist para ir a producción

Antes de lanzar tu agente a usuarios reales, verificá:

- [ ] ¿Tenés logging de latencia y errores?
- [ ] ¿Tenés un set de casos de prueba para evaluar regresiones?
- [ ] ¿Implementaste validación de inputs (lección 06)?
- [ ] ¿Hay un límite de tokens por consulta?
- [ ] ¿El agente maneja errores de herramientas graciosamente?
- [ ] ¿Tenés un mecanismo de feedback del usuario?
- [ ] ¿Sabés cuánto cuesta una interacción promedio?

---

## Abrí el notebook

En `code_samples/10-produccion.ipynb` vas a implementar:
1. Logging de observabilidad (latencia, tokens, herramientas usadas)
2. Sistema de evaluación automática con agente evaluador
3. Router de complejidad para optimizar costos
4. Dashboard simple de métricas en texto

---

## Resumen

| Pilar | Herramientas | Beneficio |
|---|---|---|
| Observabilidad | Logging, trazas, métricas | Visibilidad total del agente |
| Evaluación | Tests offline + online | Calidad sostenida en el tiempo |
| Costos | Caché, modelos pequeños, router | Escalar sin arruinarse |

---

## ¡Felicitaciones! Completaste el curso

Si llegaste hasta acá, pasaste de no saber qué es un agente de IA a poder construir sistemas multi-agente seguros, confiables y listos para producción — todo con Claude.

El siguiente paso es tu propio proyecto. Usá lo que aprendiste, rompé cosas, iterá y compartí tus avances en la comunidad.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
