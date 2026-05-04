# 2.1 Justificacion

[Volver al capitulo 2](../README.md) | [Volver al indice principal](../../README.md)

---

La necesidad de este proyecto se basa en la demanda actual de aplicaciones que mantengan al usuario informado sin necesidad de recargar la página manualmente. Sistemas de mensajería, herramientas colaborativas o plataformas de monitorización dependen de esta capacidad para ser realmente funcionales. En todos estos casos, que el usuario tenga que intervenir para ver informacion actualizada supone una experiencia deficiente y una pérdida de valor del producto.

Desde el punto de vista técnico, este trabajo se justifica por la oportunidad de aplicar arquitecturas orientadas a eventos en un entorno real de desarrollo. Este tipo de arquitecturas están cada vez mas presentes en la industria y representan una evolución natural respecto al modelo de peticion-respuesta tradicional.

Además, la creación de un componente modular y reutilizable aporta un valor práctico concreto: permite estandarizar la recepción de eventos en diferentes proyectos futuros sin tener que programar la lógica de conexion desde cero en cada ocasion. Un ejemplo claro seria un panel de administración que necesite reflejar en tiempo real los cambios producidos en una base de datos: con este componente bastaría con integrarlo en el proyecto, configurar el servidor al que conectarse y el sistema estaria operativo sin necesidad de reescribir nada.

Por ultimo, he elegido React, Vite y WebSockets ya que las tres herramientas cuentan con una comunidad activa, documentación extensa y una adopción amplia en la industria, lo que reduce los riesgos asociados al desarrollo y facilita encontrar soluciones ante problemas concretos.

---

[Anterior: Marco Teorico (intro)](../README.md) | [Siguiente: 2.2 Estado del Arte](../2.2_Estado_del_Arte/README.md)
