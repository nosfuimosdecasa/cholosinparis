# Cholos in Paris — Studio

App web estática para organizar música y ver simulaciones de publicación. Está hecha con HTML, CSS y JavaScript nativo; no necesita un proceso de build y puede desplegarse en GitHub Pages. En modo de demostración guarda datos en el navegador. Al configurar Firebase usa Authentication, Cloud Firestore y Cloud Storage con rutas privadas por usuario.

## Probar y publicar

1. Copia el contenido de esta carpeta a la raíz de tu repositorio de GitHub (incluye `assets/`, `index.html`, `app.js` y `styles.css`).
2. Activa GitHub Pages en **Settings → Pages** y selecciona la rama y carpeta raíz que contienen `index.html`.
3. Para probar localmente, sirve esta carpeta con un servidor estático (por ejemplo, `python -m http.server 8000`) y abre `http://localhost:8000`. No abras `index.html` directamente como archivo: los módulos JavaScript requieren HTTP.

## Conectar Firebase

1. Crea un proyecto de Firebase y registra una aplicación web.
2. Copia la configuración de la app web en `firebase-config.js`.
3. En Firebase Console activa Authentication y habilita Google, Apple (si está configurado en Apple Developer) y correo/contraseña.
4. Agrega el dominio local y el dominio de GitHub Pages a los dominios autorizados de Authentication.
5. Crea una base de Firestore y activa Cloud Storage. Publica las reglas incluidas en `firestore.rules` y `storage.rules`.
6. Para Apple, completa también la configuración del proveedor y sus dominios de retorno en Apple Developer y Firebase Console.

La app usa el SDK modular de Firebase desde módulos CDN para evitar un paso de compilación. Firestore guarda documentos bajo `users/{uid}/songs`, `users/{uid}/projects` y `users/{uid}/profile/main`. Imágenes y audio viven bajo `users/{uid}/...`. Las reglas incluidas solo permiten leer y escribir al usuario autenticado cuyo UID coincide con la ruta.

## Funciones incluidas

- Catálogo en lista o portadas, búsqueda, filtros y orden por fecha o nombre.
- Editor de canción con vistas General, Letra y Versiones; duración predeterminada de 3:00 y colaboradores opcionales.
- Publicar/despublicar canciones y proyectos. Los proyectos guardan referencias a canciones existentes; una canción puede ser sencillo y aparecer también dentro de un álbum con la portada de ese proyecto.
- Tracklist con búsqueda, altas, bajas y orden por botones o arrastrar y soltar.
- Simulador de perfil musical y vistas de Spotify, YouTube, SoundCloud y Apple Music usando una interfaz original inspirada en patrones de plataformas de streaming.
- Perfil de artista, tema oscuro, reproductor persistente y controles adaptados a móvil.
- Acceso con Google, Apple y correo/contraseña cuando Firebase está configurado.

## Notas

- Sin Firebase configurado se cargan datos de demostración y los cambios quedan en el almacenamiento local de ese navegador. Las subidas de audio locales sirven para escuchar durante la sesión; la nube requiere iniciar sesión en Firebase.
- GitHub Pages entrega archivos estáticos: las reglas de Firebase son las que protegen los datos; nunca pongas credenciales administrativas de Firebase en este cliente.
- La simulación no se conecta a las plataformas reales ni distribuye música. La publicación es un estado del catálogo de CHIP Studio.

## Referencias técnicas

- [Firebase: configura una app web](https://firebase.google.com/docs/web/setup)
- [Firebase Authentication: acceso con Google](https://firebase.google.com/docs/auth/web/google-signin)
- [Firebase Storage: subir archivos en Web](https://firebase.google.com/docs/storage/web/upload-files)
- [GitHub Pages: solución de errores 404](https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)
