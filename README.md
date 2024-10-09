CREATE DATABASE JPOSHOESPROYECTOCOMPLETO
USE JPOSHOESPROYECTOCOMPLETO

/*UNIVERSIDAD DOCTOR ANDRÉS BELLO REGIONAL SONSONATE.
	   FACULTAD DE TECNOLOGÍA E INNOVACIÓN.
	     LICENCIATURA EN COMPUTACIÓN.

DOCENTE: ING, KAREN LISSETH REYES DE GARCIA.

CÁTEDRA: DISEÑO E IMPLEMENTACIÓN DE BASE DE DATOS.
 
INTEGRANTES: 
	MENDOZA RIVAS, JOSE RIGOBERTO.
	OSORIO GUTIERREZ, DAMARYS ELENA.
	PEÑA ZUMBA, LUCIA.

CICLO: 02-2023*/

----TABLA DATOS GENERALES
CREATE TABLE JPOSHOES( 
 Nombre VARCHAR(12)NOT NULL,
 Direccion VARCHAR(200)NOT NULL, 
 Telefono VARCHAR(12) NOT NULL,
 Email VARCHAR(50) NOT NULL
 );

INSERT INTO JPOSHOES (Nombre, Direccion, Telefono, Email)
VALUES ('JPO SHOES', 'calle merceditas cáceres, frente a BFA, juayúa, sonsonate', '78901234', 'jposhoes@gmail.com');

select * from JPOSHOES

---TABLA CARGO
create table CARGO (
 CargoId INT PRIMARY KEY IDENTITY (1,1), 
 NombreCargo VARCHAR(25) NOT NULL
);

INSERT INTO CARGO (NombreCargo)
VALUES ('GERENTE');
INSERT INTO CARGO (NombreCargo)
VALUES ('CAJERO');
INSERT INTO CARGO (NombreCargo)
VALUES ('VENDEDOR');

Select * From CARGO;


--TABLA ESTADO 
create table ESTADO( 
EstadoId INT PRIMARY KEY IDENTITY (1,1),
 Estado VARCHAR(25) NOT NULL
 );

INSERT INTO ESTADO (Estado)
VALUES ('ACTIVO');
INSERT INTO ESTADO (Estado)
VALUES ('INACTIVO');

Select * From ESTADO;


 --TABLA EMPLEADO
create table EMPLEADO( 
 EmpleadoId INT primary key identity (1,1),
 Nombre varchar (25)NOT NULL, 
 Apellido varchar (25)NOT NULL,
 DUI varchar (10) not null, 
 Telefono varchar (12) not null,
 Sexo char (1) not null, --(F-FEMENINO)/(M-MASCULINO) 
 --relación de cargo a empleado
 CargoId int not null foreign key references CARGO(CargoId), 
 --relación de estado del empleado
 EstadoId int not null foreign key references ESTADO(EstadoId)
 );

INSERT INTO EMPLEADO (Nombre, Apellido, DUI, Telefono, Sexo, CargoId, EstadoId)
VALUES ('Juan', 'Pérez', '67345678-0', '78901235', 'M', 1,1);
-- Insertar un nuevo empleado
INSERT INTO EMPLEADO (Nombre, Apellido, DUI, Telefono, Sexo, CargoId, EstadoId)
VALUES ('Roxana', 'Flores', '45345678-6', '75063577', 'F', 2,1);
-- Insertar un nuevo empleado
INSERT INTO EMPLEADO (Nombre, Apellido, DUI, Telefono, Sexo, CargoId, EstadoId)
VALUES ('Joaquin', 'Murillo', '27345676-4', '70068045', 'M', 3,1);

select * from EMPLEADO;


 ----TABLA USUARIO
create table USUARIO (
 UsuarioId TINYINT primary key identity (1,1), 
 NombreUsuario varchar (30) NOT NULL,
 Clave varchar(15) not null, --relacion empleado con usuario⬇️
 EmpleadoId int not null foreign key references EMPLEADO(EmpleadoId), 
 --relacion del estado del usuario⬇️
 EstadoId int not null foreign key references ESTADO(EstadoId), 
 --relacion de TIPOUSUARIO a USUARIO⬇️
 CargoId int not null foreign key references CARGO(CargoId)
 );

 INSERT INTO USUARIO (NombreUsuario, Clave, EmpleadoId, EstadoId, CargoId)VALUES 
    ('JP6734', '56780', 1, 1, (select CargoId from EMPLEADO where EmpleadoId = 1)),   
	('RF4534', '56786', 2, 1, (select CargoId from EMPLEADO where EmpleadoId = 2)), 
    ('JM2734', '56764', 3, 1, (select CargoId from EMPLEADO where EmpleadoId = 3));

select * from USUARIO


 --TABLA DEPARTAMENTO
create table DEPARTAMENTO (
 DepartamentoId tinyint primary key identity (1,1), 
 Departamento varchar (25) NOT NULL
);

INSERT INTO DEPARTAMENTO (Departamento) VALUES
	('Ahuachapán'),
	('Cabañas'),
	('Chalatenango'),
	('Cuscatlán'),
	('La Libertad'),
	('La Paz'),
	('La Unión'),
	('Morazán'),
	('San Miguel'),
	('San Salvador'),
	('San Vicente'),
	('Santa Ana'),
	('Sonsonate'),
	('Usulután');

SELECT * FROM DEPARTAMENTO; 

	   
--TABLA PROVEEDOR
create table PROVEEDOR ( 
 ProveedorId smallint primary key identity (1,1),
 NomEmpresa varchar (25) NOT NULL, 
 Representante varchar (50) NOT NULL,
 Telefono varchar(12)NOT NULL, 
 Email varchar (40) NULL,
 Direccion varchar (50) NULL,
 DepartamentoId tinyint not null foreign key references DEPARTAMENTO(DepartamentoId)
 );

INSERT INTO PROVEEDOR (NomEmpresa, Representante, Telefono, Email, Direccion,DepartamentoId)
VALUES  ('Calzado Santa Maria', 'Marlon Pacheco', '70456879', ' psantamariaelcalzado@gmail.com', 'San Salvador',1 ),
		('Alpargatas S.A.', 'Karla Corado', '71025170', 'Julianne.HODARA@alpargatas.com.ar.', 'San Miguel',2 );

SELECT * FROM PROVEEDOR;


 ---TABLA TALLA
CREATE TABLE TALLA ( 
TallaId  int primary key identity (1,1),
Talla varchar (2) NOT NULL
);

INSERT INTO TALLA (Talla)
VALUES 
    ('23'),
    ('24'),
    ('26'),
    ('28'),
	('35'),
	('37'),
	('38'),
	('36'),
	('39'),
	('40'),
	('42');

SELECT * FROM TALLA;


----TABLA COLOR 
CREATE TABLE COLOR(
ColorId int primary key identity (1,1), 
Color varchar (20) NOT NULL
);

