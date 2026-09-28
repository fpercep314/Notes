# ADR-005: Tiempo real con WebSocket y STOMP dentro del monolito

- Estado: Propuesto
- Fecha: 28/09/2026
- Amplía: ADR-002

## Contexto

El alcance pide que varios usuarios editen la misma nota a la vez y en tiempo real. La aplicación es un monolito modular (ADR-001) en un único servidor, y nadie puede recibir ni enviar cambios de un equipo del que no es miembro.

## Opciones consideradas

1. **Polling**: retraso e ineficiencia; no sirve para edición simultánea.
2. **Server-Sent Events**: solo del servidor al cliente.
3. **WebSocket con STOMP dentro del monolito**: bidireccional e integrado en Spring. El *broker* en memoria solo sirve para una instancia.
4. **Servicio aparte** (por ejemplo, Hocuspocus en Node): otro lenguaje y otro despliegue; contradice el ADR-001.

## Decisión

Opción 3, como un módulo más del monolito. La conexión se autentica con el access token (ADR-004), y cada suscripción y cada envío se autorizan según la pertenencia al equipo.

Cómo se fusionan las ediciones simultáneas queda fuera de este ADR.

## Consecuencias

- Sin procesos extra; reutiliza la autenticación y las reglas de pertenencia.
- Con el *broker* en memoria, una sola instancia.
- Una conexión abierta no caduca con el token: hay que cerrarla al revocar la sesión o al expulsar a alguien de un equipo.
