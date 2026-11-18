# Datos locales

## Purpose

Permitir probar el piloto con datos ficticios y conservar el trabajo mediante archivos que se puedan descargar y cargar desde el navegador.

## ADDED Requirements

### Requirement: Demostración en un archivo autónomo
La aplicación SHALL abrir mediante doble clic en un único archivo HTML y ofrecer una interfaz adaptable con clientes, perfiles y solicitudes ficticias disponibles de inmediato sin conexión ni instalación.

#### Scenario: Primera apertura en el navegador
- **WHEN** el usuario abre el HTML sin conexión
- **THEN** puede consultar y gestionar solicitudes ficticias vigentes, próximas a vencer, vencidas y cerradas

### Requirement: Importación del directorio de clientes
La aplicación SHALL aceptar directorios CSV y JSON con identificador de cliente y nombre o razón social. Una importación válida SHALL incorporar los clientes al selector de alta. Si un archivo contiene filas inválidas o identificadores duplicados dentro del archivo o respecto al directorio, SHALL indicar el error y conservar el directorio anterior.

#### Scenario: Importación de clientes en ambos formatos
- **WHEN** el usuario importa un CSV válido y luego un JSON válido con identificadores diferentes
- **THEN** el selector de clientes incluye las entradas de ambos archivos y conserva las entradas existentes

#### Scenario: Archivo inválido o conflicto de identificación
- **WHEN** un archivo contiene una fila incompleta o un identificador duplicado
- **THEN** se informa el motivo y el directorio permanece sin cambios

### Requirement: Exportación y recuperación de la sesión
La aplicación SHALL descargar un respaldo JSON con clientes, perfiles, solicitudes e historial y SHALL permitir cargarlo en otra sesión. Antes de reemplazar los datos actuales, SHALL validar el archivo y solicitar confirmación. Un respaldo inválido SHALL dejar intacta la sesión.

#### Scenario: Restauración tras cerrar el HTML
- **WHEN** el usuario exporta el respaldo, vuelve a abrir el HTML, carga el respaldo y confirma la carga
- **THEN** se recuperan el directorio, los perfiles, las solicitudes, sus responsables, sus fechas y su historial

#### Scenario: Archivo de respaldo inválido
- **WHEN** el usuario carga un JSON mal formado o que referencia un cliente inexistente
- **THEN** se informa el problema y los datos activos permanecen intactos
