<!-- STRUCTURE DU PROJET -->
lifecard-cnsu/
├── src/
│   ├── lib/
│   │   ├── components/
│   │   │   ├── ui/                      # Composants UI réutilisables (boutons, cards, etc.)
│   │   │   ├── auth/                    # Composants d'authentification
│   │   │   │   ├── LoginForm.svelte
│   │   │   │   ├── RegisterForm.svelte
│   │   │   │   └── RoleSelector.svelte
│   │   │   ├── card/                    # Composants liés à la carte NFC/QR
│   │   │   │   ├── QRScanner.svelte
│   │   │   │   ├── NFCReader.svelte
│   │   │   │   └── CardDisplay.svelte
│   │   │   ├── patient/                 # Composants patient
│   │   │   │   ├── EmergencyInfo.svelte
│   │   │   │   ├── MedicalHistory.svelte
│   │   │   │   └── MedicationAlarms.svelte
│   │   │   ├── medecin/                 # Composants médecin
│   │   │   │   ├── PatientDossier.svelte
│   │   │   │   ├── Consultation.svelte
│   │   │   │   └── Prescription.svelte
│   │   │   ├── paramedical/             # Composants personnel auxiliaire
│   │   │   │   ├── VitalSigns.svelte
│   │   │   │   └── NursingNotes.svelte
│   │   │   └── urgence/                 # Composants urgence
│   │   │       └── QuickAccess.svelte
│   │   │
│   │   ├── stores/                      # Stores Svelte (état global)
│   │   │   ├── auth.ts
│   │   │   ├── patient.ts
│   │   │   ├── offline.ts
│   │   │   └── sync.ts
│   │   │
│   │   ├── services/                    # Services métier
│   │   │   ├── nfc.ts                   # Service NFC (WebNFC)
│   │   │   ├── qrcode.ts                # Service QR Code
│   │   │   ├── crypto.ts                # Chiffrement AES-256
│   │   │   ├── offline.ts               # Gestion offline (Service Worker)
│   │   │   ├── sync.ts                  # Synchronisation des données
│   │   │   └── biometric.ts             # Authentification biométrique
│   │   │
│   │   ├── db/                          # Base de données
│   │   │   ├── schema.ts                # Schéma Drizzle ORM
│   │   │   ├── client.ts                # Client SQLite/Turso
│   │   │   └── migrations/              # Migrations
│   │   │
│   │   ├── utils/                       # Utilitaires
│   │   │   ├── permissions.ts           # Gestion des permissions par rôle
│   │   │   ├── validators.ts            # Validation des données
│   │   │   └── formatters.ts            # Formatage des données
│   │   │
│   │   └── types/                       # Types TypeScript
│   │       ├── user.ts
│   │       ├── patient.ts
│   │       ├── medical.ts
│   │       └── card.ts
│   │
│   ├── routes/                          # Routes de l'application
│   │   ├── +page.svelte                 # Page d'accueil
│   │   ├── +layout.svelte               # Layout global (navbar, footer)
│   │   ├── +layout.server.ts            # Layout server-side
│   │   │
│   │   ├── auth/                        # Routes d'authentification
│   │   │   ├── login/
│   │   │   │   └── +page.svelte
│   │   │   ├── register/
│   │   │   │   └── +page.svelte
│   │   │   └── logout/
│   │   │       └── +server.ts
│   │   │
│   │   ├── dashboard/                   # Tableau de bord général
│   │   │   ├── +page.svelte
│   │   │   └── +layout.svelte
│   │   │
│   │   ├── patient/                     # Espace patient
│   │   │   ├── +page.svelte
│   │   │   ├── dossier/
│   │   │   │   └── +page.svelte
│   │   │   ├── medicaments/
│   │   │   │   └── +page.svelte
│   │   │   └── alarmes/
│   │   │       └── +page.svelte
│   │   │
│   │   ├── medecin/                     # Espace médecin
│   │   │   ├── +page.svelte
│   │   │   ├── scanner/
│   │   │   │   └── +page.svelte
│   │   │   ├── consultation/
│   │   │   │   └── +page.svelte
│   │   │   └── patients/
│   │   │       └── [id]/
│   │   │           └── +page.svelte
│   │   │
│   │   ├── paramedical/                 # Espace personnel auxiliaire
│   │   │   ├── +page.svelte
│   │   │   ├── patients/
│   │   │   │   └── [id]/
│   │   │   │       └── +page.svelte
│   │   │   └── soins/
│   │   │       └── +page.svelte
│   │   │
│   │   ├── urgence/                     # Accès urgence (sans auth)
│   │   │   └── +page.svelte
│   │   │
│   │   ├── admin/                       # Administration
│   │   │   ├── +page.svelte
│   │   │   ├── users/
│   │   │   └── cards/
│   │   │
│   │   └── api/                         # API Routes
│   │       ├── nfc/
│   │       │   └── +server.ts
│   │       ├── patients/
│   │       │   ├── +server.ts
│   │       │   └── [id]/
│   │       │       └── +server.ts
│   │       ├── sync/
│   │       │   └── +server.ts
│   │       └── emergency/
│   │           └── [cardId]/
│   │               └── +server.ts
│   │
│   ├── app.html                         # Template HTML racine
│   ├── app.css                          # Styles globaux
│   ├── service-worker.ts                # Service Worker pour PWA
│   └── manifest.json                    # Manifeste PWA
│
├── static/                              # Fichiers statiques
│   ├── icons/                           # Icônes PWA
│   │   ├── icon-192.png
│   │   ├── icon-512.png
│   │   └── favicon.ico
│   ├── fonts/                           # Polices
│   └── images/                          # Images
│
├── tests/                               # Tests
│   ├── unit/
│   └── integration/
│
├── drizzle/                             # Configuration Drizzle
│   └── migrations/
│
├── .env                                 # Variables d'environnement
├── .env.example
├── drizzle.config.ts                    # Config Drizzle
├── svelte.config.js                     # Config SvelteKit
├── vite.config.ts                       # Config Vite
├── tailwind.config.js                   # Config Tailwind
├── package.json
├── tsconfig.json
└── README.md




# Svelte library

Everything you need to build a Svelte library, powered by [`sv`](https://npmjs.com/package/sv).

Read more about creating a library [in the docs](https://svelte.dev/docs/kit/packaging).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```sh
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

To recreate this project with the same configuration:

```sh
# recreate this project
npx sv@0.15.3 create --template library --types ts --add prettier eslint vitest="usages:unit,component" tailwindcss="plugins:typography,forms" sveltekit-adapter="adapter:node" better-auth="demo:password" drizzle="database:sqlite+sqlite:libsql" --install npm lifecard
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

Everything inside `src/lib` is part of your library, everything inside `src/routes` can be used as a showcase or preview app.

## Building

To build your library:

```sh
npm pack
```

To create a production version of your showcase app:

```sh
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.

## Publishing

Go into the `package.json` and give your package the desired name through the `"name"` option. Also consider adding a `"license"` field and point it to a `LICENSE` file which you can create from a template (one popular option is the [MIT license](https://opensource.org/license/mit/)).

To publish your library to [npm](https://www.npmjs.com):

```sh
npm publish
```

#   L i f e C a r d  
 