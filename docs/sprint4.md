# 🧭 Sprint 4 — Client SPA amb Vue i control de rols

Aquest sprint té com a objectiu consolidar la part **client** del projecte intermodular mitjançant la creació d’una **interfície moderna, dinàmica i segura** amb **Vue.js**. 
A partir del backend ja desplegat (Laravel, API REST), s’implementaran les funcionalitats principals del frontend, incloent:

- **C1.** Desenvolupament d’una interfície SPA amb components Vue i rutes dinàmiques.
- **C2.** Integració del sistema d’autenticació i gestió de sessions mitjançant API.
- **C3.** Gestió de rols i permisos d’usuari per a un control d’accés granular.

L’objectiu és aconseguir una experiència d’usuari fluida i segura, respectant els principis de modularitat, escalabilitat i bones pràctiques de desenvolupament web professional.

---

## Índex

1. [⚡ C1. Interfície d’usuari avançada amb Vue.js](#c1--interfície-dusuari-avançada-amb-vuejs)
2. [🔐 C2. Integració de l’autenticació mitjançant API](#c2--integració-de-lautenticació-mitjançant-api)
3. [👥 C3. Gestió de rols d’usuari i permisos](#c3--gestió-de-rols-dusuari-i-permisos)

---

## C1. ⚡ Interfície d’usuari avançada amb Vue.js

### 1️⃣ Objectius

Desenvolupar una **interfície d’usuari moderna i interactiva** basada en **Vue.js**, transformant el projecte en una **SPA (Single Page Application)**. 
L’objectiu és oferir una experiència d’ús més fluida, sense recàrregues completes de pàgina, amb navegació dinàmica i actualització reactiva de dades.

Aquesta implementació permetrà:

- 🧩 Separar clarament la **lògica**, la **presentació** i el **comportament** del client.
- 🚀 Millorar la **usabilitat i velocitat** de navegació.
- 🖥️ Aconseguir una experiència semblant a una aplicació d’escriptori.

Correspon als resultats d’aprenentatge:

- **DWEC RA6.h** → Dissenya aplicacions SPA amb frameworks moderns.
- **DWEC RA6.c** → Implementa components reutilitzables i modulars.
- **DWEC RA4.f** → Aplica bones pràctiques en la manipulació del DOM i l’ús d’esdeveniments.

---

### 2️⃣ Requisits previs

✅ Node.js i npm instal·lats (**v20 o superior**) 
✅ Entorn Docker amb servei per a l’API (PHP/Laravel) i MySQL 
✅ Estructura del projecte Vue amb `vite` 
✅ Coneixement bàsic de components, props, `v-model` i rutes (`vue-router`) 
✅ Coneixement d’API REST i integració amb `axios`

📦 **Estructura orientativa del projecte Vue.js:**

```text
frontend/
├── src/
│   ├── assets/               # Recursos estàtics (imatges, icones, CSS)
│   ├── components/           # Components reutilitzables (Botons, Navbar, CardProducte)
│   ├── views/                # Vistes principals (Home, Productes, Perfil, Login)
│   ├── router/
│   │   └── index.js          # Definició de rutes SPA
│   ├── store/                # (Opcional) Gestió d’estat global amb Pinia
│   ├── App.vue               # Component arrel
│   └── main.js               # Punt d’entrada de l’aplicació
├── public/
│   └── index.html            # Pàgina HTML principal
├── package.json
├── vite.config.js
└── Dockerfile
```

---

### 3️⃣ Flux general d’implementació

🔹 **1. Inicialització del projecte**

- Crear el projecte amb `npm create vue@latest` o `npm create vite@latest`.
- Configurar l’estructura de carpetes segons bones pràctiques.

🔹 **2. Creació de components bàsics**

- `Navbar.vue`, `Footer.vue`, `CardProducte.vue`, etc.
- Utilitzar **props** per passar dades i **events** (`@click`, `@submit`) per comunicar components.

🔹 **3. Definició de rutes SPA**

- Instal·lar `vue-router` i definir rutes sense recàrrega.

🔹 **4. Integració amb el backend (API REST)**

- Utilitzar `fetch` o `axios` per recuperar i enviar dades a l’API.
- Mostrar dades dinàmicament amb `v-for`, `v-if` i `computed`.

🔹 **5. Gestió d’estat i autenticació**

- Utilitzar **Pinia** per compartir dades entre components.
- Implementar rutes protegides i redireccions després del login.

🔹 **6. Optimització i desplegament**

- Compilar l’aplicació per a producció amb `npm run build`.
- Integrar el frontend amb Nginx o el contenidor Docker corresponent.

---

### 4️⃣ Interfície i experiència d’usuari

🎨 **Disseny modern i coherent** 
🧭 **Navegació sense recàrrega** 
⚡ **Respostes instantànies** 
📱 **Disseny responsive** 
🎞️ **Transicions suaus entre vistes**

---

### 5️⃣ Bones pràctiques

🧱 **Modularitat** · 🔐 **Seguretat** · ♻️ **Reactivitat controlada** · 💬 **Feedback visual** · 🧠 **Organització del codi** · 📁 **Gestió d’estat neta**

---

### 6️⃣ Estat del desenvolupament

#### 🟦 To Do

- Crear projecte amb Vite.
- Definir rutes i components bàsics.
- Configurar comunicació amb API REST.

#### 🟨 In Progress

- Integració amb backend (login, productes, comentaris).
- Afegir animacions i transicions.
- Gestió d’estat global i autenticació.

#### 🟩 Done

- Navegació SPA funcional.
- Components modulars operatius.
- Integració visual amb backend i estils coherents.
- Optimització i desplegament complet amb Docker.

---

## C2. 🔐 Integració de l’autenticació mitjançant API

### 1️⃣ Objectius (amb mapeig DWEC)

Implementar l’autenticació de l’usuari des del **client Vue 3** comunicant-se amb el **servidor Laravel** mitjançant **crides HTTP asíncrones** amb Axios.  
L’aplicació ha de gestionar de manera segura les **sessions, tokens o cookies**, i **actualitzar la interfície** segons l’estat d’autenticació.

**Referència DWEC:**

- **RA7.f:** Implementa mecanismes de seguretat en aplicacions web del costat client.

---

### 2️⃣ Requisits previs

- API Laravel amb endpoints:
  - `POST /api/login`
  - `POST /api/logout`
  - `GET /api/user` (usuari autenticat)
- Autenticació basada en **token (Bearer)** o **cookie de sessió**.
- Front-end Vue 3 amb **Axios**, **Pinia**, **Vue Router** i **persistència local** (`localStorage` o `sessionStorage`).

---

### 3️⃣ Estructura de projecte (mòdul `auth`)

```text
src/
├─ modules/
│  ├─ auth/
│  │  ├─ views/
│  │  │  ├─ LoginView.vue
│  │  │  ├─ RegisterView.vue (opcional)
│  │  │  └─ ProfileView.vue
│  │  ├─ components/
│  │  │  ├─ AuthForm.vue
│  │  │  └─ LogoutButton.vue
│  │  ├─ store.js              # Pinia store per a auth
│  │  ├─ api.js                # Funcions Axios: login, logout, getUser
│  │  └─ guards.js             # Router guards per a rutes protegides
│  └─ ...
├─ services/
│  └─ http.js                  # Instància Axios + interceptors
└─ stores/
   └─ uiStore.js               # estat global (loading, toasts, etc.)
```

> **RA7.f:** la seguretat es centralitza i s’abstrau (no es manipulen tokens directament en components).

---

### 4️⃣ Flux d’autenticació

#### 🔹 Login

1. L’usuari ompli el formulari de login (`AuthForm.vue`).
2. `authStore.login(credentials)` → `authApi.login()`.
3. El servidor Laravel retorna:
   - Token JWT → s’emmagatzema en `localStorage`.
   - o cookie HTTP-only (si està configurat així).
4. `authStore` actualitza l’estat (`isAuthenticated = true`) i guarda `user`.
5. El router redirigeix a `/dashboard` o `/profile`.

#### 🔹 Logout

1. `authStore.logout()` → `authApi.logout()`.
2. Es netegen el token i l’usuari de `store` i `localStorage`.
3. Es redirigeix a `/login`.

#### 🔹 Refresh / Persistència

En muntar l’aplicació (`App.vue`) o en un guard del router:

- Si hi ha token vàlid → crida `authApi.getUser()` i restaura l’estat.
- Si no → redirigeix a `/login` (si la ruta és protegida).

---

### 5️⃣ Pinia Store: `authStore.js` (exemple)

```js
import { defineStore } from 'pinia'
import { login, logout, getUser } from './api'

export const useAuthStore = defineStore('auth', {
  state: () => ({
    user: null,
    token: localStorage.getItem('token') || null,
    isAuthenticated: !!localStorage.getItem('token')
  }),

  actions: {
    async login(credentials) {
      const { token, user } = await login(credentials)
      this.user = user
      this.token = token
      this.isAuthenticated = true
      localStorage.setItem('token', token)
    },

    async logout() {
      await logout()
      this.user = null
      this.token = null
      this.isAuthenticated = false
      localStorage.removeItem('token')
    },

    async fetchUser() {
      const user = await getUser()
      this.user = user
    }
  }
})
```

---

### 6️⃣ Servei HTTP i interceptors

```js
import axios from 'axios'
import { useAuthStore } from '@/modules/auth/store'

const http = axios.create({
  baseURL: 'http://localhost:8000/api',
  // Permet enviar cookies (si uses sessions/CSRF amb cookies)
  withCredentials: true
})

// Afegir token a cada petició (abans de cada request)
http.interceptors.request.use((config) => {
  const auth = useAuthStore()
  if (auth.token) {
    config.headers.Authorization = `Bearer ${auth.token}`
  }
  return config
})

// Gestió d’errors globals (401, 403)
http.interceptors.response.use(
  // Si tot va bé, retorna la resposta tal qual
  (response) => response,
  (error) => {
    const auth = useAuthStore()
    // Si hi ha un 401 (No autoritzat), tanquem sessió
    if (error.response?.status === 401) {
      auth.logout()
    }
    // Rebutgem la promesa perquè els .catch() la puguen gestionar
    return Promise.reject(error)
  }
)

export default http
```

> **RA7.f:** gestió segura del token, interceptors centralitzats, protecció davant accés no autoritzat.

---

### 7️⃣ Rutes protegides (guards)

```js
router.beforeEach((to, from, next) => {
  // to   → ruta destinació
  // from → ruta actual
  // next → continuar / redirigir / cancel·lar
  const auth = useAuthStore()

  // Si la ruta és protegida i l’usuari no està autenticat
  if (to.meta.requiresAuth && !auth.isAuthenticated) {
    next('/login')
  } else {
    next()
  }
})
```

- Rutes com `/dashboard`, `/orders`, `/profile` han d’estar protegides des del Vue Router amb `meta.requiresAuth = true`.
- Rutes públiques: `/login`, `/register`, `/about`.

---

### 8️⃣ Actualització dinàmica de la interfície

- Mostrar diferent **navbar** segons `auth.isAuthenticated`.
- Protegir seccions (botons o formularis) si l’usuari no està connectat.
- Mostrar nom d’usuari o avatar després del login.
- En logout, el contingut privat desapareix sense recarregar la pàgina.

> **RA7.f:** la UI reacciona a l’estat de seguretat de manera immediata.

---

### 9️⃣ Seguretat (client)

- No guardar contrasenyes en cap variable persistent.
- Token només en **localStorage** (si no es pot usar cookie HTTP-only).
- Tancar sessió automàticament en 401.
- Evitar exposar dades sensibles al DOM.
- Afegir `timeout` en peticions Axios i tractar errors de xarxa.

---

### 🔟 Testing i validació

- **Proves d’integració** del flux login/logout (amb API mockejada).
- **Tests unitaris** per a `authStore` i `api.js`.
- **Proves E2E (Cypress o Playwright)** per simular un login real en navegador.
- **Lint i auditoria** de dependències (vulnerabilitats).

---

### 1️⃣1️⃣ Estat del desenvolupament

#### 🟦 To Do

- Crear endpoints d’autenticació al backend Laravel (`/login`, `/logout`, `/user`).
- Configurar la instància **Axios** amb interceptors i `baseURL` comuna.
- Implementar formulari de **LoginView.vue** i validacions bàsiques.
- Definir **router guards** per a rutes protegides.

#### 🟨 In Progress

- Desenvolupament del **Pinia store (`authStore`)** amb gestió de token i usuari.
- Integració amb l’API real de Laravel i proves de resposta HTTP.
- Actualització dinàmica del **navbar** i del contingut segons l’estat de sessió.
- Afegir feedback visual (toasts, loading, errors d’autenticació).

#### 🟩 Done

- Arquitectura bàsica del mòdul `auth/` creada (views, components, api, store).
- Navegació SPA funcional amb redireccions després de login/logout.
- Gestió d’errors globals (401/403) i tancament automàtic de sessió.
- Sessió persistent amb token al `localStorage` i restauració en reobrir l’app.

---

## C3. 👥 Gestió de rols d’usuari i permisos

### 1️⃣ Objectius (amb mapeig DWEC i DWES)

Implementar un sistema de **gestió de rols i permisos** que permeta diferenciar funcionalitats segons el tipus d’usuari.  
L’aplicació ha de garantir que **només els usuaris autoritzats** poden accedir a determinades rutes, opcions o accions tant al **backend (Laravel)** com al **frontend (Vue 3)**.

**Referències:**

- **DWEC RA4.h:** Control d’accés i gestió de permisos en aplicacions web.
- **DWES RA7.e:** Gestió de seguretat en l’accés a dades i funcionalitats.
- **DWES RA7.f:** Restricció d’operacions segons rols d’usuari.
- **DWES RA7.g:** Validació i protecció d’endpoints d’API.
- **DWES RA7.h:** Implementació d’autenticació i autorització en entorns web.

---

### 2️⃣ Requisits previs

- API Laravel amb **middleware d’autenticació i autorització** (`auth:sanctum`, `can`, `role` o policies).
- Models i relacions de base de dades:
  - `users`
  - `roles`
  - `role_user` (taula pivot)
- Rols principals:
  - **Administrador (gerent):** accés complet a l’aplicació i a la gestió de tots els recursos.
  - **Venedor:** pot crear, editar i eliminar els seus propis productes.
  - **Editor:** gestiona comentaris i continguts publicats per altres usuaris.
  - **Usuari bàsic:** accés només a funcionalitats públiques o de consulta.
- Front-end Vue 3 amb **Pinia**, **Axios**, **Vue Router** i components visuals condicionals segons el rol.

---

### 3️⃣ Estructura de projecte (mòdul `roles`)

```text
src/
├─ modules/
│  ├─ roles/
│  │  ├─ composables/
│  │  │  └─ useRole.js            # composable amb helpers de verificació de rols
│  │  ├─ components/
│  │  │  ├─ RoleGuard.vue         # mostra o oculta contingut segons rol/permisos
│  │  │  └─ RoleBadge.vue         # etiqueta visual del rol (Admin, Vendor, etc.)
│  │  ├─ views/
│  │  │  └─ RoleManagementView.vue (per a admins/gerents)
│  │  ├─ store.js                 # Pinia store per a rols i permisos (opcional)
│  │  └─ api.js                   # crides Axios per obtindre/modificar rols (opcional)
│  └─ ...
├─ router/
│  └─ guards/roleGuard.js         # redirecció segons permisos de l’usuari
└─ services/
   └─ http.js                     # instància Axios amb interceptors i auth
```

> **DWES RA7.e–RA7.h:** estructura modular que separa la lògica d’autorització i evita accessos no autoritzats des del client.

---

### 4️⃣ Model de rols i permisos

| Rol | Descripció | Accions permeses |
|---|---|---|
| **Administrador / Gerent** | Control total de l’aplicació | CRUD complet, gestió d’usuaris, productes i comentaris |
| **Venedor** | Administra els seus productes | Crear, editar i eliminar productes propis |
| **Editor** | Gestiona contingut i comentaris | Moderar i eliminar comentaris, editar descripcions |
| **Usuari** | Consumidor final | Consultar productes, comentar, editar perfil |

---

### 5️⃣ Flux d’autorització al backend (Laravel)

1. **Middleware `auth:sanctum`** valida la sessió o el token.
2. Cada endpoint incorpora **polítiques (Policy)** o middleware `role:` que limiten l’accés segons el rol.
3. Els controladors Laravel criden mètodes com `authorize('update', $product)` o `Gate::allows(...)`.
4. El backend respon amb codi `403 Forbidden` si l’usuari no té permisos suficients.

> **DWES RA7.g:** protecció granular d’endpoints de l’API per rols i accions.

---

### 6️⃣ Flux d’autorització al frontend (Vue 3)

1. Després del login, el servidor envia el **rol de l’usuari** dins del token o dins de l’objecte `user`.
2. El `authStore` guarda `user.role` (Pinia).
3. El router utilitza un **guard de rol** abans d’accedir a rutes restringides:

```js
router.beforeEach((to, from, next) => {
  const auth = useAuthStore()

  // Si la ruta defineix rols permesos i el rol actual no està dins
  if (to.meta.roles && !to.meta.roles.includes(auth.user?.role)) {
    next('/forbidden')
  } else {
    next()
  }
})
```

4. En components, s’utilitza `v-if="can('delete')"` o un component `<RoleGuard>` per amagar funcionalitats no permeses.

> **DWEC RA4.h / DWES RA7.f:** gestió visual i lògica dels permisos a nivell de component i ruta.

---

### 7️⃣ Composable `useRole.js`

```js
import { storeToRefs } from 'pinia'
import { useAuthStore } from '@/modules/auth/store'

export function useRole() {
  // Convertim propietats del store a refs reactives
  const { user } = storeToRefs(useAuthStore())

  const can = (permission) => {
    // Llegim el rol de l’usuari actual
    const role = user.value?.role

    const rules = {
      admin: ['create', 'edit', 'delete', 'moderate'],
      vendor: ['create', 'edit', 'delete'],
      editor: ['moderate'],
      user: ['read']
    }

    // Retorna true si el permís està dins de les regles del rol
    return rules[role]?.includes(permission) ?? false
  }

  return { can }
}
```

**Exemple d’ús en un component Vue (SFC):**

```vue
<script setup>
import { useRole } from '@/modules/roles/composables/useRole'

const { can } = useRole()
</script>

<template>
  <!-- Si el rol ho permet, apareix el botó -->
  <button v-if="can('delete')">Eliminar</button>
</template>
```

> **DWEC RA4.h:** encapsulació de la lògica d’autorització per a ús en tota la interfície.

---

### 8️⃣ Components de control visual

- **`<RoleGuard>`:** component d’ordre superior per ocultar contingut segons permisos.
- **`<RoleBadge>`:** etiqueta visual que indica el rol actual.
- **Menús dinàmics:** elements del menú principal controlats per `v-if="auth.user?.role === 'admin'"`.

> **DWES RA7.h:** retroalimentació visual clara segons el nivell d’autorització.

---

### 9️⃣ Testing i validació

- **Tests unitaris (Vitest):** verificació de `useRole().can()` per a cada tipus d’usuari.
- **Tests d’integració:** comprovació de visibilitat d’opcions en components segons rol.
- **E2E (Cypress o Playwright):** comprovació d’accés restringit a rutes protegides i flux de login real.
- **Simulacions d’API:** respostes 403 i redireccions automàtiques.

---

### 🔟 Bones pràctiques de seguretat

- No confiar en la validació del front-end: totes les restriccions també s’apliquen al backend.
- Limitar la informació retornada per l’API segons rol (principi de mínim privilegi).
- Verificar rols a cada petició (`authorize`, `Gate`, `Policy`).
- Controlar excepcions i mostrar missatges d’error clars però no massa detallats (per evitar fugues d’informació).

---

### 1️⃣1️⃣ Estat del desenvolupament

#### 🟦 To Do

- Definir taules i relacions de rols al backend (Laravel).
- Crear middleware i policies per al control d’accés.
- Configurar `meta.roles` a les rutes Vue.
- Dissenyar components `RoleGuard` i `RoleBadge`.

#### 🟨 In Progress

- Implementació del **composable `useRole()`** i proves de permisos.
- Integració amb el **Pinia `authStore`** per llegir el rol autenticat.
- Control visual de menús i seccions segons rol.
- Validació de respostes 403 i tractament d’errors al client.

#### 🟩 Done

- Model base de rols creat a Laravel i associacions correctes.
- Assignació de rols a usuaris i proves amb API REST.
- Control d’accés funcional en rutes i components Vue.
- Gestió visual coherent segons el rol d’usuari.
