### Caso de Estudio: Sistema de Gestión de Biblioteca Universitaria

Este caso de estudio simula un sistema de gestión de biblioteca para una universidad que debe permitir la administración de sus recursos (libros, revistas), gestionar a sus usuarios (estudiantes y profesores), y registrar las operaciones de préstamos y devoluciones. El objetivo es que los estudiantes diseñen y desarrollen una base de datos que soporte las operaciones básicas de la biblioteca y su administración.

### **Descripción del Caso**
La Biblioteca Universitaria tiene una colección de libros, revistas y material audiovisual que deben ser catalogados y gestionados. Cada recurso tiene un identificador único, título, año de publicación, y un tipo (libro, revista, o multimedia). Además, los libros tienen autores y un ISBN, las revistas cuentan con una edición, y el material multimedia incluye un formato (DVD, Blu-ray).

La biblioteca ofrece préstamos de estos recursos a sus usuarios, que se dividen en **Estudiantes** y **Profesores**. Cada usuario tiene un identificador único, nombre, dirección, correo electrónico y tipo de usuario (Estudiante o Profesor). Los estudiantes tienen un número de matrícula y un curso asociado, mientras que los profesores tienen un número de empleado y un departamento asociado.

Los préstamos deben registrarse indicando el recurso prestado, el usuario que lo solicita, la fecha de préstamo y la fecha de devolución. Un recurso solo puede ser prestado a un usuario a la vez. También se desea almacenar un historial de los préstamos.

### **Requerimientos del Sistema**
1. **Usuarios**
   - Estudiantes: `ID_Estudiante`, `Nombre`, `Dirección`, `Correo`, `Número de Matrícula`, `Curso`.
   - Profesores: `ID_Profesor`, `Nombre`, `Dirección`, `Correo`, `Número de Empleado`, `Departamento`.

2. **Recursos de la Biblioteca**
   - Libros: `ID_Recurso`, `Título`, `Año_Publicación`, `ISBN`, `Autor`.
   - Revistas: `ID_Recurso`, `Título`, `Año_Publicación`, `Edición`.
   - Multimedia: `ID_Recurso`, `Título`, `Año_Publicación`, `Formato`.

3. **Préstamos**
   - `ID_Préstamo`, `ID_Usuario` (Estudiante o Profesor), `ID_Recurso`, `Fecha_Préstamo`, `Fecha_Devolución`.

4. **Historial de Préstamos**
   - Cada préstamo debe ser registrado y archivado en un historial con los datos anteriores para poder consultar el uso de cada recurso y los usuarios que lo han solicitado.

### **Flujo de los Laboratorios Basados en el Caso de Estudio**

