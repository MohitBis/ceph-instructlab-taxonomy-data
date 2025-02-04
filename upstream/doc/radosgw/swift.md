# Ceph Object Gateway Swift API {#radosgw swift}

Ceph supports a RESTful API that is compatible with the basic data
access model of the [Swift
API](https://developer.openstack.org/api-ref/object-store/index.html).

## API

::: {.toctree maxdepth="1"}
Authentication \<swift/auth\> Service Ops \<swift/serviceops\> Container
Ops \<swift/containerops\> Object Ops \<swift/objectops\> Temp URL Ops
\<swift/tempurl\> Tutorial \<swift/tutorial\> Java \<swift/java\> Python
\<swift/python\> Ruby \<swift/ruby\>
:::

## Features Support

The following table describes the support status for current Swift
functional features:

  ----------------------------------------------------------------------
  Feature                   Status        Remarks
  ------------------------- ------------- ------------------------------
  **Authentication**        Supported     

  **Get Account Metadata**  Supported     

  **Swift ACLs**            Supported     Supports a subset of Swift
                                          ACLs

  **List Containers**       Supported     

  **Delete Container**      Supported     

  **Create Container**      Supported     

  **Get Container           Supported     
  Metadata**                              

  **Update Container        Supported     
  Metadata**                              

  **Delete Container        Supported     
  Metadata**                              

  **List Objects**          Supported     

  **Static Website**        Supported     

  **Create Object**         Supported     

  **Create Large Object**   Supported     

  **Delete Object**         Supported     

  **Get Object**            Supported     

  **Copy Object**           Supported     

  **Get Object Metadata**   Supported     

  **Update Object           Supported     
  Metadata**                              

  **Expiring Objects**      Supported     

  **Temporary URLs**        Partial       No support for container-level
                            Support       keys

  **Object Versioning**     Partial       No support for
                            Support       `X-History-Location`

  **CORS**                  Not Supported 
  ----------------------------------------------------------------------
