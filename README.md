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

 División Proyecto Java N-Capas
Ideas de Ejercicios de Capacitación IA
Mejora de Calidad de Foto
Significado de "btw 19teen"
Imagen Mejorada
Foto Mejorada
Conversación con Gemini

necesito realizar un ejercicio sencillo de langchain con python ty con la ia de gemini, yo ya tenog mi clave json que me dio gcp con los servicios de vertex ia, mi clave json ya esta configurada como entorno de variable del sistema, dame un ejercicio super basico para desarrollar con langchain

Claro, aquí tienes un ejercicio súper básico para empezar con LangChain y Gemini, asumiendo que ya tienes tu autenticación de GCP configurada correctamente en tu entorno.

Este script simplemente tomará un tema (por ejemplo, "helado") y le pedirá a Gemini que sugiera un nombre divertido para una nueva marca. Es un "hola mundo" perfecto para probar que todo funcione.

Ejercicio Básico: Generador de Nombres con LangChain y Gemini

Este código utiliza los siguientes componentes de LangChain:

    ChatVertexAI: Para conectar con el modelo de Gemini en Google Cloud Vertex AI.

    ChatPromptTemplate: Para crear una plantilla de la pregunta que le haremos al modelo.

    StrOutputParser: Para obtener la respuesta del modelo como un texto simple.

1. Instalación de Librerías

Primero, asegúrate de tener instaladas las librerías necesarias. Puedes hacerlo con pip:
Bash

pip install --upgrade langchain langchain-google-vertexai

2. Código Python

Crea un archivo llamado test_langchain.py y pega el siguiente código. Está comentado para que entiendas qué hace cada línea.
Python

# -*- coding: utf-8 -*-

# Importamos las clases necesarias de LangChain
from langchain_google_vertexai import ChatVertexAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# 1. Inicializamos el modelo de Gemini
# LangChain se conectará a Vertex AI usando la autenticación
# que ya tienes configurada en tu entorno.
# "gemini-1.0-pro-001" es uno de los modelos disponibles.
llm = ChatVertexAI(model_name="gemini-1.0-pro-001")

# 2. Creamos una plantilla para el prompt (la instrucción)
# Usamos llaves {} para indicar dónde irá nuestra variable (el tema).
prompt = ChatPromptTemplate.from_messages([
    ("system", "Eres un asistente creativo experto en nombrar marcas."),
    ("user", "Sugiere un nombre divertido y corto para una nueva marca de {tema}.")
])

# 3. Creamos un "parser" para el resultado
# Esto nos asegura que la salida del modelo sea un texto simple (string).
output_parser = StrOutputParser()

# 4. Creamos la cadena (chain)
# Aquí es donde unimos los componentes en el orden en que se ejecutarán:
# Prompt -> Modelo LLM -> Parser de Salida
chain = prompt | llm | output_parser

# 5. Ejecutamos la cadena
# La función "invoke" pasa la variable a nuestro prompt y ejecuta toda la cadena.
# Puedes cambiar el valor de "tema" por lo que quieras.
print("Ejecutando la cadena de LangChain...")
response = chain.invoke({"tema": "helados de frutas"})

# Imprimimos la respuesta obtenida
print("\nRespuesta de Gemini:")
print(response)

# --- Otro ejemplo ---
print("\n--- Probando con otro tema ---")
response_cafe = chain.invoke({"tema": "cafetería para programadores"})
print("\nRespuesta de Gemini:")
print(response_cafe)

3. Cómo Ejecutarlo

    Guarda el código en un archivo llamado test_langchain.py.

    Abre una terminal o línea de comandos.

    Navega hasta la carpeta donde guardaste el archivo.

    Ejecuta el script con el siguiente comando:
    Bash

    python test_langchain.py

Resultado Esperado

La salida en tu terminal debería ser algo similar a esto (los nombres exactos variarán cada vez que lo ejecutes):

Ejecutando la cadena de LangChain...

Respuesta de Gemini:
FruityPop

--- Probando con otro tema ---

Respuesta de Gemini:
CodeBrew

Este ejercicio te confirma que tu conexión con Vertex AI funciona y que puedes construir y ejecutar una cadena básica con LangChain. ¡A partir de aquí, puedes empezar a crear cadenas mucho más complejas!

solo quiero que me creees una problematica para crear un readme y que lo resuelvan mis capacitantes no me des codigo ni nada, solo dame el contexto, las librerias que deberian de usar que deberia de hacer y asi pues nada de codigo dame un redme para que mis capacitantes lo desarrollen

Claro, aquí tienes una problemática y su correspondiente README para que tus capacitantes la desarrollen. Está diseñado para ser un desafío práctico y enfocado en un caso de uso real.

README.md

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

        Instala las librerías necesarias (langchain, langchain-google-vertexai).

        Verifica que tu variable de entorno con la clave JSON de GCP esté configurada correctamente.

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

Reto Adicional (Opcional) ⭐

Si terminas rápido, intenta modificar tu script para que, en lugar de tener una sola pregunta fija, se ejecute en un bucle while. De esta forma, el programa le pedirá al usuario que ingrese una pregunta, la procesará, dará la respuesta y luego volverá a pedir otra pregunta, creando una conversación interactiva en la terminal hasta que el usuario escriba "salir".

modifica el readme, yo ya tengo mi clave json configurada como variabke de entorno del sistema no es necesario el env

