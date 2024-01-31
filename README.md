
# Asispass

La solución Asispass, permite el registro, administración y control eficiente de la información de las marcas generadas por los
trabajadores y cualquier incidencia que acompañe al día laboral.
De manera general nuestra solución se compone de 3 elementos, el primero es nuestra controladora que tienen acceso a ciertos
puntos (Seria nuestro lector de tarjetas acompañado de un microcomputador) y son el punto de enlace entre el usuario(trabajador) y
las marcaciones diarias con el servidor: el segundo elemento el nuestro servidor principal (servidor de base de datos) que donde se
procesa y almacena la información, y por último el portal de consultas. Este último siendo el punto de comunicación de todos nuestros
usuarios con los datos al que se les permite el acceso.
Nuestro mecanismo de marcación principal es mediante la lectura de una tarjeta RFID, esta marcación se haría de manera
inmediata. Pues al acercarse a unos centímetros del lector este daría respuesta de la lectura y como muestra entregaría un ticket de la
marca realizada y un Correo electrónico al trabajador correspondiente.
Como mecanismo secundario hay una dirección en la web con libre acceso, donde con una clave temporal (Cambia con el
mantenimiento de los equipos de marcación) y un teclado es sencillamente se realizan las marcas.
La autenticación de usuario se puede simplificar como; En el momento que el usuario realiza la marca, la controladora verifica y envía
3 datos que son el tipo de marca realizado, el valor de la marca y la fecha junto a la hora. Estos datos llegan al servidor donde de
manera paralela verifica que la hora sea correcta y por otro lado verifica que la marca y el tipo sean valido y ven a quien pertenecen
para luego generar la marca del usuario y así retornar los datos solicitados para la impresión del ticket. En caso de que algún dato no
sea válido se almacena en le log de errores y se enviar un reporte con estos datos al final del día.
La confidencialidad de la información entregada se maneja usando políticas de restricción de acceso por niveles y roles de usuario
donde capacidad de lectura y escritura dependen del rol y el nivel de acceso. Nuestro estilo de negocio se basa en 4 tipos de acceso;
el acceso principal o root que es el encargado de administrar, generar y decidir todo lo correspondiente a usuarios dentro del sistema,
otro tipo de acceso es el llamado Admo de sistema, este usuario es el encargado de generar Accesa para empresas y su;
trabajadores y administra todo los correspondiente a las empresas que son nuestro cliente. El usuario Empresa, es quien está al tanto
de los datos e incidencia de los empleados de las empresas, este es nuestro cliente o la persona que designo la empresa cliente para
dirigir este rol. El usuario Trabajador, este se le habilita el acceso no más al crear sus datos dentro del sistema, este usuario tiene
accesos a todos los datos que correspondan a su persona. Y por último el usuario fiscalizador, que tiene como tarea principal la
consulta de los datos de cualquier individuo en la empresa asignada.

Por parte del hospedaje se decidió hacerlo mediante la plataforma Amazon Web Services (AWS), debido a su estabilidad y buen
servicio. Para la aplicación en si la alojamos en el servicio ELB (Elastic Load Balancing, para más información visitar el siguiente [enlace](https://aws.amazon.com/es/elasticloadbalancing/), con sus réplicas en zonas de disponibilidad en Ohio y Sao Paulo, para nuestra base
de datos usamos RDS y su servicio de alta disponibilidad llamado ’Multi AZ’ .

## Sobre el manual de usuario

acontinuacion se mostrara el manual de usuario dividido en 2 grandes partes

1. [Secciones Comunes](./0.TodosLosUsuarios/0.TodosLosUsuarios.md): la informacion que todos los usuarios manejan en comun.
2. informacion por usuario: la informacion o el flujo que es especifico por cada usuario; este a su ves tiene una clasificion por cada nivel de usuario que seria la siguiente:

* Super Admin
* Administrador de Sistema
* [Administrador De Empresas](1.AdmoEmpresas/1.AdmoEmpresas.MD)
* Fiscalizador DT
* Empleados