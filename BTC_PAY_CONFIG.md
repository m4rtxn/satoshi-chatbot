# Configuración de BTCPay Server

Este documento detalla los pasos necesarios para configurar BTCPay Server y generar las claves de API correctas para que **SatoshiBot** pueda procesar las recompensas (payouts) automáticamente.

## 1. Requisitos Previos

- Una instancia de **BTCPay Server** operativa.
- Una **Tienda (Store)** creada en BTCPay Server.
- Una **Wallet** configurada en la tienda para permitir pagos (On-Chain Bitcoin).
- BTCPay Server de ejemplo: https://testnet.demo.btcpayserver.org/

## 2. Generación de API Key

El chatbot necesita una API Key para interactuar con tu tienda y crear los pagos.

1. Inicia sesión en tu BTCPay Server.
2. Ve a **Account** (icono de usuario) > **Manage API Keys**.
3. Haz clic en **Generate API Key**.
4. En **Label**, pon un nombre descriptivo, ej: `SatoshiChatbot`.
5. En **Permissions**, selecciona las siguientes opciones (puedes limitarlas a una tienda específica o a todas):

    btcpay.store.canviewinvoices
    btcpay.store.cancreateinvoice
    btcpay.store.canmodifyinvoices
    btcpay.store.canviewstoresettings
    btcpay.store.canmanagepullpayments
    btcpay.store.cancreatepullpayments
    btcpay.store.canviewpullpayments
    btcpay.store.cancreatenonapprovedpullpayments

6. Haz clic en **Generate API Key**.
7. Copia la clave generada (API Key).

## 3. Configuración en `.env`

Abre el archivo `.env` en la raíz del proyecto y actualiza las siguientes variables:

```env
BTCPAY_URL=https://tu-instancia-btcpay.com
BTCPAY_API_KEY=tu_api_key_generada
BTCPAY_STORE_ID=tu_store_id
```

- **BTCPAY_URL**: La URL base de tu servidor
- **BTCPAY_API_KEY**: La clave que acabas de generar.
- **BTCPAY_STORE_ID**: El ID de tu tienda. Lo encuentras en *Store Settings > General > Store ID*.

## 4. Método de Pago (Payout Method)

El código actual está configurado para utilizar el método de pago `BTC` (On-Chain).

- Esto significa que el sistema espera que el usuario introduzca una **dirección de Bitcoin On-Chain**.

## 5. Procesamiento de Pagos

El bot crea el Payout y lo marca como `AwaitingPayment` (Aprobado).
- Aasegúrate de que tu BTCPay Server tenga fondos su wallet.