¡Entendido! He modificado el README para que sea más directo y elimine cualquier mención o duda sobre la configuración de las credenciales, asumiendo que ya están listas en el sistema de tus capacitantes.

Aquí está la versión actualizada:

README.md

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

Reto Adicional (Opcional) ⭐

Si terminas rápido, intenta modificar tu script para que, en lugar de tener una sola pregunta fija, se ejecute en un bucle while. De esta forma, el programa le pedirá al usuario que ingrese una pregunta, la procesará, dará la respuesta y luego volverá a pedir otra pregunta, creando una conversación interactiva en la terminal hasta que el usuario escriba "salir".

dame un concepto de langchain y de lo que debe de hacer en este proyecto, mas una estrucutura de ejemplo de como debreria de ser sin que sea un ejemplo de este ejercicio

¡Claro! Aquí tienes una explicación conceptual de LangChain, su rol en el ejercicio y una estructura de ejemplo para un proyecto diferente.

¿Qué es LangChain? 🤔

Piensa en LangChain como una caja de herramientas y un manual de instrucciones para construir aplicaciones con modelos de lenguaje (IA) como Gemini. No es la IA en sí misma, sino el pegamento y las piezas que te permiten conectar la IA con otras fuentes de datos y darle instrucciones de manera ordenada.

Su objetivo es hacer que sea mucho más fácil realizar tareas complejas que van más allá de un simple "pregunta y respuesta". En lugar de que tengas que escribir código para cada pequeño paso (formatear la pregunta, llamar a la IA, procesar la respuesta), LangChain te da "bloques" pre-construidos para que los conectes.

Los bloques más comunes son:

    Models: La conexión directa con la IA (Gemini, en este caso).

    Prompts: Plantillas para darle instrucciones a la IA de forma consistente.

    Chains (Cadenas): La idea central de LangChain. Son secuencias de pasos. La cadena más simple es: Prompt -> Model -> Output.

¿Qué Debe Hacer LangChain en Este Proyecto? 🧑‍🔧

En el ejercicio del "Asistente de Soporte Inteligente", LangChain actúa como el director de orquesta. Su trabajo es asegurarse de que la información fluya correctamente en el orden correcto para obtener la respuesta que queremos.

Específicamente, su rol es:

    Tomar los Ingredientes: Recibe la pregunta del usuario ("¿Cómo reseteo mi clave?") y la base de conocimiento (el texto con las soluciones).

    Preparar la Instrucción (Prompting): Usa la plantilla de prompt que creaste para mezclar los ingredientes en una instrucción clara para Gemini. El resultado es un texto final como: "Eres un asistente de soporte. Usando este contexto [aquí va la base de conocimiento], responde a esta pregunta: [aquí va la pregunta del usuario]".

    Comunicarse con la IA: Envía esa instrucción finalizada al modelo de Gemini de forma estandarizada, sin que tengas que preocuparte por los detalles técnicos de la API.

    Limpiar el Resultado: Recibe la respuesta completa de Gemini y, usando el StrOutputParser, la "limpia" para entregar únicamente el texto de la respuesta que le mostrarás al usuario.

En resumen, LangChain orquesta el proceso para que tú solo te preocupes por definir el contexto y la pregunta, en lugar de programar cada paso de la interacción con la IA.

Estructura de Ejemplo para Otro Proyecto (Extractor de Datos) 📑

Imagina un proyecto diferente: quieres extraer información estructurada de un texto no estructurado, como un correo electrónico de un cliente.

Objetivo: Leer un correo y extraer automáticamente el nombre del cliente, el número de pedido y el resumen del problema en un formato organizado (como un diccionario de Python).

Una estructura de LangChain para este problema se vería así:

    Entrada (Input):

        Una variable de Python que contiene el texto completo del correo electrónico del cliente.

    Componente 1: El Prompt Template (ChatPromptTemplate):

        Sería una plantilla de instrucciones muy específica.

        Instrucción: "Del siguiente texto, extrae el nombre del cliente, el número de pedido y un resumen del problema. Responde únicamente con un objeto JSON que tenga las claves nombre_cliente, numero_pedido y resumen."

        Variables: La plantilla tendría una variable para insertar el {texto_del_correo}.

    Componente 2: El Modelo (ChatVertexAI):

        El motor de Gemini, que leerá el prompt y el correo, y entenderá que debe generar un texto con formato JSON.

    Componente 3: El Parseador de Salida (JsonOutputParser):

        Este es un bloque diferente al del ejercicio. En lugar de esperar un simple texto, este parser está diseñado para tomar la respuesta en formato JSON del modelo y convertirla automáticamente en un diccionario de Python que puedes usar en tu programa.

    La Cadena (La Unión de los Componentes):

        La cadena se construiría uniendo los bloques en este orden: prompt | model | json_parser

    Salida (Output):

        El resultado final no sería un texto, sino un diccionario de Python limpio y listo para usar, como este:
        Python

{
  "nombre_cliente": "Ana García",
  "numero_pedido": "A-54321",
  "resumen": "El paquete llegó dañado y falta un artículo."
}


    Pueda recibir una pregunta sobre un tema incluido en la base de conocimiento y genere una respuesta coherente y correcta.

    Responda de forma adecuada (ej. "No tengo información sobre eso") cuando se le pregunta por algo que no está en el contexto.
