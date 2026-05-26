# Lección 04 — Herramientas (Tool Use)

Las herramientas son lo que convierte a Claude de un chatbot en un **agente que puede hacer cosas reales**.

Sin herramientas, Claude solo puede responder con texto. Con herramientas, puede buscar en internet, consultar bases de datos, calcular, enviar emails, llamar a APIs y mucho más.

---

## ¿Qué es exactamente una herramienta?

Una herramienta es simplemente una **función de Python** que le das a Claude para que la llame cuando la necesite.

```python
def calcular_precio_viaje(destino: str, dias: int) -> dict:
    """Calcula el precio estimado de un viaje."""
    precios = {"Barcelona": 150, "Cancún": 120, "Tokio": 200}
    precio_por_dia = precios.get(destino, 100)
    return {"destino": destino, "dias": dias, "total_usd": precio_por_dia * dias}
```

Claude decide *cuándo* llamarla, *con qué parámetros* y *cómo usar el resultado* — vos solo definís qué hace la función.

---

## El ciclo completo de una herramienta

```
Usuario pregunta
      ↓
Claude razona: "necesito datos que no tengo"
      ↓
Claude llama a la herramienta con los parámetros correctos
      ↓
La función Python ejecuta y devuelve el resultado
      ↓
Claude procesa el resultado y responde al usuario
```

---

## Los 5 componentes de una buena herramienta

| Componente | ¿Qué es? | Ejemplo |
|---|---|---|
| **Nombre** | Identificador claro | `calcular_precio_viaje` |
| **Descripción** | Le dice a Claude cuándo usarla | "Calcula el costo total de un viaje según destino y días" |
| **Parámetros** | Qué datos necesita | `destino: str`, `dias: int` |
| **Lógica** | Lo que hace la función | Consulta precios, hace el cálculo |
| **Retorno** | Lo que devuelve | `{"total_usd": 900}` |

---

## Tipos de herramientas más comunes

### 1. Herramientas de información
Consultan datos que Claude no tiene o que cambian en tiempo real:
- Precios de vuelos
- Estado del tiempo
- Cotizaciones de monedas

### 2. Herramientas de cálculo
Realizan operaciones matemáticas o lógicas complejas:
- Calcular costos
- Convertir unidades
- Analizar datos

### 3. Herramientas de acción
Ejecutan algo en el mundo real:
- Enviar un email
- Guardar en una base de datos
- Llamar a una API externa

> **Atención con las herramientas de acción:** antes de ejecutar algo irreversible (como enviar un email o hacer una compra), conviene pedir confirmación al usuario.

---

## Cuántas herramientas usar

No hay un número mágico, pero una buena regla:

- **1-3 herramientas:** agente simple, fácil de controlar
- **4-8 herramientas:** agente intermedio, para tareas complejas
- **8+ herramientas:** considerá dividir en múltiples agentes especializados (Patrón 3 de la lección anterior)

---

## Seguridad y buenas prácticas

1. **Validá los parámetros** — antes de ejecutar, verificá que los datos tienen sentido
2. **Manejo de errores** — si la herramienta falla, el agente debe saberlo y decírselo al usuario
3. **Bases de datos en modo lectura** — si la herramienta consulta una BD, usá solo lectura para evitar modificaciones accidentales
4. **Herramientas destructivas** — si borra o modifica algo, pedí confirmación antes

---

## Abrí el notebook

En `code_samples/04-herramientas.ipynb` vas a ver:
- Cómo definir herramientas correctamente
- Cómo combinar múltiples herramientas en un agente
- Cómo manejar errores cuando una herramienta falla
- Cómo pedir confirmación antes de ejecutar acciones importantes

---

## Resumen

| Concepto | Descripción |
|---|---|
| Tool | Función Python que el agente puede llamar |
| Schema | Descripción de la tool para que Claude sepa cuándo usarla |
| Tool Use | El ciclo completo de llamar, ejecutar y procesar |
| Confirmación | Pedir permiso antes de ejecutar acciones irreversibles |

---

## Siguiente lección

En la [Lección 05](../05-memoria-contexto/README.md) vamos a ver cómo darle **memoria** a los agentes para que recuerden información entre conversaciones.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
