# Propuesta TP DSW

## Grupo

### Integrantes

- 52904 Alonso, Lucas
- 52172 Bernaus, Marco

### Repositorios

- [frontend app](https://github.com/Nazzexx/frontend-tp-dsw)
- [backend app](https://github.com/Nazzexx/backend-tp-dsw)


## Tema

### Descripción

**Eventify** es una plataforma web de gestión integral de eventos y venta de entradas que conecta organizadores con asistentes. Los organizadores pueden crear y administrar eventos (recitales, discotecas, pasarelas y cualquier evento el cual requiera la venta de una entrada), definir tipos y precios de entrada, gestionar descuentos y hacer seguimiento de ventas en tiempo real. Los asistentes pueden explorar el catálogo de eventos y adquirir entradas.

### Modelo

[Modelo de Dominio](https://app.diagrams.net/#G1YeVLq-fw8C--I0QO49Y6gy2DhVLOH-Gl#%7B%22pageId%22%3A%22aeLrP3cNd4E7HgFAqeD7%22%7D)

## Alcance Funcional

### Alcance Mínimo

#### Regularidad

##### CRUDs Simples _(1 por integrante → 4 en total)_

| #   | CRUD Simple          | Descripción                                                                                |
| --- | -------------------- | ------------------------------------------------------------------------------------------ |
| 1   | **CRUD Categoría**   | ABM de categorías de eventos (ej: Música, Teatro, Deportes, Tecnología). Sin dependencias. |
| 2   | **CRUD Lugar**       | ABM de lugares/venues con nombre, dirección, ciudad y capacidad máxima. Sin dependencias.  |
| 3   | **CRUD Organizador** | ABM de organizadores con datos de contacto y estado de verificación. Sin dependencias.     |

##### CRUDs Dependientes _(1 cada 2 integrantes → 2 en total)_

| #   | CRUD Dependiente | Dependencias                                                                              |
| --- | ---------------- | ----------------------------------------------------------------------------------------- |
| 1   | **CRUD Evento**  | Depende de: Categoría, Lugar, Organizador. Incluye gestión de fechas y estado del evento. |

##### Listados con Filtro y Detalle _(1 cada 2 integrantes → 2 en total)_

| #   | Listado                | Filtros                                                                       | Detalle al seleccionar                                                                      |
| --- | ---------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1   | **Listado de Eventos** | Por categoría, ciudad, rango de fechas y estado (activo/cancelado/finalizado) | Muestra datos completos del evento + lugar + organizador + entradas disponibles con precios |

##### Casos de Uso de Usuario / Épics _(1 cada 2 integrantes → 2 en total)_

| #   | CUU / Epic                          | Descripción detallada                                                                                                                                                                                                                                                                                 |
| --- | ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Comprar entradas para un evento** | Un usuario navega el catálogo de eventos, selecciona un evento, elige el tipo y cantidad de entradas, opcionalmente ingresa un código de descuento, confirma la compra y recibe el/los ticket(s) digitales con código QR único por entrada adquirida. El stock disponible se decrementa al confirmar. |

---

#### Adicionales para Aprobación Directa o en Examen

##### CRUDs de todas las clases de negocio necesarias

| #   | CRUD               | Descripción                                                                                                 |
| --- | ------------------ | ----------------------------------------------------------------------------------------------------------- |
| 1   | CRUD Categoría     | (ya implementado en regularidad)                                                                            |
| 2   | CRUD Lugar         | (ya implementado en regularidad)                                                                            |
| 3   | CRUD Organizador   | (ya implementado en regularidad)                                                                            |
| 4   | CRUD Evento        | (ya implementado en regularidad)                                                                            |
| 5   | CRUD Entrada       | (ya implementado en regularidad)                                                                            |
| 6   | **CRUD Descuento** | ABM de códigos de descuento por evento: porcentaje, fecha de expiración, límite de usos. Depende de Evento. |
| 7   | **CRUD Usuario**   | Gestión de usuarios (admin). Permite ver, activar/desactivar cuentas y cambiar roles.                       |

##### Casos de Uso / Épics para Aprobación _(1 por integrante → 4 en total, mínimo 2 relacionados entre sí)_

| #   | CUU / Epic                             | Descripción detallada                                                                                                                                                                                                                                                               | Relación                      |
| --- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| 1   | **Comprar entradas**                   | Ídem regularidad, incorporando validación de descuento por fecha y usos máximos, y login de usuario obligatorio.                                                                                                                                                                    | Base para CUU 3 y 4           |
| 2   | **Cancelar orden y reintegro**         | Un usuario autenticado puede cancelar una orden confirmada dentro de un plazo definido (ej: 24 hs antes del evento). El sistema actualiza el estado de la orden, libera el stock de entradas y genera un registro de reintegro. Los tickets digitales asociados quedan invalidados. | Consume datos de CUU 1        |
| 3   | **Panel de analítica del organizador** | El organizador autenticado accede a un dashboard de su evento que muestra: total de entradas vendidas vs. disponibles por tipo, ingresos totales, cantidad de check-ins realizados vs. entradas vendidas e historial de descuentos utilizados.                                      | Consume datos de CUU 1, 2 y 3 |

---

### Alcance Adicional Voluntario

| **Listado avanzado** | Buscador global de eventos con filtros combinados (categoría + ciudad + rango de precio + fecha) y ordenamiento por popularidad (entradas vendidas) o fecha. |
| **CUU: Valoración de evento** | Un usuario que compró entradas puede dejar una calificación (1-5 estrellas) y comentario sobre el evento luego de su fecha de realización. Las valoraciones se muestran en el detalle público del evento con promedio y comentarios paginados. |
| **Notificaciones por email** | Envío automático de email con los tickets digitales (QR en PDF) al confirmar una compra. |
