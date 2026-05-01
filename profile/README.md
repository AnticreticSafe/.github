<!-- Banner -->
![AnticreticSafe Banner](https://capsule-render.vercel.app/api?type=rect&color=0f172a&height=140&section=header&text=AnticreticSafe&fontSize=46&fontColor=f8fafc)

<!-- Badges -->
[![Vite](https://img.shields.io/badge/Vite-5.x-0f172a?logo=vite&logoColor=white)](https://vitejs.dev/) [![React](https://img.shields.io/badge/React-19.x-0f172a?logo=react&logoColor=white)](https://react.dev/) [![TypeScript](https://img.shields.io/badge/TypeScript-5.x-0f172a?logo=typescript&logoColor=white)](https://www.typescriptlang.org/) [![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.x-0f172a?logo=tailwindcss&logoColor=white)](https://tailwindcss.com/) [![Solidity](https://img.shields.io/badge/Solidity-0.8+-0f172a?logo=solidity&logoColor=white)](https://docs.soliditylang.org/) [![Nox](https://img.shields.io/badge/iExec%20Nox-privacy-0f172a)](https://docs.iex.ec/nox-protocol)

AnticreticSafe is a confidential real-estate dApp built for the iExec Vibe Coding Challenge. It demonstrates how the Nox protocol and confidential tokens enable a full anticretic agreement workflow while keeping sensitive financial data private.

This repository is packaged as a monolithic delivery for the hackathon: UI, smart contracts, ABIs, hooks and product docs are present and ready for review.

## Quick Links

- Front-end entry: [front-end/src/main.tsx](../../front-end/src/main.tsx)
- App shell: [front-end/src/App.tsx](../../front-end/src/App.tsx)
- Core pages: [front-end/src/pages/LandingPage.tsx](../../front-end/src/pages/LandingPage.tsx), [front-end/src/pages/CreateAgreementPage.tsx](../../front-end/src/pages/CreateAgreementPage.tsx), [front-end/src/pages/AgreementDetailPage.tsx](../../front-end/src/pages/AgreementDetailPage.tsx)
- Contracts: [front-end/contracts/AnticreticSafe.sol](../../front-end/contracts/AnticreticSafe.sol), [front-end/contracts/AnticreticSafeUSD.sol](../../front-end/contracts/AnticreticSafeUSD.sol)
- ABIs: [front-end/src/abi](../../front-end/src/abi)
- Docs: [front-end/src/documents/Details.md](../../front-end/src/documents/Details.md), [front-end/src/documents/NoxDocumentation.md](../../front-end/src/documents/NoxDocumentation.md)

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

1. The user lands on a product page that frames the use case and routes into the demo.
2. A dashboard summarizes agreements by role and status.
3. The owner creates a new agreement by hashing the property description and submitting the core metadata.
4. Both parties progress through the agreement lifecycle, uploading hashes for legal documents and approvals.
5. The confidential finance step mints asUSD and records the encrypted amount through the Nox flow.
6. The agreement detail view shows timeline, documents, activity, and the next action for each role.

## Main Implementation Areas

- Front-end entry points: [src/main.tsx](../../front-end/src/main.tsx), [src/App.tsx](../../front-end/src/App.tsx)
- Core pages: [LandingPage.tsx](../../front-end/src/pages/LandingPage.tsx), [DashboardPage.tsx](../../front-end/src/pages/DashboardPage.tsx), [CreateAgreementPage.tsx](../../front-end/src/pages/CreateAgreementPage.tsx), [AgreementDetailPage.tsx](../../front-end/src/pages/AgreementDetailPage.tsx)
- Web3 and confidential flows: [src/hooks](../../front-end/src/hooks), [src/components/web3](../../front-end/src/components/web3)
- Domain UI: [src/components/agreement](../../front-end/src/components/agreement), [src/components/dashboard](../../front-end/src/components/dashboard), [src/components/landing](../../front-end/src/components/landing)
- Contracts and ABIs: [contracts](../../front-end/contracts), [src/abi](../../front-end/src/abi)
- Product docs: [src/documents/Details.md](../../front-end/src/documents/Details.md), [src/documents/NoxDocumentation.md](../../front-end/src/documents/NoxDocumentation.md)

## Stack

- React 19
- TypeScript
- Vite
- Tailwind CSS
- wagmi and viem
- iExec Nox packages
- Solidity smart contracts

## Notes For Judges

- The project is built around the iExec Nox confidentiality model.
- The UI is intentional and demo-friendly, but the evaluation value is in the contract flow, confidential token handling, and role-based agreement lifecycle.
- The testnet target shown in the app is Arbitrum Sepolia.
- The codebase includes mocked agreement data for demo navigation, plus the implementation surfaces needed for real on-chain integration.

## Run Locally

From the project root:

```bash
cd front-end
npm install
npm run dev
```

## For Fast Review

If you only have a few minutes, start here:

- [Landing page](../../front-end/src/pages/LandingPage.tsx)
- [Agreement creation flow](../../front-end/src/pages/CreateAgreementPage.tsx)
- [Confidential finance flow](../../front-end/src/pages/AgreementDetailPage.tsx)
- [Nox concept guide](../../front-end/src/documents/NoxDocumentation.md)

## Project Summary

AnticreticSafe is a confidential anticretic agreement platform for real-estate workflows on Arbitrum Sepolia. It shows how iExec Nox can be used to keep private amounts encrypted while preserving a readable, end-to-end agreement lifecycle for both parties and for judges evaluating the solution.
