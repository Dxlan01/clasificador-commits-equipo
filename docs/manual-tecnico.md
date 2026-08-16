# Manual Tecnico - Clasificador de Commits

## Arquitectura

El flujo de la solucion es el siguiente: el cliente (navegador o Postman) envia una peticion HTTP a la API FastAPI en el puerto 8000. La API clasifica el texto usando el motor elegido: el motor eco (reglas, sin modelo, respuesta inmediata) o el motor ollama (que consulta el modelo de lenguaje gemma3:270m corriendo en el puerto 11434). El resultado de la clasificacion se guarda en PostgreSQL, en el puerto 5432, en la tabla inferencias, y luego se devuelve al cliente como respuesta JSON con el tipo de commit y la latencia medida.

Componentes:
- Cliente: navegador o Postman, puerto de salida cualquiera.
- API FastAPI: puerto 8000, expuesto para el cliente.
- Motor ollama: puerto 11434, interno.
- PostgreSQL: puerto 5432, interno.

## Seguridad

- Puertos expuestos: 8000 para la API (acceso del cliente) y 5432 para PostgreSQL (solo desarrollo local; en produccion se restringiria a la red interna).
- Roles de base de datos: postgres es el administrador, usado solo para crear la tabla y el rol de aplicacion. app_ia es el rol que usa la API en el dia a dia, con privilegios minimos: solo SELECT e INSERT sobre la tabla inferencias, sin DELETE, UPDATE ni DROP.
- Manejo de secretos: las contraseñas se guardan en el archivo .env, que nunca se sube al repositorio (esta en .gitignore). El codigo nunca contiene contraseñas escritas directamente.
- Si se filtrara una contraseña: se rotaria de inmediato con ALTER ROLE en PostgreSQL, se revisarian los logs de conexion buscando accesos no autorizados, y se regenerarian las variables en .env.
