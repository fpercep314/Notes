# ADR-002: Edición concurrente de notas con bloqueo optimista

- Estado: Aceptado
- Fecha: 28/09/2026

## Contexto

Varios miembros de un equipo pueden editar la misma nota. Sin control, el último en guardar sobrescribe al anterior sin avisar. La edición simultánea en tiempo real llega al final del proyecto (ADR-005), y hasta entonces las notas se editan por la API REST.

## Opciones consideradas

1. **Gana el último que guarda**: sin complejidad, pero se pierden cambios en silencio.
2. **Bloqueo optimista (`@Version`)**: no bloquea a nadie; el segundo en guardar recibe un conflicto.
3. **Bloqueo pesimista**: mantiene la nota bloqueada mientras alguien edita, que en una web pueden ser minutos.
4. **Aviso de "X está editando"**: si alguien cierra la pestaña, la nota queda bloqueada hasta que caduca.

## Decisión

Opción 2. Si la nota cambió desde que el cliente la leyó, la API responde **409 Conflict**.

## Consecuencias

- Ningún cambio se pierde sin avisar.
- En caso de conflicto, el usuario tiene que recargar o sobrescribir.
- La nota necesita un campo de versión desde el principio.
- Hay que comparar la versión que envía el cliente: Hibernate solo comprueba la que cargó en la transacción.