INSERT INTO COLOR (Color)
VALUES
    ('Negro'),
    ('Café'),
    ('Blanco'),
    ('Azul'),
	('Beige'),
	('Verde'),
	('Rosado'),
	('Vino');

SELECT * FROM COLOR;


--TABLA DISENO
create table DISENO( 
DisenoId int primary key identity (1,1),
Diseno varchar (30) NOT NULL
);

INSERT INTO DISENO (Diseno)
VALUES
    ('Elegante'),
    ('Casual'),
    ('Clásico');

SELECT * FROM DISENO;


---TABLA MARCA
create table MARCA(
 MarcaId int primary key identity (1,1), 
 Marca varchar (25) NOT NULL
);

INSERT INTO MARCA (Marca)
VALUES
    ('Alden'),
    ('Trucks'),
    ('Fluchos'),
    ('Caricias');

SELECT * FROM MARCA;


--TABLA CLASIFICACION
create table CLASIFICACION(
 ClasificacionId int primary key identity (1,1), 
 Clasificacion varchar (30) NOT NULL
);

INSERT INTO CLASIFICACION (Clasificacion)
VALUES
    ('Hombre'),
    ('Mujer'),
    ('Niño'),
	('Niña');

SELECT * FROM CLASIFICACION;


--TABLA PRODUCTO
CREATE TABLE PRODUCTO( 
 ProductoID INT PRIMARY KEY IDENTITY (1,1),
 NombreProducto VARCHAR(50) NOT NULL, 
 Descripcion varchar (200) NOT NULL,
 Garantia datetime NOT NULL, 
 Precio money NOT NULL,
 CanBodega INT NOT NULL, 
 CanStock INT NOT NULL,
 --relación en la tabla producto 
 DisenoId int not null foreign key references DISENO(DisenoId),
 --relación en la tabla producto 
 MarcaId int not null foreign key references MARCA(MarcaId),
 --relación en la tabla producto 
 ClasificacionId int not null foreign key references CLASIFICACION(CLasificacionId),
 --relación en la tabla producto 
 TallaId int not null foreign key references TALLA(TallaId),
 --relación en la tabla producto 
 ColorId int not null foreign key references COLOR(ColorId),
 ProveedorId smallint not null foreign key references PROVEEDOR(ProveedorId),
 CodigoProd AS LEFT(NombreProducto, 1) + LEFT(Descripcion, 1) + '-' + RIGHT('000' + CONVERT(VARCHAR, ProductoId), 3)
);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Zapatillas', 'Elaboradas con cuero, cocidas', '2023-12-15', 40.99, 100, 50, 2, 2, 1, 8, 1, 1);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Zapatillas', 'Elaboradas con cuero, cocidas', '2023-12-15', 40.99, 100, 50, 1, 4, 2, 4, 5, 1);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Zapatillas', 'Elaboradas con cuero, cocidas', '2023-12-20', 60.00, 150, 75, 1, 1, 2, 5, 8, 1);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Zapatillas', 'Elaboradas con cuero, cocidas', '2023-12-20', 60.00, 150, 75, 2, 1, 2, 6, 1, 1);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Zapatillas', 'Elaboradas con cuero, cocidas', '2023-12-18', 36.99, 200, 120, 3, 3, 1, 7, 2, 2);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Zapatillas', 'Elaboradas con cuero, cocidas', '2023-12-18', 36.99, 200, 120, 3, 3, 1, 5, 8, 2);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Tacones', 'Elaborados con cuero, cocidos', '2023-12-22', 30.99, 200, 130, 3, 4, 2, 6, 4, 2);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Tacones', 'Elaborados con cuero, cocidos', '2023-12-22', 30.99, 200, 130, 3, 4, 2, 5, 7, 2);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Sandalias', 'Elaboradas con cuerina', '2023-12-25', 25.99, 100, 50, 2, 4, 4, 2, 2, 1);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Sandalias', 'Elaboradas con cuerina', '2023-12-25', 25.99, 100, 50, 2, 4, 4, 1, 3, 2);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Botines', 'Elaborados con cuerina', '2023-12-23', 29.95, 100, 40, 2, 1, 2, 4, 2, 1);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Botines', 'Elaborados con cuerina', '2023-12-23', 29.95, 100, 40, 2, 1, 4, 2, 1, 2);

INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Botas', 'Elaborados con cuero', '2023-12-17', 67.00, 175, 70, 2, 2, 3, 3, 1, 1);
INSERT INTO PRODUCTO 
(NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId,ProveedorId)
VALUES ('Botas', 'Elaborados con cuero', '2023-12-17', 67.00, 175, 70, 2, 3, 1, 8, 6, 2);

SELECT * FROM PRODUCTO; 

---TABLA METODOPAGO
create table METODOPAGO(
	MetodoPagoId INT primary key identity (1,1),
	Descripcion varchar (30)NOT NULL
);

INSERT INTO METODOPAGO(Descripcion)
VALUES
    ('Efectivo'),
    ('Tarjeta de Crédito'),
	('Tarjeta de Débito');

SELECT * FROM METODOPAGO

----TABLA PROMOCION
create table PROMOCION (
	PromocionId INT primary key identity (1,1),
	FechaInicio datetime NOT NULL,
	FechaFin datetime NOT NULL,
	PorcentajeDescuento varchar(5) NOT NULL,
	Descripcion varchar (50)NOT NULL,
	ProductoId int not null foreign key references PRODUCTO(ProductoId)
);

INSERT INTO PROMOCION (FechaInicio, FechaFin, PorcentajeDescuento, Descripcion, ProductoId)
VALUES
    ('2024-05-09', '2024-05-11', '50%', 'Celebración del día de la Madre', 7),
    ('2024-06-16', '2024-06-18', '50%', 'Celebración del día del Padre', 1),
    ('2024-10-05', '2024-10-05', '40%', 'Día del Profesional de la informática', 3);

SELECT * FROM PROMOCION;

----TABLA CLIENTE
create table CLIENTE(
	ClienteId TINYINT primary key identity (1,1),
	Nombres varchar (25) NOT NULL,
	Apellidos varchar (25) NOT NULL,
	DUI varchar (9) NULL,
	Direccion varchar (100) NULL,
	Telefono varchar (12) NULL,
	Email varchar (40) NULL,
	Sexo varchar (1) NOT NULL,
);

INSERT INTO CLIENTE (Nombres, Apellidos, DUI, Direccion, Telefono, Email, Sexo)
VALUES
    ('Juan','Pérez','123456789','La Guacamaya, Nahuizalco, Sonsonate','70345678','juan@gmail.com','M'),
    ('Ana','Gómez','987654321','Barrio El Calvario, Juayua, Sonsonate','78765432','ana@gmail.com','F'),
    ('Carlos','López','456789123','Casa 44 Canton San Juan De Dios, Juayua, Sonsonate','65678912','carlos@gmail.com','M');

	SELECT * FROM CLIENTE


