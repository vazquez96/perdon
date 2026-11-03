# perdon

## ¿Me perdonas?

La app permite elegir cómo compensar, seleccionar fecha y hora, y enviar esa propuesta por correo. Para usarla gratis no hace falta mantener un servidor Python: GitHub Pages aloja la página estática y EmailJS entrega el correo.

## 1. Configura EmailJS

1. Crea una cuenta gratuita en [EmailJS](https://dashboard.emailjs.com/sign-up) y conecta la cuenta de correo desde la que se enviarán las notificaciones.
2. Crea una plantilla y configura como destinatario fijo el correo que recibirá las respuestas.
3. En el asunto y el cuerpo puedes incluir estas variables:
   - `{{option}}`: plan seleccionado.
   - `{{date}}`: día elegido.
   - `{{time}}`: hora elegida.
4. En EmailJS, copia el Service ID, Template ID y Public Key.
5. En `index.html`, asígnalos al objeto `emailConfig`:

   ```js
   const emailConfig = {
     serviceId: "TU_SERVICE_ID",
     templateId: "TU_TEMPLATE_ID",
     publicKey: "TU_PUBLIC_KEY",
   };
   ```

El Public Key está pensado para usarse en el navegador. No agregues contraseñas de correo, App Passwords ni claves privadas al HTML. El destinatario se configura en la plantilla de EmailJS, no en el código público.

## 2. Publica la página gratis en GitHub Pages

1. Crea un repositorio **público** en GitHub. Con GitHub Free, el repositorio de GitHub Pages debe ser público; la página también será visible para cualquiera.
2. Sube `index.html` y la carpeta `assets/` a la raíz del repositorio. No es necesario subir `perdon-app.zip`.
3. En el repositorio, abre **Settings → Pages**.
4. En **Build and deployment**, elige **Deploy from a branch**, selecciona `main` y la carpeta `/(root)`, y guarda.
5. Cuando termine la publicación, abre la URL que aparece en esa sección y prueba el formulario.

## Limitaciones importantes

- El plan gratuito de EmailJS incluye hasta 200 solicitudes de correo al mes. No requiere tarjeta, pero las solicitudes pueden rechazarse al alcanzar el límite.
- El plan gratuito de EmailJS no incluye lista blanca de dominios. Mantén el destinatario fijo en la plantilla y no compartas credenciales privadas.
- Si faltan los IDs de EmailJS, la app mostrará un error de configuración en vez de indicar que el correo se envió.
- Para recibir una alerta en el teléfono, activa las notificaciones del correo receptor en la aplicación de correo.
- Render Free no es necesario para esta opción y bloquea el envío SMTP saliente. Para usar un backend Python habría que configurar un proveedor de correo por API y alojar el backend por separado.
