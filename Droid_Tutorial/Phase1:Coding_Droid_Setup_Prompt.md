# Coding Droid – Initial Setup Prompt  
*(File: coding-droid-setup-prompt.md)*  

## Mission  
Bootstrap the TravelVault mobile repository with a rock-solid foundation that mirrors the blueprint delivered by Planning Droid. Focus only on project skeleton, configuration, CI and Git workflow; no feature code yet.

---

## Repository & Branching  

1. Remote repository: **github.com/guillehoyob/travelvault** (create if absent).  
2. Default protected branch: `main` (production).  
3. Create integration branch: `development` and push all initial work there.  
4. Use **feature/\*** branches for subsequent tickets (e.g. `feature/doc-core`).  
5. First PR: `development → main` once CI is green.

---

## Setup Tasks (in order)  

### 1. React-Native + Expo Skeleton  
- Initiate with `expo init travelvault --template expo-template-blank-typescript`.  
- Configure **app.json** with name **TravelVault** and dark theme enabled.  
- Install core deps:  
  ```
  yarn add zustand @react-navigation/native \
          @react-navigation/bottom-tabs \
          firebase react-native-dotenv \
          @shopify/restyle
  ```

### 2. Folder Structure  
Replicate exactly:

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

Create empty `index.ts` files where relevant so imports resolve.

### 3. Design System Boot-up  
- Add `tokens.json` in `/src/constants` using the sample JSON from blueprint §4.1.  
- Implement a minimal `ThemeProvider` with Restyle pulling from those tokens.  
- Scaffold two example components: `GradientButton` and `DocCard` (empty layout).

### 4. Firebase Placeholder  
- Add `/src/services/firebase/config.ts` reading env vars (`.env.example`) for apiKey, projectId, etc.  
- DO NOT commit real keys.

### 5. State Management Skeleton  
- Create `state/userSlice.ts` and `state/uiSlice.ts` with basic interfaces and empty actions.

### 6. Linting & Formatting  
- `eslint`, `prettier`, `husky` pre-commit hook running `lint --fix`.  
- Config extends `eslint-config-react-native`, `@typescript-eslint`.

### 7. Testing  
- Unit: `jest` + `@testing-library/react-native`; include sample test that always passes.  
- E2E skeleton: `detox` config (android & ios).  

### 8. CI/CD  
- Add `.github/workflows/ci.yml` exactly as in blueprint §9, but make tests pass with current skeleton and enforce coverage ≥ 80% (use Jest’s `--coverage` and ignorePattern to count only sample test).  
- Ensure EAS CLI is installed but build step set to `--skip-build` until native code exists.

### 9. Documentation  
`README.md` top-level:  
- Quick start, scripts (`yarn ios`, `yarn android`, `yarn test`), branch policy, design token link.

### 10. Commit & Push  
- Commit message: `chore(core): bootstrap project skeleton` (Conventional Commits).  
- Push to `development`. Verify CI passes.  

---

## Acceptance Criteria  

- `yarn test`, `yarn lint`, `expo prebuild` succeed locally and in CI.  
- Repository matches folder tree.  
- `tokens.json` present and consumed by Restyle theme.  
- No hard-coded secrets.  
- CI workflow green with ≥ 80 % dummy coverage.  
- Branch `development` pushed; `main` untouched.  

---

## Output  

When complete, reply with:  

1. GitHub commit hash.  
2. Link to `development` branch CI run (green).  
3. Any caveats or next steps.  

**Start now.**  
