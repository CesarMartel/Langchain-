🚀 Ejercicio de Capacitación: Asistente Inteligente de Soporte Técnico
📝 Contexto del Problema (La Problemática)

Imagina que trabajas para una empresa de software que vende un producto muy popular.
El equipo de soporte técnico recibe cientos de correos electrónicos y tickets de usuarios todos los días con preguntas, problemas y dudas.

El problema es que muchos de estos tickets son repetitivos y consumen mucho tiempo del equipo, el cual podría enfocarse en resolver casos más complejos.
Por ello, la gerencia ha decidido implementar una primera línea de atención automatizada con IA para responder las preguntas más frecuentes.

🎯 Objetivo del Ejercicio

Tu misión es desarrollar un script en Python que funcione como un “Asistente de Soporte Inteligente”.
El asistente deberá recibir una pregunta de un usuario sobre un problema técnico y, usando un contexto predefinido (una base de conocimiento simulada), generar una respuesta útil, coherente y amigable.

El asistente deberá responder correctamente preguntas como:

“¿Cómo puedo resetear mi contraseña?”

“Mi programa no abre, ¿qué hago?”

“¿Cuáles son los requisitos del sistema para instalar el software?”

🛠️ Herramientas y Librerías Requeridas

Para completar este ejercicio, deberás usar las siguientes herramientas:

Python

LangChain: Para orquestar el flujo de la información (pregunta → prompt → modelo → respuesta).

LangChain Google Vertex AI: Para conectar tu cadena con el modelo Gemini de Google Cloud.

👣 Requisitos y Pasos a Seguir
1. Configuración del Entorno

Asegúrate de tener Python instalado.

Instala las librerías necesarias:

pip install langchain langchain-google-vertexai


No necesitas manejar archivos .env ni claves dentro del código.
Se asume que tus credenciales de Google Cloud ya están configuradas correctamente como una variable de entorno del sistema.

2. Definir la Base de Conocimiento

Crea una variable en tu script (string multilínea) que contenga información técnica básica, como si fuera una sección de “Preguntas Frecuentes”.
Este será el contexto que la IA usará para generar respuestas.

Ejemplo:

--- Base de Conocimiento Interna ---
1. Reseteo de Contraseña: El usuario debe ir a 'Configuración > Cuenta > Olvidé mi contraseña' y seguir los pasos. El enlace de reseteo se enviará a su correo.
2. Problema de Arranque: Si el software no inicia, puede deberse a un antivirus bloqueando la aplicación o una instalación corrupta. Se recomienda desactivar temporalmente el antivirus o reinstalar el programa.
3. Requisitos del Sistema: Se necesita Windows 10 o superior, 8 GB de RAM y 5 GB de espacio libre en disco.
--- Fin de la Base de Conocimiento ---

3. Crear la Cadena (Chain) de LangChain

Tu asistente debe seguir este flujo básico:

Cargar el Modelo:
Inicializa ChatVertexAI para conectar con Gemini.

Crear el Prompt Template:
Define una plantilla de instrucciones para el modelo.
El prompt debe contener dos variables:

{contexto} (la base de conocimiento)

{pregunta} (la consulta del usuario)

💡 Pista:
El prompt debe decirle al modelo algo como:

“Eres un asistente de soporte técnico. Responde la pregunta del usuario basándote únicamente en el siguiente contexto.
Si la respuesta no está en el contexto, indica que no tienes esa información.”

Construir la Cadena:
Une los componentes en orden:

Prompt → Modelo (Gemini) → Output Parser


Ejecutar la Cadena:
Pasa tu base de conocimiento y una pregunta de ejemplo para obtener la respuesta.

4. Probar el Asistente

Crea una variable con una pregunta de prueba, por ejemplo:
"No me acuerdo de mi clave, ¿qué puedo hacer?"

Invoca tu cadena con esa pregunta y muestra la respuesta en la consola.

Prueba con diferentes preguntas, incluyendo una que no esté en el contexto, para comprobar cómo maneja el modelo esas situaciones.

✅ Criterios de Éxito (¿Cuándo has terminado?)

Tu ejercicio se considerará completo cuando el script:

Se ejecute sin errores.

Responda correctamente a preguntas contenidas en la base de conocimiento.

Sea capaz de responder con algo como “No tengo información sobre eso” cuando se le pregunte algo fuera del contexto.

🧠 ¿Qué Hace LangChain en Este Proyecto?

LangChain actúa como el cerebro organizador del flujo entre el usuario y la IA.
Su rol principal es orquestar los pasos de la interacción, asegurando que la información fluya de forma lógica y estructurada.

🔹 Funciones de LangChain:

Recibir los datos: La pregunta del usuario y la base de conocimiento.

Construir el prompt: Generar la instrucción final que se enviará al modelo.

Conectarse con Gemini: Usar el modelo de Vertex AI para generar la respuesta.

Procesar la salida: Limpiar el resultado y devolver solo la parte útil al usuario.

En resumen, LangChain se encarga del flujo de datos, mientras que Gemini genera el contenido inteligente.

📑 Estructura de Ejemplo Alternativa (Otro Caso de Uso)
🧩 Proyecto: “Extractor Automático de Datos de Correos”

Objetivo:
Analizar el texto de un correo de cliente y extraer:

Nombre del cliente

Número de pedido

Resumen del problema

Componentes sugeridos:

PromptTemplate: Instrucción para extraer información estructurada.

ChatVertexAI: Modelo Gemini que analiza el texto.

JsonOutputParser: Convierte la respuesta del modelo en un objeto JSON.

Flujo:

Prompt → Modelo → Parser → Resultado estructurado


Salida esperada:

{
  "nombre_cliente": "Ana García",
  "numero_pedido": "A-54321",
  "resumen": "El paquete llegó dañado y falta un artículo."
}

