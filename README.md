# Cómo Ejecutar Satoshi Chatbot

Satoshi Chatbot es una aplicación web interactiva que permite a los usuarios aprender sobre Bitcoin y poner a prueba sus conocimientos a través de un cuestionario. Se integra con BTCPay Server para los pagos y utiliza Gemini para sus capacidades de IA.

## Stack Tecnológico

- **Backend:** Python (Flask)
- **Frontend:** HTML, CSS, JavaScript
- **IA:** Google Gemini
- **Pagos:** BTCPay Server
- **Contenerización:** Podman

## Ejecutar la aplicación con Podman

Esta guía asume que tienes Podman instalado y una imagen de contenedor pre-construida (`satoshi-chatbot.tar`).

### Instrucciones

1.  **Crear un directorio:**
    Crea una nueva carpeta en tu sistema donde almacenarás los archivos de la aplicación.

2.  **Descargar la imagen:**
    Descarga el archivo `satoshi-chatbot.tar` y colócalo en el directorio que acabas de crear.

3.  **Crear un archivo de entorno:**
    En el mismo directorio, crea un archivo llamado `.env` y añade el siguiente contenido, reemplazando los valores de ejemplo con tus credenciales reales:

    ```
    BTCPAY_URL="https"
    BTCPAY_API_KEY="tu_api_key"
    BTCPAY_STORE_ID="tu_store_id"
    GEMINI_API_KEY="tu_gemini_key"
    ```

    > **Nota sobre el proveedor de IA:**
    > Puedes configurar el chatbot para que utilice la API de Google Gemini o una instancia auto-alojada de un modelo como Llama.
    >
    > - **Para usar Gemini:** Asegúrate de que la variable `GEMINI_API_KEY` esté configurada en tu archivo `.env`.
    > - **Para usar Llama:** Añade la URL de tu servidor en la variable `LLAMA_API_URL="http://<tu-servidor-llama>:<puerto>"`. Gemini es utilizado para evaluar las respuestas del Usuario durante el Quiz. Llama es utilizado para responder preguntas sobre Bitcoin en el modo "Preguntar" sin recompensas. Ambos son requeridos para este MVP.

4.  **Cargar la imagen:**
    Abre tu terminal, navega al directorio que creaste y ejecuta el siguiente comando para cargar la imagen del contenedor en Podman:

    ```bash
    podman load -i satoshi-chatbot.tar
    ```

5.  **Ejecutar el contenedor:**
    Finalmente, ejecuta el contenedor con el siguiente comando. Esto iniciará la aplicación, mapeará el puerto 5000 y cargará tus variables de entorno.

    ```bash
    podman run -d --name satoshi-bot -p 5000:5000 --env-file .env satoshi-chatbot
    ```

6.  **Acceder a la aplicación:**
    Ahora puedes acceder al Satoshi Chatbot navegando a `http://localhost:5000` en tu navegador web.
