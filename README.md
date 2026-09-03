# Plana Comunidad

Web de la Comunidad Plana, dirigida a candidatos. Sitio estático, sin build.

Es independiente de la web de clientes, que vive en
[Plana-Clientes](https://github.com/Jaimemamalla/Plana-Clientes). Salió de ahí
el 3 sep 2026 conservando su historial, con `git subtree split`.

## Estructura

```
index.html                 la web entera, con CSS y JS inline
js/i18n.js                 motor del selector de idioma
js/dict-comunidad.js       diccionario español a inglés
css/legal.css              estilos de las páginas legales
legal/                     aviso legal, privacidad y cookies
serve.ps1                  servidor local para previsualizar
og.source.html             (pendiente) fuente de la imagen para compartir
```

## Verlo en local

```
powershell -ExecutionPolicy Bypass -File serve.ps1
```

Y abrir `http://localhost:8899`. `serve.ps1` no forma parte del sitio, no hace
falta subirlo a producción.

## El selector de idioma

`js/i18n.js` es el motor y `js/dict-comunidad.js` el diccionario. El motor lee
`window.PLANA_I18N`, así que el diccionario tiene que cargarse antes.

Traduce por nodo de texto, no por elemento, para no tocar el marcado. Los dos
titulares que la capa de punch trocea en palabras (el del FAQ y el del CTA)
van en `heads`, por elemento entero. Los demás en `text`.

**El mismo motor está en el repo de clientes.** Si se arregla algo aquí, hay
que copiarlo allí, y al revés.

Se puede forzar con `?lang=en` y se recuerda en `localStorage`.

## Pendiente

- [ ] **El endpoint del formulario.** `index.html` apunta a
      `https://formspree.io/f/TU_ENDPOINT`. Mientras siga así, el formulario
      avisa al candidato de que no está conectado y no envía nada. No finge
      que ha llegado.
- [ ] **Los datos de empresa en `legal/`.** Todo lo que falta está resaltado
      en amarillo con la clase `.todo`. Que lo revise un abogado, sobre todo
      la parte del artículo 22 del RGPD: la web dice que Planax criba y
      puntúa candidaturas, y eso obliga a informar de la lógica y a permitir
      intervención humana.
- [ ] **La `og.png`**, de 1200x630. En el repo de clientes hay una plantilla
      `og.source.html` que se renderiza con Chrome en headless.
- [ ] **El dominio.** `og:url` y `canonical` apuntan a
      `beplana.com/comunidad/`, que es donde estaba antes de separarse.
- [ ] **El enlace a la web de clientes.** Los dos `data-todo="url-clientes"`
      del nav y del footer esperan su URL.
- [ ] **Las páginas legales están duplicadas** en los dos repos. Cuando haya
      dominios decididos, conviene dejar una sola copia y que la otra web
      enlace a ella, para no mantener lo mismo en dos sitios.
