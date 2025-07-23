# ChargeX User Flow Diagrams

## 🔋 Battery Leasing User Journey

```mermaid
flowchart TD
    START([User Opens ChargeX App]) --> AUTH{Authenticated?}
    AUTH -->|No| LOGIN[Login with Internet Identity]
    AUTH -->|Yes| DASHBOARD[View Dashboard]
    LOGIN --> DASHBOARD
    
    DASHBOARD --> FIND[Find Available Batteries]
    FIND --> MAP[View Battery Map/List]
    MAP --> SELECT[Select Battery Location]
    SELECT --> CHECK{Battery Available?}
    
    CHECK -->|No| NOTIFY[Join Waitlist/Notification]
    CHECK -->|Yes| RESERVE[Reserve Battery]
    
    RESERVE --> PAYMENT[Process Payment]
    PAYMENT --> SUCCESS{Payment Success?}
    SUCCESS -->|No| RETRY[Retry Payment]
    SUCCESS -->|Yes| NFT[Mint Battery NFT]
    
    NFT --> PICKUP[Go to Pickup Location]
    PICKUP --> KIOSK[Use Kiosk Interface]
    KIOSK --> VERIFY[Verify Identity]
    VERIFY --> DISPENSE[Battery Dispensed]
    DISPENSE --> TRACK[Real-time Tracking Active]
    
    TRACK --> USE[Use Battery]
    USE --> RETURN_TIME{Return Time?}
    RETURN_TIME -->|No| CONTINUE[Continue Using]
    RETURN_TIME -->|Yes| RETURN[Return Battery]
    
    RETURN --> RETURN_KIOSK[Use Return Kiosk]
    RETURN_KIOSK --> FINALIZE[Finalize Lease]
    FINALIZE --> BURN_NFT[Burn Battery NFT]
    BURN_NFT --> END([Journey Complete])
    
    RETRY --> PAYMENT
    CONTINUE --> USE
    NOTIFY --> DASHBOARD
    
    classDef startEnd fill:#4caf50,stroke:#2e7d32,color:#fff
    classDef process fill:#2196f3,stroke:#1565c0,color:#fff
    classDef decision fill:#ff9800,stroke:#ef6c00,color:#fff
    classDef error fill:#f44336,stroke:#c62828,color:#fff
    
    class START,END startEnd
    class LOGIN,DASHBOARD,FIND,MAP,SELECT,RESERVE,PAYMENT,NFT,PICKUP,KIOSK,VERIFY,DISPENSE,TRACK,USE,RETURN,RETURN_KIOSK,FINALIZE,BURN_NFT process
    class AUTH,CHECK,SUCCESS,RETURN_TIME decision
    class RETRY,NOTIFY error
```

## ⚡ Energy Trading User Journey

```mermaid
flowchart TD
    START([User Has Excess Energy]) --> DASHBOARD[Open Trading Dashboard]
    DASHBOARD --> ENERGY_CHECK[Check Available Energy]
    ENERGY_CHECK --> ENOUGH{Sufficient Energy?}
    
    ENOUGH -->|No| WAIT[Wait for More Energy]
    ENOUGH -->|Yes| CREATE_OFFER[Create Energy Offer]
    
    CREATE_OFFER --> SET_PRICE[Set Price & Quantity]
    SET_PRICE --> SET_TERMS[Set Trading Terms]
    SET_TERMS --> PUBLISH[Publish to Marketplace]
    
    PUBLISH --> LISTED[Offer Listed]
    LISTED --> BUYER_INTEREST{Buyer Interest?}
    
    BUYER_INTEREST -->|No| WAIT_BUYER[Wait for Buyers]
    BUYER_INTEREST -->|Yes| NEGOTIATE[Price Negotiation]
    
    NEGOTIATE --> AGREE{Terms Agreed?}
    AGREE -->|No| COUNTER[Counter Offer]
    AGREE -->|Yes| EXECUTE[Execute Trade]
    
    EXECUTE --> TRANSFER[Transfer Energy]
    TRANSFER --> PAYMENT_REC[Receive Payment]
    PAYMENT_REC --> COMPLETE[Trade Complete]
    COMPLETE --> RATING[Rate Transaction]
    RATING --> END([Journey Complete])
    
    WAIT --> ENERGY_CHECK
    WAIT_BUYER --> BUYER_INTEREST
    COUNTER --> NEGOTIATE
    
    classDef startEnd fill:#4caf50,stroke:#2e7d32,color:#fff
    classDef process fill:#2196f3,stroke:#1565c0,color:#fff
    classDef decision fill:#ff9800,stroke:#ef6c00,color:#fff
    classDef trading fill:#9c27b0,stroke:#6a1b9a,color:#fff
    
    class START,END startEnd
    class DASHBOARD,ENERGY_CHECK,CREATE_OFFER,SET_PRICE,SET_TERMS,PUBLISH,LISTED,NEGOTIATE,EXECUTE,TRANSFER,PAYMENT_REC,COMPLETE,RATING process
    class ENOUGH,BUYER_INTEREST,AGREE decision
    class WAIT,WAIT_BUYER,COUNTER trading
```

