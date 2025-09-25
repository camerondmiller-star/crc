graph TD
    A[User's Browser] --> B(WPX Domain Registrar)
    B --> C(Cloud DNS Zone)
    C -- NS Delegation --> C
    A -- HTTPS Request --> D(Global HTTPS Load Balancer)
    D -- Route Traffic --> E(Backend Bucket)
    E -- Static Website Hosting) --> E
    E --> F[index.html]
    E --> G[404.html]
    D -- SSL Certificate Provisioning --> H(Google Managed SSL Cert)
    H -- Verified by DNS --> C
    D -- Cache content --> I(Cloud CDN)
    I -- Cloud Logging --> J(Cloud Logging)

    subgraph "Google Cloud"
        C
        D
        E
        F
        G
        H
        I
        J
    end

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#bbf,stroke:#333,stroke-width:2px
    style C fill:#ccf,stroke:#333,stroke-width:2px
    style D fill:#ddf,stroke:#333,stroke-width:2px
    style E fill:#eef,stroke:#333,stroke-width:2px
    style F fill:#9f9,stroke:#333,stroke-width:2px
    style G fill:#f99,stroke:#333,stroke-width:2px
    style H fill:#9f9,stroke:#333,stroke-width:2px
    style I fill:#ddf,stroke:#333,stroke-width:2px
    style J fill:#f3f3f3,stroke:#333,stroke-width:2px

    linkStyle 0 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 1 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 2 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 3 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 4 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 5 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 6 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 7 stroke:#000,stroke-width:2px,fill:none,color:#000;
    linkStyle 8 stroke:#000,stroke-width:2px,fill:none,color:#000;
