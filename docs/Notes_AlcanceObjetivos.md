# Título del proyecto: Notes

**Autor:** Francisco Pérez Cepero

**Fecha:** **/**/\*\*\*\*

**Resumen del proyecto:** Plataforma colaborativa para pequeños equipos que permite almacenar, organizar y compartir apuntes en texto plano y archivos multimedia. Incluye autenticación, CRUD completo, sistema de etiquetas flexible, búsqueda integrada y sincronización en tiempo real. Interfaz moderna en una sola página para acceso instantáneo desde cualquier dispositivo.

## 1. Propósito y alcance

* **¿Qué problema real resuelve la app? ¿Son notas personales, notas de equipo, o ambas cosas?**

  Está destinado a equipos; permite almacenar, organizar y compartir apuntes en texto plano y archivos multimedia. Similar a Google Keep para un equipo reducido de usuarios.

* **¿Qué es explícitamente lo que NO va a hacer (no-objetivos)?**

  No es un gestor de tareas o especie de pseudor ed social.

* **¿Es un proyecto de portafolio con objetivo demostrativo, o esperas que alguien lo use de verdad?**

  Es un proyecto de portafolio, pero debe ser capaz de ser desplegado en un entorno real sin problemas comunes.

* **¿Cuál es tu público objetivo al mostrar este proyecto? (reclutadores, clientes freelance, comunidad open source)**

  Completamente enfocado a reclutadores, aunque con la posibilidad de dirigirse en un futuro a clientes *freelance*.

* **¿Cuánto tiempo tienes para desarrollarlo?**

  Me gustaría tardar en torno a un mes, aunque el tiempo no es un problema grave.

## 2. Modelo de usuarios y equipos

* **¿Un usuario pertenece a un solo equipo/organización, o puede estar en varios a la vez?**

  Un usuario puede pertenecer a varios equipos simultáneamente y debe poder alternar entre las vistas de los diferentes equipos.

* **¿Quién crea los equipos: un usuario o un super admin?**

  Cada usuario puede crear un proyecto, convirtiéndose en el administrador de este.

* **¿Se debe limitar el número de tablones/equipos que puede crear un usuario?**

  Sí, por la sostenibilidad de los recursos de la aplicación.

* **¿Las notas son siempre propiedad de un equipo, o también puede haber notas privadas de un usuario individual?**

  Todas las notas deben pertenecer a un tablón.

* **¿Necesitas roles dentro de un equipo (admin, editor, lector) o todos los miembros tienen los mismos permisos?**

  Existen dos roles: administrador y miembro. Los miembros tienen control total sobre las notas del resto y sus propias notas. El administrador gestiona, además, los usuarios del tablón.

* **¿Habrá jerarquía entre equipos (ej. departamentos dentro de una organización) o es una estructura plana?**

  No, todos los usuarios son iguales (estructura plana).

* **¿Cómo se invita/añade gente a un equipo? (link de invitación, email, código, admin la añade manualmente)**

  Enlace de invitación de un solo uso.

* **¿Qué pasa si eliminas un usuario que tiene notas propias dentro de un equipo? (se transfieren, se borran, quedan huérfanas)**

  Las notas son independientes del usuario que las creó, pero dependientes del equipo al que pertenecen, eliminándose en cascada si se borra el equipo.

## 3. Datos y contenido

* **¿Las notas son solo texto, o necesitas adjuntos, imágenes, formato enriquecido?**

  Las notas siempre tendrán un título y un cuerpo; ambos podrán estar vacíos. Se podrán adjuntar archivos multimedia, no dentro del cuerpo.

  * Tamaño por archivo: 50 MB

  * Número de archivos por nota: 10

* **¿Necesitas versionado de notas (historial de cambios) o solo el estado actual?**

  No tendrán versiones, solo el estado actual.

* **¿Habrá categorías, etiquetas o carpetas para organizar notas?**

  Tendrá un sistema de etiquetas que se marcarán como sugerencias/opciones en próximas notas.

* **¿Necesitas búsqueda de notas? ¿Simple (por título) o full-text (por contenido)?**

  Buscará por texto tanto en el título como en el contenido (*full-text*).

* **¿Hay un límite de tamaño o cantidad de notas por usuario/equipo?**

  No tendrá limitación de caracteres en el cuerpo, pero sí en el título. No se limitará el número de notas.

* **¿Las notas se pueden archivar/eliminar? ¿Hay papelera de reciclaje o el borrado es permanente?**

  Todos podrán eliminar y archivar las notas. La eliminación se realizará mediante *soft delete* y a través de una papelera.

## 4. Colaboración

