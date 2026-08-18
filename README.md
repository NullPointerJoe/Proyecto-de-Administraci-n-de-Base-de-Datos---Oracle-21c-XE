# Proyecto de Administración de Base de Datos - Oracle 21c XE

## Descripción

Este proyecto consiste en la implementación de una base de datos para una empresa ficticia dedicada a la venta mundial de hardware de computadoras utilizando **Oracle Database 21c Express Edition (XE)**.

Como parte del proyecto se implementan diferentes mecanismos de administración de bases de datos, incluyendo:

- Creación de una Pluggable Database (PDB).
- Administración de usuarios.
- Creación de perfiles de seguridad.
- Administración de Tablespaces.
- Implementación del esquema OT.
- Carga de datos.
- Gestión de privilegios.
- Políticas de contraseñas.
- Auditoría de operaciones sobre la base de datos.

---

# Objetivos

- Implementar una base de datos Oracle utilizando arquitectura Multitenant.
- Aplicar buenas prácticas de administración de usuarios y seguridad.
- Configurar perfiles con restricciones de acceso.
- Administrar el almacenamiento mediante Tablespaces.
- Implementar auditoría sobre operaciones críticas.
- Utilizar el esquema de ejemplo OT (Oracle Tutorial Sample Database).

---

# Tecnologías utilizadas

- Oracle Database 21c XE
- SQL*Plus
- Oracle Multitenant Architecture
- Oracle SQL
- PL/SQL

---

# Funcionalidades implementadas

## 1. Creación de la Pluggable Database (OTPDB)

Se crea una nueva PDB denominada **OTPDB** dentro del contenedor principal.

Funciones realizadas:

- Creación de la PDB.
- Apertura de la base.
- Verificación del estado.

---

## 2. Creación del usuario OT

Se crea el usuario encargado de almacenar toda la información del sistema.

Características:

- Usuario: OT
- Privilegios:
  - CONNECT
  - RESOURCE

---

## 3. Creación del perfil APP

Se implementa un perfil de seguridad para el usuario OT.

Restricciones:

| Parámetro | Valor |
|-----------|-------|
| Sesiones simultáneas | 2 |
| Intentos fallidos | 5 |
| Tiempo de inactividad | 10 minutos |

---

## 4. Creación del Tablespace OTTBS

Se crea un Tablespace dedicado para almacenar todos los objetos del usuario OT.

Características:

- Tamaño inicial: 100 MB
- Autoextend habilitado
- Crecimiento automático de 5 MB
- Sin límite máximo

Además se establece como Tablespace predeterminado del usuario OT.

---

## 5. Implementación del esquema OT

Se ejecuta el archivo:

```

ot_schema.sql

```

Este script crea todas las tablas necesarias para la empresa ficticia.

---

## 6. Carga de datos

Se ejecuta:

```

ot_data.sql

```

El script inserta la información inicial del sistema.

---

## 7. Creación del usuario OT_USR

Se crea un usuario destinado a consultar y manipular la información almacenada.

Características:

- Contraseña expirada.
- Cambio obligatorio en el primer inicio de sesión.
- Permisos:

  - SELECT
  - INSERT
  - UPDATE
  - CREATE SESSION

---

## 8. Configuración del Tablespace para OT_USR

El usuario OT_USR utiliza igualmente el Tablespace:

```

OTTBS

```

como almacenamiento predeterminado.

---

## 9. Creación del perfil USUARIO

Se implementa un perfil de seguridad más estricto para OT_USR.

### Restricciones

| Parámetro | Valor |
|------------|-------|
| Sesiones | 10 |
| Intentos fallidos | 3 |
| Tiempo de conexión | 15 minutos |
| Vigencia de contraseña | 10 días |

Además se desarrolla una función PL/SQL que valida que las contraseñas cumplan:

- Mínimo 8 caracteres.
- Al menos una letra mayúscula.
- Al menos un número.

---

## 10. Auditoría

Se configura auditoría sobre la tabla:

```

OT.CONTACTS

```

Eventos auditados:

- SELECT
- INSERT
- UPDATE
- DELETE

Posteriormente se verifican los registros mediante la vista:

```

DBA_AUDIT_TRAIL

```

---

# Seguridad implementada

- Perfiles de usuarios.
- Restricción de sesiones.
- Bloqueo por intentos fallidos.
- Expiración automática de contraseñas.
- Validación personalizada de contraseñas.
- Administración mediante Tablespaces.
- Auditoría de operaciones DML.

---

# Competencias aplicadas

Durante el desarrollo del proyecto se utilizaron conocimientos sobre:

- Administración de Oracle Database.
- Arquitectura Multitenant.
- SQL.
- PL/SQL.
- Gestión de usuarios.
- Gestión de privilegios.
- Seguridad en bases de datos.
- Auditoría.
- Administración de almacenamiento.

---

# Requisitos

- Oracle Database 21c XE
- SQL*Plus
- Scripts:

```

ot_schema.sql
ot_data.sql

```

---

# Ejecución

1. Crear la PDB **OTPDB**.
2. Crear el usuario **OT**.
3. Crear el perfil **APP**.
4. Crear el Tablespace **OTTBS**.
5. Ejecutar **ot_schema.sql**.
6. Ejecutar **ot_data.sql**.
7. Crear el usuario **OT_USR**.
8. Configurar el perfil **USUARIO**.
9. Configurar la auditoría.
10. Verificar los registros generados.

---

# Resultados

El proyecto permite administrar una base de datos Oracle aplicando políticas de seguridad, administración de almacenamiento, control de acceso y auditoría, simulando un entorno empresarial para una compañía dedicada a la comercialización de hardware.
