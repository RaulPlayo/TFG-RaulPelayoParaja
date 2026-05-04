# Diseño y desarrollo de un sistema modular de notificaciones mediante React y WebSockets

## Hola, mi nombre es Raúl Pelayo Paraja y este será mi repositorio de Github en el que explicaré mi Trabajo de Fin de grado.

Mi trabajo de fin de grado consistirá en crear un sistema web que permita la actualización en tiempo real de documentos almacenados en base de datos, evitando la recarga manual de la página por parte del usuario. 
Para ello mediante una API de la empresa Soincon que gestione las operaciones de crear, modificar y consulta de documentos (CRUD), emitirá un evento cuando se produzca una modificación de los datos y tras ello, aparecerá una notificación en mi aplicación.
Estos eventos se enviarán al cliente mediante una conexión mediante WebSockets, lo que permitirá una comunicación bidireccional e instantánea entre el servidor y el navegador. La aplicación se suscribirá a dichos eventos y se actualizará la interfaz automáticamente, mostrando los cambios realizados. 
El proyecto abarcará el diseño de la arquitectura, el backend y el frontend, además de pruebas para medir el rendimiento y facilidad de uso, comparando cómo funciona en tiempo real en comparación con uno tradicional.
