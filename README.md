#  PROYECTO CLEVER IDEAS - SISTEMA DE LLAMADAS AUTOMÁTICAS CON IA
## Documentación Técnica Completa para Entrega de Proyecto

---

##  RESUMEN EJECUTIVO

### Descripción del Proyecto
Este proyecto implementa un **sistema completo de llamadas automáticas** que integra múltiples tecnologías de IA para generar leads y agendar demos de manera completamente automatizada. El sistema detecta el idioma del prospecto, realiza investigación automática de la empresa, y ejecuta llamadas personalizadas con agentes virtuales especializados.

### Tecnologías Principales
- **n8n**: Orquestación de workflows y automatización
- **VAPI**: Plataforma de llamadas con IA 
- **OpenAI GPT-4o**: Procesamiento de lenguaje natural
- **ElevenLabs**: Síntesis de voz natural
- **Deepgram**: Transcripción de audio
- **Langfuse**: Observabilidad y analytics

### Componentes del Sistema
1. **Formulario Web Bilingüe** (español/inglés)
2. **Workflow n8n** con detección de idioma
3. **Squad de Agentes Virtuales** (Diego + Natalia)
4. **Sistema de Herramientas Personalizadas**
5. **Dashboard de Analytics y Monitoreo**

---

## 📁 ESTRUCTURA DE DOCUMENTACIÓN

### Documentos Principales

#### 1.  [DOCUMENTACION_TECNICA_SISTEMA_CLEVER_VAPI.md](./DOCUMENTACION_TECNICA_SISTEMA_CLEVER_VAPI.md)
**Documento principal del sistema**
- Arquitectura completa del sistema
- Configuración detallada de agentes virtuales (Diego y Natalia)
- Integraciones con APIs (VAPI, OpenAI, ElevenLabs, Deepgram)
- Configuración de voz y audio
- Sistema de monitoreo con Langfuse
- Manual de despliegue completo
- Troubleshooting y mantenimiento

#### 2.  [DOCUMENTACION_FORMULARIO_WEB.md](./DOCUMENTACION_FORMULARIO_WEB.md) 
**Frontend y captura de leads**
- Arquitectura del formulario HTML/CSS/JavaScript
- Sistema de validaciones en tiempo real
- Detección automática de idioma (ES/EN)
- Integración con webhook de n8n
- Configuración visual y animaciones
- Funcionalidades avanzadas y responsive design

#### 3.  [DOCUMENTACION_HERRAMIENTAS_FUNCIONES.md](./DOCUMENTACION_HERRAMIENTAS_FUNCIONES.md)
**Tools y webhooks personalizados**
- Herramientas de Diego (send_follow_up_info, endCall)
- Herramientas de Natalia (schedule_demo, validate_email, send_confirmation, endCall)
- Esquemas de datos y validaciones
- Manejo de errores y recuperación
- Métricas y monitoreo de herramientas

#### 4.  [Archivos de Configuración]
- `clever_agent.json` - Configuración de agentes para VAPI
- `index.html` - Formulario web completo con funcionalidades
- `[CLEVER] Agent-Web Call_Outbound.json` - Workflow de n8n
- `sofia_whatsapp*.json` - Archivos adicionales del sistema

---

##  FLUJO COMPLETO DEL SISTEMA

### 1. Captura de Lead (Formulario Web)
```
Usuario llena formulario → Validaciones en tiempo real → Detección de idioma → Envío a webhook
```

### 2. Procesamiento en n8n
```
Webhook recibe datos → Detector de idioma → Investigación IA de empresa → Configuración de datos → Llamada VAPI
```

### 3. Conversación con Agentes IA
```
Diego (Discovery) → Genera interés → Transfiere a → Natalia (Scheduling) → Agenda demo → Confirmación
```

### 4. Seguimiento y Analytics
```
Langfuse registra métricas → Dashboard de performance → Reportes de conversión
```

---

##  ARQUITECTURA TÉCNICA

