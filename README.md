# Sitio de UNTANGLED

La web publica del juego. Son cuatro ficheros estaticos, sin build ni
dependencias: se sirve la carpeta tal cual.

| Fichero | Para que |
|---|---|
| `index.html` | portada |
| `privacidad.html` | la politica de privacidad, en cinco idiomas. **Esta URL es la que piden Google Play y App Store** |
| `app-ads.txt` | lo que AdMob busca para confirmar que los bloques de anuncios son tuyos |
| iconos | favicon y pantalla de inicio |

## Desplegar (GitHub Pages)

En el repositorio: **Settings → Pages → Source: Deploy from a branch**, rama
`main`, carpeta `/ (root)`. Guardar. En un par de minutos queda en:

- `https://guillehr2.github.io/untangled-web/`
- `https://guillehr2.github.io/untangled-web/privacidad.html`

Esa segunda es la que va en App Store Connect y en la ficha de Google Play.

## El `app-ads.txt` es el unico que necesita otra cosa

AdMob lo busca SOLO en la raiz del dominio que declares como web del
desarrollador. Un repositorio de proyecto se sirve en `/untangled-web/`, que no
es una raiz, asi que ahi no lo encontraria y se cobraria bastante menos.

No corre prisa: eso solo importa cuando la app este publicada e ingresando, no
para TestFlight ni para las pruebas. Cuando llegue el momento, dos salidas:

1. Renombrar este repositorio a `guillehr2.github.io`, que se sirve en la raiz
   (`https://guillehr2.github.io/app-ads.txt`). Gratis y sin DNS, pero ocupa el
   hueco de la pagina personal de GitHub.
2. Un subdominio propio en Vercel (`untangled.guillemhermidarivera.com`),
   importando este mismo repositorio y anadiendo un CNAME a
   `cname.vercel-dns.com`.

## Mantenerlo al dia

`privacidad.html` NO se edita aqui: se genera desde el juego, que es donde vive
el texto (`src/engine/privacy.ts`), para que la pantalla de dentro de la app y
la pagina web no puedan decir cosas distintas.

```bash
npm run policy
```

Eso reescribe `public/privacidad.html` en el proyecto del juego; luego se copia
aqui y se vuelve a subir.
