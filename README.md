# Sitio de UNTANGLED

La web publica del juego. Son cuatro ficheros estaticos, sin build ni
dependencias: se sirve la carpeta tal cual.

| Fichero | Para que |
|---|---|
| `index.html` | portada |
| `privacidad.html` | la politica de privacidad, en cinco idiomas. **Esta URL es la que piden Google Play y App Store** |
| `app-ads.txt` | lo que AdMob busca para confirmar que los bloques de anuncios son tuyos |
| iconos | favicon y pantalla de inicio |

## Por que un subdominio y no GitHub Pages

`app-ads.txt` tiene que estar en la **raiz del dominio** que declares como web
del desarrollador en las tiendas. GitHub Pages sirve los repos de proyecto en
`usuario.github.io/repo/`, que no es una raiz, asi que AdMob no lo encontraria
y cobrarias bastante menos.

Con un subdominio propio las dos cosas quedan bien:

- `https://untangled.guillemhermidarivera.com/privacidad.html`
- `https://untangled.guillemhermidarivera.com/app-ads.txt`

## Desplegar

1. Repositorio nuevo en GitHub, aparte del de la web personal.
2. En Vercel, **Add New → Project**, importas ese repositorio. No hay framework
   ni comando de build: Vercel sirve los estaticos directamente.
3. En el proyecto de Vercel, **Settings → Domains**, anades
   `untangled.guillemhermidarivera.com`. Vercel te dira que crees un registro
   **CNAME** apuntando a `cname.vercel-dns.com` donde tengas el DNS del
   dominio.
4. Cuando el dominio este verificado, comprueba que las dos URL de arriba
   responden. La de `app-ads.txt` tiene que salir como texto plano y sin
   redirecciones.

## Mantenerlo al dia

`privacidad.html` NO se edita aqui: se genera desde el juego, que es donde vive
el texto (`src/engine/privacy.ts`), para que la pantalla de dentro de la app y
la pagina web no puedan decir cosas distintas.

```bash
npm run policy
```

Eso reescribe `public/privacidad.html` en el proyecto del juego; luego se copia
aqui y se vuelve a subir.
