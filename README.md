<div align="center">
  <a href="#">
    <img src="http://res.cloudinary.com/dpp6gyfao/image/upload/v1765750496/u9qiibrn6hlrwexctjyg.svg" alt="Logo AgendIA" width="200">
  </a>

  <h1 style="margin-top: 20px;">AgendIA / Cyborg SaaS</h1>
  
  <p style="font-size: 1.2em;">
    <strong>El Primer Sistema Operativo Autónomo para Negocios de Servicios.</strong><br>
    Gestión de citas, clientes y crisis vía WhatsApp con Inteligencia Artificial Generativa.
  </p>

  <p>
    <a href="ARCHITECTURE.md"><strong>📐 Ingeniería</strong></a> •
    <a href="AI_WORKFLOW.md"><strong>🧠 Core IA</strong></a> •
    <a href="ROADMAP.md"><strong>🗺️ Roadmap</strong></a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Python-3.11+-blue.svg?style=for-the-badge&logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/Django-5.0-092E20.svg?style=for-the-badge&logo=django&logoColor=white" alt="Django">
    <img src="https://img.shields.io/badge/AI-LLaMA_3_&_Gemini-8A2BE2.svg?style=for-the-badge&logo=google-bard&logoColor=white" alt="AI Models">
    <img src="https://img.shields.io/badge/WhatsApp-Twilio_API-25D366.svg?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp">
    <img src="https://img.shields.io/badge/Architecture-Hexagonal-orange.svg?style=for-the-badge" alt="Architecture">
  </p>
</div>

---

## 🚀 La Propuesta de Valor

**AgendIA** (Codenamed _Cyborg_) nace para solucionar el problema de la "recepción desatendida". La mayoría de las PYMES de servicios (clínicas, barberías, talleres) pierden el 30% de sus oportunidades de venta por no poder atender el teléfono o WhatsApp al instante.

A diferencia de los chatbots tradicionales (rígidos y frustrantes), **AgendIA es un agente cognitivo**. Entiende el lenguaje natural, el contexto temporal ("mañana", "la semana que viene") y las reglas de negocio, actuando como un recepcionista humano experto disponible 24/7.

---

## 📚 Documentación Técnica (Deep Dives)

Hemos separado la documentación en tres pilares fundamentales para facilitar la auditoría técnica del sistema:

### 1. [📐 Ingeniería y Arquitectura](ARCHITECTURE.md)

Descubre cómo hemos construido un sistema modular basado en **Arquitectura Hexagonal (Ports & Adapters)**.

- **Contenido:** Diagramas de flujo de datos, desacoplamiento de proveedores, gestión de colas asíncronas (Celery/Redis) y seguridad Zero-Trust.

### 2. [🧠 El Cerebro: Workflow de IA](AI_WORKFLOW.md)

Una inmersión profunda en el **Orquestador Cognitivo**. Aquí explicamos la "magia" detrás del bot.

- **Contenido:** Cómo funciona el _Tool Calling_ (Function Calling), la inyección dinámica de contexto temporal y los mecanismos de defensa contra alucinaciones de los LLMs.

### 3. [🗺️ Roadmap y Futuro](ROADMAP.md)

El estado actual del proyecto y la visión a largo plazo.

- **Contenido:** Detalles de la Fase 1 (MVP actual), Fase 2 (CRM y Fidelización) y Fase 3 (Escalado SaaS Multitenant).

---

## 🔥 Funcionalidades Core

### 1. Recepción Autónoma vía WhatsApp

El sistema vive donde están los clientes: en WhatsApp. No requiere instalar apps ni recordar contraseñas.

- **Conversación Natural:** El cliente habla como quiere. _"Hola, ¿tienes hueco para un corte el viernes por la tarde?"_.
- **Gestión del Calendario:** La IA consulta la disponibilidad en tiempo real y ofrece huecos libres.
- **Reservas, Cambios y Cancelaciones:** Gestiona el ciclo de vida completo de la cita sin intervención humana.
- **Cold Start:** Si es un cliente nuevo, la IA sabe que debe preguntar su nombre antes de confirmar nada.

### 2. Panel de Control "Mission Control"

Una interfaz web reactiva (Django + TailwindCSS) para que el dueño del negocio supervise todo.

- **Calendario Drag & Drop:** Mover una cita con el ratón dispara automáticamente una notificación de WhatsApp al cliente informando del cambio.
- **Gestión de Equipo:** Configuración de horarios complejos, turnos partidos y especialidades por empleado.
- **Dashboard de KPIs:** Métricas en tiempo real de ocupación, ingresos estimados y captación de clientes.

### 3. Protocolo de Gestión de Crisis (Unique Selling Point)

¿Qué pasa si un empleado se pone enfermo un viernes por la mañana?

- **Detección:** El administrador marca una "Ausencia/Baja" en el sistema.
- **Cálculo:** El backend identifica inmediatamente todas las citas que entran en conflicto con esa ausencia.
- **Acción:** La IA genera mensajes personalizados disculpándose y contacta a cada cliente afectado para ofrecerle huecos alternativos con otros compañeros o en otros días.

---

## 📸 Galería del Sistema

<table border="0">
  <tr>
    <td width="50%" valign="top">
      <h3 align="center">El Cerebro (Logs de IA)</h3>
      <p align="center">Visualización de cómo la IA "piensa" y ejecuta herramientas (bloques verdes) antes de responder al usuario.</p>
      <img src="assets/screenshots/ai-logs-debugging.png" alt="Logs IA">
    </td>
    <td width="50%" valign="top">
      <h3 align="center">El Calendario</h3>
      <p align="center">Gestión visual. Soporta múltiples columnas (empleados), bloqueos visuales y estados de cita por colores.</p>
      <img src="assets/screenshots/calendar-drag-drop.png" alt="Calendario">
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3 align="center">Dashboard de Negocio</h3>
      <p align="center">Control financiero y operativo en un vistazo. Citas del día, ingresos y nuevos leads.</p>
      <img src="assets/screenshots/dashboard-kpis.png" alt="Dashboard">
    </td>
    <td width="50%" valign="top">
      <h3 align="center">Configuración Agnóstica</h3>
      <p align="center">Selector de proveedor de IA en caliente. Cambia de Groq a Gemini según la necesidad.</p>
      <img src="assets/screenshots/settings-providers.png" alt="Configuración">
    </td>
  </tr>
</table>

---

<div align="center">
  <h3>🔒 Nota de Privacidad</h3>
  <p>
    Este repositorio contiene exclusivamente documentación técnica y capturas de pantalla.<br>
    El código fuente es privado y propiedad intelectual de sus desarrolladores.
  </p>
  <p>
    ¿Interesado en el proyecto? <a href="mailto:tuemail@ejemplo.com">Contáctanos</a>
  </p>
  <br>
  <p>Copyright © 2025 AgendIA / Cyborg SaaS</p>
</div>
