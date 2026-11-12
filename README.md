# Catálogo de Zentra

La vitrina pública de los negocios que usan Zentra. Una sola página sirve a
todos: quién es el negocio lo dice la dirección.

    https://<dominio>/velas-ana

El cliente mira los productos, arma un carrito y el pedido le llega al negocio
**como un mensaje de WhatsApp**. No se guarda nada acá.

Dar de alta un negocio es prender su catálogo en la base, no publicar de nuevo:

```sql
update zentra.empresas
   set catalogo_activo = true,
       catalogo_slug = 'velas-ana',
       catalogo_color = '#C94F7C',
       catalogo_whatsapp = '0981111222'
 where nombre = '...';
```

## De dónde sale esto

No se edita acá. Se genera desde el repo de la app:

```sh
./catalogo/armar.sh        # para dominio propio
./catalogo/armar.sh /zentra-catalogo   # colgando del nombre del repo
```

`404.html` es una copia de `index.html`: un hosting estático no sabe qué es
`/velas-ana`, así que contesta con la página de "no encontrado" — y como esa
página es ésta, la dirección limpia funciona sin crear un archivo por cliente.

## Qué se puede ver desde acá

Sólo lo que va en una vidriera: nombre, foto, precio y categoría. Nunca el
costo, el stock ni el proveedor. La reja no está en esta página sino en las
vistas `catalogo_negocios` y `catalogo_articulos` de la base, que es lo único
que la clave pública puede leer.
