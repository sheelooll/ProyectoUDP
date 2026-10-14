# Diseño de la Plataforma de Estudio

## 1. Resumen

Plataforma web de estudio donde el estudiante practica con **3 ejercicios de alternativas** y cuenta con un **chatbot** que entrega las respuestas y explica el razonamiento detrás de cada una.

**Objetivo:** que el estudiante practique, se equivoque, entienda por qué y vuelva a intentar.

**Público objetivo:** estudiantes de enseñanza media y superior.

---

## 2. Alcance del MVP

| Incluido | Fuera de alcance (por ahora) |
|---|---|
| 3 ejercicios de alternativas (A, B, C, D) | Cuentas de profesor y panel docente |
| Corrección inmediata con retroalimentación | Ranking entre estudiantes |
| Chatbot que entrega respuestas y explicaciones | Banco de ejercicios ampliable |
| Resumen de resultados al finalizar | Aplicación móvil nativa |

---

## 3. Flujo de usuario

```
Inicio → Ejercicio 1 → Ejercicio 2 → Ejercicio 3 → Resultados
              ↕              ↕              ↕
                  Chatbot (siempre disponible)
```

1. El estudiante entra a la pantalla de inicio y presiona **Comenzar**.
2. Resuelve cada ejercicio eligiendo una alternativa.
3. Al responder, ve si acertó y una breve explicación.
4. En cualquier momento puede abrir el chatbot para pedir la respuesta o una explicación.
5. Al terminar los 3 ejercicios ve su puntaje y puede reintentar.

---

## 4. Pantallas

### 4.1 Inicio
- Título de la plataforma y breve descripción.
- Botón principal: **Comenzar**.
- Indicador: "3 ejercicios · alternativas · chatbot de ayuda".

### 4.2 Ejercicio (pantalla reutilizable)
- **Barra de progreso** superior: "Ejercicio 1 de 3".
- **Enunciado** en una tarjeta destacada.
- **4 alternativas** (A, B, C, D) como botones grandes seleccionables.
- Botón **Responder** (deshabilitado hasta elegir una alternativa).
- Tras responder:
  - Alternativa correcta en verde, incorrecta en rojo.
  - Mensaje de retroalimentación breve.
  - Botón **Siguiente** (o **Ver resultados** en el último).
- Botón flotante del **chatbot** en la esquina inferior derecha.

### 4.3 Chatbot
- Panel lateral (escritorio) o pantalla completa (móvil).
- Historial de mensajes con burbujas de estudiante y bot.
- Campo de texto + botón enviar.
- **Atajos rápidos** (chips):
  - "¿Cuál es la respuesta?"
  - "Explícame paso a paso"
  - "Dame una pista"
- El bot conoce el ejercicio actual y responde en ese contexto.

### 4.4 Resultados
- Puntaje total (ej. "2 de 3 correctas").
- Lista de los 3 ejercicios con ✔ / ✘.
- Botones: **Reintentar** y **Revisar con el chatbot**.

---

## 5. Los 3 ejercicios

Cada ejercicio tiene un enunciado, 4 alternativas, una respuesta correcta y una explicación. El contenido es editable; los siguientes son ejemplos de partida.

### Ejercicio 1: Álgebra básica
**Enunciado:** Si 2x + 6 = 14, ¿cuál es el valor de x?

| Alternativa | Texto |
|---|---|
| A | x = 3 |
| B | x = 4 ✅ |
| C | x = 5 |
| D | x = 10 |

**Explicación:** Se resta 6 a ambos lados (2x = 8) y luego se divide por 2 (x = 4).

### Ejercicio 2: Comprensión de ciencias
**Enunciado:** ¿Qué gas absorben las plantas durante la fotosíntesis?

| Alternativa | Texto |
|---|---|
| A | Oxígeno |
| B | Nitrógeno |
| C | Dióxido de carbono ✅ |
| D | Hidrógeno |

**Explicación:** Las plantas toman CO₂ y, con luz solar y agua, producen glucosa y liberan oxígeno.

### Ejercicio 3: Historia
**Enunciado:** ¿En qué año se declaró la Independencia de Chile?

| Alternativa | Texto |
|---|---|
| A | 1810 |
| B | 1818 ✅ |
| C | 1823 |
| D | 1833 |

**Explicación:** El proceso comenzó en 1810 con la Primera Junta de Gobierno, pero la independencia se proclamó oficialmente en 1818.

---

## 6. Diseño del chatbot

### 6.1 Comportamiento
- Responde **sobre el ejercicio que el estudiante tiene abierto**.
- Entrega la **respuesta correcta** cuando se le pide, junto con la explicación.
- Si el estudiante pide una **pista**, orienta sin revelar la respuesta.
- Mantiene un tono cercano, claro y breve.
- Si la pregunta no tiene relación con los ejercicios, redirige amablemente.

### 6.2 Ejemplo de conversación

