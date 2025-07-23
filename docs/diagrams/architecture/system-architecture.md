# ChargeX System Architecture

## 🏗️ High-Level Architecture Diagram

```mermaid
graph TB
    subgraph "User Interface Layer"
        UI[React.js Frontend]
        Kiosk[Raspberry Pi Kiosk]
        Mobile[Mobile App]
    end
    
    subgraph "Internet Computer Protocol (ICP)"
        subgraph "Canisters"
            LTC[Leasing & Trading<br/>Canister]
            TDC[Telemetry Data<br/>Canister]
            AIC[AI Inference<br/>Canister]
            UPC[User Profile<br/>Canister]
            NAC[Notification Alert<br/>Canister]
        end
        
        subgraph "ICP Services"
            II[Internet Identity]
            HTTP[HTTPS Outcalls]
            TIMER[Timer Service]
        end
        
        subgraph "Token Standards"
            ICRC7[ICRC-7 NFTs<br/>Battery Tokens]
            CKBTC[ckBTC<br/>Payments]
            ICRC1[ICRC-1/2<br/>Custom Tokens]
        end
    end
    
    subgraph "IoT Hardware Layer"
        subgraph "Battery Monitoring"
            ESP32[ESP32 Monitor]
            SENSORS[Sensors<br/>V/I/T/GPS]
            BMS[Battery Management<br/>System]
        end
        
        subgraph "Physical Infrastructure"
            BATT[Li-ion Batteries]
            STATION[Charging Stations]
            DISP[Dispensing Units]
        end
    end
    
    subgraph "External Services"
        GPS_SVC[GPS Services]
        ALERT_SVC[Push Notifications]
        BACKUP[Data Backup]
    end
    
    %% User Interface Connections
    UI --> II
    UI --> LTC
    UI --> TDC
    UI --> UPC
    Kiosk --> LTC
    Kiosk --> UPC
    Mobile --> NAC
    
    %% Canister Interconnections
    LTC --> ICRC7
    LTC --> CKBTC
    LTC --> ICRC1
    TDC --> AIC
    AIC --> NAC
    UPC --> II
    NAC --> HTTP
    
    %% Hardware Connections
    ESP32 --> SENSORS
    ESP32 --> BMS
    ESP32 --> TDC
    BMS --> BATT
    SENSORS --> GPS_SVC
    
    %% External Service Connections
    HTTP --> ALERT_SVC
    TDC --> BACKUP
    SENSORS --> GPS_SVC
    
    %% Data Flow
    BATT -.->|Power| ESP32
    ESP32 -.->|Telemetry| TDC
    TDC -.->|Analytics| AIC
    AIC -.->|Predictions| NAC
    NAC -.->|Alerts| Mobile
    
    classDef icpCanister fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    classDef hardware fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef token fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef ui fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    
    class LTC,TDC,AIC,UPC,NAC icpCanister
    class ESP32,SENSORS,BMS,BATT,STATION,DISP hardware
    class ICRC7,CKBTC,ICRC1 token
    class UI,Kiosk,Mobile ui
```

## 🔧 Component Details

### Frontend Layer
- **React.js Web App**: Main user interface served from ICP Asset Canister
- **Raspberry Pi Kiosk**: Physical battery dispensing interface
- **Mobile Integration**: Push notifications and mobile-optimized UI

### ICP Canister Layer
- **Leasing & Trading**: Battery lease management and P2P energy trading
- **Telemetry Data**: IoT data storage and real-time processing
- **AI Inference**: On-chain predictive maintenance and analytics
- **User Profile**: User management and preferences
- **Notification Alert**: Alert system and external communications

### Token Standards
- **ICRC-7 NFTs**: Unique battery representation and ownership
- **ckBTC**: Bitcoin-based payments and settlements
- **ICRC-1/2**: Custom tokens for energy trading

### Hardware Layer
- **ESP32 Monitors**: Battery telemetry collection and transmission
- **Sensor Array**: Voltage, current, temperature, and GPS sensors
- **Battery Management**: Safety and charge management systems

## 🔄 Data Flow Architecture

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant LTC as Leasing Canister
    participant TDC as Telemetry Canister
    participant ESP32
    participant Battery
    
    User->>Frontend: Request Battery Lease
    Frontend->>LTC: Create Lease Request
    LTC->>LTC: Mint ICRC-7 Battery NFT
    LTC->>Frontend: Lease Approved
    Frontend->>User: Battery Available
    
    Battery->>ESP32: Continuous Telemetry
    ESP32->>TDC: Send Sensor Data
    TDC->>TDC: Store & Process Data
    TDC->>AIC: Trigger AI Analysis
    AIC->>NAC: Health Predictions
    NAC->>User: Alert Notifications
```

## 🔒 Security Architecture

```mermaid
graph LR
    subgraph "Authentication"
        II[Internet Identity]
        PRINCIPAL[Principal ID]
    end
    
    subgraph "Authorization"
        RBAC[Role-Based Access]
        CANISTER_AUTH[Canister-Level Auth]
    end
    
    subgraph "Data Security"
        ENCRYPTION[End-to-End Encryption]
        IMMUTABLE[Immutable Storage]
        AUDIT[Audit Trail]
    end
    
    subgraph "Hardware Security"
        SECURE_BOOT[Secure Boot]
        TLS[TLS Communication]
        TAMPER[Tamper Detection]
    end
    
    II --> PRINCIPAL
    PRINCIPAL --> RBAC
    RBAC --> CANISTER_AUTH
    CANISTER_AUTH --> ENCRYPTION
    ENCRYPTION --> IMMUTABLE
    IMMUTABLE --> AUDIT
    
    SECURE_BOOT --> TLS
    TLS --> TAMPER
```
