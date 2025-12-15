# 🏗️ Arquitectura del Sistema

AgendIA ha sido diseñado siguiendo principios de **Ingeniería de Software Moderna**, priorizando la modularidad, la escalabilidad y la seguridad en la gestión de datos. El sistema implementa una variación de **Arquitectura Hexagonal (Ports & Adapters)** para desacoplar la lógica de negocio de los proveedores externos (IA y Mensajería).

## 📐 Diagrama de Alto Nivel

El siguiente diagrama ilustra el flujo de datos desde que un usuario envía un mensaje hasta que se procesa una respuesta o acción.

```mermaid
graph TD
    User((Usuario Final)) -->|WhatsApp| Twilio[Gateway Twilio]
    Twilio -->|Webhook (POST)| API[API Gateway / DRF]

    subgraph "Core del Sistema (Backend)"
        API --> Orchestrator[Orquestador Cognitivo]

        Orchestrator -->|Inyección de Contexto| ContextBuilder[Context Builder]
        Orchestrator -->|Inferencia| AI_Adapter[Adaptador IA (Polimórfico)]

        AI_Adapter -.->|1. Groq / Llama 3| GroqCloud
        AI_Adapter -.->|2. Google Gemini| GoogleCloud
        AI_Adapter -.->|3. Modelos Locales| Ollama

        Orchestrator -->|Ejecución de Tools| Services[Capa de Servicios]

        Services -->|Atomic Transactions| DB[(PostgreSQL)]
        Services -->|Eventos Asíncronos| Celery[Cola de Tareas]
    end

    Celery -->|Procesamiento| Redis[Broker Redis]
    Services -->|Resultado Estructurado| Orchestrator
    Orchestrator -->|Respuesta Natural| Twilio
```

## 🧩 Componentes Principales

### 1. Capa de Infraestructura (Adapters)

Esta capa aísla al sistema de las herramientas externas. Permite cambiar proveedores tecnológicos sin modificar la lógica de negocio (Vendor Lock-in prevention).

- **AI Adapters:** Implementación del patrón _Strategy_. Permite cambiar "el cerebro" del sistema en tiempo real (ej. usar Groq para velocidad en saludos y Gemini Pro para razonamiento complejo en conflictos de agenda).
- **Messaging Adapter:** Encapsula la lógica de Twilio/WhatsApp, gestionando la normalización de números telefónicos y el manejo de Webhooks.

### 2. Capa de Aplicación (El Orquestador)

El `Orchestrator` actúa como el controlador principal del flujo conversacional. No contiene reglas de negocio, su función es puramente de coordinación:

1.  Recibe el input crudo.
2.  Construye un contexto enriquecido (Fecha actual, servicios disponibles, estado del cliente).
3.  Gestiona el historial de conversación.
4.  Decide si la respuesta de la IA requiere una acción en el sistema (Tool Call) o es puramente conversacional.

### 3. Capa de Dominio (Services)

Aquí reside la inteligencia de negocio y las reglas críticas. Es el único punto de acceso a la base de datos para operaciones de escritura.

- **AvailabilityService:** Motor matemático que calcula huecos libres. Considera:
  - Horarios laborales complejos (JSON).
  - Duración de servicios + Tiempos de buffer (limpieza/preparación).
  - Bloqueos por festivos (`BusinessHoliday`) o ausencias personales (`TimeOff`).
- **BookingService:** Gestiona la transaccionalidad de las reservas. Utiliza `transaction.atomic` para asegurar que nunca se generen dos citas en el mismo hueco (Race Conditions).
- **TimeOffService:** Gestiona las bajas del personal. Incluye un sistema de "Detección de Crisis" que identifica automáticamente citas afectadas por una nueva ausencia.

### 4. Arquitectura Asíncrona (Event-Driven)

Para operaciones que no requieren respuesta inmediata o son intensivas, utilizamos **Celery** con **Redis**:

- **Gestión de Crisis:** Si un empleado marca una baja médica, el sistema dispara un proceso en segundo plano que:
  1.  Identifica todos los clientes afectados.
  2.  Cancela las citas internamente.
  3.  Usa la IA para generar mensajes de disculpa personalizados y masivos.
- **Recordatorios:** Cronjobs diarios que notifican a los clientes sobre sus citas del día siguiente.

## 🔒 Seguridad y Protocolo "Zero-Trust"

El diseño asume que los Modelos de Lenguaje (LLMs) no son deterministas y pueden "alucinar". Por ello, implementamos un protocolo de seguridad estricto:

1.  **Read-Only por Defecto:** La IA no tiene permisos de escritura directa en la DB.
2.  **Validación de Tools:** Cualquier intento de la IA de ejecutar una acción (ej. `book_appointment`) es interceptado y validado por la Capa de Dominio. Si la IA inventa una fecha o un servicio que no existe, el sistema rechaza la operación y devuelve un error controlado.
3.  **Sanitización de Inputs:** Todos los datos provenientes de WhatsApp son limpiados y validados antes de procesarse.

---
