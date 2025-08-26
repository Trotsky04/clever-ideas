# DOCUMENTACIÓN TÉCNICA - FORMULARIO WEB GENIUS AI
## Sistema de Captura de Leads con Detección de Idioma

---

##  ÍNDICE

1. [Resumen del Formulario](#resumen-del-formulario)
2. [Arquitectura Frontend](#arquitectura-frontend)
3. [Sistema de Validaciones](#sistema-de-validaciones)
4. [Detección de Idioma](#detección-de-idioma)
5. [Integración con Backend](#integración-con-backend)
6. [Configuración Visual](#configuración-visual)
7. [Funcionalidades Avanzadas](#funcionalidades-avanzadas)

---

##  RESUMEN DEL FORMULARIO

### Propósito
El formulario web **Genius AI** de Clever IDEAS es un sistema de captura de leads diseñado para:
- Recopilar información de prospectos interesados en soluciones de IA
- Detectar automáticamente el idioma preferido del usuario
- Validar datos en tiempo real con feedback visual
- Integrar directamente con el workflow de n8n para llamadas automáticas
- Proporcionar una experiencia de usuario moderna y responsive

### URL del Formulario
```
https://demoai.cleverideas.com.mx/
```

### Tecnologías Utilizadas
- **HTML5**: Estructura semántica
- **CSS3**: Diseño responsive con animaciones
- **JavaScript ES6+**: Validaciones y lógica de negocio
- **Font Awesome**: Iconografía
- **Google Fonts**: Tipografía (Space Grotesk, Inter)

---

##  ARQUITECTURA FRONTEND

### Estructura HTML Principal
```html
<!DOCTYPE html>
<html lang="es" data-theme="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="color-scheme" content="light">
    <title>Genius AI | Agentes Virtuales Inteligentes - Clever Ideas</title>
    <!-- Recursos externos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
</head>
```

### Paleta de Colores
```css
:root {
    --neural-primary: #6366f1;      /* Azul principal */
    --neural-secondary: #8b5cf6;    /* Púrpura secundario */
    --neural-accent: #06b6d4;       /* Cyan de acento */
    --neural-green: #10b981;        /* Verde neural */
    --clever-green: #22c55e;        /* Verde Clever */
    --error-red: #ef4444;           /* Rojo de error */
    --success-green: #22c55e;       /* Verde de éxito */
    --title-color: #1e293b;         /* Color de títulos */
    --text-primary: #334155;        /* Texto principal */
    --text-secondary: #64748b;      /* Texto secundario */
}
```

### Componentes Principales

#### 1. Navegación
```html
<nav class="navbar">
    <div class="nav-content">
        <img src="logo-clever.png" alt="Clever Ideas" class="nav-logo">
        <ul class="nav-links">
            <li><a href="#que-es">¿Qué es?</a></li>
            <li><a href="#beneficios">Beneficios</a></li>
            <li><a href="#diferenciadores">Diferenciadores</a></li>
            <li><a href="#casos-uso">Casos de Uso</a></li>
            <li><a href="#form-section">Demo</a></li>
        </ul>
        <div class="language-toggle" onclick="toggleLanguage()">
            <img src="flag-mexico.svg" class="language-flag" id="currentFlag">
            <span class="language-text" id="currentLanguage">ESP</span>
        </div>
    </div>
</nav>
```

#### 2. Hero Section
```html
<section class="hero">
    <div class="hero-content">
        <div class="hero-badge">
            <i class="fas fa-brain"></i>
            <span data-es="Tecnología de IA Avanzada" data-en="Advanced AI Technology">
                Tecnología de IA Avanzada
            </span>
        </div>
        <h1 class="hero-title">
            <span data-es="Agentes Virtuales" data-en="Virtual Agents">Agentes Virtuales</span><br>
            <span class="clever-accent">Genius AI</span>
        </h1>
        <p class="hero-subtitle">
            Experimenta la próxima generación de asistentes virtuales inteligentes...
        </p>
        <a href="#form-section" class="hero-cta" onclick="scrollToForm()">
            <i class="fas fa-rocket"></i>
            <span data-es="Solicitar Demo de Genius AI" data-en="Request Genius AI Demo">
                Solicitar Demo de Genius AI
            </span>
        </a>
    </div>
</section>
```

---

##  SISTEMA DE VALIDACIONES

### Reglas de Validación
```javascript
const validationRules = {
    nombre: {
        pattern: /^[a-zA-ZÀ-ÿ\u00f1\u00d1\s]{1,40}$/,
        message: { 
            es: 'El nombre debe contener máximo 40 caracteres y solo letras',
            en: 'Name must contain maximum 40 characters and only letters'
        }
    },
    telefono: {
        pattern: /^\d{10}$/,
        message: { 
            es: 'El teléfono debe contener exactamente 10 dígitos',
            en: 'Phone must contain exactly 10 digits'
        }
    },
    email: {
        pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
        message: { 
            es: 'Ingrese un correo electrónico válido',
            en: 'Enter a valid email address'
        }
    },
    empresa: {
        pattern: /^.{1,40}$/,
        message: { 
            es: 'El nombre de la empresa debe contener máximo 40 caracteres',
            en: 'Company name must contain maximum 40 characters'
        }
    },
    giro: {
        pattern: /^.+$/,
        message: { 
            es: 'Selecciona un giro empresarial',
            en: 'Select a business sector'
        }
    }
};
```

### Estados de Validación Visual
```css
/* Estado válido */
.form-input.valid, .form-select.valid {
    border-color: var(--success-green) !important;
    background: rgba(34, 197, 94, 0.1) !important;
    box-shadow: 0 0 20px rgba(34, 197, 94, 0.3) !important;
}

/* Estado de error */
.form-input.error, .form-select.error {
    border-color: var(--error-red) !important;
    background: rgba(239, 68, 68, 0.1) !important;
    box-shadow: 0 0 20px rgba(239, 68, 68, 0.3) !important;
    animation: shakeError 0.5s ease-in-out;
}

/* Animación de error */
@keyframes shakeError {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-5px); }
    75% { transform: translateX(5px); }
}
```

### Sistema de Captcha
```html
<div class="captcha-container">
    <div class="captcha-question" id="captchaQuestion">
        Verificación de seguridad: ¿Cuánto es 5 + 3?
    </div>
    <input type="number" class="captcha-input" id="captchaInput" placeholder="?" required>
    <div class="error-message" id="captchaError">
        Respuesta incorrecta. Inténtalo de nuevo.
    </div>
</div>
```

```javascript
let captchaPairs = [
    { 
        question: { 
            es: "Verificación de seguridad: ¿Cuánto es 5 + 3?", 
            en: "Security verification: What is 5 + 3?" 
        }, 
        answer: 8 
    },
    { 
        question: { 
            es: "Verificación de seguridad: ¿Cuánto es 7 + 2?", 
            en: "Security verification: What is 7 + 2?" 
        }, 
        answer: 9 
    },
    // ... más pares de preguntas
];
```

---

##  DETECCIÓN DE IDIOMA

### Sistema Bilingüe
El formulario soporta **español** e **inglés** con cambio dinámico de contenido.

### Estructura de Datos Multiidioma
```html
<!-- Elementos con atributos data para ambos idiomas -->
<span data-es="Tecnología de IA Avanzada" data-en="Advanced AI Technology">
    Tecnología de IA Avanzada
</span>

<input type="text" 
       data-placeholder-es="Nombre completo" 
       data-placeholder-en="Full name" 
       placeholder="Nombre completo">
```

### Función de Cambio de Idioma
```javascript
let currentLanguage = 'es';

function toggleLanguage() {
    currentLanguage = currentLanguage === 'es' ? 'en' : 'es';
    updateLanguage();
}

function updateLanguage() {
    const elements = document.querySelectorAll('[data-es][data-en]');
    const flagElement = document.getElementById('currentFlag');
    const languageText = document.getElementById('currentLanguage');
    
    elements.forEach(element => {
        const text = element.getAttribute(`data-${currentLanguage}`);
        if (text) {
            if (element.tagName === 'INPUT') {
                element.placeholder = text;
            } else {
                element.textContent = text;
            }
        }
    });
    
    // Actualizar bandera y texto
    if (currentLanguage === 'en') {
        flagElement.src = "flag-usa.svg";
        languageText.textContent = "ENG";
    } else {
        flagElement.src = "flag-mexico.svg";
        languageText.textContent = "ESP";
    }
}
```

### Sectores Empresariales
```html
<select class="form-select" name="giro" required>
    <option value="" data-es="Selecciona tu giro empresarial" data-en="Select your business sector">
        Selecciona tu giro empresarial
    </option>
    <option value="tecnologia" data-es="Tecnología e Informática" data-en="Technology & IT">
        Tecnología e Informática
    </option>
    <option value="salud" data-es="Salud y Medicina" data-en="Health & Medicine">
        Salud y Medicina
    </option>
    <option value="educacion" data-es="Educación" data-en="Education">
        Educación
    </option>
    <option value="financiero" data-es="Servicios Financieros" data-en="Financial Services">
        Servicios Financieros
    </option>
    <option value="inmobiliario" data-es="Inmobiliario" data-en="Real Estate">
        Inmobiliario
    </option>
    <option value="retail" data-es="Retail y Comercio" data-en="Retail & Commerce">
        Retail y Comercio
    </option>
    <option value="restaurantes" data-es="Restaurantes y Hotelería" data-en="Restaurants & Hospitality">
        Restaurantes y Hotelería
    </option>
    <option value="automotriz" data-es="Automotriz" data-en="Automotive">
        Automotriz
    </option>
    <option value="construccion" data-es="Construcción" data-en="Construction">
        Construcción
    </option>
    <option value="manufactura" data-es="Manufactura" data-en="Manufacturing">
        Manufactura
    </option>
    <option value="logistica" data-es="Logística y Transporte" data-en="Logistics & Transportation">
        Logística y Transporte
    </option>
    <option value="otros" data-es="Otros" data-en="Others">
        Otros
    </option>
</select>
```

---

##  INTEGRACIÓN CON BACKEND

### Endpoint del Webhook
```javascript
const WEBHOOK_URL = 'https://workflows.cleverideas.com.mx/webhook/form-web';
```

### Estructura de Datos Enviados
```javascript
const data = {
    nombre: "string",           // Nombre completo del prospecto
    telefono: "string",         // Teléfono de 10 dígitos
    email: "string",            // Email válido
    empresa: "string",          // Nombre de la empresa
    giro: "string",             // Sector empresarial
    dominio: "string",          // Dominio extraído del email
    idioma: "es|en"             // Idioma detectado
};
```

### Función de Envío
```javascript
form.addEventListener('submit', async function(e) {
    e.preventDefault();
    
    // Validación final
    if (hasErrors) return;
    
    const originalText = submitBtn.innerHTML;
    const buttonText = currentLanguage === 'es' ? 
        '<i class="fas fa-spinner fa-spin"></i> Conectando...' : 
        '<i class="fas fa-spinner fa-spin"></i> Connecting...';
    submitBtn.innerHTML = buttonText;
    submitBtn.disabled = true;
    
    try {
        const formData = new FormData(this);
        const data = Object.fromEntries(formData);
        
        // Extraer dominio del email
        const emailDomain = data.email.split('@')[1];
        data.dominio = `https://${emailDomain}`;
        
        // Agregar idioma actual
        data.idioma = currentLanguage;
        
        const response = await fetch(WEBHOOK_URL, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(data)
        });
        
        if (response.ok) {
            const successText = currentLanguage === 'es' ? 
                '<i class="fas fa-check"></i> ¡Conexión con Genius AI Establecida!' : 
                '<i class="fas fa-check"></i> Genius AI Connection Established!';
            submitBtn.innerHTML = successText;
            submitBtn.style.background = 'linear-gradient(135deg, #10b981, #059669)';
            this.reset();
            createGeniusSuccess(); // Animación de éxito
        }
    } catch (error) {
        const errorText = currentLanguage === 'es' ? 
            '<i class="fas fa-exclamation-triangle"></i> Error de Conexión' : 
            '<i class="fas fa-exclamation-triangle"></i> Connection Error';
        submitBtn.innerHTML = errorText;
        submitBtn.style.background = 'linear-gradient(135deg, #ef4444, #dc2626)';
    }
});
```

---

##  CONFIGURACIÓN VISUAL

### Animaciones CSS

#### Background Neural Network
```css
.neural-canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 1;
    pointer-events: none;
}
```

```javascript
// Animación de red neuronal
const canvas = document.getElementById('neuralCanvas');
const ctx = canvas.getContext('2d');
const nodes = [];
const nodeCount = 50;

// Crear nodos
for (let i = 0; i < nodeCount; i++) {
    nodes.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        vx: (Math.random() - 0.5) * 0.5,
        vy: (Math.random() - 0.5) * 0.5,
        radius: Math.random() * 3 + 1
    });
}
```

#### Cursor Personalizado
```css
.neural-cursor {
    position: fixed;
    width: 20px;
    height: 20px;
    background: radial-gradient(circle, var(--clever-green), transparent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    mix-blend-mode: screen;
}

.neural-cursor::before {
    content: '';
    position: absolute;
    top: -10px;
    left: -10px;
    width: 40px;
    height: 40px;
    border: 2px solid var(--clever-green);
    border-radius: 50%;
    opacity: 0.3;
    animation: cursorPulse 2s infinite;
}
```

#### Animación de Chat Demo
```html
<div class="ai-chat-demo">
    <div class="chat-message">
        <div class="message-avatar"><i class="fas fa-robot"></i></div>
        <div class="message-content">
            Hola, soy Genius AI, tu asistente virtual inteligente...
        </div>
    </div>
    <div class="voice-visualizer">
        <div class="voice-bar"></div>
        <!-- Más barras de visualización -->
    </div>
</div>
```

### Responsive Design
```css
@media (max-width: 768px) {
    .nav-links { display: none; }
    .hero-title { font-size: 2.5rem; }
    .form-container { padding: 40px 30px; }
    .features-grid { grid-template-columns: 1fr; }
}

@media (max-width: 480px) {
    .neural-demo { min-height: 250px; margin: 30px 10px; }
    .ai-chat-demo { padding: 10px; gap: 10px; }
}
```

---

##  FUNCIONALIDADES AVANZADAS

### 1. Validación en Tiempo Real
```javascript
inputs.forEach(input => {
    input.addEventListener('input', () => validateField(input));
    input.addEventListener('blur', () => validateField(input));
});

function validateField(input) {
    const rule = validationRules[input.name];
    const value = input.value.trim();
    const isValid = rule.pattern.test(value);
    
    if (isValid && value) {
        input.classList.remove('error');
        input.classList.add('valid');
        validationState[input.name] = true;
    } else if (value) {
        input.classList.remove('valid');
        input.classList.add('error');
        validationState[input.name] = false;
    }
    
    updateSubmitButton();
}
```

### 2. Animación de Éxito
```javascript
function createGeniusSuccess() {
    const colors = ['#6366f1', '#8b5cf6', '#10b981'];
    for (let i = 0; i < 50; i++) {
        const particle = document.createElement('div');
        particle.style.cssText = `
            position: fixed;
            width: 8px;
            height: 8px;
            background: ${colors[Math.floor(Math.random() * colors.length)]};
            border-radius: 50%;
            left: ${Math.random() * 100}%;
            top: -10px;
            pointer-events: none;
            z-index: 10000;
            box-shadow: 0 0 20px currentColor;
        `;
        
        document.body.appendChild(particle);
        
        particle.animate([
            { transform: 'translateY(-10px) rotate(0deg)', opacity: 1 },
            { transform: `translateY(${window.innerHeight + 20}px) rotate(${Math.random() * 360}deg)`, opacity: 0 }
        ], {
            duration: Math.random() * 3000 + 2000,
            easing: 'cubic-bezier(0.25, 0.46, 0.45, 0.94)'
        }).onfinish = () => particle.remove();
    }
}
```

### 3. Smooth Scrolling
```javascript
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
            target.scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
        }
    });
});
```

### 4. Extracción Automática de Dominio
```javascript
// Extraer dominio del email para investigación IA
const emailDomain = data.email.split('@')[1];
data.dominio = `https://${emailDomain}`;
```

---

## 📊 MÉTRICAS Y TRACKING

### Eventos Trackeable
1. **Form View**: Usuario ve el formulario
2. **Language Toggle**: Cambio de idioma
3. **Field Focus**: Usuario enfoca un campo
4. **Validation Error**: Error de validación
5. **Form Submit**: Envío exitoso
6. **Connection Error**: Error de conexión

### Integración con Analytics
```javascript
// Google Analytics 4 events
gtag('event', 'form_start', {
    'event_category': 'engagement',
    'event_label': currentLanguage
});

gtag('event', 'form_submit', {
    'event_category': 'conversion',
    'event_label': currentLanguage,
    'value': 1
});
```

---

## 🔧 CONFIGURACIÓN DE DESARROLLO

### Variables de Entorno
```javascript
const CONFIG = {
    WEBHOOK_URL: 'https://workflows.cleverideas.com.mx/webhook/form-web',
    DEBUG_MODE: false,
    ANALYTICS_ID: 'GA_MEASUREMENT_ID',
    VERSION: '1.0.0'
};
```

### Build Process
```bash
# Minificar CSS
npm run build:css

# Optimizar JavaScript
npm run build:js

# Comprimir imágenes
npm run build:images

# Deploy
npm run deploy
```

---
