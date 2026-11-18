# Diseño técnico del piloto

## Context

El repositorio contiene la configuración de OpenSpec y aún carece de una aplicación. El piloto debe funcionar desde una URL local `file://` y permitir que el usuario gestione y conserve los datos desde la interfaz.

## Goals / Non-Goals

**Objetivos.** Mantener una entrega autocontenida, definir un formato de respaldo verificable y asegurar que la bandeja y el historial reflejen la misma lógica de negocio.

**Límites.** Los perfiles son selectores de simulación. La sesión vive en memoria y su continuidad depende del respaldo manual. El archivo no ofrece aislamiento entre usuarios ni almacenamiento seguro de datos reales.

## Decisions

- **Empaquetado.** Situar el HTML, CSS y JavaScript en `index.html`, con estilos y script incrustados. Esto permite distribuir un único archivo y evita que abrirlo localmente dependa de un servidor o una CDN. Usar objetos y arreglos JavaScript para clientes, perfiles, solicitudes y eventos.
- **Operaciones de dominio.** Centralizar la creación, reasignación, transiciones y cierre en funciones que comprueben las reglas antes de actualizar la solicitud y añadir un evento al historial. La bandeja y el detalle se vuelven a renderizar desde ese estado. Aplicar la misma comprobación de rol en la interfaz y en las operaciones internas.
- **Estados.** Permitir iniciar la atención desde ASIGNADO, alternar entre EN_PROCESO y PENDIENTE_TERCERO, resolver desde EN_PROCESO y cerrar desde RESUELTO con la comunicación registrada. CERRADO es terminal en el piloto. Permitir registrar la comunicación con fecha y hora entre la resolución y el momento actual.
- **Fechas e identificación.** Almacenar instantes ISO 8601 en UTC y presentar la hora de Colombia (`America/Bogota`). Calcular el límite sumando 48 horas al instante de recepción. Derivar el prefijo mensual en la zona de Colombia y obtener el siguiente consecutivo de los casos existentes del mes, incluidos los restaurados. Si se agotan los cuatro dígitos, informar el límite sin reutilizar identificadores.
- **Archivos.** Leer archivos seleccionados con la API del navegador y descargar el respaldo con un Blob. Usar JSON con versión explícita del formato, clientes, perfiles, solicitudes y eventos. Definir para el directorio CSV encabezados `cliente_id,nombre`, comas como separador y soporte de comillas y UTF-8. Aceptar JSON como arreglo de objetos con esos campos. Validar todos los registros y sus referencias antes de cambiar el estado. En importación conservar el directorio existente y rechazar el lote si hay duplicados.
- **Datos ficticios.** Sembrar casos con fechas relativas a la apertura para mantener útiles los escenarios de vencimiento. Insertar los datos escritos o importados como texto para evitar que el navegador los interprete como HTML.

## Risks / Trade-offs

- **Pérdida de la sesión al cerrar el archivo.** Mostrar en la interfaz que los cambios se conservan mediante exportación JSON y confirmar el reemplazo al importar un respaldo.
- **Desfase del reloj.** Los plazos dependen del reloj del equipo y el piloto carece de una fuente horaria compartida.
- **Confusión entre perfil y permisos.** Identificar los roles como simulados y usar exclusivamente datos ficticios para la prueba.

## Migration Plan

Entregar `index.html` para abrirlo en el navegador y mostrar el recorrido con datos ficticios. Si se sustituye una copia del piloto, conservar el respaldo antes de abrir otra versión y restaurarlo solo si el formato es compatible.
