# 🧬 NovaMaterial

> **The Operating System for Material Truth.**
> The engine for Digital Product Passports (DPP), material lineage tracking, and circular supply chain transparency.

[](https://www.google.com/search?q=https://github.com/novaeco-tech/novamaterial/actions)
[](https://opensource.org/licenses/MIT)
[](https://www.google.com/search?q=https://materials.novaeco.tech)

**NovaMaterial** is the Horizontal Enabler responsible for the **Identity of Atoms**. While `NovaIdentity` tracks *people*, **NovaMaterial** tracks *matter*.

It generates and hosts **Digital Product Passports (DPP)**—secure, immutable records that travel with a product from extraction to manufacturing (`NovaMake`), through usage (`NovaRetail`), and finally to recovery (`NovaRecycle`). It creates the "Digital Twin" required by the **EU Ecodesign for Sustainable Products Regulation (ESPR)**.

-----

## 🎯 Value Proposition

In a linear economy, products are "black boxes"—we don't know what chemicals are inside or where the metal came from. **NovaMaterial** turns on the lights:

1.  **Regulatory Compliance:** Automatically generating compliant JSON-LD passports for batteries, textiles, and construction products (ESPR ready).
2.  **Trustless Sourcing:** Proving that a batch of recycled plastic in `NovaTrade` is actually "Food Grade" via cryptographic lineage, not just a paper certificate.
3.  **Value Retention:** A building with a detailed Material Passport (`NovaBuild`) is a "Material Bank"; one without is just a future demolition cost.

-----

## 🏗️ Architecture (The Thread of Truth)

NovaMaterial acts as a graph database, linking raw materials to components, and components to finished goods (Bill of Materials - BOM).

```mermaid
graph TD
    User((Designer)) -->|1. Create Spec| UI[NovaMaterial Dashboard]
    UI -->|REST| API[NovaMaterial API]
    
    subgraph "The Input (Creation)"
        API -->|Register Batch| Make[NovaMake / NovaTextile]
        Make -->|Send Composition| API
    end

    subgraph "The Enrichment Layer"
        API -->|Request Impact| Worker[Worker-LCA (NovaBalance)]
        Worker -->|Verified CO2| API
        API -->|Check Hazards| Policy[NovaPolicy]
    end

    subgraph "The Lifecycle (Updates)"
        Retail[NovaRetail] -->|Update: In Use| API
        Recycle[NovaRecycle] -->|Update: Recovered| API
        Trade[NovaTrade] -->|Read: Value| API
    end
```

### Integrated Services

  * **[NovaBalance](https://www.google.com/search?q=https://balance.novaeco.tech):** The auditor. NovaMaterial sends the BOM (Bill of Materials) to the `LCACalc` worker. It receives back a verified Carbon Footprint to stamp onto the passport.
  * **[NovaPolicy](https://www.google.com/search?q=https://compliance.novaeco.tech):** The screener. Checks the chemical list against REACH databases. If a "Forever Chemical" (PFAS) is found, the Passport is flagged with a warning.
  * **[NovaRecycle](https://www.google.com/search?q=https://recycling.novaeco.tech):** The closer. When a product is shredded, NovaRecycle terminates the old Passport and spawns new Passports for the recovered raw materials.

-----

## ✨ Key Features

### 1\. The Passport Generator (DPP)

Generates a public-facing URL and QR code for every item.

  * **Standards:** Outputs data in **GS1 Digital Link** and **W3C JSON-LD** format.
  * **Transparency:** Consumers scan the QR to see "Who made this?", "Is it recyclable?", and "How do I fix it?"

### 2\. Recursive BOM Tracking

Handles the complexity of nested assemblies.

  * *Example:* A Car (`NovaMake`) contains a Battery (`NovaTronix`). The Battery contains Cobalt (`NovaRecycle`).
  * NovaMaterial maintains the graph links so that an update to the Cobalt's provenance automatically updates the Car's sustainability score.

### 3\. Chain of Custody (CoC)

Tracks ownership transfer via `NovaTrade`.

  * **Mass Balance:** Ensures that if you buy 1 ton of "Certified Organic Cotton," you cannot sell 2 tons of products made from it.
  * Prevents "Greenwashing" by strictly linking output volume to input volume.

### 4\. Circularity Metrics

Calculates the **Material Circularity Indicator (MCI)**.

  * **Formula:** Input from Recycled Sources vs. Virgin Feedstock.
  * **Output:** A score (0.0 - 1.0) stamped on the passport, determining the product's tax rating in `NovaPolicy`.

-----

## 🚀 Getting Started

We use **DevContainers** to provide a consistent development environment.

### Prerequisites

  * Docker Desktop
  * VS Code (with Remote Containers extension)

### Installation

1.  **Clone the repo:**
    ```bash
    git clone https://github.com/novaeco-tech/novamaterial.git
    cd novamaterial
    ```
2.  **Open in VS Code:**
      * Run `code .`
      * Click **"Reopen in Container"** when prompted.
3.  **Start the Enabler:**
    ```bash
    make dev
    ```
      * **Passport Viewer:** http://localhost:3000
      * **API:** http://localhost:8000/docs

### Configuration (`.env`)

```ini
# DPP Standards
STANDARD_VERSION=ESPR_2026_DRAFT
URI_PREFIX=https://id.novaeco.tech/

# Integrations
NOVABALANCE_WORKER_URL=http://novabalance-worker-lca-calculator:8080
NOVAPOLICY_URL=http://novapolicy-api:8000
```

-----

## 📂 Repository Structure

This is a Monorepo containing the enabler's specific logic.

```text
novamaterial/
├── api/                # Python/FastAPI (Domain Logic)
│   ├── src/
│   │   ├── passport/   # JSON-LD generators and QR code logic
│   │   ├── graph/      # NetworkX logic for BOM traversal
│   │   └── coc/        # Chain of Custody ledger logic
├── app/                # React/Next.js Frontend (Passport Manager)
│   ├── src/
│   │   ├── viewer/     # Public-facing Passport UI
│   │   └── builder/    # Admin UI for defining BOMs
├── website/            # Documentation (Docusaurus)
└── tests/              # Integration tests
```

-----

## 🧪 Testing

We use **Graph Validation** for testing.

  * **Schema Test:** `make test-dpp`
      * Generates a sample Passport and validates it against the official EU JSON schema.
  * **Traceability Test:** `make test-trace`
      * Simulates a supply chain of 3 tiers. Updates a raw material at Tier 3 and asserts that the Tier 1 product reflects the change (e.g., "Contains Conflict Minerals").

-----

## 🤝 Contributing

We need contributors with backgrounds in **Supply Chain**, **Linked Data (Semantic Web)**, and **Materials Science**.
See [CONTRIBUTING.md](https://www.google.com/search?q=../.github/CONTRIBUTING.md) for details.

**Maintainers:** `@novaeco-tech/maintainers-enabler-novamaterial`