----TABLA VENTA
CREATE TABLE VENTA(
	VentaId INT PRIMARY KEY identity (1,1),
	fechaHora DATETIME NOT NULL,
	NombreCliente VARCHAR(50) NOT NULL,
	Total MONEY NOT NULL,
	MetodoPagoId int not null foreign key references METODOPAGO(MetodoPagoId),
	ClienteId tinyint not null foreign key references CLIENTE(ClienteId),
	UsuarioId tinyint not null foreign key references USUARIO(UsuarioId)
);

INSERT INTO VENTA (fechaHora, NombreCliente, Total, MetodoPagoId, ClienteId, UsuarioId)
VALUES
    ('2023-12-01 14:30:00', 'Juan Pérez', 100.50, 1, 1, 1),
    ('2023-12-02 15:45:00', 'Ana Gómez', 75.25, 2, 2, 2),
    ('2023-12-03 12:15:00', 'Carlos López', 120.75, 3, 3, 3);

SELECT * FROM VENTA; 

----TABLA DETVENTA
CREATE TABLE DETVENTA(
	DetVentaId INT PRIMARY KEY IDENTITY (1,1),
	PrecioUnitario money NOT NULL,
	Cantidad INT NOT NULL,
	Total money NOT NULL,
	Descuento money not null,
	VentaId int not null foreign key references VENTA(VentaId),
	ProductoId int not null foreign key references PRODUCTO(ProductoId)
);

INSERT INTO DETVENTA (PrecioUnitario, Cantidad, Total, Descuento, VentaId, ProductoId)
VALUES
    (40.99, 2, 81.98, 0, 1, 1),  
    (60.00, 1, 60.00, 0, 2, 3),  
    (36.99, 3, 110.97, 0, 3, 5);


----TABLA TODA TABLA
CREATE TABLE TODATABLA(
	TablaId int primary key identity (1,1),
	Tabla varchar (50)
);

INSERT INTO TODATABLA (Tabla) VALUES ('JPOSHOES');
INSERT INTO TODATABLA (Tabla) VALUES ('CARGO');
INSERT INTO TODATABLA (Tabla) VALUES ('ESTADO');
INSERT INTO TODATABLA (Tabla) VALUES ('EMPLEADO');
INSERT INTO TODATABLA (Tabla) VALUES ('USUARIO');
INSERT INTO TODATABLA (Tabla) VALUES ('DEPARTAMENTO');
INSERT INTO TODATABLA (Tabla) VALUES ('PROVEEDOR');
INSERT INTO TODATABLA (Tabla) VALUES ('TALLA');
INSERT INTO TODATABLA (Tabla) VALUES ('COLOR');
INSERT INTO TODATABLA (Tabla) VALUES ('DISENO');
INSERT INTO TODATABLA (Tabla) VALUES ('MARCA');
INSERT INTO TODATABLA (Tabla) VALUES ('CLASIFICACION');
INSERT INTO TODATABLA (Tabla) VALUES ('PRODUCTO');
INSERT INTO TODATABLA (Tabla) VALUES ('METODOPAGO');
INSERT INTO TODATABLA (Tabla) VALUES ('PROMOCION');
INSERT INTO TODATABLA (Tabla) VALUES ('CLIENTE');
INSERT INTO TODATABLA (Tabla) VALUES ('VENTA');
INSERT INTO TODATABLA (Tabla) VALUES ('DETVENTA');
INSERT INTO TODATABLA (Tabla) VALUES ('TODATABLA');

SELECT * FROM TODATABLA;


----TABLA PERMISOS
CREATE TABLE PERMISO(
	PermisoId int primary key identity (1,1),
	Permiso varchar (50),
	TablaId int not null foreign key references TODATABLA(TablaId)
);

INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 1);		-- Permiso de lectura en JPOSHOES
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('MODIFICACION', 2);	-- Permiso de modificación en CARGO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('ELIMINACION', 3);	-- Permiso de eliminación en ESTADO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 4);		-- Permiso de lectura en EMPLEADO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('MODIFICACION', 5);	-- Permiso de modificación en USUARIO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('ELIMINACION', 6);	-- Permiso de eliminación en DEPARTAMENTO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 7);		-- Permiso de lectura en PROVEEDOR
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('MODIFICACION', 8);	-- Permiso de modificación en TALLA
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('ELIMINACION', 9);	-- Permiso de eliminación en COLOR
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 10);		-- Permiso de lectura en DISENO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('MODIFICACION', 11);	-- Permiso de modificación en MARCA
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('ELIMINACION', 12);	-- Permiso de eliminación en CLASIFICACION
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 13);		-- Permiso de lectura en PRODUCTO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('MODIFICACION', 14);	-- Permiso de modificación en METODOPAGO
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('ELIMINACION', 15);	-- Permiso de eliminación en PROMOCION
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 16);		-- Permiso de lectura en CLIENTE
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('MODIFICACION', 17); -- Permiso de modificación en VENTA
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('ELIMINACION', 18);	-- Permiso de eliminación en DETVENTA
INSERT INTO PERMISO (Permiso, TablaId) VALUES ('LECTURA', 19);		-- Permiso de lectura en TODATABLA

SELECT * FROM PERMISO


----TABLA USUARIOPERMISO
CREATE TABLE USUARIOPERMISO(
	UsuarioPermisoId int primary key identity (1,1),
	UsuarioId tinyint not null foreign key references USUARIO(UsuarioId),
	PermisoId int not null foreign key references PERMISO(PermisoId),
	TablaId int not null foreign key references TODATABLA(TablaId)
);

INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (1, 1, 1); -- Usuario 1 tiene permiso de lectura en JPOSHOES
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (1, 2, 2); -- Usuario 1 tiene permiso de modificación en CARGO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (1, 3, 3); -- Usuario 1 tiene permiso de eliminación en ESTADO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 4, 4); -- Usuario 2 tiene permiso de lectura en EMPLEADO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 5, 5); -- Usuario 2 tiene permiso de modificación en USUARIO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 6, 6); -- Usuario 2 tiene permiso de eliminación en DEPARTAMENTO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 7, 7); -- Usuario 3 tiene permiso de lectura en PROVEEDOR
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 8, 8);  -- Usuario 3 tiene permiso de modificación en TALLA
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 9, 9);   -- Usuario 3 tiene permiso de eliminación en COLOR
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (1, 10, 10); -- Usuario 1 tiene permiso de lectura en DISENO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 11, 11); -- Usuario 2 tiene permiso de modificación en MARCA
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 12, 12); -- Usuario 2 tiene permiso de eliminación en CLASIFICACION
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 13, 13); -- Usuario 3 tiene permiso de lectura en PRODUCTO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 14, 14); -- Usuario 3 tiene permiso de modificación en METODOPAGO
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 15, 15); -- Usuario 3 tiene permiso de eliminación en PROMOCION
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (1, 16, 16); -- Usuario 1 tiene permiso de lectura en CLIENTE
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 17, 17); -- Usuario 2 tiene permiso de modificación en VENTA
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (2, 18, 18); -- Usuario 2 tiene permiso de eliminación en DETVENTA
INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId) VALUES (3, 19, 19); -- Usuario 3 tiene permiso de lectura en TODATABLA

