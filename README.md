Proyecto de Integración Curricular

Etapa 1 — Planeación del Software

Sistema de Gestión de Finanzas Personales (API-first)
Versión ampliada (sin IA) — con enfoque funcional avanzado y opción de despliegue para un público pequeño en un área geográfica limitada

1. Resumen ejecutivo

Este documento presenta la planeación completa del Sistema de Gestión de Finanzas Personales implementado como API-first (backend en Go) y con un frontend web/móvil opcional. El sistema no emplea IA: en su lugar incorpora funcionalidades completas y robustas —multicuenta, presupuestos, calendario financiero, OCR para facturas, facturación PDF, export/import, control de suscripciones, gestión de deudas, auditoría, sincronización offline— pensadas para ser desarrolladas en Go. Además incluye una estrategia de despliegue para un público pequeño dentro de un área geográfica reducida (ej. comunidad, pyme local, campus universitario).

2. Objetivos del sistema

Permitir a usuarios gestionar ingresos, egresos, transferencias, presupuestos y metas.

Soportar múltiples cuentas y múltiples monedas.

Automatizar tareas cotidianas (recordatorios, facturas PDF, OCR de facturas).

Proveer un API RESTful claro para conectar frontends web y móvil.

Ofrecer seguridad, auditoría y respaldo.

Ser desplegable localmente para una comunidad pequeña o negocio local (modo "área limitada").

3. Alcance funcional (módulos principales)

Módulo A — Autenticación y seguridad

Registro/login (email + contraseña).

OAuth2 (Google) opcional.

JWT para autenticación de API.

TOTP (2FA) o verificación por correo.

Roles: admin, usuario.

Módulo B — Cuentas y monedas

Crear/editar/eliminar cuentas (banco, tarjeta, efectivo).

Soporte multi-moneda por cuenta.

Conversión de moneda mediante llamada a API de tasas (opcional).

Módulo C — Transacciones

Registrar ingresos, gastos y transferencias internas.

Asociar categoría, etiqueta, cuenta y nota.

Marcar transacciones como recurrentes (sistema de recurrencia configurable).

Módulo D — Presupuestos

Crear presupuestos mensuales por categoría.

Seguimiento y alertas (umbral configurable).

Módulo E — Metas de ahorro

Crear metas (monto, fecha límite).

Simulación de plan de ahorro (sin IA: cálculo matemático determinista).

Visualización de progreso.

Módulo F — Suscripciones y pagos recurrentes

Registrar suscripciones (monto, frecuencia, próximo pago).

Cálculo de gasto anual por suscripciones.

Módulo G — Deudas y préstamos

Registrar préstamos recibidos/otorgados.

Registrar pagos parciales y calcular saldo.

Módulo H — Calendarización y recordatorios

Calendario con eventos financieros (vencimientos, sueldos).

Notificaciones por email o push (cuando aplique).

Módulo I — Import/Export y reportes

Importar CSV/Excel bancario (mapeo de columnas configurable).

Exportar transacciones a CSV, Excel y PDF.

Reportes: flujo de caja, por categorías, comparativo mensual/anual.

Módulo J — OCR de facturas (sin IA)

Subida de imagen/PDF, extracción con Tesseract OCR para campos: fecha, monto, NIT/cédula, proveedor.

Asistente de validación manual (usuario confirma/corrige los datos antes de guardar).

Módulo K — Generación de documentos

Generar facturas o comprobantes en PDF con gofpdf.

Opción: incluir código QR con link a comprobante/verificación.

Módulo L — Auditoría y backups

Registro de cambios (usuario, timestamp, acción).

Exportar backup en JSON/SQL.

Restauración básica desde backup.

Módulo M — Modo offline/Sync (para área limitada)

Frontend almacena localmente (IndexedDB / SQLite móvil).

Sincronización con la API cuando hay conectividad.

Resolución de conflictos simple: última modificación gana o estrategia por usuario/admin.
