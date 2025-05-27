---
title: "Mermaid flowchart"
linkTitle: "mermaid flowchart"
weight: 60
---

```mermaid
flowchart LR
    %% Security Tools Section
    subgraph SecurityTools[Security Data Sources]
        direction TB
        A[Firewalls]:::securityTool
        B[Endpoints]:::securityTool
        C[Email Gateways]:::securityTool
        D[Threat Intel Feeds]:::securityTool

        A & B & C & D --> SIEM((SIEM)):::core
    end

    %% Core SOAR Platform
    SIEM -->|Alerts/Incidents| SOAR[FortiSOAR]:::core

    %% SOAR Actions
    SOAR -->|1\. Enrichment|E[Enrichment Services]:::action
    SOAR -->|2\. Ticketing|T[Ticketing System]:::action
    SOAR -->|3\. Alert|Analyst[SOC Team/Stakeholders]:::team
    SOAR -->|4\. Reporting|Dash[Dashboards]:::action
    SOAR -->|5\. Response|R[Response Controls]:::action

    %% Integration Details
    subgraph Integrations[Integrations]
        direction TB
        ThreatIntel[Threat Intel APIs]:::integration
        ITSM[ITSM Platform]:::integration
        Firewalls2[Firewall/NGFW]:::integration
        EDR[EDR Solution]:::integration
    end

    %% Integration Connections
    E -.->|Enrich IOCs| ThreatIntel
    T -.->|Track Cases| ITSM
    R -.->|Block Traffic| Firewalls2
    R -.->|Isolate Hosts| EDR

    %% Styling
    classDef core fill:#2d5a88,stroke:#1a365d,stroke-width:2px,color:#fff,rx:10
    classDef securityTool fill:#ff9999,stroke:#cc0000,stroke-width:2px,rx:5
    classDef action fill:#99ccff,stroke:#0066cc,stroke-width:2px,rx:5
    classDef team fill:#99ff99,stroke:#009900,stroke-width:2px,rx:5
    classDef integration fill:#ffcc99,stroke:#ff9933,stroke-width:2px,rx:5

    %% Subgraph Styling
    style SecurityTools fill:#fff4f4,stroke:#ff6666,stroke-width:2px
    style Integrations fill:#fff9f0,stroke:#ffb366,stroke-width:2px

    %% Link Styling
    linkStyle default stroke:#666,stroke-width:2px
    linkStyle 0,1,2,3,4 stroke:#2d5a88,stroke-width:3px
    linkStyle 5,6,7,8,9 stroke:#ff9933,stroke-width:2px,stroke-dasharray: 5 5
```

This is a high-level overview of the FortiSOAR architecture. The platform integrates with various security tools and data sources, enriches alerts, and automates response actions. The SOC team interacts with the platform to manage incidents and generate reports. The great part about FortiSOAR is its ability to integrate with **third-party tools** and platforms, enabling seamless data sharing and response actions.
