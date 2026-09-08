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
og.source.html             fuente de og.png, se renderiza con Chrome headless
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

Traduce por nodo de texto, no por elemento, para no tocar el marcado. Los
titulares que la capa de punch trocea en palabras van en `heads`, por
elemento entero, y los demás en `text`. Ahora mismo `heads` está vacío: los
dos titulares que iban ahí se fueron con el FAQ y el cierre.

**El mismo motor está en el repo de clientes.** Si se arregla algo aquí, hay
que copiarlo allí, y al revés.

Se puede forzar con `?lang=en` y se recuerda en `localStorage`.

## Qué hay aquí ahora

Solo la sección de la Comunidad Plana. El manifiesto, el FAQ y el cierre
se movieron a la web de clientes el 8 sep 2026: hablaban a la empresa, no
al candidato. El FAQ de candidatos y el cierre nuevo los tiene que escribir
Marina.

## Pendiente

- [ ] **El FAQ de candidatos y el cierre.** La web se queda en una sola
      sección hasta que existan.
- [ ] **El endpoint del formulario.** `index.html` apunta a
      `https://formspree.io/f/TU_ENDPOINT`. Mientras siga así, el formulario
      avisa al candidato de que no está conectado y no envía nada. No finge
      que ha llegado.
- [ ] **Los datos de empresa en `legal/`.** Todo lo que falta está resaltado
      en amarillo con la clase `.todo`. Que lo revise un abogado, sobre todo
      la parte del artículo 22 del RGPD: la web dice que Planax criba y
      puntúa candidaturas, y eso obliga a informar de la lógica y a permitir
      intervención humana.
- [ ] **El dominio.** `og:url`, `og:image`, `canonical` y `twitter:image`
      llevan un marcador de Netlify. Hay que poner el definitivo al desplegar.
- [ ] **El enlace a la web de clientes.** Los dos `data-todo="url-clientes"`
      del nav y del footer esperan su URL.
- [ ] **Las páginas legales están duplicadas** en los dos repos. Cuando haya
      dominios decididos, conviene dejar una sola copia y que la otra web
      enlace a ella, para no mantener lo mismo en dos sitios.
