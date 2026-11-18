# Seguimiento de solicitudes

## Purpose

Permitir que Comercial Aurora registre las solicitudes de servicio, conozca su responsable y verifique si la solución se comunicó a tiempo.

## ADDED Requirements

### Requirement: Registro manual con responsable obligatorio
La aplicación SHALL registrar una solicitud con un cliente del directorio, contacto, canal, categoría, descripción y un agente elegido manualmente. El número de pedido SHALL ser opcional. Cada alta válida SHALL generar un identificador único con formato AUR-AAAAMM-XXXX, registrar la fecha y hora de recepción y comenzar en ASIGNADO.

#### Scenario: Alta válida sin pedido
- **WHEN** el usuario completa los campos obligatorios y elige un agente sin indicar número de pedido
- **THEN** la solicitud se guarda como ASIGNADO con un identificador único y la fecha y hora de recepción

#### Scenario: Alta sin responsable o con cliente desconocido
- **WHEN** el usuario intenta registrar una solicitud sin agente o sin un cliente válido del directorio
- **THEN** la aplicación explica qué debe corregirse y la solicitud no se guarda

#### Scenario: Clasificación de la solicitud
- **WHEN** el usuario registra una solicitud
- **THEN** puede elegir CORREO, WHATSAPP, TELEFONO o WEB como canal de origen y ESTADO_PEDIDO, NOVEDAD_DESPACHO, COTIZACION, FACTURACION, DEVOLUCION u OTRO como categoría

### Requirement: Bandejas simuladas y reasignación
La aplicación SHALL permitir cambiar entre los perfiles simulados de cuatro agentes y un coordinador. Cada agente SHALL ver y gestionar solo los casos asignados a su perfil. Coordinación SHALL ver todos los casos y podrá reasignar el responsable a otro agente.

#### Scenario: Visibilidad tras reasignar
- **WHEN** coordinación reasigna una solicitud del agente A al agente B
- **THEN** la solicitud desaparece de la bandeja de A, aparece en la de B y se conserva en la de coordinación

### Requirement: Estados e historial
La aplicación SHALL gestionar los estados ASIGNADO, EN_PROCESO, PENDIENTE_TERCERO, RESUELTO y CERRADO. El historial de cada solicitud SHALL mostrar cronológicamente los cambios de estado, reasignaciones y comunicaciones con su fecha, hora y perfil que los registró.

#### Scenario: Transiciones y trazabilidad
- **WHEN** un agente inicia la atención, pone el caso en espera de un tercero, retoma la atención y lo resuelve
- **THEN** el estado final es RESUELTO, la fecha y hora de resolución quedan registradas y cada transición aparece en el historial

### Requirement: Plazo de 48 horas corridas
La aplicación SHALL fijar el vencimiento en 48 horas corridas desde la recepción. Para casos sin completar, SHALL mostrar el tiempo restante y señales visuales y textuales de vigencia o vencimiento. El cumplimiento SHALL evaluarse en el momento posterior entre la resolución y la comunicación registrada, y será oportuno si dicho momento no supera el vencimiento.

#### Scenario: Señales antes y después del vencimiento
- **WHEN** un caso aún carece de resolución o comunicación
- **THEN** el indicador muestra verde con más de 24 horas restantes, amarillo entre 12 y 24 horas inclusive, rojo con menos de 12 horas y estado vencido una vez superado el límite

#### Scenario: Resolución oportuna con comunicación tardía
- **WHEN** el agente resuelve el caso a las 40 horas y comunica la solución a las 49 horas
- **THEN** el sistema muestra que el caso incumplió el plazo

#### Scenario: Comunicación en el límite exacto
- **WHEN** la resolución ya se registró y la comunicación ocurre exactamente 48 horas después de la recepción
- **THEN** el sistema muestra el caso como atendido dentro del plazo

### Requirement: Comunicación y cierre
La aplicación SHALL permitir registrar la fecha, hora y canal con que se comunicó la solución. SHALL permitir cerrar la solicitud únicamente cuando esté resuelta y tenga registrada esa comunicación. La nota de evidencia será opcional.

#### Scenario: Solicitud resuelta sin comunicación
- **WHEN** se intenta cerrar una solicitud resuelta antes de registrar la comunicación
- **THEN** la aplicación mantiene el estado RESUELTO e indica el dato pendiente

#### Scenario: Cierre sin nota de evidencia
- **WHEN** el agente registra la fecha, hora y canal de comunicación de una solicitud resuelta y solicita el cierre
- **THEN** la aplicación guarda la comunicación en el historial y cambia el estado a CERRADO sin exigir nota de evidencia
