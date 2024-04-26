# HTTPS Gratis

## Descripción

Bienvienidos, voy a explicar como generar un https para nuestra app web.
Voy a presentar como se haria con las siguentes tecnologias, pero puede hacerce con la de tu preferencia, esto tomalo como guia ya no no varia mucho.

## ⚙ Tecnologias

Tecnologias para esta guia:

| OS                   | Servidor                                           |
| :------------------------ | :----------------------------------------------- |
| Windows Server             | Nginx                            |


> Cabe destacar que deberemos tener un direccion DNS que apunte a nuestro servidor (direccion IP Publica).

> Ademas deberemos tener abierto el puerto 443 y 80 de nuestro router si fuera el caso.


## 🔰 Comenzando

1. Vamos a necesitar instalar [Certbot](https://certbot.eff.org/).
2. Crear una nueva carpeta vacia llamada "Certbot" en la raiz "C:/" de nuestro sistema.
3. Abrimos la terminal y escribimos el siguiente codigo:
  - si podemos detener nuestra app.
```sh
  certbot certonly --standalone
```
- si no podemos detener nuestra app.
```sh
  certbot certonly --webroot
```
5. Eso es todo.

## 🧞 Nginx
Nuestra config de nginx deberia asegurar tener una configurarcion como la siguente a modo ejemplo.

```
    server {
      listen 80;
      server_name www.example.mydns.org example.mydns.org;

      return 301 https://example.mydns.org/;
    }
    server {
    listen 443 ssl;
    server_name www.example.mydns.org example.mydns.org;
    ...

```

> [!IMPORTANT]
> Agregar nuestros certificados que generamos.

```sh
    ssl_certificate C:/Certbot/live/www.example.mydns.org/fullchain.pem;
    ssl_certificate_key C:/Certbot/live/www.example.mydns.org/privkey.pem;
```

Esto es todo. verificar que nuestro dns tenga https, no tarda en aplicarse los cambios es rapido.


## 👀 Referencia

- [Certbot](https://certbot.eff.org/)

- [Configuring HTTPS servers](https://nginx.org/en/docs/http/configuring_https_servers.html)