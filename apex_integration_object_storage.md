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
        - Name: **apex-demo-compartment**
        - Description: **Compartment for APEX demo projects**
        - Parent compartment: **(root)**
    - Confirm by clicking **Create compartment**
2. Create the domain `apex-demo-domain` 
    - Select **Identity & Security**
    - Select **Domains**
    - Click the button **Create domain**
    - Enter the following details:
        - Name: **apex-demo-domain**
        - Description: **Domain for APEX demo projects**
        - Domain type: **free**
        - Domain administrator: *uncheck (do not create)*
        - Compartment: `apex-demo-compartment`  
    - Confirm by clicking **Create domain**
3. Create the group `apex-demo-group` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Groups**
    - Click the button **Create group**
    - Enter the following details:
        - Name: **apex-demo-group**
        - Description: **Group for APEX demo projects**
    - Confirm by clicking **Create group** 
4. Create the policy `apex-demo-policy-object-storage` 
    - Select **Identity & Security**
    - Select **Policies**
    - Click the button **Create policy**
    - Enter the following details:
        - Name: **apex-demo-policy-storage**
        - Description: **Policy for APEX demo projects object storage**
        - Compartment: `apex-demo-compartment`  
        - Policy builder: *(enable manual editor and enter the following)*
            - *Allow group 'apex-demo-domain'/'apex-demo-group' to read buckets in compartment apex-demo-compartment*
            - *Allow group 'apex-demo-domain'/'apex-demo-group' to read objects in compartment apex-demo-compartment*
            - *Allow group 'apex-demo-domain'/'apex-demo-group' to manage objects in compartment apex-demo-compartment where any {request.permission='OBJECT_CREATE', request.permission='OBJECT_INSPECT'}*
    - Confirm by clicking **Create policy** 
5. Create the user `apex-demo-agent` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Users**
    - Click the button **Create user**
    - Enter the following details:
        - Last name: **APEX demo agent**
        - Username: **apex-demo-agent**
        - Email: **agent@apex.com**
        - Groups: `apex-demo-group`
    - Confirm by clicking **Create user** 
6. Edit the user `apex-demo-agent` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Users**
    - Select `apex-demo-agent`
    - Click the button **Edit user capabilities**
    - Uncheck all items except **API keys**
    - Confirm by clicking **Save changes**
7. Generate the API keys for the user `apex-demo-agent` 
    - Select **Identity & Security**
    - Select **Domains**
    - Select `apex-demo-domain`
    - Select **Users**
    - Select `apex-demo-agent`
    - Select **API keys**
    - Click the button  **Add API key**
    - Select **Generate API key pair**
    - Click the button **Download private key**
    - Confirm by clicking **Add**
8. Create the bucket `apex-demo-bucket`
    - Select **Storage**
    - Select **Object Storage & Archive Storage**
    - Ensure that the `apex-demo-compartment` is selected
    - Click the button **Create bucket**
    - Enter the following details:
        - Name: **apex-demo-bucket**
        - Storage tier: **Standard**
        - Encryption: **Encrypt using Oracle managed keys**
    - Confirm by clicking **Create bucket** 