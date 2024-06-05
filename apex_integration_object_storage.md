# Oracle APEX Integration with OCI Object Storage

This page provides a comprehensive guide and sample project demonstrating how to integrate Oracle Application Express (APEX) with Object Storage using REST APIs. 

This guide is inspired by the article *Better File Storage in Oracle Cloud* by *Adrian Png*.  You can find the original article [here](https://blogs.oracle.com/connect/post/better-file-storage-in-oracle-cloud).

## OCI Setup

Complete the following tasks using the Oracle Cloud Infrastructure (OCI) console and an account that has administrative rights within the tenancy (the root compartment).

1. Create the compartment `apex-demo-compartment` 
    - Select **Identity & Security**
    - Select **Compartments**
    - Click the button **Create compartment**
    - Enter the following details:
        - name: **apex-demo-compartment**
        - description: **Compartment for APEX demo projects**
        - parent compartment: **(root)**
    - Click the button **Create compartment**
2. Create the domain `apex-demo-domain` 
    - Select **Identity & Security**
    - Select **Domains**
    - Click the button **Create domain**
    - Enter the following details:
        - name: **apex-demo-domain**
        - description: **Domain for APEX demo projects**
        - domain type: **free**
        - domain administrator: *uncheck (do not create)*
        - compartment: `apex-demo-compartment`  
    - Click the button **Create domain**
3. Create the group `apex-demo-group` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Groups**
    - Click the button **Create group**
    - Enter the following details:
        - name: **apex-demo-group**
        - description: **Group for APEX demo projects**
4. Create the policy `apex-demo-policy-storage-read` 
    - Select **Identity & Security**
    - Select **Policies**
    - Click the button **Create policy**
    - Enter the following details:
        - name: **apex-demo-policy-storage-read**
        - description: **Policy for APEX demo projects object storage read**
        - compartment: `apex-demo-compartment`  
        - policy use case: **Storage Management**
        - policy template: **Let users download objects from Object Storage buckets**
        - identity domain: `apex-demo-domain`
        - group: `apex-demo-group`
        - location: `apex-demo-compartment`  
5. Create the policy `apex-demo-policy-storage-write` 
    - Select **Identity & Security**
    - Select **Policies**
    - Click the button **Create policy**
    - Enter the following details:
        - name: **apex-demo-policy-storage-write**
        - description: **Policy for APEX demo projects object storage write**
        - compartment: `apex-demo-compartment`  
        - policy use case: **Storage Management**
        - policy template: **Let users write objects to Object Storage buckets**
        - identity domain: `apex-demo-domain`
        - group: `apex-demo-group`
        - location: `apex-demo-compartment`  
6. Create the user `apex-demo-agent` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Users**
    - Click the button **Create user**
    - Enter the following details:
        - last name: **APEX demo agent**
        - username: **apex-demo-agent**
        - email: **agent@apex.com**
        - groups: `apex-demo-group`
7. Edit the user `apex-demo-agent` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Users**
    - Select `apex-demo-agent`
    - Click the button **Edit user capabilities**
    - Uncheck all items except **API keys**
8. Generate the API keys for the user `apex-demo-agent` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Users**
    - Select `apex-demo-agent`
    - Select **API keys**
    - Click the button  **Add API key**
    - Select **Generate API key pair**
    - Click the button  **Download private key**
    - Click the button  **Add**