## 🤖 AI Predictive Maintenance Flow

```mermaid
flowchart TD
    SENSOR[Sensor Data Collection] --> TRANSMIT[ESP32 Transmits Data]
    TRANSMIT --> RECEIVE[Telemetry Canister Receives]
    RECEIVE --> STORE[Store Historical Data]
    
    STORE --> AI_TRIGGER[AI Analysis Triggered]
    AI_TRIGGER --> ANALYZE[Analyze Battery Health]
    ANALYZE --> PREDICT[Generate Predictions]
    
    PREDICT --> RISK{High Risk Detected?}
    RISK -->|No| NORMAL[Normal Operation]
    RISK -->|Yes| ALERT[Generate Alert]
    
    ALERT --> CLASSIFY[Classify Alert Type]
    CLASSIFY --> URGENT{Urgent Issue?}
    
    URGENT -->|No| SCHEDULE[Schedule Maintenance]
    URGENT -->|Yes| IMMEDIATE[Immediate Action Required]
    
    IMMEDIATE --> NOTIFY_USER[Notify User]
    NOTIFY_USER --> DISABLE[Disable Battery if Needed]
    DISABLE --> DISPATCH[Dispatch Technician]
    
    SCHEDULE --> PLAN[Plan Maintenance Window]
    PLAN --> NOTIFY_PLAN[Notify Planned Maintenance]
    
    NORMAL --> MONITOR[Continue Monitoring]
    MONITOR --> SENSOR
    
    DISPATCH --> RESOLVE[Issue Resolved]
    NOTIFY_PLAN --> EXECUTE_MAINT[Execute Maintenance]
    EXECUTE_MAINT --> RESOLVE
    RESOLVE --> MONITOR
    
    classDef sensor fill:#4caf50,stroke:#2e7d32,color:#fff
    classDef ai fill:#9c27b0,stroke:#6a1b9a,color:#fff
    classDef alert fill:#f44336,stroke:#c62828,color:#fff
    classDef maintenance fill:#ff9800,stroke:#ef6c00,color:#fff
    
    class SENSOR,TRANSMIT,RECEIVE,STORE sensor
    class AI_TRIGGER,ANALYZE,PREDICT ai
    class ALERT,NOTIFY_USER,DISABLE,IMMEDIATE alert
    class SCHEDULE,PLAN,NOTIFY_PLAN,EXECUTE_MAINT,DISPATCH,RESOLVE maintenance
```

## 🏪 Kiosk Interaction Flow

```mermaid
flowchart TD
    APPROACH([User Approaches Kiosk]) --> WAKE[Kiosk Wakes Up]
    WAKE --> WELCOME[Display Welcome Screen]
    WELCOME --> ACTION{User Action?}
    
    ACTION -->|Pickup| PICKUP_FLOW[Battery Pickup Flow]
    ACTION -->|Return| RETURN_FLOW[Battery Return Flow]
    ACTION -->|Info| INFO[Display Information]
    
    PICKUP_FLOW --> SCAN_QR[Scan QR Code/ID]
    SCAN_QR --> VERIFY_USER[Verify User Identity]
    VERIFY_USER --> CHECK_LEASE[Check Active Lease]
    CHECK_LEASE --> VALID{Valid Lease?}
    
    VALID -->|No| ERROR[Display Error]
    VALID -->|Yes| DISPENSE[Dispense Battery]
    DISPENSE --> CONFIRM[Confirm Pickup]
    CONFIRM --> RECEIPT[Print/Display Receipt]
    
    RETURN_FLOW --> INSERT[Insert Battery]
    INSERT --> CHECK_BATTERY[Check Battery Condition]
    CHECK_BATTERY --> VERIFY_RETURN[Verify Return]
    VERIFY_RETURN --> ACCEPT[Accept Return]
    ACCEPT --> UPDATE_LEASE[Update Lease Status]
    UPDATE_LEASE --> FINAL_RECEIPT[Generate Final Receipt]
    
    INFO --> DISPLAY_INFO[Show Platform Info]
    DISPLAY_INFO --> BACK[Back to Main Menu]
    
    ERROR --> RETRY{Retry?}
    RETRY -->|Yes| PICKUP_FLOW
    RETRY -->|No| TIMEOUT
    
    RECEIPT --> TIMEOUT[Session Timeout]
    FINAL_RECEIPT --> TIMEOUT
    BACK --> ACTION
    TIMEOUT --> SLEEP[Kiosk Sleep Mode]
    SLEEP --> END([Session End])
    
    classDef kiosk fill:#2196f3,stroke:#1565c0,color:#fff
    classDef success fill:#4caf50,stroke:#2e7d32,color:#fff
    classDef error fill:#f44336,stroke:#c62828,color:#fff
    classDef info fill:#ff9800,stroke:#ef6c00,color:#fff
    
    class WAKE,WELCOME,SCAN_QR,VERIFY_USER,CHECK_LEASE,DISPENSE,CONFIRM,INSERT,CHECK_BATTERY,VERIFY_RETURN,ACCEPT,UPDATE_LEASE kiosk
    class RECEIPT,FINAL_RECEIPT,TIMEOUT,SLEEP success
    class ERROR,RETRY error
    class INFO,DISPLAY_INFO,BACK info
```

