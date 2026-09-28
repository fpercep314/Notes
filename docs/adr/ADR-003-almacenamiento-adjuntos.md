# ADR-003: Adjuntos en almacenamiento de objetos compatible con S3

- Estado: Propuesto
- Fecha: 28/09/2026

## Contexto

Cada nota admite hasta 10 adjuntos de hasta 50 MB. Solo los miembros del equipo pueden verlos, y la aplicación se despliega en contenedores que pueden recrearse en cualquier momento.

## Opciones consideradas

1. **En PostgreSQL**: archivo y metadatos en la misma transacción, pero la base de datos y sus backups crecen con cada archivo.
2. **Disco del servidor**: lo más simple, pero se pierde al recrear el contenedor y complica los backups.
3. **Almacenamiento de objetos compatible con S3**: escala aparte y permite cambiar de proveedor sin tocar el código. Es un servicio más, sin transacción común con la base de datos.

## Decisión

Opción 3. La base de datos guarda solo los metadatos de cada archivo.

## Consecuencias

- La base de datos se mantiene pequeña y los archivos sobreviven a los despliegues.
- Sin transacción común, hay que evitar objetos huérfanos y borrar los archivos al borrar notas o equipos.
- El aislamiento entre equipos también tiene que aplicarse a las descargas.
- El servicio local y el proveedor de producción se eligen más adelante.