SELECT * FROM USUARIOPERMISO





/*[|][|][|][|][|][|][|][|][|][|]|[|][|][|][|][|][|][|] PROCEDIMIENTOS ALMACENADOS[|][|][|][|][|][|][|][|][|][|]|[|][|][|][|][|][|][|]*/


/*______________________________TABLA CARGO______________________________*/
----------------------------- INSERCION-------------------------------------------
create procedure InsertCARGO
    @NombreCargo varchar(25)
as
begin
    insert into CARGO (NombreCargo) values (@NombreCargo);
end

exec InsertCARGO 'VENDEDOR';
-------------------------------------ELIMINACION----------------------------------------
delete from CARGO where CargoId >= 1; 

--------------------------- ACTUALIZACION-----------------------------------
update CARGO set NombreCargo = 'Vendedor' where CargoId = 3; 

------------------------------- SELECCION---------------------------------------
select * from CARGO order by CargoId asc;

create procedure SelectAllCargo
as 
begin
    select * from CARGO order by CargoId asc;
end

exec SelectAllCargo;





/*______________________________TABLA ESTADO______________________________*/
----------------------------- INSERCION-------------------------------------------
CREATE PROCEDURE InsertESTADO
    @Estado VARCHAR(25)
AS
BEGIN
    INSERT INTO ESTADO (Estado) VALUES (@Estado);
END

EXEC InsertESTADO 'ACTIVO';

-------------------------------------ELIMINACION----------------------------------------
DELETE FROM ESTADO WHERE EstadoId >= 1; 

--------------------------- ACTUALIZACION O MODIFICACION DE REGISTRO-----------------------------------
UPDATE ESTADO SET Estado = 'Activo' WHERE EstadoId = 1;

------------------------------- SELECCION---------------------------------------

CREATE PROCEDURE SelectAllEstado
AS 
BEGIN
    SELECT * FROM ESTADO ORDER BY EstadoId ASC;
END

EXEC SelectAllESTADO;





/*______________________________TABLA EMPLEADO______________________________*/
CREATE PROCEDURE InsertEMPLEADO
    @Nombre VARCHAR(25),
    @Apellido VARCHAR(25),
    @DUI VARCHAR(10),
    @Telefono VARCHAR(12),
    @Sexo CHAR(1),
    @CargoId INT,
    @EstadoId INT
AS
BEGIN
    INSERT INTO EMPLEADO (Nombre, Apellido, DUI, Telefono, Sexo, CargoId, EstadoId) 
    VALUES (@Nombre, @Apellido, @DUI, @Telefono, @Sexo, @CargoId, @EstadoId);
END

EXEC InsertEMPLEADO 'Daniel', 'Valenzuela', '67854309-0', '76543219', 'M', 3, 1;

-------------------------------------ELIMINACION-----------------------------------------
Delete FROM EMPLEADO WHERE EmpleadoId = 2; --(EL 1 ES EL ID DEL PROVEEDOR QUE SE DESEA ELIMINAR)

--------------------------- ACTUALIZACION O MODIFICACION DE REGISTRO-----------------------------------
Update EMPLEADO set Nombre = 'Josue' where EmpleadoId 3;
Update EMPLEADO set Apellido = 'Castillo' where EmpleadoId 3;
Update EMPLEADO set DUI = '09567378-0' where EmpleadoId 3;
Update EMPLEADO set Telefono = '75340921' where EmpleadoId 3;
Update EMPLEADO set Sexo = 'M' where EmpleadoId 3;
Update EMPLEADO set CargoId = 2 where EmpleadoId 3;
Update EMPLEADO set EstadoId = 2 where EmpleadoId 3;

------------------------------- SELECCION---------------------------------------
select * from EMPLEADO

Select E.EmpleadoId, E.Nombre, E.Apellido, E.DUI, E.Telefono, E.Sexo,  C.NombreCargo, T.Estado
From EMPLEADO E
Join CARGO C On C.CargoId = E.CargoId
Join ESTADO T On T.EstadoId = E.EstadoId;
select * from EMPLEADO





/*______________________________TABLA USUARIO______________________________*/
----------------------------- INSERCION-------------------------------------------
CREATE PROCEDURE InsertUSUARIO
    @NombreUsuario VARCHAR(30),
	@Clave varchar(15),
	@EmpleadoId INT,
    @EstadoId INT,
    @CargoId INT

AS
BEGIN
    INSERT INTO USUARIO (NombreUsuario, Clave, EmpleadoId, EstadoId, CargoId) 
    VALUES (@NombreUsuario, @Clave, @EmpleadoId, @EstadoId, @CargoId );
END

EXEC InsertUSUARIO 'JP0967', '0102004', 1, 1,1;

-------------------------------------ELIMINACION-----------------------------------------
DELETE FROM USUARIO WHERE UsuarioId = 1; -- (EL 1 ES EL ID DEL EMPLEADO QUE SE DESEA ELIMINAR)

--------------------------- ACTUALIZACION O MODIFICACION DE REGISTRO-----------------------------------
UPDATE USUARIO SET NombreUsuario = 'JP0967' WHERE UsuarioId = 1;
UPDATE USUARIO SET Clave = '0102004' WHERE UsuarioId = 1;
UPDATE USUARIO SET EmpleadoId = 3 WHERE UsuarioId = 1;
UPDATE USUARIO SET EstadoId = 2 WHERE UsuarioId = 1;
UPDATE USUARIO SET CargoId = 2 WHERE UsuarioId = 1;

------------------------------- SELECCION---------------------------------------
CREATE PROCEDURE SelectAllUSUARIO
AS 
BEGIN
    SELECT U.UsuarioId as 'Codigo', U.NombreUsuario, U.Clave, E.Nombre, E.Apellido, T.Estado, C.NombreCargo
FROM USUARIO U, EMPLEADO E, CARGO C, ESTADO T
 WHERE E.EmpleadoId = U.EmpleadoId AND T.EstadoId = U.EstadoId AND C.CargoId = U.CargoId 
 ORDER BY E.Nombre;
END

EXEC SelectAllUSUARIO;






