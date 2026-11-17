# 3. Diagrama Mermaid: estructura IT/OT y papel de la IA

```mermaid
flowchart TB
    subgraph OT["OT - Planta (producción)"]
        direction LR
        A["Recepción de pescado"] --> B["Preparación y precocción"]
        B --> C["Envasado y llenado"]
        C --> D["Esterilización en autoclave"]
        D --> E["Etiquetado y paletizado"]
        S["Sensores IIoT y PLC"] -.-> A
        S -.-> C
        S -.-> D
        V["Cámaras de visión artificial"] -.-> C
        V -.-> E
        SC["SCADA"]
        S --> SC
    end

    subgraph IA["Capa de IA y datos"]
        direction LR
        DL["Plataforma de datos (data lake)"]
        M1["IA: mantenimiento predictivo"]
        M2["IA: control de calidad por visión"]
        M3["IA: previsión de demanda"]
        M4["IA: optimización de planificación"]
        DL --> M1
        DL --> M2
        DL --> M3
        DL --> M4
    end

    subgraph IT["IT - Negocio (gestión)"]
        direction LR
        MES["MES"]
        ERP["ERP"]
        CRM["CRM"]
        LOG["Logística y almacén"]
        WEB["Tienda online"]
        MES <--> ERP
        ERP <--> CRM
        ERP <--> LOG
        CRM <--> WEB
    end

    SC --> MES
    SC --> DL
    V --> DL
    MES --> DL
    ERP --> DL
    CRM --> DL
    M1 -->|"alertas de mantenimiento"| SC
    M2 -->|"rechazo de unidades"| C
    M3 -->|"demanda prevista"| ERP
    M4 -->|"órdenes optimizadas"| MES
    ERP -->|"pedidos y compras"| A
```

## Lectura del diagrama
- **OT (arriba):** línea de producción con sensores, visión artificial y SCADA.
- **IT (abajo):** sistemas de gestión: MES, ERP, CRM, logística y venta online.
- **Capa de IA (centro):** recibe datos de ambos mundos y devuelve decisiones a cada uno (alertas, rechazos, previsiones, órdenes).