* **¿Varios usuarios pueden editar la misma nota? ¿Simultáneamente (tiempo real) o por turnos?**

  Pueden editar de manera simultánea en tiempo real.

* **¿Necesitas comentarios sobre notas, o solo edición directa?**

  No tendrá comentarios; la edición es directa.

* **¿Hace falta un sistema de notificaciones (alguien editó, comentó, etc.)?**

  No es necesario un sistema de notificaciones.

* **¿Necesitas historial de "quién hizo qué"? (auditoría/actividad, más allá del versionado de contenido)**

  Habrá un historial para el administrador con fechas, usuarios y detalles del cambio (número de caracteres modificados, título modificado, archivos adjuntos añadidos/modificados, etc.).

* **¿Puedes mencionar a otro usuario dentro de una nota (@usuario)?**

  Sí, mostrando con un color más llamativo la parte en la que eres mencionado.

## 5. Seguridad y acceso

* **¿Autenticación simple (usuario/contraseña) o necesitas OAuth, SSO, etc.?**

  Las dos: autenticación propia con Spring Security (el estándar de la industria en Java) e inicio de sesión con Google mediante OAuth 2.0.

* **¿Qué nivel de privacidad necesitas entre equipos? ¿Un equipo puede ver notas de otro equipo o están completamente aisladas?**

  Cada equipo es individual y están completamente aislados.

* **¿Vas a manejar recuperación de contraseña, verificación de email?**

  Sí, ambas, porque hay autenticación propia: verificación de email al registrarse y recuperación de contraseña mediante enlace de un solo uso con caducidad. Las cuentas que entran con Google no necesitan verificación, porque Google ya garantiza el email.

* **¿Piensas cifrar datos sensibles o es suficiente con autenticación estándar?**

  El cifrado dependerá de la sensibilidad: contraseñas, obviamente sí.

* **¿Necesitas control de sesión? (cerrar sesión en todos los dispositivos, expiración de tokens)**

  Debe tener expiración por token y, de manera opcional, revocar sesiones remotamente.

## 6. Alcance técnico

* **¿Es solo backend + frontend web, o también planeas versión móvil/API pública?**

  Es solo backend + frontend web.

* **¿Tienes ya restricción de stack tecnológico, o eso se decide después de definir objetivos?**

  El *stack* está decidido, pero está abierto a cambios.

* **¿Vas a desplegar la app en algún sitio accesible (demo en vivo) o solo repositorio de código?**

  Tendrá una demo funcional accesible en cualquier momento.

* **¿Necesitas tests automatizados como parte del alcance, o solo pruebas manuales documentadas?**

  Debe tener testing a nivel profesional, además de pruebas manuales documentadas.

## 7. Escalado y rendimiento

* **¿Cuántos usuarios/equipos simulados esperas soportar como prueba de concepto?**

  Unos 100 usuarios repartidos entre 10 y 15 equipos.

* **¿Te importa el rendimiento con muchas notas, o el foco está solo en que funcione correctamente?**

  El rendimiento en distintas situaciones es parte de un funcionamiento correcto, así que sí.

## 8. Mantenimiento y futuro

* **¿El proyecto termina cuando entregas la versión 1, o planeas iterar después?**

  El proyecto tendrá una única versión, aunque bien documentada por si es necesario realizar pequeños cambios a futuro.

* **¿Vas a versionar el proyecto (v1.0, v1.1) o es una entrega única?**

  No, entrega única.

## 9. Criterios de éxito

* **¿Cómo vas a saber que el proyecto "está terminado"?**

  Cuando todos los puntos de este documento se hayan integrado de manera correcta, con un diseño estético y funcional.

* **¿Qué tres o cuatro funcionalidades son innegociables (MVP) y cuáles son "si sobra tiempo"?**

  Ninguna funcionalidad es "si sobra tiempo". El MVP marca el **orden** de desarrollo, no el alcance: es lo primero que se construye y se despliega. El proyecto no está terminado hasta que también estén integradas las funcionalidades posteriores al MVP, que son las que completan lo prometido en el resumen.

### MVP:

* Auth (propia con Spring Security + Google) + equipos + notas (CRUD básico).

* Adjuntos multimedia con validación real (Magic bytes, 50 MB, 10 por nota).

* Búsqueda *full-text* (título + contenido).

* Roles y aislamiento entre equipos (admin/miembro, equipos aislados).

### Después del MVP (obligatorio para dar el proyecto por terminado):

* Edición simultánea en tiempo real.

* Menciones @usuarios con *highlighting*.

* Sistema de etiquetas.

* *Audit log* / historial de auditoría.

* Revocación remota de sesiones.