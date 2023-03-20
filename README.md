# Leer!

## GPT Discord Bot

Plantilla de bot de discord escrito en Python que usa la [completions API](https://beta.openai.com/docs/api-reference/completions) para mantener conversaciones gracias al modelo `text-davinci-003`, y [moderations API](https://beta.openai.com/docs/api-reference/moderations) para filtrar mensajes.

**Esto es un Chatbot que funciona a menor escala que Chatgpt, NO ES CHAT GPT.**

Este proyecto esta utilizando las librerias de [OpenAI Python](https://github.com/openai/openai-python) y [discord.py](https://discordpy.readthedocs.io/).

## Features

- `/chat` inicia un hilo publico, con un argumento `message` cual es el primer mensaje que se le envia al bot
- El modelo generara una respuesta para cada mensaje de usuario en cualquier hilo iniciado con `/chat`
- El hilo entero sera procesado por el modelo para cada peticion, por lo que el modelo recordara los mensajes anteriores en el hilo
- Cuando el limite de contexto en el hilo sea alcanzado o se llegue a un maximo de mensajes, el bot cerrara el hilo
- Puedes personalizar las intrucciones del bot modificando el archivo `config.yaml` 
- Puedes cambiar el modelo que usa, el valor hardcodeado es `text-davinci-003` en completion.py linea 51.

## Setup

1. Llena las variables en el archivo `.env` bajo la informacion proporcionada en los siguientes puntos
1. Ve hacia https://beta.openai.com/account/api-keys, genera una nueva api key. Esta key ira en `OPENAI_API_KEY` dentro del archivo .env
1. Crea una nueva aplicacion en https://discord.com/developers/applications
1. Ve hacia la pestaña de bot y clickea en "Add Bot"
    - Clickea en "Reset Token", este token deberas insertarlo en `DISCORD_BOT_TOKEN` dentro del archivo .env1
    - Disable "Public Bot" unless you want your bot to be visible to everyone
    - Desabilita el ticket en "Public BOT", a no ser que quieras que tu bot sea visible para todo el mundo
    - Habilita "Messsage Content Intent" en "Privileged Gateway Intents"
1. Ve hacia la pestaña de OAuth2, copia tu "Client ID", y ponlo en `DISCORD_CLIENT_ID` dentro del archivo .env
1. Copia el ID del servidor en el que quieres que el bot sea usado, clickeando el icono del servidor y clickeando "Copy ID", el id insertalo en `ALLOWED_SERVER_IDS`. Si quieres permitir multiples servidores, separa los IDs por "," como `server_id_1,server_id_2`
1. Genera un entorno virtual con venv (https://docs.python.org/3/library/venv.html) y activalo.
    
    Windows:
    ```shell
    python -m venv <ruta a tu entorno virtual>
    <ruta a tu entorno virtual>\Scripts\activate.bat (o activate.ps1 si estas desde powershell)
    ```
    Linux:
    ```shell
    python3 -m venv <ruta a tu entorno virtual>
    source <ruta a tu entorno virtual>/bin/activate
    ```

    En caso de que quieras o necesites desactivar el entorno virtual, debes hacer lo siguiente:
    ```shell
    deactivate
    ```

1. Instala las dependencias y corre el bot
    ```
    pip install -r requirements.txt
    python -m src.main
    ```
    Deberias ver una URL de invitacion en la consola. Copiala y pegala en tu navegador para agregar el bot a tu servidor.
    Nota: asegurate de estar usando Python 3.9+ (verifica con python --version)

## Configuracion opcional

1. Si quieres mensajes de moderacion, crea y copia un id de canal para cada servidor en el que quieras que los mensajes de moderacion se envien en `SERVER_TO_MODERATION_CHANNEL`. Esto deberia tener el formato: `server_id:channel_id,server_id_2:channel_id_2`
1. Si quieres cambiar la personalidad del bot, ve a `src/config.yaml` y edita las instrucciones
1. Si quieres cambiar la configuracion de moderacion para que mensajes se marquen o bloqueen, edita los valores en `src/constants.py`. Un valor mas bajo significa menos probabilidad de que se active.

## FAQ

> Porque mi bot no responde a los comandos?

Asegurate que el bot tenga los permisos necesarios para ejecutar los comandos.
- Enviar mensajes / Send Messages
- Enviar mensajes en hilos / Send Messages in Threads
- Crear hilos publicos / Create Public Threads 
- Administrar mensajes (solo para moderacion para borrar mensajes bloqueados) / Manage Messages (only for moderation to delete blocked messages)
- Administrar hilos / Manage Threads
- Leer el historial de mensajes / Read Message History
- Usar comandos de aplicacion / Use Application Commands

## Repo original

**El codigo original fue proporcionado por OpenAI:** https://github.com/openai/gpt-discord-bot

**Para cualquier problema al ejecutar este bot especifico:** [Discord Project Post](https://discord.com/channels/974519864045756446/1055336272543092757)

**Para problemas generales con la API de OpenAI o preguntas:** [Discord API Discussions](https://discord.com/channels/974519864045756446/1037561178286739466)