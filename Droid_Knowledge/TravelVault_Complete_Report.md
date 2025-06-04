# TravelVault – Complete Product Blueprint  

*(Cyberpunk-fresh, minimalist & enterprise-secure)*  

---

## 1. Identidad de Marca  

| Opción | Nombre | Eslogan | Rationale |
|---------|--------|---------|-----------|
| 1 | **TravelVault** | “Your world, secured in your pocket.” | Seguridad + movilidad, directo. |
| 2 | **NomadSafe** | “Travel light, protect heavy.” | Contraste liviano-seguro para nómadas. |
| 3 | **SecureJourney** | “Documents in check, adventure unlocked.” | Liga certeza documental con espíritu viajero. |

---

## 2. Personas Objetivo  

### Persona 1 – Mara, Digital Nomad  
• 32 años, UX Designer remoto.  
• 6 países/año, visados frecuentes.  
• Necesita alertas de expiración y compartir visa selectivamente.  

### Persona 2 – Luis, Family Planner  
• 44 años, Manager marketing, 2 hijos.  
• Gestiona docs grupales, consentimientos y copias offline.  

### Persona 3 – Aya, Adventure Guide  
• 27 años, guía de trekking.  
• Crea grupos de 10-15 clientes, comparte tarjetas rápidas en cruces de frontera.  

### Persona 4 – Dr. Chen, Exec Sensible  
• 55 años, ejecutivo farmacéutico.  
• Exige cifrado extremo y ventanas de lectura acotadas.  

---

## 3. Propuesta de Valor Única (≤ 80 palabras)  
TravelVault combina almacenamiento cero-conocimiento, controles de compartición dinámicos y una Traveler Card instantánea que condensa tu identidad de viaje. Con cifrado AES-256, acceso biométrico y funcionamiento offline-first, es el único compañero que protege y agiliza documentos para individuos, familias y equipos, todo envuelto en un estilo cyberpunk-minimalista. *(79 palabras)*  

---

## 4. Design System  

### 4.1 Tokens (extracto)  
```json
{
  "color": {
    "bg": {"primary":"#111318","secondary":"#1A1D24"},
    "accent": {"cyan":"#00FFE0","magenta":"#AE00FF","danger":"#FF365E"},
    "text": {"primary":"#FFFFFF","secondary":"#B0B7C3"}
  },
  "radius":{"sm":4,"md":8,"lg":12,"pill":9999},
  "font":{"heading":"SpaceGrotesk-SemiBold","body":"Inter-Regular"},
  "shadow":{"glowCyan":"0 0 12px rgba(0,255,224,.4)"}
}
```

### 4.2 Inventario de Componentes  

| Componente | Props clave | Estado |
|------------|-------------|--------|
| `GradientButton` | variant, icon, onPress | Ready |
| `DocCard` | doc, expanded, actions[] | Ready |
| `TravelerCard` | data, shareLevel, theme | In dev |
| `BottomNav` | routes[], accentColor | Ready |
| `VisibilityToggle` | status, onChange | Ready |
| `Toast` | type, message | Ready |

*(todos WCAG AA, micro-glow 200 ms)*  

---

## 5. Arquitectura de Carpetas (React Native + Expo)  
```
/src
 ├─ app.tsx
 ├─ navigation/
 ├─ screens/{auth,profile,documents,groups,travelerCard,trips}
 ├─ components/{common,documents,groups,travelerCard,trips}
 ├─ hooks/
 ├─ state/          # Zustand slices
 ├─ services/{firebase,ocr,notifications}
 ├─ utils/
 ├─ constants/
 ├─ i18n/
 └─ types/
```

---

## 6. Firestore Schema & Rules  

### 6.1 Colecciones  
`users/{uid}` · `documents/{docId}` · `groups/{groupId}` · `trips/{tripId}` · `travelerCards/{cardId}`  

### 6.2 Security Rules (extracto)  
```
rules_version = '2';
service cloud.firestore {
 match /databases/{db}/documents {
  function signedIn() { return request.auth != null; }

  match /users/{userId} {
    allow read,update,delete: if signedIn() && request.auth.uid==userId;
    allow create: if signedIn();
  }

  match /documents/{docId} {
    allow read: if resource.data.uid==request.auth.uid
                || resource.data.visibility.public
                || resource.data.visibility.groups[request.auth.uid] != "none";
    allow write,delete: if signedIn() && request.resource.data.uid==request.auth.uid;
  }

  match /groups/{groupId} {
    allow read: if signedIn() && resource.data.members[request.auth.uid] != null;
    allow write: if signedIn() && resource.data.members[request.auth.uid] in ['owner','admin'];
  }

  match /travelerCards/{cardId} {
    allow read,write,delete: if signedIn() && resource.data.uid==request.auth.uid;
  }
 }
}
```

