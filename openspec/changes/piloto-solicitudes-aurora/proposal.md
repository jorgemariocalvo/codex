# Piloto de solicitudes para Comercial Aurora

## Why

Comercial Aurora necesita una bandeja común para registrar solicitudes de servicio, identificar a su responsable y saber si la solución se comunicó a tiempo. El piloto permitirá validar ese flujo en el navegador con datos ficticios.

## What Changes

- Entregar un HTML autónomo que abra con doble clic y contenga interfaz adaptable, lógica y datos de demostración.
- Registrar solicitudes por canal con asignación manual obligatoria, vistas simuladas por rol e historial.
- Medir el plazo de 48 horas corridas con base en la resolución y la comunicación al cliente.
- Importar clientes por CSV y JSON y permitir respaldo y recuperación de la sesión mediante JSON.

## Capabilities

### New Capabilities

- `seguimiento-solicitudes` — registro, asignación, bandejas, estados, historial y plazo de atención.
- `datos-locales` — demostración, importación de clientes y respaldo recuperable en el navegador.

### Modified Capabilities

## Impact

La futura entrega será `index.html` en la raíz del proyecto. El piloto opera en una sesión de navegador. La ingesta automática, el ERP A01, la autenticación, el acceso concurrente, el almacenamiento compartido y la analítica operativa quedan para fases posteriores.
