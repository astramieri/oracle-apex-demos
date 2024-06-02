# Oracle APEX Integration with OCI Object Storage

This page  provides a comprehensive guide and sample project demonstrating how to integrate Oracle Application Express (APEX) with Object Storage using REST APIs. 

## OCI Setup

1. Create the `apex-demo-compartment` compartment
2. Create the `apex-demo-domain` domain
3. Create the `APEX Demo Users` group
4. Create the `APEXDemoReadObjectsStorage` policy
    - Select `Storage Management` and `Let users download objects from object Storage buckets`
5. Create the `APEXDemoWriteObjectsStorage` policy
    - Select `Storage Management` and `Let users write objects to object storage buckets`
6. Create the `apex-demo-agent` user
    - Edit user capabilities and select only `API Keys`