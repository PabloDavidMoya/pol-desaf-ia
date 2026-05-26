# Lección 01 — ¿Qué es un Agente de IA?

Bienvenido a la primera lección del curso.

Antes de escribir una sola línea de código, necesitamos entender **qué es exactamente un agente de IA** y por qué es diferente a simplemente hablar con ChatGPT o Claude.

---

## La diferencia clave: responder vs. actuar

Cuando le hacés una pregunta a Claude en la web, él te *responde*. Eso es todo.

Un **agente de IA** es diferente: no solo responde, sino que puede **hacer cosas**. Puede buscar información, ejecutar código, enviar emails, guardar archivos o llamar a APIs externas — y decide *por sí mismo* qué pasos seguir para cumplir tu objetivo.

> Piénsalo así: la diferencia entre un asistente que te dice "deberías reservar el vuelo" y uno que **reserva el vuelo por vos**.

---

## Los 3 componentes de todo agente

Todo sistema agente, sin importar su complejidad, tiene tres partes:

| Componente | ¿Qué hace? | Ejemplo |
|---|---|---|
| **Entorno** | El mundo en el que opera | Internet, tu computadora, una base de datos |
| **Sensores** | Cómo percibe el estado actual | Leer un archivo, recibir un mensaje |
| **Actuadores** | Cómo ejecuta acciones | Escribir un email, llamar a una API |

---

## ¿Cuándo usar un agente?

Los agentes son ideales cuando:

- El problema **no tiene una solución fija** — requiere razonamiento
- La tarea tiene **múltiples pasos** que dependen entre sí
- Necesitás que el sistema **mejore o se adapte** con el tiempo

Ejemplos concretos:
- Un agente que investiga un tema en internet y te genera un resumen
- Un agente que analiza tus ventas y detecta patrones
- Un agente que responde consultas de clientes usando tu documentación

---

## Tu primer agente con Claude

En esta lección vas a construir un **agente de recomendaciones de viaje**. El agente va a:

1. Recibir tu consulta ("quiero un destino cálido")
2. Usar una herramienta para consultar destinos disponibles
3. Razonar y elegir la mejor recomendación para vos

Abrí el notebook `code_samples/01-primer-agente.ipynb` para seguir el ejemplo paso a paso.

---

## Conceptos clave de esta lección

- **Agente de IA:** sistema que usa un LLM para razonar y tomar acciones en el mundo real
- **Tool (herramienta):** función de Python que el agente puede llamar para obtener información o ejecutar algo
- **Bucle agente:** el ciclo de razonar → actuar → observar resultado → razonar de nuevo
- **System prompt:** las instrucciones que le dicen al agente quién es y cómo debe comportarse

---

## Resumen

| Concepto | Descripción |
|---|---|
| LLM | El "cerebro" del agente — razona y decide |
| Herramientas | Las "manos" del agente — ejecutan acciones |
| Bucle agente | El ciclo que repite hasta completar la tarea |
| System prompt | La "personalidad" e instrucciones del agente |

---

## Siguiente lección

En la [Lección 02](../02-frameworks-agentes/README.md) vamos a explorar los principales frameworks para construir agentes y cuándo conviene usar cada uno.

---

*Lección inspirada en [ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) de Microsoft (MIT License), adaptada para Claude por Pablo David Moya.*
