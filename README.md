# SafeChat — Privacy-Preserving Family Safety & Cyberbullying Protection

SafeChat is an AI-assisted, privacy-first family safety platform designed to protect children from online harms—including cyberbullying, social coercion, predatory behavior, and doxxing—while honoring their personal privacy through a zero-raw-message architecture.

---

## Key Features

### 1. Zero-Raw-Message Privacy Architecture
- **Client-Side & Edge Redaction**: Automatically scrubs personally identifiable information (phone numbers, physical addresses, emails, passwords, and sensitive tokens) before behavioral analysis.
- **Behavioral Signal Extraction**: Analyzes interaction patterns (coercion, secrecy demands, channel migration, exclusion) rather than exposing verbatim private conversations to parents.
- **Child Trust Model**: The child's device interface remains a clean, respectful chat environment with no intrusive scoring or surveillance overlays.

### 2. Family Safety Pulse & Risk Concentration
- **Executive Status**: High-level, parent-friendly status indicators (*Good* vs. *Attention Needed*) with live protection metrics.
- **Dynamic Risk Concentration**: Real-time breakdown of threat exposure across monitored channels:
  - Gaming Platforms (Discord, Steam)
  - School & Class Group Chats
  - Unknown Contacts & Direct Messages
  - Social Media Networks
- **Child Profiles**: Individual safety cards displaying current status, active devices, last synchronization, and overall risk levels.

### 3. Comprehensive Incident & Threat Forensics
- **Deep Threat Analysis**: Risk severity scoring (Low, Medium, High, Critical) with pattern breakdown.
- **Contextual Behavioral Timeline**: Chronological events and flagged triggers without leaking raw transcripts.
- **Actionable Parental Guidance**:
  - Empathetic conversation starters for discussing digital safety with children.
  - School and group mediation letter templates.
  - Device security and safety escalation steps.

### 4. Synthetic Test Conversation Studio
- **Pre-Built Scenarios**:
  - *Cyberbullying & Exclusion*: Hostile peer pressure and targeted harassment.
  - *Coercion & Doxxing Threats*: Account takeover, extortion, and location threats.
  - *Grooming & Secrecy Demands*: Off-platform migration and secrecy cues.
  - *Safe Baseline*: Normal peer collaboration and study discussions.
- **Interactive Multi-Turn Builder**: Add sender and child messages, specify channels, and instantly run AI behavioral assessments.
- **Safe Isolation**: All test data is strictly tagged (`is_test_data: true`), isolating test simulations from production telemetry.

### 5. Child Device Simulator
- **Realistic Mobile Preview**: Interactive smartphone simulator displaying simulated child messaging.
- **Two Operational Modes**:
  - *Child Screen View*: Verifies the child experience remains private, normal, and non-intrusive.
  - *Telemetry Ingestion*: Simulates real-time event dispatching and verifies parent alert triggers.

### 6. Secure Device Pairing
- **6-Digit Pairing Codes**: Time-limited cryptographic pairing system to safely connect new children's mobile devices and tablets.
- **Multi-Child Support**: Manage multiple children and devices from a unified parent account.

---

## Architecture & Tech Stack

```
├── src/
│   ├── components/            # React UI components
│   │   ├── FamilyOverview.tsx           # Main family safety dashboard
│   │   ├── ChildProtectionView.tsx      # Child-specific safety details
│   │   ├── ThreatForensicsView.tsx      # Detailed incident investigation
│   │   ├── ChildDeviceSimulator.tsx     # Simulated mobile child view
│   │   ├── CreateTestConversationModal.tsx # Synthetic test scenario builder
│   │   ├── AddChildPairingModal.tsx     # 6-digit device pairing flow
│   │   └── ParentAccountSettingsModal.tsx
│   ├── lib/
│   │   ├── privacyFilter.ts   # PII scrubbing & data sanitization
│   │   └── riskEngine.ts      # Behavioral risk classification & heuristics
│   ├── types.ts               # Shared TypeScript domain interfaces
│   ├── App.tsx                # Main application orchestrator
│   └── main.tsx               # Frontend client entry point
├── server.ts                  # Express backend & API proxy server
└── dist/                      # Production build assets
```

### Technologies

- **Frontend**:
  - [React 19](https://react.dev/) + [TypeScript](https://www.typescriptlang.org/)
  - [Vite](https://vitejs.dev/) for fast asset compilation and bundling
  - [Tailwind CSS v4](https://tailwindcss.com/) for modern styling
  - [Lucide React](https://lucide.dev/) for icons
  - [Recharts](https://recharts.org/) for analytics and risk distribution charts
  - [Motion](https://motion.dev/) for fluid UI transitions
- **Backend**:
  - [Express](https://expressjs.com/) REST API on Node.js
  - [@google/genai SDK](https://www.npmjs.com/package/@google/genai) for behavioral safety analysis
  - Built-in in-memory data store for responsive prototyping and live simulations
  - `tsx` and `esbuild` for TypeScript execution and bundling

---

## Getting Started

### Prerequisites

- Node.js (v18 or higher recommended)
- npm or yarn

### Installation

1. **Clone or extract the repository**:
   ```bash
   git clone <repository-url>
   cd safechat
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure Environment Variables**:
   Copy `.env.example` to `.env` and configure your API keys if using server-side AI evaluation:
   ```bash
   cp .env.example .env
   ```
   Add your Gemini API key:
   ```env
   GEMINI_API_KEY=your_gemini_api_key_here
   ```
   *(Note: SafeChat includes robust local heuristic fallbacks so all synthetic scenarios and dashboards function even without an external API key).*

### Running Locally

To run both the backend server and frontend development server:

```bash
npm run dev
```

The application will start on **`http://localhost:3000`**.

### Building for Production

To create an optimized production build:

```bash
npm run build
```

To run the production server:

```bash
npm run start
```

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/parent/me` | Fetch active parent account and notification settings |
| `GET` | `/api/parent/children` | Fetch all registered children and protection status |
| `GET` | `/api/incidents` | List detected safety incidents with risk levels |
| `GET` | `/api/incidents/:id` | Get deep incident forensics and parental advice |
| `POST` | `/api/device/chat-event` | Ingest message telemetry from a child device |
| `POST` | `/api/conversations/test-conversation` | Analyze synthetic test conversations |
| `GET` | `/api/analytics/risk-concentration` | Fetch aggregated risk concentration across sources |
| `POST` | `/api/pairing/generate-code` | Generate a 6-digit device pairing code |
| `POST` | `/api/pairing/verify-code` | Verify and pair a child device |

---

## Security & Privacy Highlights

- **Zero Raw Chat Storage**: Verbatim chat text is never permanently stored in unencrypted or raw format for parent viewing.
- **Automatic PII Scrubbing**: Names, addresses, and phone numbers are redacted via `src/lib/privacyFilter.ts` prior to threat evaluation.
- **Parental Guidance, Not Spyware**: The platform guides proactive parent-child conversations rather than covert tracking.
