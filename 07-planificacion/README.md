# Lección 07 — Planificación

Hasta ahora tus agentes reaccionan a preguntas. En esta lección van a aprender a **planificar** — a dividir una tarea compleja en pasos antes de ejecutarla.

La planificación es lo que separa un agente simple de uno que puede resolver problemas del mundo real.

---

## ¿Por qué planificar?

Imaginate que le pedís a un agente: *"Organizame un viaje de 7 días a Europa"*.

Un agente sin planificación intenta resolver todo de una vez y se pierde. Un agente con planificación primero divide el problema:

```
Tarea: Viaje a Europa 7 días
  ↓
Plan:
  1. Buscar vuelos (alta prioridad)
  2. Reservar hotel (depende de 1)
  3. Seleccionar actividades (depende de 2)
  4. Calcular presupuesto total (depende de 1, 2 y 3)
```

Cada subtarea es simple. En conjunto resuelven algo complejo.

---

## Los 3 elementos del patrón de planificación

### 1. Descomposición de tareas

Dividir el objetivo grande en subtareas manejables, cada una con:
- **Descripción clara** de qué hacer
- **Prioridad** (alta, media, baja)
- **Dependencias** (qué debe completarse antes)
- **Agente responsable** de ejecutarla

### 2. Plan estructurado

El plan se genera como JSON — formato que tanto el código como otros agentes pueden procesar:

```json
{
  "objetivo": "Viaje familiar a París, 7 días, USD 5000",
  "subtareas": [
    {
      "id": 1,
      "descripcion": "Buscar vuelos Buenos Aires → París",
      "agente": "agente_vuelos",
      "prioridad": "alta",
      "dependencias": []
    },
    {
      "id": 2,
      "descripcion": "Reservar hotel céntrico para 7 noches",
      "agente": "agente_hotel",
      "prioridad": "alta",
      "dependencias": [1]
    }
  ]
}
```

### 3. Ejecución del plan

Un agente ejecutor toma el plan y ejecuta cada subtarea en el orden correcto, respetando las dependencias.

---

## Los dos roles del patrón

| Rol | ¿Qué hace? | Analogía |
|---|---|---|
| **Agente planificador** | Divide el objetivo en subtareas y genera el plan | El arquitecto que diseña |
| **Agente ejecutor** | Toma el plan y ejecuta cada paso con herramientas | El constructor que ejecuta |

Esta separación de roles hace que el sistema sea mucho más mantenible: podés mejorar el planificador sin tocar el ejecutor, y viceversa.

---

## Planificación iterativa

A veces el plan necesita ajustarse sobre la marcha:

```
Plan inicial → Ejecutar paso 1 → Resultado inesperado
                                        ↓
                              Re-planificar desde ese punto
                                        ↓
                              Continuar con el plan ajustado
```

Esto es especialmente útil cuando el usuario da feedback ("prefiero un vuelo sin escalas") o cuando una herramienta falla.

---

## Casos de uso del patrón

- **Investigación:** dividir un tema en subtemas, investigar cada uno y sintetizar
- **Desarrollo de contenido:** planificar estructura → escribir secciones → revisar → publicar
- **Soporte complejo:** diagnosticar → identificar causa → proponer solución → verificar
- **Proyectos:** dividir en entregables → asignar → hacer seguimiento

---

## Abrí el notebook

En `code_samples/07-planificacion.ipynb` vas a construir:
1. Un agente planificador que genera planes en JSON
2. Un agente ejecutor que lleva a cabo el plan con herramientas
3. Un sistema completo planificador + ejecutor que funciona de punta a punta

---

## Resumen

| Concepto | Descripción |
|---|---|
| Descomposición | Dividir la tarea grande en subtareas manejables |
| Plan estructurado | JSON con subtareas, prioridades y dependencias |
| Agente planificador | Genera el plan |
| Agente ejecutor | Ejecuta el plan con herramientas |
| Planificación iterativa | Replanificar cuando hay cambios o errores |

---

## Siguiente lección

En la [Lección 08](../08-multi-agente/README.md) vamos a ver los **sistemas multi-agente** — cómo hacer que múltiples agentes trabajen juntos en paralelo y con flujos condicionales.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
