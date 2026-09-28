# ADR-001: Monolito modular con Spring Modulith

- Estado: Aceptado
- Fecha: 28/09/2026

## Contexto

Notes lo desarrolla una sola persona, para unos 100 usuarios repartidos en 10-15 equipos, con muchas funcionalidades y aislamiento total entre equipos. Hace falta una estructura con límites claros entre funcionalidades, sin pagar el coste de un sistema distribuido.

## Opciones consideradas

1. **Monolito por capas**: sencillo, pero cada funcionalidad queda repartida y nada limita las dependencias.
2. **Monolito modular sin herramienta**: los límites dependen solo de la disciplina.
3. **Monolito modular con Spring Modulith**: los límites se verifican en un test y los módulos se comunican con eventos. Es una herramienta más que aprender.
4. **Microservicios desde el inicio**: red, varios despliegues y consistencia eventual sin ningún requisito que lo justifique.

## Decisión

Opción 3: un módulo por funcionalidad, comunicados preferentemente con eventos de dominio.

Sin microservicios desde el inicio. Cuando el monolito funcione, se extraerán módulos sin estado, y cada extracción tendrá su propio ADR.

## Consecuencias

- Un solo despliegue y una sola base de datos, con los límites comprobados en los tests.
- No se puede escalar ni desplegar un módulo por separado hasta extraerlo.
- Hay que aprender las reglas de Spring Modulith junto a Spring.