---

## 7. Backlog MVP (priorizado)  

| # | Historia de Usuario | Criterios de Aceptación | Pts |
|---|---------------------|-------------------------|-----|
| 1 | Registro + perfil | Email/Google/Apple, 2FA, biometric toggle | 5 |
| 2 | Escanear pasaporte con OCR | Guiado de cámara, extracción MRZ, cifrado local | 8 |
| 3 | Añadir docs múltiples | PDF/JPG, metadatos por tipo, tags | 8 |
| 4 | Recordatorios expiración | Push 90-30-7, .ics export | 5 |
| 5 | Traveler Card v1 | Selección campos, QR estático, guardar Wallet | 8 |
| 6 | Offline cache & sync | Persistencia, cola retry, indicadores | 13 |
| 7 | Crear grupos y roles | Invite link, owner/admin/member/viewer | 8 |
| 8 | Permisos granulares | Nivel none/metadata/full por doc y grupo | 13 |
| 9 | Planificador de viajes | Destinos, checklist, validación docs | 8 |
| 10 | Dashboard readiness | Alertas, quick actions, resumen | 5 |

Total = 82 pts  

---

## 8. Roadmap 2025  

| Q | Epics | Person-Weeks |
|---|-------|-------------|
| Q1 | Auth, Doc core, Traveler Card, Offline, Beta | 28 |
| Q2 | Grupos & sharing, Trips, Perf, Analytics | 20 |
| Q3 | Chat ligero, Health wallet, PDF export, Web | 23 |
| Q4 | AI recommender, Enterprise SSO, Multilingual, BLE tracker | 28 |

---

## 9. CI/CD (`.github/workflows/ci.yml` resumen)  
```yaml
name: mobile-ci
on: [pull_request,push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
        with: {node-version: 18, cache: 'yarn'}
      - run: yarn install --frozen-lockfile
      - run: yarn test --coverage
      - run: |
          pct=$(jq '.total.lines.pct' coverage/coverage-summary.json)
          if (( $(echo "$pct < 80" | bc -l) )); then exit 1; fi
  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: expo/expo-github-action@v8
        with: {eas-version: latest, token: ${{secrets.EXPO_TOKEN}}}
      - run: eas build --profile preview --platform all --non-interactive
```

---

## 10. Mermaid – Edge Cases (texto)  
```
flowchart TD
 A[Scan Doc] -->|Offline| Q[Queue + Encrypt]
 Q --> R{Conn?}
 R -->|Yes| U[Upload]
 R -->|No| Q
 U --> M[Meta Write] --> T{Regenerate Card?}
 T -->|Yes| C[CF Build Card]
```

---

## 11. KPIs & Objetivos  

| Área | KPI | Meta 2025 |
|------|-----|-----------|
| Adopción | MAU | 50 k |
| Engagement | Docs subidos / usuario | ≥ 5 |
| Retención | Day 7 | > 40 % |
| Técnica | Crash-free sessions | ≥ 99.5 % |
| Seguridad | Incidentes críticos | 0 |
| Negocio | Conversión premium | 10 % MAU |

---

## 12. Riesgos & Mitigaciones  

| Riesgo | Impacto | Prob | Mitigación |
|--------|---------|------|------------|
| Brecha de datos | 5 | 2 | AES-256, pen-tests, bug-bounty |
| Costos Firebase altos | 3 | 4 | Compresión, cold storage, cuotas tier |
| OCR baja precisión | 4 | 4 | Modelo entrenado + edición manual |
| Sync conflictos offline | 4 | 3 | Versionado y resolución last-write-wins + UI |
| Competencia nativa Apple/Google | 4 | 2 | Diferenciación en grupos y UX cross-platform |
| Cumplimiento regulatorio | 5 | 3 | Asesoría legal continua, data residency opts |

---

**Fin del Blueprint – listo para que Coding Droid arranque Sprint 0.**  
