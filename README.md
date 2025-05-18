# Taller-practico

Parte 1: Replicación del Diagrama MER

![Imagen de WhatsApp 2025-05-17 a las 20 47 39_2189eca8](https://github.com/user-attachments/assets/eba95e1f-f3ad-4441-afc7-f295598652b6)

 Parte 2: Generación del Script DDL

 CREATE DATABASE IF NOT EXISTS TiendaDB;
USE TiendaDB;

-- Tabla cliente
CREATE TABLE cliente (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(45) NOT NULL,
    apellido VARCHAR(45) NOT NULL,
    email VARCHAR(45) UNIQUE NOT NULL,
    telefono VARCHAR(20),
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabla empleado
CREATE TABLE empleado (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(45) NOT NULL,
    apellido VARCHAR(45) NOT NULL,
    cargo VARCHAR(45),
    salario DOUBLE,
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabla categoria
CREATE TABLE categoria (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(45) NOT NULL,
    descripcion VARCHAR(45),
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Tabla producto
CREATE TABLE producto (
    id INT AUTO_INCREMENT PRIMARY KEY,
    categoria_id INT,
    nombre VARCHAR(45) NOT NULL,
    precio DOUBLE NOT NULL,
    cantidad INT DEFAULT 0,
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (categoria_id) REFERENCES categoria(id)
);

-- Tabla detalle_venta
CREATE TABLE detalle_venta (
    id INT AUTO_INCREMENT PRIMARY KEY,
    producto_id INT,
    cantidad INT NOT NULL,
    precio_unitario DOUBLE NOT NULL,
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (producto_id) REFERENCES producto(id)
);

-- Tabla venta
CREATE TABLE venta (
    id INT AUTO_INCREMENT PRIMARY KEY,
    detalle_venta_id INT,
    cliente_id INT,
    empleado_id INT,
    num_venta VARCHAR(45) NOT NULL,
    metodo_pago VARCHAR(45),
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (detalle_venta_id) REFERENCES detalle_venta(id),
    FOREIGN KEY (cliente_id) REFERENCES cliente(id),
    FOREIGN KEY (empleado_id) REFERENCES empleado(id)
);

-- Índices sugeridos para mejorar rendimiento en búsquedas frecuentes
CREATE INDEX idx_cliente_email ON cliente(email);
CREATE INDEX idx_producto_nombre ON producto(nombre);
CREATE INDEX idx_venta_num ON venta(num_venta);

Parte 3: Versionamiento en GitHub

Estructura del Repositorio IS-DB-Implementation

IS-DB-Implementation/
│
├── README.md
├── model/
│   └── modelo.mwb
├── scripts/
│   └── TuApellido_DDL_DB.sql
├── docs/
│   ├── diagrama_original.png
│   ├── diagrama_implementado.png
│   └── decisiones.md

README.md 

# IS-DB-Implementation

Este proyecto contiene la implementación de una base de datos relacional para una tienda comercial, utilizando MySQL Workbench y DDL. Se incluyen el modelo, scripts de creación, documentación y evidencia visual.

## Estructura
- `/model`: Archivo del modelo MER en formato .mwb
- `/scripts`: Script DDL SQL
- `/docs`: Capturas de pantalla y documentación

decisiones.md

# Decisiones de Implementación

- Se utilizaron claves foráneas explícitas para mantener integridad referencial.
- Se agregaron timestamps automáticos para facilitar trazabilidad.
- Se añadieron índices para campos comúnmente buscados como `email` y `num_venta`.
- Se aplicaron tipos de datos adecuados para asegurar precisión (ej. DOUBLE para precios y salarios).
