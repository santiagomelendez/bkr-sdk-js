# bkr-sdk-js
Us&aacute; nuestra biblioteca para generar un QR de pago, mostrarlo en un popup en tu sitio web y verificar el resultado.

## Antes de usar

#### 1. Incluir la biblioteca BKR al proyecto
Agreg&aacute; la biblioteca [bkr-sdk.min.js](https://bkr-sdk.s3.amazonaws.com/js/bkr-sdk.min.js) en tu c&oacute;digo html.
```html
<script src="https://bkr-sdk.s3.amazonaws.com/js/bkr-sdk.min.js"></script>
```

#### 2. Crear una instancia de BKR
Solicit&aacute; los par&aacute;metros `id` y `token` de tu comercio a: `sdk {at} bkr.com.ar.`

Cre&aacute; una instancia de BKR utilizando los par&aacute;metros `id` y `token`.

```html
<script>
        const id    = 0;
        const token = "store_token";

        const bkr = new window.BKR(token, id);
</script>
```

## ¿Como se usa?
### **Promise**: Forma asincr&oacute;nica 
1. Llam&aacute; a la funci&oacute;n **checkout**  de **BKR** pasando como parametros un identificador de la transacci&oacute;n, el monto a pagar y un comentario _(opcional)_.
Obt&eacute;n el resultado de la transacci&oacute;n en un promise.
```javascript
function realizarPago(transactionId, amount, comment) 
{
   const promise = bkr.checkout(transactionId, amount, comment);
   ...
}
```
2. Utiliz&aacute; el **Promise** para verificar el resultado de la transacci&oacute;n.
```javascript
function realizarPago(transactionId, amount, comment) 
   {
      const promise = bkr.checkout(transactionId, amount, comment);
      promise.then((result) => {
        if (result.status === 'processed')
          console.log(`Pago ${transactionId} exitoso!`);
        if (result.status === 'canceled')
          console.log(`Pago ${transactionId} cancelado.`); 
      })
      .catch((error) => {
        console.log(`Pago ${transactionId} rechazado.`);
      });
   }
```
### **async & await**: Forma sincr&oacute;nica usando 
1. Llam&aacute; a la funci&oacute;n **checkout**  de **BKR** pasando como parametros un identificador de la transacci&oacute;n, el monto a pagar y un comentario _(opcional)_.
Obt&eacute;n el resultado de la transacci&oacute;n.
```javascript
async function realizarPago(transactionId, amount, comment) 
{
    const result = await bkr.checkout(transactionId, amount, comment);
    ...
}
```
2. Verific&aacute; el resultado de la transacci&oacute;n.
```javascript
async function realizarPago(transactionId, amount, comment) 
{
  const result = await bkr.checkout(transactionId, amount, comment);
  if (result.status === 'processed')
    console.log('Pago exitoso!');
  if (result.status === 'canceled')
    console.log('Pago cancelado!');
}
```
## Confirmar el resultado con backend
Confirm&aacute; el resultado obtenido en backend utilizando la API de **BKR**

```bash
curl -X GET 'https://api.bankar.app/store/<store_id>/checkout/ticket/<transaction_id>'
``` 
