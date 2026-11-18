# Tareas de implementación

## 1. Estructura y demostración

- [ ] 1.1 Crear `index.html` con HTML, CSS y JavaScript incrustados. Abrirlo con doble clic sin conexión y comprobar la interfaz en un ancho de escritorio y uno móvil.
- [ ] 1.2 Cargar clientes, cuatro agentes, un coordinador y solicitudes ficticias. Comprobar que la primera apertura muestra casos vigentes, próximos a vencer, vencidos y cerrados.

## 2. Registro y seguimiento

- [ ] 2.1 Implementar el formulario y las reglas de alta. Verificar el rechazo sin responsable o cliente válido y el alta con pedido opcional, identificador único y estado ASIGNADO.
- [ ] 2.2 Implementar bandejas, detalle y reasignación. Alternar entre agentes y coordinación para confirmar la visibilidad, la aparición del caso bajo el nuevo responsable y su evento en el historial.
- [ ] 2.3 Implementar transiciones, comunicación y cierre. Verificar el recorrido desde ASIGNADO hasta CERRADO, la espera de tercero, el bloqueo sin comunicación y el cierre sin nota.
- [ ] 2.4 Implementar el cálculo y los indicadores de plazo. Probar los límites de 24, 12 y 0 horas restantes, así como resolución a las 40 horas con comunicación a las 49 y comunicación en el límite exacto.

## 3. Archivos y recuperación

- [ ] 3.1 Implementar la importación de directorios en CSV y JSON y mostrar su formato en la interfaz. Probar ambos formatos, campos entrecomillados en CSV y rechazo de filas inválidas o identificadores duplicados sin cambios parciales.
- [ ] 3.2 Implementar exportación y restauración de JSON con validación y confirmación. Tras reabrir el HTML, comprobar que se conservan los casos y su historial, que un respaldo inválido deja la sesión intacta y que la siguiente alta conserva la unicidad del identificador.

## 4. Validación integrada

- [ ] 4.1 Ejecutar en un navegador, desde el HTML local, un recorrido que importe un cliente, registre una solicitud, la reasigne, registre resolución y comunicación, la cierre y recupere el resultado desde el respaldo.