/*______________________________TABLA DEPARTAMENTO______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertDEPARTAMENTO
    @Departamento VARCHAR(25)
AS
BEGIN
    INSERT INTO DEPARTAMENTO (Departamento) VALUES (@Departamento);
END

EXEC InsertDEPARTAMENTO 'SAN MIGUEL'
-----------------------------------ELIMINACION

CREATE PROCEDURE DeleteDEPARTAMENTO
    @DepartamentoId TINYINT
AS
BEGIN
    DELETE FROM DEPARTAMENTO WHERE DepartamentoId = @DepartamentoId;
END

EXEC DeleteDEPARTAMENTO @DepartamentoId =3;

-----------------------------------MODIFICACION
Update DEPARTAMENTO set Departamento = 'SAN MIGUEL' Where DeparatmentoId = 1;

-----------------------------------BUSQUEDA
SELECT * FROM DEPARTAMENTO;






/*______________________________TABLA PROVEEDOR______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertProveedor
    @NomEmpresa VARCHAR(25),
    @Representante VARCHAR(50),
    @Telefono VARCHAR(12),
    @Email VARCHAR(40),
    @Direccion VARCHAR(50),
    @DepartamentoId TINYINT
AS
BEGIN
    INSERT INTO PROVEEDOR (NomEmpresa, Representante, Telefono, Email, Direccion, DepartamentoId)
    VALUES (@NomEmpresa, @Representante, @Telefono, @Email, @Direccion, @DepartamentoId);
END

EXEC InsertProveedor
    @NomEmpresa = 'Payless',
    @Representante = 'Carlos Garcia',
    @Telefono = '22238305',
    @Email = 'payless@gmail.com',
    @Direccion = 'Centro Comercial Galerias Loal #32',
    @DepartamentoId = 4; -- ID del departamento correspondiente

-----------------------------------ELIMINACION
CREATE PROCEDURE DeleteProveedor
    @ProveedorId SMALLINT
AS
BEGIN
    DELETE FROM PROVEEDOR WHERE ProveedorId = @ProveedorId;
END

EXEC DeleteProveedor @ProveedorId = 1; --(EL 1 ES EL ID DEL PROVEEDOR QUE SE DESEA ELIMINAR)

-----------------------------------MODIFICACION
Update PROVEEDOR set NomEmpresa = 'Nombre de la empresa' where ProveedorId =1;
Update PROVEEDOR set Representante = 'Damarys Osorio' where ProveedorId = 2;
Update PROVEEDOR set Telefono = '00000000' where ProveedorId = 1;
Update PROVEEDOR set Email = 'modificar email' where ProveedorId = 1;
Update PROVEEDOR set Direccion = 'Cambio Direccion' where ProveedorId = 1;
Update PROVEEDOR set DepartamentoId = 'Departamento' where ProveedorId =1;

-----------------------------------BUSQUEDA
SELECT * FROM PROVEEDOR;

SELECT P.ProveedorId, P.NomEmpresa, P.Representante, P.Telefono, P.Email, P.Direccion, D.Departamento
FROM PROVEEDOR P
JOIN DEPARTAMENTO D ON P.DepartamentoId = D.DepartamentoId;






/*______________________________TABLA TALLA______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertTalla
    @Talla VARCHAR(2)
AS
BEGIN
    INSERT INTO Talla (Talla) VALUES (@Talla);
END

EXEC InsertTalla @Talla = '28';

-----------------------------------ELIMINACION
CREATE PROCEDURE DeleteTalla
    @TallaId INT
AS
BEGIN
    DELETE FROM Talla WHERE TallaId = @TallaId;
END

EXEC DeleteTalla @TallaId = 1;

-----------------------------------MODIFICACION
Update Talla set Talla = '40' where TallaId = 1;

-----------------------------------BUSQUEDA
select * from TALLA;






/*______________________________TABLA COLOR______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertCOLOR
    @Color VARCHAR(20)
AS
BEGIN
    INSERT INTO COLOR (Color) VALUES (@Color);
END

EXEC InsertCOLOR @Color = 'Azul';

-----------------------------------ELIMINACION
CREATE PROCEDURE DeleteColor
    @ColorId INT
AS
BEGIN
    DELETE FROM COLOR WHERE ColorId = @ColorId;
END

EXEC DeleteCOLOR @ColorId = 1;

-----------------------------------MODIFICACION
Update COLOR set Color = 'Rosa' where ColorId = 1;

-----------------------------------BUSQUEDA
select * from COLOR;






/*______________________________TABLA DISENO______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertDISENO
    @Diseno VARCHAR(30)
AS
BEGIN
    INSERT INTO DISENO (Diseno) VALUES (@Diseno);
END

EXEC InsertDISENO @Diseno = 'ELEGANTES';
-----------------------------------ELIMINACION
CREATE PROCEDURE DeleteDISENO
    @DisenoId INT
AS
BEGIN
    DELETE FROM DISENO WHERE DisenoId = @DisenoId;
END

EXEC DeleteDISENO @DisenoId = 2;
-----------------------------------MODIFICACION
Update DISENO set Diseno = 'ELEGANTES' where DisenoId = 1;

-----------------------------------BUSQUEDA
SELECT * FROM DISENO;






/*______________________________TABLA MARCA______________________________*/
-------------------------INSERSION
CREATE PROCEDURE InsertMarca
    @Marca VARCHAR(25)
AS
BEGIN
    INSERT INTO MARCA (Marca) VALUES (@Marca);
END 

EXEC InsertMarca @Marca = 'CARICIAS';
-------------------------ELIMINACION
CREATE PROCEDURE DeleteMarca
    @MarcaId INT
AS
BEGIN
    DELETE FROM MARCA WHERE MarcaId = @MarcaId;
END

EXEC DeleteMarca @MarcaId = 1;
-------------------------MODIFICZCION
UPDATE MARCA SET Marca = 'Caricias' WHERE MarcaId = 21;
-------------------------SELECCION. 
SELECT * FROM MARCA;






/*______________________________TABLA CLASIFICACION______________________________*/
-------------------------INSERSION.
CREATE PROCEDURE InsertCLASIFICACION
    @Clasificacion VARCHAR(30)
AS
BEGIN
    INSERT INTO CLASIFICACION (Clasificacion) VALUES (@Clasificacion);
END

EXEC InsertCLASIFICACION @Clasificacion = 'Mujer';

-------------------------ELIMINACION.
CREATE PROCEDURE DeleteCLASIFICACION
    @ClasificacionId INT
AS
BEGIN
    DELETE FROM CLASIFICACION WHERE ClasificacionId = @ClasificacionId;
END

EXEC DeleteCLASIFICACION @ClasificacionId = 1;

-------------------------MODIFICZCION.
UPDATE CLASIFICACION SET Clasificacion = 'MUJER' WHERE ClasificacionId = 1;

-------------------------SELECCION. 
SELECT * FROM CLASIFICACION;






/*______________________________TABLA PRODUCTO______________________________*/
-------------------------INSERSION.
CREATE PROCEDURE InsertPRODUCTO
    @NombreProducto VARCHAR(50),
    @Descripcion VARCHAR(200),
    @Garantia DATETIME,
    @Precio MONEY,
    @CanBodega INT,
    @CanStock INT,
    @DisenoId INT,
    @MarcaId INT,
    @ClasificacionId INT,
    @TallaId INT,
    @ColorId INT,
    @ProveedorId SMALLINT
