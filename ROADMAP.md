# 🗺️ Roadmap de Desarrollo

Este documento detalla el estado actual del proyecto, las funcionalidades completadas y la hoja de ruta técnica para las próximas versiones de **AgendIA**.

> **Estado Actual:** `v1.0-beta` (MVP Estable)
> **Última Actualización:** Diciembre 2025

---

## ✅ Fase 1: Core & Infraestructura (Completado)

_El objetivo de esta fase fue construir un núcleo robusto, seguro y capaz de gestionar el ciclo de vida completo de una cita sin intervención humana._

### 🧠 Motor de IA & Orquestación

- [x] **Arquitectura de Agentes:** Implementación del patrón de orquestación para separar lógica de conversación y ejecución de herramientas.
- [x] **Tool Calling Seguro:** Desarrollo de herramientas de lectura (`check_availability`) y escritura (`book`, `cancel`) con validación estricta en backend.
- [x] **Adaptadores Multi-Modelo:** Soporte intercambiable para **Llama 3 (Groq/SambaNova)** para velocidad y **Gemini 3 Pro** para razonamiento complejo.
- [x] **Persistencia de Contexto:** Historial de chat almacenado en base de datos relacional para mantener el hilo de la conversación.

### 📅 Gestión de Agenda (Backend & Frontend)

- [x] **Motor de Disponibilidad:** Algoritmo matemático que calcula huecos libres considerando horarios JSON complejos, buffers de limpieza y solapamientos.
- [x] **Panel Administrativo (UI):** Interfaz reactiva con TailwindCSS.
- [x] **Drag & Drop:** Funcionalidad JavaScript para mover citas visualmente, disparando notificaciones automáticas de cambio vía WhatsApp.
- [x] **Gestión de Ausencias (Crisis Mode):** Sistema que permite marcar bajas/vacaciones y automáticamente detecta conflictos, cancela citas y notifica a los clientes afectados.

### 🔌 Conectividad

- [x] **Integración WhatsApp:** Webhooks seguros vía Twilio.
- [x] **Sistema de Logs:** Auditoría técnica (`raw_json`) de cada decisión tomada por la IA.

---

## 🚧 Fase 2: CRM & Fidelización (En Desarrollo - Q1 2026)

_El foco cambia de la "gestión operativa" a la "retención de clientes" y el aumento del valor de vida del cliente (LTV)._

### 💎 Sistema de Lealtad (Loyalty Engine)

- [ ] **Billetera de Puntos:** Modelado de datos para transacciones de puntos (ganancia por servicio / canje por regalos).
- [ ] **Catálogo de Recompensas:** Interfaz administrativa para definir premios.
- [ ] **IA Vendedora:** Actualización del prompt del sistema para que la IA pueda consultar el saldo de puntos del cliente y sugerir canjes proactivamente en el chat.

### 📢 Marketing Reactivo (Automation)

- [ ] **Recuperación de Clientes:** Tareas programadas (Celery Beat) que detectan clientes inactivos (> X meses) y generan mensajes personalizados mediante IA para invitarlos a volver.
- [ ] **Recordatorios de Cumpleaños:** Trigger automático para felicitaciones y ofertas especiales.

### 📱 Portal del Cliente (Client-Facing App)

- [ ] **Magic Links:** Acceso sin contraseña (vía token JWT en WhatsApp) a un portal web personal.
- [ ] **Dashboard Cliente:** Visualización de historial de citas y saldo de puntos.

---

## 🚀 Fase 3: Escala SaaS & Monetización (Q2-Q3 2026)

_Preparación de la arquitectura para soportar múltiples negocios de forma aislada y segura._

### 🏢 Arquitectura Multi-Tenant

- [ ] **Aislamiento de Datos:** Refactorización de ORM para asegurar que todas las consultas filtren estrictamente por `business_id` (Middleware de Tenant).
- [ ] **Configuración Dinámica:** Panel para que cada negocio configure sus propias API Keys (Twilio/Groq) y personalice el branding (Logo/Colores) sin despliegue de código.

### 💳 Finanzas

- [ ] **Pagos Previos (Stripe):** Integración para solicitar depósitos/señales antes de confirmar una cita vía WhatsApp.
- [ ] **Suscripción SaaS:** Gestión de licencias y facturación recurrente para los negocios que usan el software.

### 🎙️ Voice AI (I+D)

- [ ] **Integración STT/TTS:** Implementación de modelos Whisper (OpenAI) para permitir que los usuarios envíen notas de voz por WhatsApp y la IA las transcriba y procese como texto.

---

## 🛠️ Deuda Técnica & Mejora Continua

- **Testing:** Aumentar cobertura de tests unitarios (Pytest) especialmente en el `AvailabilityService`.
- **CI/CD:** Pipelines de GitHub Actions para despliegue automático en producción.
- **Monitoring:** Integración con Sentry para trazas de errores en tiempo real.
