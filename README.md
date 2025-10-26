# utils-scripts

Colección de scripts de utilidad para automatizar tareas locales.

## update-kiddo

Script que actualiza el repositorio de KiddoClimbs con una rama específica.

### Configuración

1. Edita el archivo [`env/update-kiddo.env`](env/update-kiddo.env) y actualiza el valor de `SOURCE_REPOSITORY` con la ruta local del repositorio de KiddoClimbs.
2. Ajusta `TAILSCALE_BUILD_COMMAND` y `TAILSCALE_START_COMMAND` si necesitas personalizar los comandos de compilación o arranque.
   * Por defecto se ejecutará `npm run build` y luego `npm run start` en segundo plano.
   * Deja `TAILSCALE_BUILD_COMMAND` vacío para omitir la compilación previa.
3. Opcional: agrega el directorio raíz de este proyecto a tu `PATH` o crea un alias para ejecutar el script desde cualquier lugar.

### Uso

```bash
./update-kiddo <rama>
```

El script hará lo siguiente:

1. Validará que se haya indicado la rama.
2. Cargará la ruta del repositorio desde el archivo de environment.
3. Cambiará a la rama indicada.
4. Ejecutará `git pull origin <rama>` para traer los cambios más recientes.

Si ejecutas el script con la opción `--restart`, además compilará la
aplicación con el comando configurado y volverá a iniciar el servicio con
la versión precompilada. Tras el reinicio, el script verifica que el
proceso siga activo y muestra automáticamente las últimas líneas del log
si detecta un fallo inmediato.

Ejemplo:

```bash
./update-kiddo develop
```

Para mostrar la ayuda, ejecuta:

```bash
./update-kiddo --help
```
