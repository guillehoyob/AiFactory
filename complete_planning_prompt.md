# complete-planning-prompt.md  

⚠️ **IMPORTANTE — LEE PRIMERO**  
Recibirás el brief en **DOS PARTES**:

1. **Parte A – VISIÓN & ESTILO** (español): inspiración visual, estética cyber-punk-fresh minimalista, flujos UX y ejemplos UI detallados.  
2. **Parte B – SUPLEMENTO TÉCNICO** (este documento): arquitectura mobile-first, workflow Git, criterios de éxito y lista exacta de entregables.

Por favor **espera ambas partes** antes de analizar y responder.  

---

## 1 · Contexto & Rol

Actúa como un **consorcio de élite** formado por  
• Diseñadores UX/UI con la sensibilidad de **Jony Ive**  
• Estrategas de producto con la visión de **Elon Musk**  
• Arquitectos de software expertos en apps **serverless & mobile-first**

Objetivo: transformar la visión (Parte A) en un **producto móvil robusto, seguro y escalable**, listo para que el Coding Droid lo implemente.

---

## 2 · Resumen de Visión & Estilo (de la Parte A)

Mantén la estética **cyberpunk-fresh minimalista**:  
dark-mode, acentos neón (#00FFE0, #AE00FF, #FF365E), iconografía universal, botones con degradado y bordes redondeados, tarjetas expandibles, información densa pero clara.

---

## 3 · Requisitos Funcionales Refinados

| Área | Alcance |
|------|---------|
| Gestión de Documentos | Escaneo cámara + OCR, subida, cifrado AES-256, recordatorios, visibilidad granular (grupo/campo). |
| Tarjeta de Viajero | Auto-generada, campos seleccionables, temas, QR + link firmado, actualizaciones en tiempo real. |
| Sistema de Grupos | Roles (owner, admin, member, view-only), historial, invitaciones, chat ligero opcional. |
| Organizador de Viajes | Crear viaje, destinos, checklist equipaje, requisitos de documentos. |
| Seguridad & Privacidad | Firebase Auth (email, Google, Apple), 2FA, biométrico, GDPR, cifrado en tránsito y reposo. |
| Roadmap Futuro | Wallet de salud, exporte PDF, IA recomendadora, soporte multilingüe. |

---

## 4 · Arquitectura Técnica Propuesta

Frontend — **React Native + Expo (TypeScript)**  
Estado — Zustand o Redux Toolkit  
Backend — Firebase (Auth · Firestore · Storage), Cloud Functions (Node 18)  
OCR — Expo-Camera + ML Kit  
Offline-First — cache Firestore + cola de sync  
CI/CD — GitHub Actions → EAS Build → TestFlight / Play Internal  
Testing — Jest + RNTL, Detox e2e, Expo Go  
Analytics — Sentry + Firebase Analytics  

### Esquema Firestore inicial
```
users/{uid}
documents/{docId}
groups/{groupId}
trips/{tripId}
travelerCards/{cardId}
```

---

## 5 · Flujo de Usuario (alto nivel)

Onboarding → Dashboard (Profile · Docs · Card · Trips · Settings) →  
• Profile: editar info, contactos, privacidad  
• Docs: lista ▸ expandir ▸ acciones rápidas  
• Card: personalizar ▸ preview ▸ compartir (QR/link)  
• Groups: crear/unirse ▸ ver miembros ▸ compartir docs/cards  
• Trips: crear ▸ checklist ▸ requisitos ▸ compartir viaje

---

## 6 · Workflow Git & DevOps

```
main          ← producción estable
development   ← integración continua
feature/*     ← rama por funcionalidad
fix/*         ← hotfix
```
• PR contra **development** (tests automáticos)  
• Merge Squash + Conventional Commits  
• EAS Build al fusionar a **main**  

---

## 7 · Entregables & Formato EXIGIDOS

| # | Entregable | Formato requerido |
|---|------------|-------------------|
| 1 | **Identidad de Marca** | Tabla con 3 opciones de Nombre + Eslogan + Justificación (máx 120 car.) |
| 2 | **Personas Objetivo** | 3-4 fichas (Nombre, edad, contexto, necesidades, frustraciones, escenario de uso) |
| 3 | **Propuesta de Valor Única** | 1 párrafo ≤ 80 palabras |
| 4 | **Design System** | a) tokens (JSON); b) tabla de componentes con props clave & estados; c) mockups miniatura (link Figma opcional) |
| 5 | **Arquitectura Carpeta RN** | Árbol de carpetas con descripción de cada directorio |
| 6 | **Esquema Firestore + Reglas** | Diagrama + tabla campos (nombre, tipo, restricciones) + fichero `.rules` comentado |
| 7 | **Backlog Prioritario (MVP)** | Tabla: id, épica, historia de usuario, criterio aceptación, tamaño (pts) |
| 8 | **Roadmap Trimestral** | Tabla Q1-Q4 con épicas, esfuerzo (person-wks) |
| 9 | **CI/CD Pipeline** | Archivo `ci.yml` + pasos EAS Build, cobertura ≥80 % |
|10 | **Mermaid Diagram Final** | Diagrama actualizado con edge-cases (errores, offline, reintentos) |
|11 | **KPIs & Éxito** | Lista de métricas (DAU, tasa share, tiempo scan) + objetivos numéricos |
|12 | **Riesgos & Mitigaciones** | Tabla riesgo, impacto, mitigación |

---

## 8 · Criterios de Éxito

- Coherencia total con la visión (Parte A).  
- Seguridad y privacidad a nivel enterprise.  
- Experiencia de usuario rápida, accesible (WCAG AA).  
- Código mantenible (coverage ≥ 80 %).  
- Flujo Git + CI/CD profesional.  

---

## 9 · Formato de Respuesta

```
# 1. Identidad de Marca
<table>...</table>

# 2. Personas Objetivo
## Persona 1
- Perfil...
## Persona 2
...

# 3. PVU
...

# 4. Design System
### 4.1 Tokens (JSON)
{
  "color-primary": "#00FFE0",
  ...
}
### 4.2 Componentes
| Componente | Props | Estados | Uso |
|------------|-------|---------|-----|
...

# 5. Arquitectura Carpetas RN
<árbol carpetas>

...

# 12. Riesgos & Mitigaciones
| Riesgo | Impacto | Mitigación |
|--------|---------|------------|
```

---

💎 **Objetivo final:** entregar un documento maestro que sirva de base inquebrantable para el Coding Droid, con todos los detalles listos para implementación profesional.  
