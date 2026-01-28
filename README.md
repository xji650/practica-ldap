# 📘 README – Infraestructura LDAP con Docker y OpenLDAP

## Descripción general

Este proyecto despliega una **infraestructura LDAP completa** utilizando **Docker Compose**, basada en **OpenLDAP (osixia/openldap)** y **LDAP Account Manager (LAM)** como interfaz gráfica.

El objetivo es crear automáticamente una estructura LDAP con **usuarios y grupos**, y verificar su correcta creación mediante un cliente LDAP, sustituyendo un script Bash complejo por una solución **rápida, reproducible y mantenible**.

---

## Estructura LDAP

### Unidades organizativas (OU)

- ou=groups
- ou=users
- ou=system

Base DN:
```
dc=amsa,dc=udl,dc=cat
```

---



## Estructura Docker

Servicios definidos en `docker-compose.yml`:

- **ldap-server**: Servidor OpenLDAP
- **lam**: LDAP Account Manager (interfaz web)
- **ldap-client**: Cliente Ubuntu para pruebas

Incluye persistencia de datos y red Docker dedicada.

---

## Dockerfile

- Imagen base: `osixia/openldap:1.5.0`
- TLS/SSL automático
- Carga automática del fichero `bootstrap.ldif`
- Variables de entorno configuradas para el dominio y DN base

---

## Requisitos Previos

- Docker
- Docker Compose

Comprobación:
```bash
docker --version
docker-compose --version
```

---

## Ejecución

Desde la carpeta del proyecto:

```bash
docker-compose up -d --build
```

Esto construye la imagen, inicializa LDAP y carga usuarios y grupos automáticamente.

---

## Verificación

### Acceder al cliente LDAP

```bash
docker exec -it ldap-client bash
```

### Buscar a Jordi

```bash
ldapsearch -x -H ldap://ldap-server \
-b "dc=amsa,dc=udl,dc=cat" \
-D "cn=admin,dc=amsa,dc=udl,dc=cat" \
-w adminpassword "(uid=jordi)"
```

Resultado esperado:
- uidNumber: 4000

### Buscar a Manel

```bash
ldapsearch -x -H ldap://ldap-server \
-b "dc=amsa,dc=udl,dc=cat" \
-D "cn=admin,dc=amsa,dc=udl,dc=cat" \
-w adminpassword "(uid=manel)"
```

Resultado esperado:
- uidNumber: 4001

---

## 🌐 Acceso a LDAP Account Manager

URL:
```
http://localhost:8080
```

Credenciales:
- Usuario: admin
- Contraseña: adminpassword

---

