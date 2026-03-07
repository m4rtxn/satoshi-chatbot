
## SatoshiBot

SatoshiBot es una herramienta educativa interactiva que combina inteligencia artificial con incentivos reales en Bitcoin para llevar educación financiera a usuarios mexicanos. 

La aplicación tiene dos modos:

- Quiz con recompensa en sats: El usuario responde 5 preguntas progresivas sobre Bitcoin. Si supera el puntaje mínimo, recibe sats automáticamente en su wallet.
- Chat libre sobre Bitcoin: Impulsado con Inteligencia Artificial responde cualquier pregunta sobre Bitcoin y su uso en México.


## Stack Tecnológico

- **Backend:** Python (Flask)
- **Frontend:** HTML, CSS, JavaScript
- **IA:** Google Gemini
- **Pagos:** BTCPay Server
- **Contenerización:** Podman

Se integra con BTCPay Server para procesar pagos y utiliza Gemini + Llama para sus capacidades de IA.


## Presentación
[![Ver video en YouTube](https://img.youtube.com/vi/Gwo-qit64zE/0.jpg)](https://www.youtube.com/watch?v=Gwo-qit64zE)
## Demostración

[![Demostración](https://img.youtube.com/vi/MCToE2nmSGA/0.jpg)](https://www.youtube.com/watch?v=MCToE2nmSGA)

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


    > **Nota sobre BTC Pay Server:**
    > Es necesario configurar BTCPay Server para probar este proyecto, lee BTC_PAY_CONFIG

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
