# examenDataBases
Este proyecto detalla el diseño y la creación de una base de datos llamada campusBikes, destinada a gestionar la información relacionada con los clientes, proveedores, productos, envíos y ventas de una tienda de bicicletas.

Estructura del Proyecto



## 1. Diagrama Entidad-Relación (DER)



El DER incluye las siguientes entidades principales:

- **Clientes**

- **Proveedores**

- **Envios**

- **Productos**

- **Ventas**

- **ventaProducto**



## 2. Comandos SQL para Crear la Base de Datos Física



#### Creación de la Base de Datos

**CREATE DATABASE campusBikes;**
**USE campusBikes;**

## Tablas y sus Estructuras

#### 1. Tabla Clientes:

Contiene la información de los clientes registrados.

**CREATE TABLE Clientes (
    idCliente INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL,
    email VARCHAR(200)
);**


#### 2. Tabla Proveedores:

Contiene los datos de los proveedores.

**CREATE TABLE Proveedores (
    idProveedor INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL
);**


#### 3. Tabla Envio:

Almacena el estado de los envíos relacionados con los proveedores.

**CREATE TABLE Envio (
    idEnvio INT PRIMARY KEY AUTO_INCREMENT,
    estadoEnvio ENUM('Pendiente', 'Entregado', 'En camino', 'Cancelado') DEFAULT 'Pendiente',
    idProveedor INT,
    FOREIGN KEY (idProveedor) REFERENCES Proveedores(idProveedor)
);**


#### 4. Tabla Productos:

Contiene información sobre las categorías de productos, disponibilidad, y envíos.

**CREATE TABLE Productos (
    idProducto INT PRIMARY KEY AUTO_INCREMENT,
    categoria ENUM('Bicicleta', 'Repuesto', 'Accesorio') NOT NULL,
    disponible ENUM('Si', 'No') NOT NULL,
    precio INT NOT NULL,
    stock INT NOT NULL,
    idEnvio INT,
    FOREIGN KEY (idEnvio) REFERENCES Envio(idEnvio)
);**


#### 5. Tabla ventaProducto:

Registra los productos vendidos en cada transacción.

**CREATE TABLE ventaProducto (
    idVentaProducto INT PRIMARY KEY AUTO_INCREMENT,
    cantidad INT NOT NULL,
    idProducto INT,
    FOREIGN KEY (idProducto) REFERENCES Productos(idProducto),
    idCliente INT,
    FOREIGN KEY (idCliente) REFERENCES Clientes(idCliente)
);**


#### 6. Tabla Ventas:

Administra el registro de cada venta realizada.

**CREATE TABLE Ventas (
    idVenta INT PRIMARY KEY AUTO_INCREMENT,
    fecha DATE NOT NULL,
    precioTotal INT NOT NULL,
    cantidadArticulos INT NOT NULL,
    idCliente INT,
    FOREIGN KEY (idCliente) REFERENCES Clientes(idCliente),
    idVentaProducto INT,
    FOREIGN KEY (idVentaProducto) REFERENCES ventaProducto(idVentaProducto)
);**

## Explicación de las Relaciones

#### 1. Relación entre Proveedores y Envio:

Un proveedor puede tener múltiples envíos, pero un envío pertenece a un único proveedor.

- **Relación: 1:N**

#### 2. Relación entre Envio y Productos:

Un envío puede contener varios productos, pero un producto pertenece a un único envío.

- **Relación: 1:N**

#### 3. Relación entre Clientes y ventaProducto:

Un cliente puede comprar varios productos, pero una compra pertenece a un único cliente.

- **Relación: 1:N**

#### 4. Relación entre Productos y ventaProducto:

Un producto puede ser vendido varias veces, pero una venta específica pertenece a un único producto.

- **Relación: 1:N**

#### 5. Relación entre Clientes y Ventas:

Un cliente puede realizar varias ventas, pero una venta pertenece a un único cliente.

- **Relación: 1:N**

#### 6. Relación entre Ventas y ventaProductos:

Una venta puede incluir varios productos, pero un registro en ventaProducto pertenece a una única venta.

- **Relación: 1:N**

### Este proyecto refleja un modelo relacional eficiente y escalable para gestionar la información de una tienda de bicicletas.
