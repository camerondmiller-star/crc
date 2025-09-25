Cloud Resume ArchitectureThis diagram illustrates the secure, scalable, and globally available deployment you built for cloudresume.thecammiller.com.graph TD
    A[User's Browser] --> B(WPX Domain Registrar)
    B --> C(Cloud DNS Zone)
    C -- NS Delegation --> C
    A -- HTTPS Request --> D(Global HTTPS Load Balancer)
    D -- Route Traffic --> E(Backend Bucket)
    E -- Static Website Hosting --> E
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

Explanation of the FlowWPX Domain Registrar: Your main domain thecammiller.com is managed here. You've configured a NS record to delegate the subdomain cloudresume.thecammiller.com.Cloud DNS Zone: This is the dedicated zone for your subdomain within Google Cloud. It holds the A record that points to your load balancer's IP address.User's Browser: When a user requests https://cloudresume.thecammiller.com, the request first goes to the registrar, which redirects it to the Google Cloud DNS zone.Global HTTPS Load Balancer: This is the entry point for all web traffic. It provides a static IP, handles HTTPS/SSL termination, and directs traffic to the backend. It also uses Cloud Logging to record requests.Google Managed SSL Cert: This certificate is automatically provisioned and renewed by Google. Its activation depends on the DNS records correctly pointing to the load balancer.Backend Bucket: This is your Google Cloud Storage bucket where the static files (index.html and 404.html) are stored. It's configured to serve index.html as the main page and 404.html as the error page.Cloud CDN: A single checkbox in the load balancer configuration, Cloud CDN caches your content at Google's edge locations, ensuring fast global loads.Cloud Logging: Enabled on the backend, this provides observability and helps you track traffic and troubleshoot issues.This visual representation should be helpful in explaining the architecture in a clear and concise way, which can be useful for interviews or for your own reference.
