# Casa Marx — sitio web

Sitio de una sola página de Casa Marx, red internacional de casas culturales.
HTML estático, sin dependencias ni compilación: un solo archivo, `index.html`,
con los estilos y el script adentro.

## Publicarlo en GitHub Pages

1. Crear un repositorio en GitHub (por ejemplo `casa-marx`), público.
2. Subir `index.html` y `.nojekyll` a la raíz del repositorio.
   Desde la web: **Add file → Upload files**, arrastrar los dos archivos, **Commit changes**.
   Desde la terminal:

   ```bash
   git init
   git add .
   git commit -m "Primera versión del sitio"
   git branch -M main
   git remote add origin https://github.com/USUARIO/casa-marx.git
   git push -u origin main
   ```

3. En el repositorio: **Settings → Pages**. En *Source* elegir **Deploy from a branch**,
   rama `main` y carpeta `/ (root)`. Guardar.
4. A los dos o tres minutos el sitio queda en
   `https://USUARIO.github.io/casa-marx/`.

## Conectar el dominio propio (cuando lo compres)

1. En el panel del registrador donde compres el dominio, crear estos registros DNS:

   | Tipo  | Nombre | Valor |
   |-------|--------|-------|
   | A     | @      | 185.199.108.153 |
   | A     | @      | 185.199.109.153 |
   | A     | @      | 185.199.110.153 |
   | A     | @      | 185.199.111.153 |
   | CNAME | www    | USUARIO.github.io |

2. En **Settings → Pages → Custom domain** escribir el dominio y guardar.
   GitHub crea un archivo `CNAME` en el repositorio.
3. Esperar a que la verificación termine y marcar **Enforce HTTPS**.

La propagación del DNS puede tardar desde unos minutos hasta 24 horas.

## Qué editar

Todo está en `index.html`, en secciones marcadas con comentarios:

- **PORTADA** — título, consigna y bajada.
- **CASAS** — un bloque `<a class="casa">` por casa. Para agregar una:
  copiar un bloque completo, cambiar el `href` del Instagram, el número,
  el país, la ciudad y la cuenta.
- **MAPA** — un bloque `<a class="pin">` por casa. La posición está en
  `transform="translate(X Y)"`, en coordenadas del dibujo
  (`viewBox="0 0 1000 480"`): X de 0 a 1000 de oeste a este,
  Y de 0 a 480 de norte a sur. Para mover un pin, cambiar esos dos números.
  El ancho del cartel negro es `width` del `<rect>`, y su `x` es la mitad
  de ese ancho en negativo, para que quede centrado.
- **CULTURA** — cuatro notas enlazadas a mano. Para cambiarlas, reemplazar
  el `href`, el titular y la fecha.
- **PIE** — reemplazar `CORREO@EJEMPLO.COM` por el correo de contacto.

Los colores están definidos una sola vez, arriba del CSS, en `:root`:
`--papel`, `--tinta`, `--rojo`, `--azul`, `--amarillo`. Cambiar ahí
cambia todo el sitio.

## Pendiente

- Correo de contacto en el pie.
- Si más adelante se quiere que la sección Cultura se actualice sola:
  una GitHub Action programada que lea el RSS de La Izquierda Diario
  y escriba un archivo JSON en el repositorio, que la página lea al cargar.