1. [Laboratorio 1: Diseño del Diagrama ERD](#laboratorio-1-diseño-del-diagrama-erd-para-el-sistema-de-biblioteca)
2. [Laboratorio 2: Creación de Tablas en SQL](#laboratorio-2-creación-de-tablas-en-sql-para-el-sistema-de-biblioteca)
3. [Laboratorio 3: Relaciones y Constraints](#laboratorio-3-relaciones-y-constraints-en-el-sistema-de-biblioteca)
4. [Laboratorio 4: Normalización y Optimización](#laboratorio-4-normalización-y-optimización-del-sistema-de-biblioteca)
5. [Laboratorio 5: Inserción y Manipulación de Datos](#laboratorio-5-inserción-y-manipulación-de-datos-en-el-sistema-de-biblioteca)

---

### **Laboratorio 1: Diseño del Diagrama ERD para el Sistema de Biblioteca**
**Objetivo:** Crear un diagrama entidad-relación (ERD) para el sistema de gestión de la Biblioteca Universitaria.

1. **Instrucciones:**
   - **Identificar las entidades:** Usuarios (Estudiantes y Profesores), Recursos (Libros, Revistas, Multimedia), Préstamos e Historial de Préstamos.
   - **Definir atributos para cada entidad:** Por ejemplo, `ID_Usuario`, `Nombre`, `Dirección`, `Correo`, `Número de Matrícula` para los Estudiantes, y `ID_Recurso`, `Título`, `Año_Publicación` para los Recursos.
   - **Establecer las relaciones** entre las entidades: 
     - Usuarios ↔ Préstamos.
     - Préstamos ↔ Recursos.
   - **Definir las claves primarias y foráneas**: Cada entidad debe tener una clave primaria (`ID_Estudiante`, `ID_Profesor`, `ID_Recurso`, `ID_Préstamo`).
   - **Determinar cardinalidad**: Un recurso puede ser prestado a un solo usuario a la vez, pero un usuario puede solicitar varios préstamos.

2. **Resultado esperado:** Un diagrama ERD completo y correcto, que muestre las relaciones entre Usuarios, Recursos y Préstamos.

---

### **Laboratorio 2: Creación de Tablas en SQL para el Sistema de Biblioteca**
**Objetivo:** Convertir el ERD diseñado en sentencias SQL para crear las tablas del sistema de biblioteca.

1. **Instrucciones:**
   - Crear la base de datos con la instrucción `CREATE DATABASE Biblioteca`.
   - Crear tablas para:
     - **Estudiantes:** `CREATE TABLE Estudiantes (ID_Estudiante INT PRIMARY KEY, Nombre VARCHAR(100), Dirección VARCHAR(100), Correo VARCHAR(100), Num_Matricula INT, Curso VARCHAR(100));`
     - **Profesores:** `CREATE TABLE Profesores (ID_Profesor INT PRIMARY KEY, Nombre VARCHAR(100), Dirección VARCHAR(100), Correo VARCHAR(100), Num_Empleado INT, Departamento VARCHAR(100));`
     - **Recursos:** `CREATE TABLE Recursos (ID_Recurso INT PRIMARY KEY, Título VARCHAR(100), Año_Publicación INT, Tipo VARCHAR(50));`
     - **Préstamos:** `CREATE TABLE Prestamos (ID_Préstamo INT PRIMARY KEY, ID_Usuario INT, ID_Recurso INT, Fecha_Préstamo DATE, Fecha_Devolución DATE, FOREIGN KEY (ID_Usuario) REFERENCES Usuarios(ID_Usuario), FOREIGN KEY (ID_Recurso) REFERENCES Recursos(ID_Recurso));`
   - Crear las restricciones `NOT NULL`, `UNIQUE` y `CHECK` según el diseño ERD.

2. **Resultado esperado:** Tablas correctamente creadas con sus restricciones de integridad y relaciones.

---

### **Laboratorio 3: Relaciones y Constraints en el Sistema de Biblioteca**
**Objetivo:** Definir las relaciones y constraints entre las tablas para garantizar la integridad referencial.

1. **Instrucciones:**
   - Crear relaciones entre las tablas utilizando `FOREIGN KEY` en las tablas de Préstamos.
   - Implementar constraints adicionales:
     - `UNIQUE` para el correo de los usuarios.
     - `CHECK` para asegurar que `Año_Publicación` de un recurso sea mayor a 1900.
   - Comprobar el comportamiento de las restricciones con comandos `INSERT` y `DELETE`.

2. **Resultado esperado:** Relaciones y constraints correctamente implementadas, con las restricciones verificadas.

---

### **Laboratorio 4: Normalización y Optimización del Sistema de Biblioteca**
**Objetivo:** Normalizar las tablas según las formas normales para eliminar redundancias y mejorar el diseño.

1. **Instrucciones:**
   - Revisar las tablas y aplicar:
     - **Primera forma normal (1FN)**: Asegurar que cada columna tiene valores atómicos.
     - **Segunda forma normal (2FN)**: Eliminar dependencias parciales.
     - **Tercera forma normal (3FN)**: Eliminar dependencias transitivas.
   - Ajustar el diseño si se encuentran dependencias adicionales.

2. **Resultado esperado:** Tablas normalizadas hasta la tercera forma normal.

---

### **Laboratorio 5: Inserción y Manipulación de Datos en el Sistema de Biblioteca**
**Objetivo:** Insertar datos en las tablas y realizar consultas SQL para manipular la base de datos.

1. **Instrucciones:**
   - Insertar datos de prueba para Estudiantes, Profesores, Recursos y Préstamos.
   - Realizar consultas avanzadas con `JOIN` para obtener:
     - Los recursos prestados por cada usuario.
     - El historial de préstamos de un recurso.
   - Crear índices para mejorar el rendimiento de las consultas más complejas.

2. **Resultado esperado:** Base de datos completa con datos de prueba y consultas avanzadas.

--- 

Este caso de estudio proporciona un contexto claro para que los estudiantes implementen cada aspecto del diseño y desarrollo de bases de datos a través de los laboratorios propuestos.