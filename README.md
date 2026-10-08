# Mapa de Usos CABA

Consulta de habilitación por rubro y dirección según el Código Urbanístico de la Ciudad de Buenos Aires.

Escribís una frase como «quiero habilitar una cafetería de 120 m2 en Corrientes 2500». El mapa detecta el Área de Mixtura de Usos de esa cuadra y te dice si se puede habilitar, con qué condiciones, si necesita aprobación del Consejo o si no se puede. También pinta toda la Ciudad según el rubro elegido y calcula qué porcentaje de la superficie lo admite.

## Contenido

| Archivo | Qué es |
|---|---|
| `index.html` | La aplicación, encriptada con tu contraseña (lo generás con `encriptar.html`, ver abajo) |
| `cu_raster.png` | Áreas de Mixtura en una imagen de 4,5 m por píxel, para la vista general (los contornos nítidos se dibujan desde zoom 15) |
| `calles.json` | Callejero de la Ciudad con numeración por vereda, para ubicar direcciones y rotular calles |
| `parcelas_geo.png` | Contorno de las 318.127 parcelas, empaquetado sin pérdida dentro de una imagen PNG (se decodifica en el navegador) |
| `parcelas.txt` | Las 318.127 parcelas con SMP, mixtura, altura, distrito, barrio y comuna |
| `plano.jpg` | Plano oficial de Edificabilidad y Usos (Anexo IV) |
| `datos/cuadro_usos_3_3.csv` / `.json` | Cuadro de Usos 3.3 en formato abierto |

## Contraseña

La aplicación se publica encriptada (AES-256, clave derivada con PBKDF2). Quien abra el sitio ve una pantalla que pide la contraseña; sin ella, el código es ilegible incluso mirando el repositorio. Los archivos de datos quedan visibles porque el repositorio es público, pero son datos abiertos de la Ciudad.

Para generar o cambiar la contraseña, abrí `generar-contraseña/encriptar.html` en tu computadora (doble clic), escribí la clave y tocá «Generar index.html». Subí ese `index.html` al repositorio, reemplazando el anterior. **No subas `encriptar.html`**: contiene la aplicación sin encriptar.

## Publicar en GitHub Pages

1. Creá un repositorio nuevo en GitHub (por ejemplo `mapa-usos-caba`), público.
2. Subí el `index.html` que generaste y **todo el contenido de la carpeta `subir-a-github`** a la raíz del repositorio: en la página del repo, *Add file → Upload files*, arrastrá los archivos y la carpeta `datos`, y confirmá con *Commit changes*.
3. Andá a *Settings → Pages*. En *Build and deployment*, elegí *Deploy from a branch*, rama `main` y carpeta `/ (root)`. Guardá.
4. En uno o dos minutos el sitio queda en `https://TU-USUARIO.github.io/mapa-usos-caba/`.

La aplicación tiene que abrirse desde ese enlace (o desde cualquier servidor web). Si abrís `index.html` con doble clic desde tu computadora, el navegador bloquea la carga de `calles.json` y de la capa de mixtura.

Para probarla en tu computadora antes de subirla: abrí una terminal en esta carpeta, ejecutá `python3 -m http.server` y entrá a `http://localhost:8000`.

## Fuentes

- Código Urbanístico, Ley 6.099 y modificatorias. Cuadro de Usos del Suelo N° 3.3, texto ordenado al 31/12/2024.
- Capa parcelaria del Código Urbanístico y callejero: Buenos Aires Data (data.buenosaires.gob.ar).
- Planchetas de Edificabilidad y Usos, Anexo IV, actualizado al 31/12/2024.

## Partidas inmobiliarias

Publicada en GitHub Pages, la página consulta los servicios web de la Ciudad (normalizador de direcciones de USIG, catastro y datos útiles) para traer la partida matriz, las partidas horizontales y otros datos de la parcela. Si esos servicios no responden, la ficha muestra los datos locales (SMP estimado, mixtura, distrito, barrio, comuna).

## Aviso

Herramienta orientativa. No reemplaza el Certificado Urbanístico ni la consulta al organismo competente. Las direcciones se ubican por altura y vereda sobre el callejero, y el SMP es la parcela de esa vereda donde cae el punto: en cuadras de lotes angostos puede ser la vecina, así que confirmalo con la partida. Los distritos especiales (APH, U, UP, etc.) tienen normativa propia.