## 📱 Mobile Notification Flow

```mermaid
flowchart TD
    TRIGGER[Event Trigger] --> CLASSIFY[Classify Event Type]
    CLASSIFY --> BATTERY{Battery Alert?}
    BATTERY -->|Yes| BATTERY_ALERT[Battery Health Alert]
    BATTERY -->|No| TRADING{Trading Alert?}
    
    TRADING -->|Yes| TRADING_ALERT[Trading Notification]
    TRADING -->|No| SYSTEM{System Alert?}
    
    SYSTEM -->|Yes| SYSTEM_ALERT[System Notification]
    SYSTEM -->|No| IGNORE[Ignore Event]
    
    BATTERY_ALERT --> URGENT_BATT{Urgent?}
    URGENT_BATT -->|Yes| PUSH_URGENT[Push Urgent Notification]
    URGENT_BATT -->|No| QUEUE_BATT[Queue Standard Notification]
    
    TRADING_ALERT --> TRADING_TYPE{Type?}
    TRADING_TYPE -->|Offer| OFFER_NOTIF[New Offer Notification]
    TRADING_TYPE -->|Sale| SALE_NOTIF[Sale Completed Notification]
    TRADING_TYPE -->|Price| PRICE_NOTIF[Price Alert Notification]
    
    SYSTEM_ALERT --> SYS_TYPE{Type?}
    SYS_TYPE -->|Maintenance| MAINT_NOTIF[Maintenance Notification]
    SYS_TYPE -->|Update| UPDATE_NOTIF[System Update Notification]
    
    PUSH_URGENT --> DELIVERED{Delivered?}
    QUEUE_BATT --> BATCH_SEND[Batch Send]
    OFFER_NOTIF --> BATCH_SEND
    SALE_NOTIF --> BATCH_SEND
    PRICE_NOTIF --> BATCH_SEND
    MAINT_NOTIF --> BATCH_SEND
    UPDATE_NOTIF --> BATCH_SEND
    
    BATCH_SEND --> DELIVERED
    DELIVERED -->|Yes| LOG_SUCCESS[Log Success]
    DELIVERED -->|No| RETRY_SEND[Retry Send]
    
    RETRY_SEND --> RETRY_COUNT{Retry < 3?}
    RETRY_COUNT -->|Yes| DELIVERED
    RETRY_COUNT -->|No| LOG_FAILED[Log Failed]
    
    LOG_SUCCESS --> END([Complete])
    LOG_FAILED --> END
    IGNORE --> END
    
    classDef trigger fill:#9c27b0,stroke:#6a1b9a,color:#fff
    classDef urgent fill:#f44336,stroke:#c62828,color:#fff
    classDef normal fill:#2196f3,stroke:#1565c0,color:#fff
    classDef success fill:#4caf50,stroke:#2e7d32,color:#fff
    
    class TRIGGER,CLASSIFY trigger
    class PUSH_URGENT,URGENT_BATT urgent
    class QUEUE_BATT,BATCH_SEND,OFFER_NOTIF,SALE_NOTIF,PRICE_NOTIF,MAINT_NOTIF,UPDATE_NOTIF normal
    class LOG_SUCCESS,DELIVERED success
```
