# Sistema de gestión de tickets 

## Descripción del sistema
Este repositorio contiene el análisis y diseño de un sistema de gestión de turnos o tickets, orientado a facilitar la atención organizada de usuarios en un entorno físico (como bancos, clínicas o servicios públicos). El sistema permite a los usuarios solicitar un ticket, consultar su lugar en la fila, cancelar turnos y recibir notificaciones. Al mismo tiempo, los administradores pueden gestionar la fila y avanzar con la atención de forma ordenada.

- Diagrama de Caso de Uso  
- Diagrama de Clases  
- Diagrama de Integración  

---

## Diagrama de caso de uso

![Diagrama de caso de uso](https://github.com/user-attachments/assets/d6de0e12-ea1f-4797-9ef7-af7c54d68885)

---

### Actores del sistema

En el sistema participan dos actores principales:

- **Usuario**: puede solicitar un ticket, consultar su número en la fila, cancelar un ticket y, si lo desea, recibir notificaciones relacionadas con su turno.
  
- **Admin**: es quien gestiona el sistema y se encarga de llamar al siguiente número para la atención.

---

## Justificación del uso de relaciones `<<include>>` y `<<extend>>`

Durante el diseño del diagrama de caso de uso decidí usar las relaciones `<<include>>` y `<<extend>>` para reflejar correctamente cómo funciona el sistema.

### Uso de `<<include>>`

Utilicé `<<include>>` para representar acciones que son obligatorias o comunes en distintos procesos. Esto me permitió mantener el diagrama más limpio y evitar repetir funcionalidades.

- En el caso de `Solicitar ticket`, decidí incluir `Ver número de espera`, ya que siempre que un usuario solicita un turno debe poder ver su posición.
  
- También usé `<<include>>` entre `Gestión de tickets` y `Cancelar ticket`, porque cancelar el ticket es una acción estándar dentro de esa gestión.

- El admin, al ingresar a la sección de gestión, siempre debe poder llamar al siguiente número, por lo que `Llamar próximo número` también está incluido.

### Uso de `<<extend>>`

En cambio, usé `<<extend>>` cuando una acción es opcional o depende de una condición específica.

- Por ejemplo, cuando el usuario solicita un ticket, puede elegir recibir una notificación, pero esto no es obligatorio. Por eso modelé `Recibir notificación` como una extensión de `Solicitar ticket`.

## Diagrama de clases UML

![image](https://github.com/user-attachments/assets/1ee501e2-09d6-41f8-87cb-9b665a428b28)

El diseño del sistema aplica tres patrones de diseño clave: Singleton, Prototype y Adapter. Cada uno se utiliza para resolver una necesidad específica dentro del sistema de turnos, optimizando su arquitectura y facilitando su mantenimiento.

## Singleton Control central del sistema
Se aplicó el patrón Singleton en la clase SistemaTickets para asegurar que solo exista una instancia del sistema que gestione los tickets. Esto permite mantener un estado global coherente y evitar inconsistencias al registrar, cancelar o consultar turnos.

## Prototype Clonación de tickets
El patrón Prototype se usó en la clase Ticket, que implementa clone(). Esto permite duplicar turnos sin crear uno nuevo desde cero, lo cual es útil cuando se generan tickets con estructuras similares, como plantillas.

## Adapter – Integración de servicios externos
El patrón Adapter se aplica en NotificadorAdapter, que adapta el servicio ServicioSMS a la interfaz general Notificador. Esto permite enviar notificaciones a los usuarios sin depender directamente del servicio externo, manteniendo bajo acoplamiento y mayor flexibilidad.

# Diagrama de implementacion de clases UML

![image](https://github.com/user-attachments/assets/4e06c729-2059-4534-b127-33884391b94b)
Este diagrama representa la arquitectura física del sistema de gestión de turnos, mostrando cómo se distribuyen los componentes en diferentes nodos y cómo se comunican entre sí.
## Estructura general

## Cliente Web/Móvil:
Contiene la interfaz con la que interactúan usuarios y administradores. Se conecta al servidor de aplicaciones mediante HTTP/HTTPS.

## Servidor de Aplicaciones:
Es el núcleo del sistema, compuesto por los siguientes componentes:

 SistemaTickets.jar: Implementa el patrón Singleton para garantizar que solo exista una instancia que gestione los tickets.

 PlantillaTicket.jar: Aplica el patrón Prototype para clonar tickets a partir de una estructura base.

 AdaptadorSMS.jar: Utiliza el patrón Adapter para conectar con un servicio externo de mensajería sin acoplamiento directo.

## Servidor de Base de Datos:
Almacena la información de los tickets y las operaciones realizadas. Se comunica con el sistema a través de JDBC/SQL.

## Proveedor de SMS:
Servicio externo que recibe las solicitudes de notificación por parte del sistema mediante una API.

# Reflexión final

Este proyecto me permitió aplicar de manera práctica los conocimientos adquiridos en mi clase de Patrones de Diseño con el profesor Giovanni Cáceres. Gracias a este trabajo, entendí cómo los patrones como Singleton, Prototype y Adapter pueden resolver problemas reales de diseño de software y mejorar la estructura del sistema.

También reforcé la importancia de planificar, modelar y documentar antes de programar. Esta experiencia me ayudó a desarrollar una visión más profesional y estructurada del desarrollo de software.