> **Estudiante:** No entiendo el ejercicio 1.
> **Bot:** Tenemos 2x + 6 = 14. Primero, ¿qué operación puedes hacer para dejar la x más sola? Si quieres, te doy una pista.
> **Estudiante:** ¿Cuál es la respuesta?
> **Bot:** La respuesta es **B (x = 4)**. Restamos 6 a ambos lados y queda 2x = 8; luego dividimos por 2.

### 6.3 Contexto enviado al modelo
```json
{
  "ejercicio_actual": 1,
  "enunciado": "Si 2x + 6 = 14, ¿cuál es el valor de x?",
  "alternativas": { "A": "3", "B": "4", "C": "5", "D": "10" },
  "respuesta_correcta": "B",
  "explicacion": "Se resta 6 y se divide por 2.",
  "respuesta_estudiante": "C",
  "mensaje": "¿Por qué no es la C?"
}
```

### 6.4 Prompt del sistema (base)
```
Eres un tutor amable de una plataforma de estudio. Ayudas a estudiantes con
3 ejercicios de alternativas. Conoces el enunciado, las alternativas y la
respuesta correcta del ejercicio actual. Cuando te pidan la respuesta, entrégala
con una explicación breve paso a paso. Si piden una pista, orienta sin revelar
la respuesta. Responde en español, en un tono claro y cercano. Si la consulta no
tiene relación con los ejercicios, redirige con amabilidad.
```

---

## 7. Diseño visual

### 7.1 Paleta
| Uso | Color |
|---|---|
| Primario | `#4F46E5` (índigo) |
| Fondo | `#F8FAFC` |
| Tarjetas | `#FFFFFF` |
| Texto | `#0F172A` |
| Correcto | `#16A34A` |
| Incorrecto | `#DC2626` |
| Acento chatbot | `#0EA5E9` |

### 7.2 Tipografía
- Títulos: **Poppins** (600–700)
- Texto: **Inter** (400–500)
- Tamaño base: 16 px; enunciados 20 px.

### 7.3 Componentes
- **Tarjeta de ejercicio:** bordes redondeados (16 px), sombra suave.
- **Alternativa:** botón de ancho completo, letra a la izquierda, estados *normal*, *hover*, *seleccionada*, *correcta*, *incorrecta*.
- **Barra de progreso:** 3 segmentos que se llenan al avanzar.
- **Burbujas del chat:** estudiante a la derecha (primario), bot a la izquierda (gris claro).

### 7.4 Responsive
- **Móvil (< 640 px):** una columna, chatbot a pantalla completa.
- **Escritorio:** ejercicio al centro y chatbot como panel lateral de 360 px.

---

## 8. Accesibilidad
- Contraste mínimo AA en todos los textos.
- Navegación completa por teclado (Tab, Enter, flechas entre alternativas).
- Los estados correcto/incorrecto usan **ícono + color**, no solo color.
- Etiquetas `aria` en alternativas y en el campo del chat.
- Respeto por `prefers-reduced-motion`.

---

## 9. Arquitectura sugerida

| Capa | Tecnología sugerida |
|---|---|
| Frontend | React + Tailwind CSS |
| Backend | Node.js (Express) o Python (FastAPI) |
| Chatbot | API de Claude (Anthropic) |
| Datos de ejercicios | Archivo JSON (MVP) → base de datos después |

### Endpoints
| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/ejercicios` | Lista los 3 ejercicios (sin la respuesta correcta) |
| POST | `/api/ejercicios/:id/responder` | Valida la alternativa elegida |
| POST | `/api/chat` | Envía el mensaje del estudiante y devuelve la respuesta del bot |

### Modelo de datos
```json
{
  "id": 1,
  "tema": "Álgebra básica",
  "enunciado": "Si 2x + 6 = 14, ¿cuál es el valor de x?",
  "alternativas": { "A": "3", "B": "4", "C": "5", "D": "10" },
  "correcta": "B",
  "explicacion": "Se resta 6 a ambos lados y se divide por 2."
}
```

> **Nota de seguridad:** la respuesta correcta no debe enviarse al navegador hasta que el estudiante responda; la validación ocurre en el servidor.

---

## 10. Criterios de aceptación
- [ ] El estudiante puede completar los 3 ejercicios en orden.
- [ ] Cada respuesta muestra retroalimentación inmediata.
- [ ] El chatbot entrega la respuesta correcta y su explicación cuando se le pide.
- [ ] El chatbot responde en el contexto del ejercicio abierto.
- [ ] La pantalla de resultados muestra el puntaje correcto.
- [ ] La plataforma funciona en móvil y escritorio.
- [ ] Cumple los requisitos de accesibilidad de la sección 8.

---

## 11. Próximos pasos
1. Validar el contenido de los 3 ejercicios con el material real de estudio.
2. Prototipar las pantallas en Figma.
3. Implementar el MVP.
4. Probar con un grupo pequeño de estudiantes y ajustar el chatbot.