AS
BEGIN
    INSERT INTO PRODUCTO (NombreProducto, Descripcion, Garantia, Precio, CanBodega, CanStock, DisenoId, MarcaId, ClasificacionId, TallaId, ColorId, ProveedorId)
    VALUES (@NombreProducto, @Descripcion, @Garantia, @Precio, @CanBodega, @CanStock, @DisenoId, @MarcaId, @ClasificacionId, @TallaId, @ColorId, @ProveedorId);
END

EXEC InsertPRODUCTO
    @NombreProducto = 'Zandalias',
    @Descripcion = 'Zandalias clasicas, comodas echas de cuero',
    @Garantia = '2023-12-30', -- Fecha de garantía;
    @Precio = 26.90, -- Precio en dólares
    @CanBodega = 50, -- Cantidad en bodega
    @CanStock = 100, -- Cantidad en stock
    @DisenoId = 3, -- ID del diseño
    @MarcaId = 1, -- ID de la marca
    @ClasificacionId = 1, -- ID de la clasificación
    @TallaId = 2, -- ID de la talla
    @ColorId = 2, -- ID del color
    @ProveedorId = 2; -- ID del proveedor;


-------------------------MODIFICACION.
UPDATE PRODUCTO SET NombreProducto = 'Zandalias' WHERE ProductoID = 3;
UPDATE PRODUCTO SET Descripcion = 'Zandalias clasicas, comodas echas de cuero' WHERE ProductoID = 3;
UPDATE PRODUCTO SET Garantia = '2024-12-31' WHERE ProductoID = 3;
UPDATE PRODUCTO SET Precio = 109.99 WHERE ProductoID = 3;
UPDATE PRODUCTO SET CanBodega = 60 WHERE ProductoID = 3;
UPDATE PRODUCTO SET CanStock = 120 WHERE ProductoID = 3;
UPDATE PRODUCTO SET DisenoId = 1 WHERE ProductoID = 3;
UPDATE PRODUCTO SET MarcaId = 1  WHERE ProductoID = 3;
UPDATE PRODUCTO SET ClasificacionId = 1 WHERE ProductoID = 3;
UPDATE PRODUCTO SET TallaId = 1 WHERE ProductoID = 3;
UPDATE PRODUCTO SET ColorId = 1 WHERE ProductoID = 3;
UPDATE PRODUCTO SET ProveedorId = 1 WHERE ProductoID = 3;

-------------------------ELIMINACION.
CREATE PROCEDURE deletePRODUCTO
    @ProductoID INT
AS
BEGIN
    DELETE FROM PRODUCTO WHERE ProductoID = @ProductoID;
END

EXEC deletePRODUCTO @ProductoID = 3; 
--DROP PROCEDURE deletePRODUCTO;

-------------------------SELECCION. 
SELECT * FROM PRODUCTO;

Select P.ProductoID, P.NombreProducto, P.Descripcion, P.Garantia, P.Precio, P.CanBodega, P.CanStock, D.Diseno, M.Marca, C.Clasificacion, T.Talla, L.Color, R.NomEmpresa
From PRODUCTO P
Join DISENO D On D.DisenoId = P.DisenoId
Join MARCA M On M.MarcaId = P.MarcaId
Join CLASIFICACION C On C.ClasificacionId = P.ClasificacionId
Join TALLA T On T.TallaId = P.TallaId
Join COLOR L On L.ColorId = P.ColorId
Join PROVEEDOR R On R.ProveedorId = P.ProveedorId;






/*______________________________TABLA METODOPAGO______________________________*/
-------------------------INSERSION.
CREATE PROCEDURE InsertMETODOPAGO
    @Descripcion VARCHAR(30)
AS
BEGIN
    INSERT INTO METODOPAGO (Descripcion) VALUES (@Descripcion);
END

EXEC InsertMETODOPAGO @Descripcion = 'EFECTIVO';
-------------------------ELIMINACION.
CREATE PROCEDURE DeleteMETODOPAGO
    @MetodoPagoId INT
AS
BEGIN
    DELETE FROM METODOPAGO WHERE MetodoPagoId = @MetodoPagoId;
END

EXEC DeleteMETODOPAGO @MetodoPagoId = 1;
-------------------------MODIFICACION.
UPDATE METODOPAGO SET Descripcion = 'TARJETA DE CREDITO' WHERE MetodoPagoId = 1;

-------------------------SELECCION. 
SELECT * FROM METODOPAGO;






/*______________________________TABLA PROMOCION______________________________*/
-------------------------INSERSION.
CREATE PROCEDURE InsertPROMOCION
   @FechaInicio DATETIME,
   @FechaFin DATETIME,
   @PorcentajeDescuento VARCHAR(5),
   @Descripcion VARCHAR(50),
   @ProductoId INT
AS
BEGIN
   INSERT INTO PROMOCION (FechaInicio, FechaFin, PorcentajeDescuento, Descripcion, ProductoId)
   VALUES (@FechaInicio, @FechaFin, @PorcentajeDescuento, @Descripcion, @ProductoId);
END;

EXEC InsertPROMOCION
   @FechaInicio = '2023-12-24',
   @FechaFin = '2023-12-26',
   @PorcentajeDescuento = '40%',
   @Descripcion = 'Promoción de navidad',
   @ProductoId = 3; -- Id del producto.
-------------------------ELIMINACION.
CREATE PROCEDURE DeletePROMOCION
   @PromocionId INT
AS
BEGIN
   DELETE FROM PROMOCION WHERE PromocionId = @PromocionId;
END;

EXEC DeletePROMOCION @PromocionId = 1; -- PromocionId que deseas eliminar
-------------------------MODIFICZCION.
UPDATE PROMOCION SET FechaInicio = '2023-12-24' WHERE PromocionId = 1;
UPDATE PROMOCION SET FechaFin = '2023-12-26' WHERE PromocionId = 1;
UPDATE PROMOCION SET PorcentajeDescuento = '40%' WHERE PromocionId = 1;
UPDATE PROMOCION SET Descripcion = 'Promocion de navidad' WHERE PromocionId = 1;
UPDATE PROMOCION SET ProductoId = 3 WHERE PromocionId = 1;

-------------------------SELECCION. 
select * from PROMOCION;
Select P.PromocionId, P.FechaInicio, P.FechaFin, P.PorcentajeDescuento, P.Descripcion, N.NombreProducto
From PROMOCION P
Join PRODUCTO N On N.ProductoID = P.ProductoID






/*______________________________TABLA CLIENTE______________________________*/
----------------------------- INSERCION-------------------------------------------
create procedure InsertCLIENTE
	@Nombres varchar(25),
	@Apellidos varchar(25),
	@DUI varchar(9),
	@Direccion varchar(100),
	@Telefono varchar(12),
	@Email varchar(40),
	@Sexo varchar(1)
as
	begin
		insert into CLIENTE (Nombres, Apellidos, DUI, Direccion, Telefono, Email, Sexo)
		values (@Nombres, @Apellidos, @DUI, @Direccion, @Telefono, @Email, @Sexo);
	end

