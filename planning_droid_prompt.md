# ⚠️ IMPORTANTE  
**Este documento es un SUPLEMENTO TÉCNICO y MOBILE-FIRST**  
Debe enviarse **DESPUÉS** de tu sección original en español _«Idea, Style & Flow»_.  
Parte de la base visual, conceptual y de experiencia ya descrita allí y **no la sustituye**; la amplía con especificaciones de arquitectura, flujo DevOps y pruebas en dispositivos móviles.

---

# Planning Droid Prompt: Cyberpunk-Fresh Minimalist Travel Document Manager

_(Se asume que ya se entregó la sección “Idea, Style & Flow” completa en español. Este archivo añade detalles técnicos, mobile-first y flujo profesional de desarrollo)._  

## 1. Contexto
Actúa como un consorcio de élite formado por:  
• Diseñadores **UX/UI** (sensibilidad de Jony Ive)  
• Estrategas de producto (visión de Elon Musk)  
• Arquitectos de software mobile-first y serverless  
Objetivo: convertir la visión presentada en español en un **producto móvil robusto, seguro y escalable**.

## 2. Producto – Visión & Estilo (resumen)
Se mantiene la estética **cyberpunk-fresh minimalista** establecida: dark mode, acentos neón (#00FFE0, #AE00FF, #FF365E), iconografía universal, tarjetas expandibles, botones con degradado y bordes redondeados.

Añadir:  
- Guía de componentes (botones, inputs, cards, nav-bar, modals, toasts).  
- Tokens de diseño (colores, tipografía, radios, sombras).  

## 3. Funcionalidades Clave (refinadas)
| Área | Detalle |
|------|---------|
| Gestión de Documentos | Escaneo cámara + OCR, subida, cifrado AES-256, recordatorios, visibilidad granular (grupo/campo). |
| Tarjeta de Viajero | Auto-generada, selección de campos, temas, QR + link firmado, actualizaciones en tiempo real. |
| Sistema de Grupos | Roles (owner, admin, member, view-only), historial, invitaciones, chat ligero opcional. |
| Organizador de Viajes | Crear viaje, destinos, checklist equipaje, requisitos de documentos. |
| Seguridad & Privacidad | Firebase Auth (email, Google, Apple), 2FA, biométrico, GDPR, cifrado en tránsito y reposo. |
| Roadmap Futuro | Wallet de salud, exporte PDF, IA recomendadora, soporte multilingüe. |

## 4. Arquitectura Técnica
- **Frontend móvil:** React Native + Expo (TypeScript)  
- **Estado global:** Zustand o Redux Toolkit  
- **Backend:** Firebase (Auth, Firestore, Storage), Cloud Functions (Node 18)  
- **OCR:** Expo-Camera + ML Kit  
- **CI/CD:** GitHub Actions → EAS Build → TestFlight / Google Play Internal  
- **Testing:** Jest + React Native Testing Library, Detox e2e, Expo Go  
- **Analytics & Crash:** Sentry + Firebase Analytics  
- **Offline-first:** Cache Firestore, cola de sync, detección de red  

### Esquema Firestore
```
users/{uid}
documents/{docId}
groups/{groupId}
trips/{tripId}
travelerCards/{cardId}
```
Incluye índices e reglas de seguridad.

## 5. User Flow (alto nivel)
1. Onboarding → Registro/Login (biométrico si disponible)  
2. Dashboard (bottom-nav: Profile · Docs · Card · Trips · Settings)  
3. Profile → Edit info, contactos, privacidad  
4. Docs → Lista ▸ Expandir ▸ Acciones rápidas  
5. Traveler Card → Personalizar ▸ Preview ▸ Compartir (QR/link)  
6. Groups → Crear/Unirse ▸ Ver miembros ▸ Compartir docs/cards  
7. Trips → Crear ▸ Checklist ▸ Requisitos ▸ Compartir viaje  
8. Settings → Dark/Light, seguridad, notificaciones  

## 6. Git Workflow Requerido
```
main          ← producción estable
development   ← integración continua
feature/*     ← una característica
fix/*         ← hotfix
```
- PR contra **development** (tests automáticos)  
- Merge Squash + Conventional Commits  
- EAS Build al hacer merge en **main**

## 7. Entregables Solicitados al Planning Droid
1. Validar coherencia visual/funcional con la sección en español.  
2. Completar guía de estilos y tokens.  
3. Detallar arquitectura de carpetas RN y scripts CI.  
4. Priorizar backlog (MVP vs stretch).  
5. Mejorar Mermaid con edge-cases (errores, offline).  
6. Roadmap trimestral con esfuerzos estimados.  

## 8. Criterios de Éxito
- Coherencia total con la visión original.  
- Seguridad y privacidad de nivel enterprise.  
- Experiencia de usuario rápida y accesible.  
- Código mantenible (coverage ≥ 80 %).  
- CI/CD profesional y ramas limpias.  

---

**Envía este suplemento después del bloque “Idea, Style & Flow” para que el Planning Droid disponga de todo el contexto visual y conceptual, además de estas especificaciones técnicas y mobile-first.**
