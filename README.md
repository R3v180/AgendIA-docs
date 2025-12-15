# 🤖 AgendIA: SaaS de Gestión de Citas con IA (WhatsApp Native)

> **Nota:** Este repositorio contiene la documentación técnica y roadmap del proyecto. El código fuente es privado (Propietario).

**AgendIA** es una plataforma SaaS diseñada para automatizar la gestión de reservas mediante Inteligencia Artificial Generativa. No es un simple chatbot: es un **agente autónomo** capaz de entender el calendario, negociar huecos, gestionar cancelaciones y manejar situaciones complejas (como bajas de personal) en tiempo real a través de WhatsApp.

## 📸 Vistazo Rápido

### 🧠 El Cerebro: IA Transparente

El sistema utiliza un orquestador que decide qué herramientas usar. A diferencia de otros bots, AgendIA no "alucina" horas; consulta la base de datos en tiempo real.
![Logs de IA](assets/screenshots/ai-logs-debugging.png)
_Panel de auditoría donde se ve cómo la IA ejecuta la tool `check_availability` y `book_appointment`._

### 📅 Calendario Interactivo

Panel administrativo para el negocio. Soporta **Drag & Drop**, múltiples empleados y bloqueos visuales.
![Calendario](assets/screenshots/calendar-drag-drop.png)

### 📊 Dashboard de Negocio

Control total de KPIs, ingresos estimados y flujo de clientes.
![Dashboard](assets/screenshots/dashboard-kpis.png)

## 🛠️ Stack Tecnológico

El núcleo está construido sobre una arquitectura robusta y escalable:

- **Backend:** Python / Django 5.0
- **API:** Django Rest Framework (DRF)
- **Asincronía:** Celery + Redis (para recordatorios y gestión de crisis en segundo plano).
- **Base de Datos:** PostgreSQL.
- **Frontend:** TailwindCSS + JavaScript (Server Side Rendering).
- **IA Core:** Arquitectura de adaptadores agnóstica:
  - Soporte actual: **Google Gemini 3 Pro**, **Groq (Llama 3)**, **SambaNova**.
  - Capacidad de _Tool Calling_ y razonamiento recursivo.

## ✨ Funcionalidades Clave (Technical Highlights)

1.  **Protocolo Zero-Trust:** La IA nunca escribe directamente en la base de datos. Solicita acciones al Backend, el cual valida reglas de negocio (horarios, festivos, bloqueos) y devuelve éxito o error.
2.  **Gestión de Crisis Automática:** Si un empleado se pone enfermo, el sistema detecta los conflictos, bloquea la agenda y la IA contacta proactivamente a los clientes afectados para reagendar.
3.  **Multitenancy:** Diseño preparado para SaaS, donde cada negocio tiene su configuración de tono de IA, horarios y servicios aislados.
4.  **Simulador Integrado:** Entorno de pruebas ("sandbox") para testear prompts sin coste de mensajería real.

## 🗺️ Roadmap Público

### ✅ Fase 1: Core & MVP (Completado)

- [x] Motor de IA con persistencia de contexto.
- [x] Integración WhatsApp (Twilio).
- [x] Calendario Drag & Drop con validación en tiempo real.
- [x] Sistema de Logs y Auditoría de IA.

### 🚧 Fase 2: Fidelización & CRM (En Desarrollo)

- [ ] Sistema de Puntos y Recompensas.
- [ ] Campañas de Marketing automatizadas por IA (Recuperación de clientes).
- [ ] Panel de métricas avanzado (LTV, Churn).

### 🚀 Fase 3: Expansión

- [ ] App Móvil Nativa (PWA).
- [ ] Integración de Pagos (Stripe) para reservas.
- [ ] Voice AI (Agendar por llamadas de voz).

---

_Desarrollado por [Tu Nombre/Empresa]_
