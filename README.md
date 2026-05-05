# Diseño y desarrollo de un sistema modular de notificaciones mediante React y WebSockets

---

## Resumen
 
El presente Trabajo Fin de Grado consiste en la creación de un sistema web que permite la actualización en tiempo real de documentos almacenados en base de datos, evitando la recarga manual de la página por parte del usuario.
 
Para ello, se utiliza una API de la empresa Soincon que gestiona las operaciones de crear, modificar y consultar documentos (CRUD). Cuando se produce una modificación en los datos, el servidor emite un evento que desencadena una notificación en la aplicación cliente. Estos eventos se transmiten mediante una conexión WebSocket, lo que permite una comunicación bidireccional e instantánea entre el servidor y el navegador.
 
El proyecto abarca el diseño de la arquitectura, el backend y el frontend, además de pruebas para medir el rendimiento y facilidad de uso, comparando el comportamiento en tiempo real frente a un sistema tradicional basado en polling.
 
 
---
 
## Estructura del repositorio
 
```
/
├── README.md                          <- Este archivo
├── imagenes/                          <- Diagramas en PlantUML e imágenes
│
├── Capitulo1_Introduccion/
│   └── README.md
│
├── Capitulo2_MarcoTeorico/
│   ├── README.md
│   ├── 2.1_Justificacion/
│   ├── 2.2_Estado_del_Arte/
│   ├── 2.3_Solucion_Propuesta/
│   ├── 2.4_Objetivos/
│   ├── 2.5_Alcance/
│   └── 2.6_Estructura/
│
├── Capitulo3_Requerimientos/
│   ├── README.md
│   ├── 3.1_Modelo_del_Dominio/
│   ├── 3.2_Disciplina_de_Requisitos/
│   ├── 3.3_Requisitos_No_Funcionales/
│   └── 3.4_Mockups/
│
├── Capitulo4_Analisis_Diseño/
│   ├── README.md
│   ├── 4.1_Analisis_Arquitectura/
│   ├── 4.2_Analisis_Casos_de_Uso/
│   ├── 4.3_Analisis_Clases/
│   ├── 4.4_Analisis_Paquetes/
│   ├── 4.5_Diseño_Arquitectura/
│   ├── 4.6_Diseño_Casos_de_Uso/
│   ├── 4.7_Diseño_Clases/
│   └── 4.8_Diseño_Paquetes/
│
├── Capitulo5_Solucion_Propuesta/
│   └── README.md
│
├── Capitulo6_Conclusiones/
│   └── README.md
│
├── Capitulo7_Referencias/
│   └── README.md
│
└── Capitulo8_Anexos/
    └── README.md
```
 
