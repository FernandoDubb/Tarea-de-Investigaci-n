area de Investigación – Métodos PUT y DELETE (Semana 6)

Este proyecto es la base de la Semana 6 del curso de Desarrollo Móvil.
Aquí se trabaja con Node.js, Express y Sequelize para conectarse a una base de datos MySQL y realizar un CRUD (Crear, Leer, Actualizar y Eliminar) sobre la tabla Estudiantes.

En esta investigación explico cómo funciona la aplicación, para qué sirve cada archivo y cómo se integraron los métodos PUT y DELETE.

1. Archivo: Conexion/database.js

Este archivo es el encargado de crear la conexión con MySQL utilizando Sequelize.

Se configura el nombre de la base de datos: universidad

Usuario: admin123

Contraseña: admin123

Host: localhost

Puerto: 3306

Si la conexión funciona, muestra “conexión establecida”.
Si falla, muestra un error.

Este archivo se importa en el modelo para poder trabajar con la BD.

2. Archivo: Modelos/Estudiantes.js

Aquí se define el modelo de la tabla Estudiantes.
Es como crear una “clase” que representa una tabla.

El modelo incluye:

Campo	Tipo	Descripción
IdEstudiante	ENTERO	Llave primaria, autoincrement
NombreEstudiante	STRING	Nombre del estudiante
EdadEstudiante	ENTERO	Edad
Genero	STRING	Género

Este modelo es el que se usa para poder hacer findAll, create, update y destroy
3. Archivo: index.js (el servidor)

Aquí está Express configurado y todas las rutas del CRUD:

 GET /estudiante

Obtiene la lista de todos los estudiantes.

 POST /estudiante

Crea un nuevo estudiante con los datos enviados en el cuerpo.

 PUT /estudiante/:IdEstudiante

Actualiza un estudiante según su ID.

Código principal: const [updated] = await Estudiante.update(req.body, {
  where: { IdEstudiante: idestudiante },
});
Si se actualiza, responde “registro actualizado”.
Si no existe, devuelve error.

DELETE /estudiante/:idEstudiante

Elimina un estudiante por ID.

Código principal:const deleted = await Estudiante.destroy({
  where: { IdEstudiante: req.params.idEstudiante },
});
Si elimina correctamente, responde “Eliminado correctamente”.
4. Cómo funcionan PUT y DELETE
PUT (Actualizar)

Este método se usa para modificar un registro ya existente.

Ejemplo de cuerpo enviado en Insomnia / Postman:{
  "NombreEstudiante": "Carlos López",
  "EdadEstudiante": 20,
  "Genero": "Masculino"
}
Y la ruta sería:PUT http://localhost:5000/estudiante/3
Esto actualizaría el estudiante con ID 3.
DELETE (Eliminar)

Este método sirve para borrar un registro de la base de datos.

Ruta de ejemplo:DELETE http://localhost:5000/estudiante/4
Esto elimina al estudiante con ID 4.
5. Conclusión

La aplicación base ya incluía los métodos GET y POST.
En esta tarea se realizó la integración de los métodos PUT y DELETE, que permiten actualizar y eliminar estudiantes desde la API.

Express maneja las rutas, Sequelize se encarga de la comunicación con MySQL y cada función responde correctamente con mensajes y códigos HTTP.

Este backend permite tener un CRUD completo y funcional para la tabla Estudiantes.
