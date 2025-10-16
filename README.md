🚀 Ejercicio de Capacitación: Asistente Inteligente de Soporte Técnico

Contexto del Problema (La Problemática) 📝

Imagina que trabajas para una empresa de software que vende un producto muy popular. El equipo de soporte técnico recibe cientos de correos electrónicos y tickets de usuarios todos los días con preguntas, problemas y dudas.

El problema es que muchos de estos tickets son repetitivos y consumen mucho tiempo del equipo, que podría estar resolviendo problemas más complejos. La gerencia ha decidido implementar una primera línea de defensa con IA para automatizar las respuestas a las preguntas más frecuentes.

Objetivo del Ejercicio 🎯

Tu misión es desarrollar un script en Python que actúe como un "Asistente de Soporte Inteligente". Este script debe ser capaz de recibir una pregunta de un usuario sobre un problema técnico y, utilizando un contexto predefinido (un pequeño manual o base de conocimiento), generar una respuesta útil y amigable para el usuario.

El objetivo es que el asistente pueda responder preguntas como:

    "¿Cómo puedo resetear mi contraseña?"

    "Mi programa no abre, ¿qué hago?"

    "¿Cuáles son los requisitos del sistema para instalar el software?"

Herramientas y Librerías Requeridas 🛠️

Para este ejercicio, deberás utilizar las siguientes herramientas:

    Python

    LangChain: Para orquestar el flujo de la información (pregunta -> prompt -> modelo -> respuesta).

    LangChain Google Vertex AI: Para conectar con el modelo de IA de Gemini.

Requisitos y Pasos a Seguir 👣

No necesitas crear una interfaz gráfica. Todo el ejercicio se desarrollará en la terminal.

    Configuración del Entorno:

        Asegúrate de tener Python instalado.

        Instala las librerías necesarias: pip install langchain langchain-google-vertexai.

        Autenticación: No necesitas manejar archivos .env ni claves dentro del código. Se asume que tus credenciales de Google Cloud ya están configuradas como una variable de entorno en tu sistema, por lo que la autenticación será automática.

    Definir la Base de Conocimiento:

        Dentro de tu script de Python, crea una variable de texto (un string multi-línea) que simule ser un pequeño manual de usuario o una sección de "Preguntas Frecuentes". Este será el contexto que la IA usará para encontrar las respuestas.

        Ejemplo de contexto:

        --- Base de Conocimiento Interna ---
        1. Reseteo de Contraseña: El usuario debe ir a 'Configuración > Cuenta > Olvidé mi contraseña' y seguir los pasos. El enlace de reseteo se enviará a su correo.
        2. Problema de Arranque: Si el software no inicia, las causas comunes son: un antivirus bloqueando la aplicación o una instalación corrupta. La solución es desactivar temporalmente el antivirus o reinstalar el programa.
        3. Requisitos del Sistema: Se necesita Windows 10 o superior, 8 GB de RAM y 5 GB de espacio en disco.
        --- Fin de la Base de Conocimiento ---

    Crear la Cadena (Chain) de LangChain:

        Cargar el Modelo: Inicializa el modelo ChatVertexAI para conectar con Gemini.

        Crear el Prompt Template: Diseña una plantilla de prompt que le dé instrucciones claras al modelo. El prompt debe incluir dos variables de entrada: el contexto (tu base de conocimiento) y la pregunta del usuario.

            Pista: El prompt debería decirle a Gemini algo como: "Eres un asistente de soporte técnico. Responde la pregunta del usuario basándote únicamente en el siguiente contexto. Si la respuesta no está en el contexto, indica que no tienes esa información."

        Construir la Cadena: Une el prompt, el modelo y un StrOutputParser para que la salida sea un texto limpio.

    Probar el Asistente:

        Define una variable con una pregunta de ejemplo (ej. "No me acuerdo de mi clave, ¿qué puedo hacer?").

        Invoca tu cadena de LangChain pasándole tanto la base de conocimiento como la pregunta del usuario.

        Imprime en la consola la respuesta generada por Gemini.

        Realiza pruebas con diferentes preguntas, incluyendo algunas cuyas respuestas no estén en la base de conocimiento para ver cómo reacciona el asistente.

Criterios de Éxito (¿Cuándo has terminado?) ✅

El ejercicio se considerará completado cuando tu script:

    Se ejecute sin errores.

    Pueda recibir una pregunta sobre un tema incluido en la base de conocimiento y genere una respuesta coherente y correcta.

    Responda de forma adecuada (ej. "No tengo información sobre eso") cuando se le pregunta por algo que no está en el contexto.
