# Propuesta TP DSW

## Grupo

### Integrantes

- 52904 Alonso, Lucas
- 52172 Bernaus, Marco

### Repositorios

- [Frontend app](https://github.com/lucasalonso05/frontend-tp-dsw)

- [Backend app](https://github.com/lucasalonso05/backend-tp-dsw)


## Tema

### Descripción

**Eventify** es una plataforma web de gestión integral de eventos y venta de entradas que conecta organizadores con asistentes. Los organizadores pueden crear y administrar eventos (recitales, discotecas, pasarelas y cualquier evento el cual requiera la venta de una entrada), definir tipos y precios de entrada y hacer seguimiento de ventas en tiempo real. Los asistentes pueden explorar el catálogo de eventos y adquirir entradas.

### Modelos

- [Modelo de Dominio](https://app.diagrams.net/#G1YeVLq-fw8C--I0QO49Y6gy2DhVLOH-Gl#%7B%22pageId%22%3A%22aeLrP3cNd4E7HgFAqeD7%22%7D)
- [Modelo E-R](https://app.diagrams.net/#G1evoEeu5em70AoNBYQtrcQK7Xg6rDGpo3#%7B%22pageId%22%3A%22YW967FpKlnsLeLXvUvun%22%7D)


## Alcance Funcional

##### CRUDs Simples

| #   | CRUD Simple          | Descripción                                                                                |
| --- | -------------------- | ------------------------------------------------------------------------------------------ |
| 1   | **CRUD Lugar**       | ABM de lugares/venues con nombre, dirección, ciudad y capacidad máxima. Sin dependencias.  |
| 2   | **CRUD Persona**     | ABM de organizadores, compradores y asistentes. Sin dependencias.                          |


##### CRUDs Dependientes

| #   | CRUD Dependiente | Dependencias                                                                              |
| --- | ---------------- | ----------------------------------------------------------------------------------------- |
| 1   | **CRUD Evento**  | Depende de: Lugar, Organizador. Incluye gestión de fechas y estado del evento.            |
| 2   | **CRUD Entrada** | Depende de evento. Incluye creacion de tipos de entrada, horarios y precios especificos.  |


##### Listados con Filtro y Detalle

| #   | Listado                | Filtros                                                                          | Detalle al seleccionar                                                                      |
| --- | ---------------------- | -----------------------------------------------------------------------------    | ------------------------------------------------------------------------------------------- |
| 1   | **Listado de Eventos** | Por categoría, ubicacion, rango de fechas y estado (activo/cancelado/finalizado) | Muestra datos completos del evento + lugar + organizador + entradas disponibles con precios |

##### CRUDs de todas las clases de negocio necesarias

| #   | CRUD               | Descripción                                                                                                 |
| --- | ------------------ | ----------------------------------------------------------------------------------------------------------- |
| 1   | CRUD Lugar         | (ya implementado en regularidad)                                                                            |
| 2   | CRUD Persona       | (ya implementado en regularidad)                                                                            |
| 3   | CRUD Evento        | (ya implementado en regularidad)                                                                            |
| 4   | CRUD Entrada       | (ya implementado en regularidad)                                                                            |

##### Casos de Uso / Épics

| #   | CUU / Epic                             | Descripción detallada                                                                                                                                                                                                                                                               | Relación                      |
| --- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| 1   | **Comprar entradas**                   | Un usuario navega el catálogo de eventos, selecciona un evento, elige el tipo y cantidad de entradas, confirma la compra y recibe el/los ticket(s) digitales con código QR único por entrada adquirida. El stock disponible se decrementa al confirmar.|                                                                                                                                                                | Base para CUU 2           |
| 2   | **Panel de analítica del organizador** | El organizador autenticado accede a un dashboard de su evento que muestra: total de entradas vendidas vs. disponibles por tipo, ingresos totales, cantidad de check-ins realizados vs. entradas vendidas e historial de descuentos utilizados.                                      | Consume datos de CUU 1 |
| 3   |**Escaneo de Ticket** | Escenar ticket QR, mediante celular/tablet, consiste en leer QR con camára y llamar a un endpoint para que la redima. Validar que el ticket no haya sido ya canjeado. Se podría cambiar por buscador global. | Finaliza el ciclo de vida de la entrada.           |


### Alcance Adicional

| Req | Detalle |
|-----|---------|
| Listado avanzado | Buscador global de eventos con filtros combinados (categoría + ciudad + rango de precio + fecha) y ordenamiento por popularidad (entradas vendidas) o fecha. |
| Notificaciones por email | Envío automático de email con los tickets digitales (QR en PDF) al confirmar una compra. Uso de Nodemailer o similar. |
