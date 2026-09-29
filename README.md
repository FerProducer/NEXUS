# NEXUS ERP

ERP comercial responsive para ventas, clientes, crédito, inventario, compras, entregas, garantías y operación administrativa.

## Stack
- Next.js App Router + TypeScript
- PostgreSQL + Prisma ORM
- JWT HttpOnly cookie
- Zod para validación
- Tailwind CSS v4
- Arquitectura modular preparada para crecer

## Módulos incluidos
- Login y roles
- Clientes con número único
- Productos/SKU y stock
- Ventas contado/crédito
- Flujo de aprobación de crédito
- Referencias y aval
- Kardex de inventario
- Confirmación transaccional de ventas y descuento de existencias
- Panel de crédito
- Documentos imprimibles de venta y copia de cliente
- Pagaré como bloque documental pendiente de validación jurídica
- Auditoría de clientes

## Inicio local

Requisitos: Node 20+, PostgreSQL 14+.

```bash
cp .env.example .env
npm install
npx prisma db push
npm run db:seed
npm run dev
```

Abre `http://localhost:3000`.

Usuarios demo:
- admin@nexus.local / Admin123!
- ventas@nexus.local / Ventas123!
- credito@nexus.local / Credito123!

**Cambia estas credenciales y AUTH_SECRET antes de cualquier entorno real.**

## GitHub

```bash
git init
git add .
git commit -m "Initial Nexus ERP"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/nexus-erp.git
git push -u origin main
```

## Deploy recomendado

El repositorio puede desplegarse en Vercel/otro proveedor compatible con Next.js y usar PostgreSQL gestionado. Configura:

- DATABASE_URL
- AUTH_SECRET
- APP_URL

Luego ejecuta la migración de producción según tu flujo CI/CD:

```bash
npx prisma migrate deploy
```

## Producción: pendientes obligatorios antes de vender

1. Sustituir almacenamiento de referencias de documentos por object storage privado (S3/R2/etc.) con URLs firmadas.
2. Implementar MFA para administración/crédito.
3. Conectar almacenamiento privado de documentos (S3/R2) para identificación, ingresos y avales; la versión inicial usa referencias de expediente, no guarda archivos directamente.
4. Rate limiting y protección anti-abuso en autenticación/API.
5. Backups, restauración probada y observabilidad.
6. Firma electrónica y validación jurídica de contratos/pagarés.
7. Integración fiscal por país; para México, adaptar CFDI/PAC y catálogos fiscales vigentes.
8. Aviso de privacidad, consentimiento y políticas de conservación de datos revisadas por abogado.
9. Pruebas automatizadas unitarias/e2e y revisión de seguridad antes de producción.
10. Configuración de almacenamiento documental cifrado y control de acceso.
11. Separar tenant/organización con pruebas de aislamiento.

## Seguridad

Los datos de identificación, ingresos, domicilio y crédito son sensibles para el negocio. El sistema usa sesiones HttpOnly y RBAC; para producción deben añadirse controles de seguridad, almacenamiento documental privado, auditoría completa, MFA, backups y revisión legal.