exec InsertCLIENTE 'Juan', 'Canales', '02345678-6', 'Barrio el angel sonsonate', '70710234', 'juanC@gmail.com', 'M';

--------------------------- ACTUALIZACION O MODIFICACION DE REGISTRO-----------------------------------
update CLIENTE set Nombres = 'JUAN', Apellidos = 'PINEDA' where ClienteId = 1;
update CLIENTE set DUI = '12345678-9' where ClienteId = 1;
UPDATE CLIENTE set Direccion = 'Calle 4ta' where ClienteId = 1;
UPDATE CLIENTE set Telefono = '56710234' where ClienteId = 1;
UPDATE CLIENTE set Email = 'juan@gmail.com' where ClienteId = 1;

-------------------------------------ELIMINACION----------------------------------------
delete from CLIENTE where ClienteId = 2;

------------------------------- SELECCION---------------------------------------
select * from CLIENTE






/*______________________________TABLA VENTA______________________________*/
----------------------------- INSERCION-------------------------------------------
CREATE PROCEDURE InsertVENTA
    @fechaHora DATETIME,
	@NombreCliente VARCHAR(50),
    @Total MONEY,
    @CargoId INT,
	@MetodoPagoId INT,
	@ClienteId TINYINT,
	@UsuarioId TINYINT
AS
BEGIN
    INSERT INTO VENTA (fechaHora, NombreCliente, Total, MetodoPagoId, ClienteId, UsuarioId) 
    VALUES (@fechaHora, @NombreCliente, @Total, @MetodoPagoId, @ClienteId, @UsuarioId);
END

EXEC InsertVENTA '2023-11-11 23:25:00.000', 'Juan Canales', 50.00, 3, 3, 4, 3;
select * from METODOPAGO
SELECT * FROM CLIENTE
SELECT * FROM USUARIO

--------------------------- ACTUALIZACION O MODIFICACION DE REGISTRO-----------------------------------
UPDATE VENTA SET fechaHora = '2023-11-11 16:30:00' WHERE VentaId = 1;
UPDATE VENTA SET NombreCliente = 'Cristian Guevara' WHERE VentaId = 1;
UPDATE VENTA SET Total = '150.00' WHERE VentaId = 1;
UPDATE VENTA SET MetodoPagoId = 1 WHERE VentaId = 1;
UPDATE VENTA SET ClienteId = 2 WHERE VentaId = 1;
UPDATE VENTA SET UsuarioId = 1 WHERE VentaId = 1;


-------------------------------------ELIMINACION-----------------------------------------
DELETE FROM VENTA WHERE VentaId = 1; 

------------------------------- SELECCION---------------------------------------
select * from VENTA;

Select V.VentaId, V.fechaHora, V.NombreCliente, V.Total, D.Descripcion as MetodoPago, C.ClienteId, U.NombreUsuario
From VENTA V
Join METODOPAGO D On D.MetodoPagoId = V.MetodoPagoId
Join CLIENTE C On C.ClienteId = V.ClienteId
Join USUARIO U On U.UsuarioId = V.UsuarioId






/*______________________________TABLA DETVENTA______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertDETVENTA
    @PrecioUnitario MONEY,
    @Cantidad INT,
    @Total MONEY,
    @Descuento MONEY,
    @VentaId INT,
    @ProductoId INT
AS
BEGIN
    INSERT INTO DETVENTA (PrecioUnitario, Cantidad, Total, Descuento, VentaId, ProductoId)
    VALUES (@PrecioUnitario, @Cantidad, @Total, @Descuento, @VentaId, @ProductoId);
END

EXEC InsertDETVENTA
    @PrecioUnitario = 26.90,
    @Cantidad = 1,
    @Total = 26.90,
    @Descuento = 0.00,
    @VentaId = 1,
    @ProductoId = 2; -- IDs correspondientes a la venta y al producto

-----------------------------------ELIMINACION
CREATE PROCEDURE DeleteDETVENTA
    @DetVentaId INT
AS
BEGIN
    DELETE FROM DETVENTA WHERE DetVentaId = @DetVentaId;
END

EXEC DeleteDETVENTA @DetVentaId = 1;
-----------------------------------MODIFICACION
Update DETVENTA set PrecioUnitario = 26.90 where DetVentaId 2;
Update DETVENTA set Cantidad = 1 where DetVentaId 2;
Update DETVENTA set Total = 'total a pagar' where DetVentaId 1;
Update DETVENTA set Descuento = 'Descuento aplicado' where DetVentaId 2;
Update DETVENTA set VentaId = 'Venta' where DetVentaId 2;
Update DETVENTA set ProductoId = 'Producto' where DetVentaId 2;

-----------------------------------BUSQUEDA
CREATE PROCEDURE SelectAllDETVENTA
AS 
BEGIN
    SELECT D.DetVentaId as 'Codigo', D.PrecioUnitario, D.Cantidad, D.Total, D.Descuento, V.VentaId, P.NombreProducto

FROM DETVENTA D, VENTA V, PRODUCTO P
 WHERE V.VentaId = D.VentaId AND P.ProductoId = D.ProductoId 
 ORDER BY D.DetVentaId;
END

EXEC SelectAllDETVENTA;
 
--drop procedure SelectAllDETVENTA






/*______________________________TABLA TODA TABLA______________________________*/
-----------------------------------INSERSION
CREATE PROCEDURE InsertTabla
   @Tabla VARCHAR(50)
AS
BEGIN
   INSERT INTO TODATABLA (Tabla) VALUES (@Tabla);
END

EXEC InsertTabla @Tabla = 'JPOSHOES';
-----------------------------------ELIMINACION
CREATE PROCEDURE DeleteTabla
   @TablaId INT
AS
BEGIN
   DELETE FROM TODATABLA WHERE TablaId = @TablaId;
END

EXEC DeleteTabla @TablaId = 1;
-----------------------------------MODIFICACION
CREATE PROCEDURE UpdateTabla
   @TablaId INT,
   @Tabla VARCHAR(50)
AS
BEGIN
   UPDATE TODATABLA SET Tabla = @Tabla WHERE TablaId = @TablaId;
END

EXEC UpdateTabla @TablaId = 1, @Tabla = 'Nuevo nombre de la tabla';
-----------------------------------BUSQUEDA
CREATE PROCEDURE SelectTabla
AS
BEGIN
   SELECT * FROM TODATABLA;
END

EXEC SelectTabla;






/*______________________________TABLA PERMISO______________________________*/
-------------------------INSERSION.
CREATE PROCEDURE insertPERMISO
	@Permiso varchar(50),
	@TablaId INT
as
begin
	insert into PERMISO (Permiso, TablaId)
	values(@Permiso, @TablaId);
end

exec insertPERMISO 
	@Permiso = '',
	@TablaId = 1;

-------------------------ELIMINACION
CREATE PROCEDURE ELIMINARPERMISO
   @PermisoId INT
AS
BEGIN
   DELETE FROM PERMISO WHERE PermisoId = @PermisoId;
END;

