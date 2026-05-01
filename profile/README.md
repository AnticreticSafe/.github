<!-- Banner -->
![AnticreticSafe Banner](https://capsule-render.vercel.app/api?type=rect&color=0f172a&height=140&section=header&text=AnticreticSafe&fontSize=46&fontColor=f8fafc)

<!-- Badges -->
[![Vite](https://img.shields.io/badge/Vite-5.x-0f172a?logo=vite&logoColor=white)](https://vitejs.dev/) [![React](https://img.shields.io/badge/React-19.x-0f172a?logo=react&logoColor=white)](https://react.dev/) [![TypeScript](https://img.shields.io/badge/TypeScript-5.x-0f172a?logo=typescript&logoColor=white)](https://www.typescriptlang.org/) [![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.x-0f172a?logo=tailwindcss&logoColor=white)](https://tailwindcss.com/) [![Solidity](https://img.shields.io/badge/Solidity-0.8+-0f172a?logo=solidity&logoColor=white)](https://docs.soliditylang.org/) [![Nox](https://img.shields.io/badge/iExec%20Nox-privacy-0f172a)](https://docs.iex.ec/nox-protocol) [![Live Demo](https://img.shields.io/badge/Live%20Demo-Open-00c853?logo=vercel&logoColor=white)](https://anticreticsafe.vercel.app/)

AnticreticSafe is a confidential real-estate dApp built for the iExec Vibe Coding Challenge. It demonstrates how the Nox protocol and confidential tokens enable a full anticretic agreement workflow while keeping sensitive financial data private.

This repository is packaged as a monolithic delivery for the hackathon: UI, smart contracts, ABIs, hooks and product docs are present and ready for review.

## Quick Links

- Live demo: https://anticreticsafe.vercel.app/
- Front-end entry: https://github.com/AnticreticSafe/front-end/blob/main/src/main.tsx
- App shell: https://github.com/AnticreticSafe/front-end/blob/main/src/App.tsx
- Core pages: https://github.com/AnticreticSafe/front-end/blob/main/src/pages/LandingPage.tsx, https://github.com/AnticreticSafe/front-end/blob/main/src/pages/CreateAgreementPage.tsx, https://github.com/AnticreticSafe/front-end/blob/main/src/pages/AgreementDetailPage.tsx
- Contracts: https://github.com/AnticreticSafe/front-end/blob/main/contracts/AnticreticSafe.sol, https://github.com/AnticreticSafe/front-end/blob/main/contracts/AnticreticSafeUSD.sol
- ABIs: https://github.com/AnticreticSafe/front-end/tree/main/src/abi
- Feedback: https://github.com/AnticreticSafe/front-end/blob/main/feedback.md

## What The Product Does

AnticreticSafe models the lifecycle of an anticretic agreement, a real-estate arrangement where the occupant provides a deposit and the owner transfers temporary possession of the property.

The application lets the parties:

- create an agreement on-chain,
- hash and register sensitive property documentation,
- track the agreement state through a structured workflow,
- mint confidential asUSD for the anticretic amount,
- register and read encrypted balances through Nox-enabled flows,
- close the agreement with a complete activity trail.

## Why It Matters

Real-estate and RWA workflows often require public verifiability without exposing private terms. AnticreticSafe shows a practical way to keep addresses and contract actions transparent while protecting confidential amounts and document contents.

This makes the project a good fit for the challenge theme because it combines:

- a real use case with clear business value,
- confidential token mechanics,
- Nox encryption and handle-based flows,
- a polished front-end that can be judged quickly,
- a contract-first architecture that is easy to review.

## End-to-End Flow

```mermaid
graph TD
    A["Landing Page<br/>Product Overview"] -->|User Action| B["Connect Wallet<br/>Arbitrum Sepolia"]
    B -->|Select Role| C{Owner or<br/>Occupant?}
    C -->|Owner| D["Create Agreement<br/>Hash Property Data"]
    C -->|Either| E["Dashboard<br/>View My Agreements"]
    D -->|Submit On-Chain| F["AnticreticSafe Contract<br/>State: Created"]
    E -->|Select Agreement| G["Agreement Detail Page<br/>View Timeline"]
    F -->|Upload Documents| H["Register Hashes<br/>Title Report, Contract"]
    H -->|Both Approve| I["State: ApprovedByParties"]
    I -->|Mint Confidential Amount| J["AnticreticSafeUSD<br/>Nox Mint Flow"]
    J -->|Register Encrypted| K["Nox Precompile<br/>euint256 Registration"]
    K -->|Update State| L["State: ConfidentialAmountRegistered"]
    L -->|Complete Workflow| M["State: Active → Closed<br/>with Activity Trail"]
    G -.->|View Activity| M
```

1. The user lands on a product page that frames the use case and routes into the demo.
2. A dashboard summarizes agreements by role and status.
3. The owner creates a new agreement by hashing the property description and submitting the core metadata.
4. Both parties progress through the agreement lifecycle, uploading hashes for legal documents and approvals.
5. The confidential finance step mints asUSD and records the encrypted amount through the Nox flow.
6. The agreement detail view shows timeline, documents, activity, and the next action for each role.

## Main Implementation Areas

```mermaid
graph TB
    subgraph "Pages"
        LP["Landing Page<br/>Product intro"]
        DP["Dashboard Page<br/>My agreements"]
        CAP["Create Agreement Page<br/>New anticretic"]
        ADP["Agreement Detail Page<br/>Full lifecycle"]
    end
    
    subgraph "Components"
        AC["Agreement Components<br/>Header, Tabs, Progress,<br/>Activity, Docs"]
        DC["Dashboard Components<br/>Summary, Stats, Timeline"]
        LC["Landing Components<br/>Hero, Problem, Solution,<br/>How it Works"]
        W3C["Web3 Components<br/>WalletConnect,<br/>MintPanel,<br/>RegisterPanel"]
    end
    
    subgraph "Hooks & Logic"
        H1["useMyAgreements<br/>useAgreementProgress<br/>useNextAction"]
        H2["useMintConfidentialAsUSD<br/>useRegisterConfidentialAmount<br/>useConfidentialAsUSDBalance"]
        H3["useAgreementWriter<br/>useNoxEncrypt<br/>useConnectedRole"]
    end
    
    subgraph "Chain Layer"
        SC["Smart Contracts<br/>AnticreticSafe<br/>AnticreticSafeUSD"]
        NOX["Nox Protocol<br/>Confidential Compute"]
    end
    
    LP --> LC
    DP --> DC
    CAP --> AC
    ADP --> AC
    
    AC --> H1
    AC --> H2
    DC --> H1
    W3C --> H2
    
    H1 --> H3
    H2 --> H3
    
    H3 --> SC
    SC --> NOX
    
    style LP fill:#0f172a,color:#f8fafc,stroke:#7c3aed
    style DP fill:#0f172a,color:#f8fafc,stroke:#7c3aed
    style CAP fill:#0f172a,color:#f8fafc,stroke:#7c3aed
    style ADP fill:#0f172a,color:#f8fafc,stroke:#7c3aed
    style SC fill:#1e293b,color:#f8fafc,stroke:#06b6d4
    style NOX fill:#1e293b,color:#f8fafc,stroke:#06b6d4
```

- Front-end entry points: [src/main.tsx](front-end/src/main.tsx), [src/App.tsx](front-end/src/App.tsx)
- Core pages: [LandingPage.tsx](front-end/src/pages/LandingPage.tsx), [DashboardPage.tsx](front-end/src/pages/DashboardPage.tsx), [CreateAgreementPage.tsx](front-end/src/pages/CreateAgreementPage.tsx), [AgreementDetailPage.tsx](front-end/src/pages/AgreementDetailPage.tsx)
- Web3 and confidential flows: [hooks/](front-end/src/hooks), [components/web3/](front-end/src/components/web3)
- Domain UI: [components/agreement/](front-end/src/components/agreement), [components/dashboard/](front-end/src/components/dashboard), [components/landing/](front-end/src/components/landing)
- Contracts and ABIs: [contracts/](front-end/contracts), [src/abi/](front-end/src/abi)
- Product docs: [Documents/Details.md](Documents/Details.md), [NoxDocumentation.md](front-end/src/documents/NoxDocumentation.md)

## Blockchain Architecture

### Contract Interaction Model

```mermaid
graph LR
    subgraph "Smart Contracts"
        AS["AnticreticSafe<br/>Lifecycle Manager<br/>12-State Workflow"]
        ASU["AnticreticSafeUSD<br/>ERC-7984 Token<br/>Confidential Balance"]
    end
    
    subgraph "Nox Confidential Layer"
        NOX["Nox Precompile<br/>euint256 Encryption<br/>Handle-Based Access"]
    end
    
    subgraph "Frontend Integration"
        HOOKS["Custom React Hooks<br/>useAgreementProgress()<br/>useMintConfidentialAsUSD()<br/>useRegisterConfidentialAmount()"]
        UI["UI Components<br/>AgreementDetailPage<br/>ConfidentialFinancePanel"]
    end
    
    AS -->|"Calls mint/burn"| ASU
    ASU -->|"Encrypts amounts"| NOX
    NOX -->|"Handles secrets"| ASU
    AS -->|"Manages state"| HOOKS
    HOOKS -->|"Renders"| UI
    UI -->|"Calls hooks"| HOOKS
    
    style AS fill:#0f172a,color:#f8fafc,stroke:#7c3aed,stroke-width:2px
    style ASU fill:#0f172a,color:#f8fafc,stroke:#7c3aed,stroke-width:2px
    style NOX fill:#1e293b,color:#f8fafc,stroke:#06b6d4,stroke-width:2px
    style HOOKS fill:#312e81,color:#f8fafc,stroke:#8b5cf6
    style UI fill:#312e81,color:#f8fafc,stroke:#8b5cf6
```

### Agreement State Lifecycle

```mermaid
stateDiagram-v2
    [*] --> Created
    Created --> TitleReportUploaded: Owner submits<br/>property hash
    TitleReportUploaded --> ApprovedByParties: Both parties<br/>approve
    ApprovedByParties --> AgreementContractUploaded: Upload agreement<br/>contract hash
    AgreementContractUploaded --> PublicRegistryProofUploaded: Upload registry<br/>proof hash
    PublicRegistryProofUploaded --> ConfidentialAmountRegistered: Mint asUSD &<br/>register encrypted amount
    ConfidentialAmountRegistered --> PossessionDeliveryPending: Prepare delivery
    PossessionDeliveryPending --> Active: Agreement<br/>becomes active
    Active --> MoneyReturned: Occupant returns<br/>funds
    MoneyReturned --> PropertyReturned: Owner returns<br/>property
    PropertyReturned --> Closed: Agreement closes<br/>with activity trail
    
    Active --> Disputed: Conflict or<br/>issue detected
    Disputed --> Closed: Resolution
    
    Closed --> [*]
```

### Smart Contracts

The project features two core smart contracts deployed on **Arbitrum Sepolia**:

#### 1. **AnticreticSafe.sol**
The main agreement lifecycle contract that:
- Manages the complete anticretic agreement workflow through 12 distinct states
- Stores agreement metadata (parties, property hash, document hashes)
- Handles document registration and tracking (title reports, agreements, registry proofs, etc.)
- Integrates with Nox for encrypted amount handling via `euint256`
- Emits events for state transitions and document uploads
- Provides role-based access control for owner and occupant operations

Key structures:
- `AgreementStatus` enum: 12-state lifecycle (Created → Closed/Disputed)
- `Agreement` struct: Centralized state container with all agreement data
- Support for confidential amount management via Nox precompile

#### 2. **AnticreticSafeUSD.sol**
Confidential ERC-7984 token contract that:
- Implements the ERC-7984 standard for confidential balance tracking
- Mints confidential asUSD tokens for agreement amounts
- Burns tokens when agreements close
- Uses Nox encryption primitives (`euint256`, `externalEuint256`)
- Only the contract owner (AnticreticSafe) can mint/burn
- Fully compatible with Nox confidential asset workflows

### Technical Details

- **Solidity Version**: 0.8.28 (EVM Cancun)
- **Chain**: Arbitrum Sepolia (chainId: 421614)
- **Dependencies**:
  - `@iexec-nox/nox-protocol-contracts` - Nox SDK and precompile interfaces
  - `@iexec-nox/nox-confidential-contracts` - ERC-7984 and confidential token standards
  - `@openzeppelin/contracts` (v5.6.1) - Ownable pattern and access control
- **Build Tool**: Hardhat with TypeScript
- **Testing**: Full test suite included (`npm test`)

### Deployment

Deploy to Arbitrum Sepolia:
```bash
cd Contract-Blockchain-ERC7984
npm install
npx hardhat ignition deploy ignition/modules/AnticreticSafeUSD.ts --network arbitrumSepolia
```

See [Contract-Blockchain-ERC7984/README.md](Contract-Blockchain-ERC7984/README.md) for detailed deployment instructions.

### Deployed Contracts

On Arbitrum Sepolia:
- **AnticreticSafe**: `0x40e75D0648BCB2F374dF053DeEa8A70e74699545`
- **AnticreticSafe USD (asUSD)**: `0x5e57022c7dfE939456f2aad9B11153d6beAEC06D`

## Stack

```mermaid
graph LR
    subgraph "Frontend Stack"
        REACT["React 19<br/>Component Framework"]
        TS["TypeScript<br/>Type Safety"]
        VITE["Vite<br/>Build Tool"]
        TAILWIND["Tailwind CSS<br/>Styling"]
    end
    
    subgraph "Web3 Integration"
        WAGMI["wagmi<br/>React Hooks"]
        VIEM["viem<br/>Low-level Client"]
        ABIS["Contract ABIs<br/>Type-safe Interfaces"]
    end
    
    subgraph "Blockchain & Cryptography"
        SOL["Solidity 0.8.28<br/>Smart Contracts"]
        NOX["iExec Nox<br/>Confidential Computing"]
        ERC7984["ERC-7984<br/>Confidential Tokens"]
    end
    
    subgraph "Infrastructure"
        HARDHAT["Hardhat<br/>Development Framework"]
        ARBITRUM["Arbitrum Sepolia<br/>Testnet"]
        IPFS["IPFS<br/>Document Storage Ready"]
    end
    
    REACT --> TS
    TS --> VITE
    VITE --> TAILWIND
    
    REACT --> WAGMI
    WAGMI --> VIEM
    VIEM --> ABIS
    
    ABIS --> SOL
    SOL --> NOX
    NOX --> ERC7984
    
    SOL --> HARDHAT
    HARDHAT --> ARBITRUM
    ARBITRUM --> IPFS
    
    style REACT fill:#087ea4,color:#fff,stroke:#0891b2
    style TS fill:#2563eb,color:#fff,stroke:#1d4ed8
    style VITE fill:#646cff,color:#fff,stroke:#5f5f9f
    style TAILWIND fill:#06b6d4,color:#fff,stroke:#0891b2
    style NOX fill:#7c3aed,color:#fff,stroke:#6d28d9
    style ERC7984 fill:#7c3aed,color:#fff,stroke:#6d28d9
```

### By Layer

**Frontend**:
- React 19 - Modern component framework
- TypeScript - Full type safety
- Vite - Fast build and dev server
- Tailwind CSS - Utility-first styling
- wagmi & viem - Web3 React integration

**Blockchain & Cryptography**:
- Solidity 0.8.28 - Smart contracts
- iExec Nox - Confidential computing protocol
- ERC-7984 - Confidential token standard
- Hardhat - Development and testing framework

**Infrastructure**:
- Arbitrum Sepolia - Testnet deployment
- IPFS-ready - For document storage integration

## Notes For Judges

- The project is built around the iExec Nox confidentiality model.
- The UI is intentional and demo-friendly, but the evaluation value is in the contract flow, confidential token handling, and role-based agreement lifecycle.
- The testnet target shown in the app is Arbitrum Sepolia.
- The app reads and writes live on-chain data for the main workflow.
- See [feedback.md](front-end/feedback.md) for iExec tools usage notes and recommendations.

## User Interaction Flows

```mermaid
graph TD
    START["User Visits App"] -->|"No Wallet"| CONNECT["Connect Wallet<br/>Arbitrum Sepolia"]
    CONNECT -->|"Connected"| ROLE{"Select Role"}
    
    ROLE -->|"Owner"| OWNER_FLOW["Owner Workflow"]
    ROLE -->|"Occupant"| OCC_FLOW["Occupant Workflow"]
    
    OWNER_FLOW --> CREATE["Create Agreement<br/>Hash Property"]
    CREATE --> UPLOAD1["Upload Document Hashes<br/>Title Report"]
    UPLOAD1 --> WAIT["Wait for Occupant"]
    
    OCC_FLOW --> DASH["View Dashboard<br/>See My Agreements"]
    DASH --> SELECT["Select Agreement<br/>from List"]
    SELECT --> APPROVE["Approve Agreement<br/>Sign Off"]
    
    WAIT --> APPROVE
    APPROVE --> BOTH["Both Complete<br/>Next Step"]
    
    BOTH --> UPLOAD2["Upload Agreement<br/>Contract Hash"]
    UPLOAD2 --> UPLOAD3["Upload Registry<br/>Proof Hash"]
    UPLOAD3 --> FINANCE["Confidential Finance<br/>Mint asUSD"]
    
    FINANCE --> REGISTER["Register Encrypted<br/>Amount via Nox"]
    REGISTER --> ACTIVE["Agreement<br/>Becomes Active"]
    
    ACTIVE --> TRACK["Track Activity<br/>View Timeline"]
    TRACK --> CLOSE["Close Agreement<br/>with Proof Trail"]
    CLOSE --> END["✅ Complete"]
    
    style CREATE fill:#0f172a,color:#f8fafc,stroke:#7c3aed
    style FINANCE fill:#1e293b,color:#f8fafc,stroke:#06b6d4
    style REGISTER fill:#1e293b,color:#f8fafc,stroke:#06b6d4
    style ACTIVE fill:#0f7938,color:#f8fafc,stroke:#10b981
    style END fill:#0f7938,color:#f8fafc,stroke:#10b981
```

## Hackathon Compliance

- ✅ End-to-end flow without mocked data in the main path
- ✅ Live demo: https://anticreticsafe.vercel.app/
- ✅ Live contracts on Arbitrum Sepolia (see Deployed Contracts above)
- ✅ iExec tools feedback: https://github.com/AnticreticSafe/front-end/blob/main/feedback.md
- ✅ Nox protocol integration for confidential amounts and encrypted balances
- ✅ ERC-7984 confidential token implementation
- Demo video (<= 4 min): pending link

## Run Locally

From the project root:

```bash
cd front-end
npm install
npm run dev
```

## For Fast Review

If you only have a few minutes, start here:

- https://github.com/AnticreticSafe/front-end/blob/main/src/pages/LandingPage.tsx
- https://github.com/AnticreticSafe/front-end/blob/main/src/pages/CreateAgreementPage.tsx
- https://github.com/AnticreticSafe/front-end/blob/main/src/pages/AgreementDetailPage.tsx
- https://github.com/AnticreticSafe/front-end/blob/main/src/documents/NoxDocumentation.md

## Project Summary

AnticreticSafe is a confidential anticretic agreement platform for real-estate workflows on Arbitrum Sepolia. It shows how iExec Nox can be used to keep private amounts encrypted while preserving a readable, end-to-end agreement lifecycle for both parties and for judges evaluating the solution.