### Diagrama de Flujo Principal
```
🌐 Formulario Web (ES/EN)
    ↓
📡 Webhook n8n (form-web)
    ↓
🔍 Detector de Idioma
    ↓
🤖 Investigación IA (OpenAI)
    ↓
⚙️ Configuración de Datos
    ↓
📞 VAPI Call API
    ↓
👨‍💼 Squad Diego-Natalia
    ↓
🎵 ElevenLabs (Voz) + 🎤 Deepgram (Transcripción)
    ↓
📊 Langfuse (Analytics)
```

### Componentes Clave

#### Agente Diego - Discovery Specialist
- **Personalidad**: Profesional, cálido, entusiasta, consultivo
- **Objetivo**: Discovery de necesidades → Despertar interés → Transferir
- **Herramientas**: send_follow_up_info, endCall
- **Duración máxima**: 30 minutos (1800 segundos)

#### Agente Natalia - Scheduling Specialist  
- **Personalidad**: Organizada, amable, eficiente, detallista
- **Objetivo**: Recopilar información → Agendar demo → Confirmar
- **Herramientas**: schedule_demo_appointment, validate_email_format, send_demo_confirmation, endCall
- **Duración máxima**: 15 minutos (900 segundos)

---

##  CONFIGURACIÓN Y DESPLIEGUE

### Prerrequisitos del Sistema
```bash
# APIs requeridas
VAPI_API_KEY=a6e56ec9-20e9-4b6f-aae1-8.........
OPENAI_API_KEY=sk-...
ELEVENLABS_API_KEY=...
DEEPGRAM_API_KEY=...
LANGFUSE_PUBLIC_KEY=...

# Infraestructura
n8n_instance=workflows.cleverideas.com.mx
webhook_url=https://workflows.cleverideas.com.mx/webhook/form-web
```

### URLs Principales
- **Formulario**: https://demoai.cleverideas.com.mx/
- **Webhook Principal**: https://workflows.cleverideas.com.mx/webhook/form-web
- **Herramientas**: https://workflows.cleverideas.com.mx/webhook/agent-web-tools
- **End-of-Call**: https://workflows.cleverideas.com.mx/webhook/web_agent_endcall

### Números Telefónicos VAPI
- **Español**: 6d8a5395-4aab-4546-9014-fb8cdc2a6512
- **Inglés**: 6d8a5395-4aab-4546-9014-fb8cdc2a6512

---

##  MÉTRICAS Y KPIs

### Métricas de Performance
- **Form Completion Rate**: % de formularios completados vs iniciados
- **Call Success Rate**: % de llamadas conectadas exitosamente
- **Discovery to Demo Rate**: % de transferencias Diego → Natalia
- **Demo Booking Rate**: % de demos agendadas exitosamente
- **Voice Quality Score**: Latencia y claridad de audio
- **Transcription Accuracy**: Precisión de Deepgram

### Analytics Disponibles
- **Langfuse Dashboard**: Traces completos de conversaciones
- **Call Duration**: Duración promedio por agente
- **Transfer Success**: Éxito en transferencias entre agentes
- **Tool Execution**: Performance de herramientas personalizadas
- **Error Tracking**: Monitoreo de errores y recuperación

---

##  SEGURIDAD Y COMPLIANCE

### Medidas de Seguridad
- **API Keys**: Almacenadas de forma segura en variables de entorno
- **Webhook Security**: Validación de origen y payload
- **Data Encryption**: Datos sensibles encriptados en tránsito
- **Access Control**: Acceso restringido a configuraciones

### Manejo de Datos Personales
- **Captcha**: Validación anti-bot en formulario
- **Email Validation**: Verificación de formato y dominio
- **Phone Validation**: Formato internacional requerido
- **Data Retention**: Políticas de retención de datos de llamadas

---

##  FUNCIONALIDADES DESTACADAS

### Inteligencia Artificial Avanzada
- **Detección de Idioma**: Automática según formulario
- **Investigación de Empresa**: IA busca información contextual
- **Conversación Natural**: GPT-4o con prompts especializados
- **Adaptación de Personalidad**: Diferentes estilos según género detectado

