# ADR-004: Autenticación con JWT de corta duración y refresh token

- Estado: Propuesto
- Fecha: 28/09/2026

## Contexto

El frontend es una SPA en React. Se puede entrar con cuenta propia o con Google, y los dos caminos tienen que acabar en la misma sesión. El alcance pide expiración por token y revocación remota de sesiones. Los riesgos principales son XSS (robo de tokens) y CSRF (cookies que se envían solas).

## Opciones consideradas

1. **Sesión en servidor**: simple y revocable al instante, pero exige protección CSRF en toda la API.
2. **JWT de corta duración + refresh token guardado en BD**: la API no consulta la BD en cada petición y las sesiones se pueden revocar. Un access token ya emitido vale hasta que caduca.
3. **JWT de larga duración sin refresh**: no se puede revocar.
4. **Servidor de autorización** (Keycloak, Spring Authorization Server): excesivo para una sola aplicación.

## Decisión

Opción 2:

- Access token de corta duración, guardado solo en memoria en el cliente.
- Refresh token opaco en una cookie `HttpOnly`, guardado hasheado en BD y rotado en cada uso.
- El inicio de sesión con Google termina emitiendo los mismos tokens.

## Consecuencias

- Autenticar una petición no requiere consultar la BD.
- Las sesiones se pueden listar y revocar.
- Tras revocar una sesión, su access token sigue siendo válido hasta que caduca.
- Hay que proteger el refresco frente a CSRF y probar los ataques (token caducado, manipulado o reutilizado).
