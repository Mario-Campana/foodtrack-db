# foodtrack-db
Homework Henry - Módulo 2

# 🚚 FoodTrack DB

Base de datos relacional para la gestión de operaciones de foodtrucks en distintos puntos de una ciudad. Desarrollada en **Microsoft SQL Server**, gestionada con **DBeaver** y versionada con **Git/GitHub**.

---

## 📋 Descripción del proyecto

FoodTrack es una plataforma que permite administrar:

- **Foodtrucks**: información de cada unidad operativa.
- **Productos**: menú disponible por foodtruck.
- **Ubicaciones**: puntos de la ciudad donde operan los foodtrucks.
- **Pedidos**: registro de órdenes realizadas.
- **Detalle de pedidos**: ítems individuales de cada orden.

El objetivo es simular un entorno de desarrollo profesional, aplicando modelado relacional, control de versiones y buenas prácticas desde el inicio del proyecto.

---

## 🗂️ Estructura del repositorio

```
foodtrack-db/
│
├── /scripts/          # Scripts SQL del esquema (DDL y modificaciones)
│   ├── 01_create_tables.sql
│   ├── 02_relationships.sql
│   └── 03_alter_tables.sql
│
├── /data/             # Archivos CSV con los datos fuente
│   ├── foodtrucks.csv
│   ├── products.csv
│   ├── orders.csv
│   ├── order_items.csv
│   └── locations.csv
│
└── README.md          # Documentación general del proyecto
```

---

## 🧩 Modelo relacional

### Tablas

| Tabla         | Descripción                                      |
|---------------|--------------------------------------------------|
| `foodtrucks`  | Datos de cada foodtruck (nombre, propietario, etc.) |
| `products`    | Productos disponibles asociados a cada foodtruck |
| `locations`   | Ubicaciones de la ciudad donde operan            |
| `orders`      | Pedidos realizados por los clientes              |
| `order_items` | Detalle de productos por pedido                  |

### Relaciones principales

- Un **foodtruck** puede tener muchos **productos**.
- Un **foodtruck** puede operar en muchas **ubicaciones**.
- Un **pedido** pertenece a un **foodtruck** y una **ubicación**.
- Un **pedido** tiene muchos **ítems** (`order_items`), cada uno asociado a un **producto**.

### Diagrama ER (simplificado)

```
foodtrucks ─────< products
     │
     └─────< orders >─────< order_items >───── products
                │
           locations
```

---

## ⚙️ Tecnologías utilizadas

- **Microsoft SQL Server** — motor de base de datos
- **DBeaver** — cliente SQL para diseño y ejecución de scripts
- **Git / GitHub** — control de versiones

---

## 🚀 Cómo ejecutar los scripts

1. Cloná el repositorio:
   ```bash
   git clone https://github.com/Mario-Campana/foodtrack-db.git
   cd foodtrack-db
   ```

2. Abrí **DBeaver** y conectate a tu instancia de SQL Server.

3. Ejecutá los scripts en orden desde la carpeta `/scripts/`:
   ```
   01_create_tables.sql   → Crea las tablas con PKs y restricciones
   02_relationships.sql   → Agrega las claves foráneas
   03_alter_tables.sql    → Modificaciones estructurales posteriores
   ```

---

## 📦 Carga de datos (opcional)

### Opción 1 — Importación desde SSMS

Usar el asistente de importación de **SQL Server Management Studio** con los archivos `.csv` de la carpeta `/data/`.

### Opción 2 — BULK INSERT

```sql
BULK INSERT dbo.foodtrucks
FROM 'C:\ruta\data\foodtrucks.csv'
WITH (
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '\n',
    FIRSTROW = 2
);
```

### Opción 3 — Script Python (`cargar_datos.py`)

```bash
pip install pyodbc
python cargar_datos.py
```

> El script se conecta a SQL Server via `pyodbc`, carga los datos programáticamente y registra errores de inserción en la tabla auxiliar `failed_orders`.

---

## 📌 Convención de commits

```
feat: crear tablas base del esquema
feat: agregar claves foráneas y restricciones
alter: agregar columna comentarios en orders
fix: corregir tipo de dato en products.precio
docs: actualizar README con diagrama ER
```

---

## 👤 Autor

**Mario Campana**  
[github.com/Mario-Campana](https://github.com/Mario-Campana)