EXEC ELIMINARPERMISO @PermisoId = 1; 

------MODIFICACION
Update PERMISO set Permiso = '26.90' where PermisoId = 1;
Update PERMISO set TablaId = 1 where PermisoId = 1;

---------SELECCIONAR
SELECT * FROM PERMISO;

Select P.PermisoId, P.Permiso, T.Tabla
From PERMISO P
Join TODATABLA T On T.TablaId = P.TablaId






/*______________________________TABLA USUARIOPERMISO______________________________*/
----------INSERCION
CREATE PROCEDURE insertUSUARIOPERMISO
   @UsuarioId TINYINT,
   @PermisoId INT,
   @TablaId INT
AS
BEGIN
   INSERT INTO USUARIOPERMISO (UsuarioId, PermisoId, TablaId)
   VALUES (@UsuarioId, @PermisoId, @TablaId);
END;

EXEC insertUSUARIOPERMISO @UsuarioId = 1, @PermisoId = 2, @TablaId = 3;

---------ELIMINACION
CREATE PROCEDURE deleteUSUARIOPERMISO
   @UsuarioPermisoId INT
AS
BEGIN
   DELETE FROM USUARIOPERMISO WHERE UsuarioPermisoId = @UsuarioPermisoId;
END;

EXEC deleteUSUARIOPERMISO @UsuarioPermisoId = 1;

-----MODIFICACION.
Update USUARIOPERMISO set UsuarioId = 1 where UsuarioPermisoId = 1;
Update USUARIOPERMISO set PermisoId = 1 where UsuarioPermisoId = 1;
Update USUARIOPERMISO set TablaId = 1 where UsuarioPermisoId = 1;

----SELECCION
SELECT * FROM USUARIOPERMISO

SELECT U.UsuarioPermisoId, S.NombreUsuario, P.Permiso, T.Tabla
FROM USUARIOPERMISO U
JOIN USUARIO S ON S.UsuarioId = U.UsuarioId
JOIN PERMISO P ON P.PermisoId = U.PermisoId
JOIN TODATABLA T ON T.TablaId = U.TablaId;



/*-------------------------------------CONSULTAS IMPORTANTES------------------------------------------------*/
------------------------------------------------------------------------------------------------------------
/*________________________________________________________CAJERO________________________________________ */


--¿CANTIDAD DE VENTAS REGISTRADAS?
SELECT COUNT(*) AS CantidadVentasRegistradas
FROM VENTA;

--TOTAL DE DINERO INGRESADO EN EL DIA.
DECLARE @FechaConsulta DATETIME = '2023-12-15 21:55:00.000';

SELECT 
    SUM(Total) AS TotalGenerado
FROM 
    VENTA
WHERE 
    CONVERT(DATE, fechaHora) = CONVERT(DATE, @FechaConsulta);
	


--¿QUE PRECIO TIENEN LOS PRODUCTOS?
SELECT NombreProducto, Precio
FROM PRODUCTO;


/*________________________________________________________GERENTE________________________________________ */

--¿CUANTOS EMPLEADO HAY EN EL LOCAL?
SELECT COUNT(*) AS TotalEmpleados
FROM EMPLEADO;

--TOTAL DE VENTAS QUE REALIZA CADA CAJERO.
SELECT U.NombreUsuario AS Cajero, COUNT(V.VentaId) AS TotalVentas
FROM VENTA V
JOIN USUARIO U ON V.UsuarioId = U.UsuarioId
WHERE U.CargoId = 3 -- EL ID DEL CAJERO
GROUP BY U.NombreUsuario;

--¿CUANTAS VENTAS SON REALIZADAS POR MES?
SELECT 
    MONTH(fechaHora) AS Mes,
    COUNT(*) AS VentasRealizadas
FROM 
    VENTA
GROUP BY 
    MONTH(fechaHora);

--CANTIDAD DE PRODUCTO EN BODEGA Y STOCK.
-- Consulta productos en bodega
SELECT SUM(CanBodega) AS TotalEnBodega
FROM PRODUCTO;

-- Consulta productos en stock
SELECT SUM(CanStock) AS TotalEnStock
FROM PRODUCTO;



/*________________________________________________________VENDEDRO________________________________________ */

--¿CUANTOS PRODUCTOS HAY EN INVENTARIO?
SELECT COUNT(*) AS TotalProductosEnInventario
FROM PRODUCTO;

--¿CUANTOS PRODUCTOS HAY EN LAS CATEGORIAS.
SELECT
    C.Clasificacion,
    COUNT(P.ProductoId) AS CantidadProductos
FROM
    CLASIFICACION C
JOIN
    PRODUCTO P ON C.ClasificacionId = P.ClasificacionId
GROUP BY
    C.Clasificacion;

--¿CUANTOS PRODUCTOS ESTAN EN PROMOCION?
SELECT COUNT(ProductoId) AS CantidadProductosEnPromocion
FROM PROMOCION;


/*__________________________________________________________________________________________________________ */
------------------------DISEÑO DE FACTURA FINAL PARA LA ADQUISISION DE PRODUCTOS-----------------------------
/*__________________________________________________________________________________________________________ */


CREATE PROCEDURE GenerarFactura
    @VentaId INT
AS
BEGIN
    -- se almacena la información
    DECLARE @FechaVenta DATETIME;
    DECLARE @NombreCliente VARCHAR(50);
    DECLARE @MetodoPago VARCHAR(30);
    DECLARE @TotalVenta MONEY;

    -- información
    SELECT
        @FechaVenta = fechaHora,
        @NombreCliente = NombreCliente,
        @MetodoPago = Descripcion,
        @TotalVenta = Total
    FROM VENTA
    INNER JOIN METODOPAGO ON VENTA.MetodoPagoId = METODOPAGO.MetodoPagoId
    WHERE VentaId = @VentaId;

    -- encabezado
    PRINT '----------------------------------------------';
    PRINT '                FACTURA DE VENTA               ';
    PRINT '----------------------------------------------';
    PRINT 'Fecha de Venta: ' + CONVERT(VARCHAR, @FechaVenta, 120);
    PRINT 'Cliente: ' + @NombreCliente;
    PRINT 'Método de Pago: ' + @MetodoPago;
    PRINT '----------------------------------------------';

    -- detalles de la venta
    SELECT
        P.NombreProducto AS Producto,
        DV.Cantidad AS Cantidad,
        DV.PrecioUnitario AS 'Precio Unitario',
        DV.Descuento AS Descuento,
        DV.Total AS Subtotal
    FROM DETVENTA DV
    INNER JOIN PRODUCTO P ON DV.ProductoId = P.ProductoId
    WHERE DV.VentaId = @VentaId;

    -- total de la venta
    PRINT '----------------------------------------------';
    PRINT 'Total: ' + CONVERT(VARCHAR, @TotalVenta, 2);
    PRINT '----------------------------------------------';
END

EXEC GenerarFactura @VentaId = 2;

SELECT * FROM VENTA
