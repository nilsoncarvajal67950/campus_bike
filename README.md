# campus_bike 🚲🚴‍♀️

# CÓDIGO 💻

```sql
CREATE DATABASE Campus_bike;
USE Campus_bike;

CREATE TABLE Pais (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100)
);

CREATE TABLE Region (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  idPais_fk INT,
  CONSTRAINT FK_PaisRegion FOREIGN KEY (idPais_fk) REFERENCES Pais(id)
);

CREATE TABLE Ciudad (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  idRegion_fk INT,
  CONSTRAINT FK_RegionCiudad FOREIGN KEY (idRegion_fk) REFERENCES Region(id)
);

CREATE TABLE Sucursal (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Direccion VARCHAR(100),
  idCiudad_fk INT,
  CONSTRAINT FK_CiudadSucursal FOREIGN KEY (idCiudad_fk) REFERENCES Ciudad(id)
);

CREATE TABLE TotalVentas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Total DECIMAL(10,2),
  Fecha DATE,
  idSucursal_fk INT,
  CONSTRAINT FK_SucursalTotalVentas FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE SectorVentas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  idSucursal_fk INT,
  CONSTRAINT FK_SucursalSectorVentas FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE Empleado (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Cargo VARCHAR(50),
  Telefono VARCHAR(13),
  Email VARCHAR(100),
  idSucursal_fk INT,
  CONSTRAINT FK_SucursalEmpleado FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE Proveedor (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Telefono VARCHAR(13),
  Direccion VARCHAR(255),
  Email VARCHAR(100),
  idPais_fk INT,
  CONSTRAINT FK_PaisProveedor FOREIGN KEY (idPais_fk) REFERENCES Pais(id)
);

CREATE TABLE Repuesto (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Precio DECIMAL(10,2),
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorRepuesto FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE CuentaSaldar (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Monto DECIMAL(10,2),
  FechaVencimiento DATE,
  Estado VARCHAR(50),
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorCuentaSaldar FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE Producto (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Categoria VARCHAR(100),
  Precio DECIMAL(10,2),
  Stock INT,
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorProducto FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE Bicicleta (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Marca VARCHAR(100),
  Tipo VARCHAR(50),
  Valor DECIMAL(10,2),
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorBicicleta FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE Stock (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Cantidad INT,
  idProducto_fk INT,
  idSucursal_fk INT,
  CONSTRAINT FK_ProductoStock FOREIGN KEY (idProducto_fk) REFERENCES Producto(id),
  CONSTRAINT FK_SucursalStock FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE Estado (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Transito VARCHAR(30),
  Entrega VARCHAR(30),
  Entregado VARCHAR(30),
  idProducto_fk INT,
  CONSTRAINT FK_ProductoEstado FOREIGN KEY (idProducto_fk) REFERENCES Producto(id)
);

CREATE TABLE Cliente (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Direccion VARCHAR(50),
  Telefono VARCHAR(13),
  Email VARCHAR(150),
  idPais_fk INT,
  CONSTRAINT FK_PaisCliente FOREIGN KEY (idPais_fk) REFERENCES Pais(id)
);

CREATE TABLE Pedido (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Cantidad INT,
  Fecha DATE,
  idEstado_fk INT,
  idCliente_fk INT,
  idProducto_fk INT,
  CONSTRAINT FK_EstadoPedido FOREIGN KEY (idEstado_fk) REFERENCES Estado(id),
  CONSTRAINT FK_ClientePedido FOREIGN KEY (idCliente_fk) REFERENCES Cliente(id),
  CONSTRAINT FK_ProductoPedido FOREIGN KEY (idProducto_fk) REFERENCES Producto(id)
);

CREATE TABLE Fecha (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  Descripcion VARCHAR(50)
);

CREATE TABLE Venta (
  id INT AUTO_INCREMENT PRIMARY KEY,
  idFecha_fk INT,
  Cantidad INT,
  Total DECIMAL(20,2),
  idCliente_fk INT,
  idBicicleta_fk INT,
  idEmpleado_fk INT,
  CONSTRAINT FK_FechaVenta FOREIGN KEY (idFecha_fk) REFERENCES Fecha(id),
  CONSTRAINT FK_ClienteVenta FOREIGN KEY (idCliente_fk) REFERENCES Cliente(id),
  CONSTRAINT FK_EmpleadoVenta FOREIGN KEY (idEmpleado_fk) REFERENCES Empleado(id)
);

CREATE TABLE Pago (
  id INT AUTO_INCREMENT PRIMARY KEY,
  TipoPago VARCHAR(50),
  Monto DECIMAL(20,2),
  Fecha DATE,
  idVenta_fk INT,
  CONSTRAINT FK_VentaPago FOREIGN KEY (idVenta_fk) REFERENCES Venta(id)
);

CREATE TABLE Facturacion (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Total DECIMAL(20,2),
  idVenta_fk INT,
  CONSTRAINT FK_VentaFacturacion FOREIGN KEY (idVenta_fk) REFERENCES Venta(id)
);
```