### Experiencia de Usuario
- **Formulario Bilingüe**: Cambio dinámico ES/EN
- **Validación en Tiempo Real**: Feedback visual inmediato
- **Animaciones**: Efectos visuales y cursor personalizado
- **Responsive Design**: Adaptable a móviles y tablets

### Automatización Completa
- **Workflow Sin Intervención**: Desde formulario hasta demo agendada
- **Transferencia Inteligente**: Entre agentes según contexto
- **Confirmaciones Automáticas**: Email + SMS para demos
- **Seguimiento**: Analytics automático de cada interacción

---

##  CASOS DE USO PRINCIPALES

### 1. Lead Qualification Automático
- Prospecto llena formulario → Diego califica necesidades → Transferencia a Natalia

### 2. Demo Scheduling 24/7
- Disponibilidad completa → Validación de datos → Agenda automática

### 3. Seguimiento Inteligente
- Información personalizada → Email/SMS automático → CRM integration

### 4. Multi-idioma Support
- Español nativo → Inglés nativo → Detección automática

---

##  MANTENIMIENTO Y SOPORTE

### Monitoreo Regular
```bash
# Verificar status de n8n
curl -X GET "http://workflows.cleverideas.com.mx/healthz"

# Verificar VAPI calls
curl -X GET "https://api.vapi.ai/call" -H "Authorization: Bearer $VAPI_API_KEY"

# Verificar Langfuse traces
https://langfuse.com/project/clever-ideas/traces
```

### Backup y Recuperación
```bash
# Backup workflow n8n
curl -X GET "http://workflows.cleverideas.com.mx/api/v1/workflows/tOK30nqcNH3MSSal" > backup.json

# Backup configuraciones
cp /root/.n8n/config.json backup_config.json
```

### Actualizaciones
- **Prompts de Agentes**: Optimización continua basada en analytics
- **Voces**: Ajuste de parámetros para mejor naturalidad  
- **Herramientas**: Mejoras en funcionalidades según feedback
- **Validaciones**: Refinamiento de reglas de formulario

---

## 📈 ROADMAP Y MEJORAS FUTURAS

### Corto Plazo (1-3 meses)
- [ ] A/B testing de diferentes voces
- [ ] Optimización de prompts basada en datos
- [ ] Integración con CRM (HubSpot/Salesforce)
- [ ] Dashboard personalizado de métricas

### Mediano Plazo (3-6 meses)
- [ ] Soporte para más idiomas (portugués, francés)
- [ ] IA para análisis de sentimientos en tiempo real
- [ ] Integración con WhatsApp Business API
- [ ] Automatización de follow-ups post-demo

### Largo Plazo (6-12 meses)
- [ ] Modelo de IA personalizado para el sector
- [ ] Reconocimiento de voz emocional
- [ ] Integración con sistemas de videoconferencia
- [ ] Análisis predictivo de conversión

---

## 👥 EQUIPO Y CONTACTOS

### Desarrollado por
**Darig Samuel Rosales** - Arquitecto de Soluciones Empresariales con IA

### Soporte Técnico
- **Email**: darig.soporte@gmail.com
- **URL Base**: https://www.linkedin.com/in/darig-rosales/
- **Documentación**: Este repositorio de documentación técnica

### Versión del Sistema
- **Versión**: 1.0.0
- **Fecha de Entrega**: Agosto 2025
- **Última Actualización**: Agosto 2025

---

## 📋 CHECKLIST DE ENTREGA

### ✅ Documentación Completa
- [x] Arquitectura del sistema
- [x] Configuración de agentes virtuales
- [x] Integraciones de APIs
- [x] Formulario web y frontend
- [x] Herramientas y funciones personalizadas
- [x] Manual de despliegue
- [x] Guía de troubleshooting

### ✅ Archivos de Configuración
- [x] Workflow n8n exportado
- [x] Configuración de agentes VAPI
- [x] Formulario web HTML completo
- [x] Esquemas de validación
- [x] Variables de entorno documentadas


*Agosto 2025 - Versión 1.0.0*
