# Object Operations

## Put Object

Adds an object to a bucket. You must have write permissions on the
bucket to perform this operation.

### Syntax

    PUT /{bucket}/{object} HTTP/1.1

### Request Headers

  -------------------------------------------------------------------------------------------
  Name                      Description         Valid Values                       Required
  ------------------------- ------------------- ---------------------------------- ----------
  **content-md5**           A base64 encoded    A string. No defaults or           No
                            MD-5 hash of the    constraints.                       
                            message.                                               

  **content-type**          A standard MIME     Any MIME type. Default:            No
                            type.               `binary/octet-stream`              

  **x-amz-meta-\<\...\>**   User metadata.      A string up to 8kb. No defaults.   No
                            Stored with the                                        
                            object.                                                

  **x-amz-acl**             A canned ACL.       `private`, `public-read`,          No
                                                `public-read-write`,               
                                                `authenticated-read`               
  -------------------------------------------------------------------------------------------

## Copy Object

To copy an object, use `PUT` and specify a destination bucket and the
object name.

### Syntax

    PUT /{dest-bucket}/{dest-object} HTTP/1.1
    x-amz-copy-source: {source-bucket}/{source-object}

### Request Headers

+--------------------+--------------------------+------------+------+
| Name               | Description              | Valid      | Requ |
|                    |                          | Values     | ired |
+====================+==========================+============+======+
| **x                | The source bucket name + | {buc       | Yes  |
| -amz-copy-source** | object name.             | ket}/{obj} |      |
+--------------------+--------------------------+------------+------+
| **x-amz-acl**      | A canned ACL.            | `private`, | No   |
|                    |                          | `pub       |      |
|                    |                          | lic-read`, |      |
|                    |                          | `public-re |      |
|                    |                          | ad-write`, |      |
|                    |                          | `authentic |      |
|                    |                          | ated-read` |      |
+--------------------+--------------------------+------------+------+
| **x-amz-copy-i     | > Copies only if         | >          | No   |
| f-modified-since** | > modified since the     |  Timestamp |      |
|                    | > timestamp.             |            |      |
+--------------------+--------------------------+------------+------+
| **x-amz-copy-if-   | > Copies only if         | >          | No   |
| unmodified-since** | > unmodified since the   |  Timestamp |      |
|                    | > timestamp.             |            |      |
+--------------------+--------------------------+------------+------+
| **x-a              | > Copies only if object  | > Entity   | No   |
| mz-copy-if-match** | > ETag matches ETag.     | > Tag      |      |
+--------------------+--------------------------+------------+------+
| **x-amz-co         | > Copies only if object  | > Entity   | No   |
| py-if-none-match** | > ETag doesn\'t match.   | > Tag      |      |
+--------------------+--------------------------+------------+------+

### Response Entities

+-------------------+----------+--------------------------------------+
| Name              | Type     | Description                          |
+===================+==========+======================================+
| **C               | C        | > A container for the response       |
| opyObjectResult** | ontainer | > elements.                          |
+-------------------+----------+--------------------------------------+
| **LastModified**  | Date     | > The last modified date of the      |
|                   |          | > source object.                     |
+-------------------+----------+--------------------------------------+
| **Etag**          | String   | > The ETag of the new object.        |
+-------------------+----------+--------------------------------------+

## Remove Object

Removes an object. Requires WRITE permission set on the containing
bucket.

### Syntax

    DELETE /{bucket}/{object} HTTP/1.1

## Get Object

Retrieves an object from a bucket within RADOS.

### Syntax

    GET /{bucket}/{object} HTTP/1.1

### Request Headers

  ------------------------------------------------------------------------------------------
  Name                      Description                 Valid Values              Required
  ------------------------- --------------------------- ------------------------- ----------
  **range**                 The range of the object to  Range:                    No
                            retrieve.                   bytes=beginbyte-endbyte   

  **if-modified-since**     Gets only if modified since Timestamp                 No
                            the timestamp.                                        

  **if-unmodified-since**   Gets only if not modified   Timestamp                 No
                            since the timestamp.                                  

  **if-match**              Gets only if object ETag    Entity Tag                No
                            matches ETag.                                         

  **if-none-match**         Gets only if object ETag    Entity Tag                No
                            matches ETag.                                         
  ------------------------------------------------------------------------------------------

### Response Headers

  ------------------------------------------------------------------------------
  Name                Description
  ------------------- ----------------------------------------------------------
  **Content-Range**   Data range, will only be returned if the range header
                      field was specified in the request

  ------------------------------------------------------------------------------

## Get Object Info

Returns information about object. This request will return the same
header information as with the Get Object request, but will include the
metadata only, not the object data payload.

### Syntax

    HEAD /{bucket}/{object} HTTP/1.1

### Request Headers

  ------------------------------------------------------------------------------------------
  Name                      Description                 Valid Values              Required
  ------------------------- --------------------------- ------------------------- ----------
  **range**                 The range of the object to  Range:                    No
                            retrieve.                   bytes=beginbyte-endbyte   

  **if-modified-since**     Gets only if modified since Timestamp                 No
                            the timestamp.                                        

  **if-unmodified-since**   Gets only if not modified   Timestamp                 No
                            since the timestamp.                                  

  **if-match**              Gets only if object ETag    Entity Tag                No
                            matches ETag.                                         

  **if-none-match**         Gets only if object ETag    Entity Tag                No
                            matches ETag.                                         
  ------------------------------------------------------------------------------------------

## Get Object ACL

### Syntax

    GET /{bucket}/{object}?acl HTTP/1.1

### Response Entities

  ------------------------------------------------------------------------------------
  Name                    Type        Description
  ----------------------- ----------- ------------------------------------------------
  `AccessControlPolicy`   Container   A container for the response.

  `AccessControlList`     Container   A container for the ACL information.

  `Owner`                 Container   A container for the object owner\'s `ID` and
                                      `DisplayName`.

  `ID`                    String      The object owner\'s ID.

  `DisplayName`           String      The object owner\'s display name.

  `Grant`                 Container   A container for `Grantee` and `Permission`.

  `Grantee`               Container   A container for the `DisplayName` and `ID` of
                                      the user receiving a grant of permission.

  `Permission`            String      The permission given to the `Grantee` object.
  ------------------------------------------------------------------------------------

## Set Object ACL

### Syntax

    PUT /{bucket}/{object}?acl

### Request Entities

  ------------------------------------------------------------------------------------
  Name                    Type        Description
  ----------------------- ----------- ------------------------------------------------
  `AccessControlPolicy`   Container   A container for the response.

  `AccessControlList`     Container   A container for the ACL information.

  `Owner`                 Container   A container for the object owner\'s `ID` and
                                      `DisplayName`.

  `ID`                    String      The object owner\'s ID.

  `DisplayName`           String      The object owner\'s display name.

  `Grant`                 Container   A container for `Grantee` and `Permission`.

  `Grantee`               Container   A container for the `DisplayName` and `ID` of
                                      the user receiving a grant of permission.

  `Permission`            String      The permission given to the `Grantee` object.
  ------------------------------------------------------------------------------------

## Initiate Multi-part Upload

Initiate a multi-part upload process.

### Syntax

    POST /{bucket}/{object}?uploads

### Request Headers

  -------------------------------------------------------------------------------------------
  Name                      Description         Valid Values                       Required
  ------------------------- ------------------- ---------------------------------- ----------
  **content-md5**           A base64 encoded    A string. No defaults or           No
                            MD-5 hash of the    constraints.                       
                            message.                                               

  **content-type**          A standard MIME     Any MIME type. Default:            No
                            type.               `binary/octet-stream`              

  **x-amz-meta-\<\...\>**   User metadata.      A string up to 8kb. No defaults.   No
                            Stored with the                                        
                            object.                                                

  **x-amz-acl**             A canned ACL.       `private`, `public-read`,          No
                                                `public-read-write`,               
                                                `authenticated-read`               
  -------------------------------------------------------------------------------------------

### Response Entities

  ----------------------------------------------------------------------------------------------
  Name                                Type        Description
  ----------------------------------- ----------- ----------------------------------------------
  `InitiatedMultipartUploadsResult`   Container   A container for the results.

  `Bucket`                            String      The bucket that will receive the object
                                                  contents.

  `Key`                               String      The key specified by the `key` request
                                                  parameter (if any).

  `UploadId`                          String      The ID specified by the `upload-id` request
                                                  parameter identifying the multipart upload (if
                                                  any).
  ----------------------------------------------------------------------------------------------

## Multipart Upload Part

### Syntax

    PUT /{bucket}/{object}?partNumber=&uploadId= HTTP/1.1

### HTTP Response

The following HTTP response may be returned:

  --------------------------------------------------------------------------
  HTTP       Status Code    Description
  Status                    
  ---------- -------------- ------------------------------------------------
  **404**    NoSuchUpload   Specified upload-id does not match any initiated
                            upload on this object

  --------------------------------------------------------------------------

## List Multipart Upload Parts

### Syntax

    GET /{bucket}/{object}?uploadId=123 HTTP/1.1

### Response Entities

  -----------------------------------------------------------------------------------
  Name                     Type        Description
  ------------------------ ----------- ----------------------------------------------
  `ListPartsResult`        Container   A container for the results.

  `Bucket`                 String      The bucket that will receive the object
                                       contents.

  `Key`                    String      The key specified by the `key` request
                                       parameter (if any).

  `UploadId`               String      The ID specified by the `upload-id` request
                                       parameter identifying the multipart upload (if
                                       any).

  `Initiator`              Container   Contains the `ID` and `DisplayName` of the
                                       user who initiated the upload.

  `ID`                     String      The initiator\'s ID.

  `DisplayName`            String      The initiator\'s display name.

  `Owner`                  Container   A container for the `ID` and `DisplayName` of
                                       the user who owns the uploaded object.

  `StorageClass`           String      The method used to store the resulting object.
                                       `STANDARD` or `REDUCED_REDUNDANCY`

  `PartNumberMarker`       String      The part marker to use in a subsequent request
                                       if `IsTruncated` is `true`. Precedes the list.

  `NextPartNumberMarker`   String      The next part marker to use in a subsequent
                                       request if `IsTruncated` is `true`. The end of
                                       the list.

  `MaxParts`               Integer     The max parts allowed in the response as
                                       specified by the `max-parts` request
                                       parameter.

  `IsTruncated`            Boolean     If `true`, only a subset of the object\'s
                                       upload contents were returned.

  `Part`                   Container   A container for `LastModified`, `PartNumber`,
                                       `ETag` and `Size` elements.

  `LastModified`           Date        Date and time at which the part was uploaded.

  `PartNumber`             Integer     The identification number of the part.

  `ETag`                   String      The part\'s entity tag.

  `Size`                   Integer     The size of the uploaded part.
  -----------------------------------------------------------------------------------

## Complete Multipart Upload

Assembles uploaded parts and creates a new object, thereby completing a
multipart upload.

### Syntax

    POST /{bucket}/{object}?uploadId= HTTP/1.1

### Request Entities

  ------------------------------------------------------------------------------------
  Name                        Type        Description                       Required
  --------------------------- ----------- --------------------------------- ----------
  `CompleteMultipartUpload`   Container   A container consisting of one or  Yes
                                          more parts.                       

  `Part`                      Container   A container for the `PartNumber`  Yes
                                          and `ETag`.                       

  `PartNumber`                Integer     The identifier of the part.       Yes

  `ETag`                      String      The part\'s entity tag.           Yes
  ------------------------------------------------------------------------------------

### Response Entities

  ------------------------------------------------------------------------------------
  Name                                Type        Description
  ----------------------------------- ----------- ------------------------------------
  **CompleteMultipartUploadResult**   Container   A container for the response.

  **Location**                        URI         The resource identifier (path) of
                                                  the new object.

  **Bucket**                          String      The name of the bucket that contains
                                                  the new object.

  **Key**                             String      The object\'s key.

  **ETag**                            String      The entity tag of the new object.
  ------------------------------------------------------------------------------------

## Abort Multipart Upload

### Syntax

    DELETE /{bucket}/{object}?uploadId= HTTP/1.1

## Append Object

Append data to an object. You must have write permissions on the bucket
to perform this operation. It is used to upload files in appending mode.
The type of the objects created by the Append Object operation is
Appendable Object, and the type of the objects uploaded with the Put
Object operation is Normal Object. **Append Object can\'t be used if
bucket versioning is enabled or suspended.** **Synced object will become
normal in multisite, but you can still append to the original object.**
**Compression and encryption features are disabled for Appendable
objects.**

### Syntax

    PUT /{bucket}/{object}?append&position= HTTP/1.1

### Request Headers

  -------------------------------------------------------------------------------------------
  Name                      Description         Valid Values                       Required
  ------------------------- ------------------- ---------------------------------- ----------
  **content-md5**           A base64 encoded    A string. No defaults or           No
                            MD-5 hash of the    constraints.                       
                            message.                                               

  **content-type**          A standard MIME     Any MIME type. Default:            No
                            type.               `binary/octet-stream`              

  **x-amz-meta-\<\...\>**   User metadata.      A string up to 8kb. No defaults.   No
                            Stored with the                                        
                            object.                                                

  **x-amz-acl**             A canned ACL.       `private`, `public-read`,          No
                                                `public-read-write`,               
                                                `authenticated-read`               
  -------------------------------------------------------------------------------------------

### Response Headers

  --------------------------------------------------------------------------------
  Name                             Description
  -------------------------------- -----------------------------------------------
  **x-rgw-next-append-position**   Next position to append object

  --------------------------------------------------------------------------------

### HTTP Response

The following HTTP response may be returned:

  ----------------------------------------------------------------------------
  HTTP Status Status Code                Description
  ----------- -------------------------- -------------------------------------
  **409**     PositionNotEqualToLength   Specified position does not match
                                         object length

  **409**     ObjectNotAppendable        Specified object can not be appended

  **409**     InvalidBucketstate         Bucket versioning is enabled or
                                         suspended
  ----------------------------------------------------------------------------

## Put Object Retention

Places an Object Retention configuration on an object.

### Syntax

    PUT /{bucket}/{object}?retention&versionId= HTTP/1.1

### Request Entities

+-----------+------+------------------------------------------+------+
| Name      | Type | Description                              | >    |
|           |      |                                          | Requ |
|           |      |                                          | ired |
+===========+======+==========================================+======+
| `R        | C    | A container for the request.             | >    |
| etention` | onta |                                          |  Yes |
|           | iner |                                          |      |
+-----------+------+------------------------------------------+------+
| `Mode`    | St   | Retention mode for the specified object. |      |
|           | ring | Valid Values: GOVERNANCE/COMPLIANCE \|   |      |
|           |      | Yes                                      |      |
+-----------+------+------------------------------------------+------+
| `RetainU  | T    | Retention date. Format:                  |      |
| ntilDate` | imes | 2020-01-05T00:00:00.000Z \| Yes          |      |
|           | tamp |                                          |      |
+-----------+------+------------------------------------------+------+

## Get Object Retention

Gets an Object Retention configuration on an object.

### Syntax

    GET /{bucket}/{object}?retention&versionId= HTTP/1.1

### Response Entities

+-----------+------+------------------------------------------+------+
| Name      | Type | Description                              | >    |
|           |      |                                          | Requ |
|           |      |                                          | ired |
+===========+======+==========================================+======+
| `R        | C    | A container for the request.             | >    |
| etention` | onta |                                          |  Yes |
|           | iner |                                          |      |
+-----------+------+------------------------------------------+------+
| `Mode`    | St   | Retention mode for the specified object. |      |
|           | ring | Valid Values: GOVERNANCE/COMPLIANCE \|   |      |
|           |      | Yes                                      |      |
+-----------+------+------------------------------------------+------+
| `RetainU  | T    | Retention date. Format:                  |      |
| ntilDate` | imes | 2020-01-05T00:00:00.000Z \| Yes          |      |
|           | tamp |                                          |      |
+-----------+------+------------------------------------------+------+

## Put Object Legal Hold

Applies a Legal Hold configuration to the specified object.

### Syntax

    PUT /{bucket}/{object}?legal-hold&versionId= HTTP/1.1

### Request Entities

+--------+------+----------------------------------------------+-----+
| Name   | Type | Description                                  | >   |
|        |      |                                              |  Re |
|        |      |                                              | qui |
|        |      |                                              | red |
+========+======+==============================================+=====+
| `Lega  | C    | A container for the request.                 | >   |
| lHold` | onta |                                              | Yes |
|        | iner |                                              |     |
+--------+------+----------------------------------------------+-----+
| `S     | St   | Indicates whether the specified object has a | >   |
| tatus` | ring | Legal Hold in place. Valid Values: ON/OFF    | Yes |
+--------+------+----------------------------------------------+-----+

## Get Object Legal Hold

Gets an object\'s current Legal Hold status.

### Syntax

    GET /{bucket}/{object}?legal-hold&versionId= HTTP/1.1

### Response Entities

+--------+------+----------------------------------------------+-----+
| Name   | Type | Description                                  | >   |
|        |      |                                              |  Re |
|        |      |                                              | qui |
|        |      |                                              | red |
+========+======+==============================================+=====+
| `Lega  | C    | A container for the request.                 | >   |
| lHold` | onta |                                              | Yes |
|        | iner |                                              |     |
+--------+------+----------------------------------------------+-----+
| `S     | St   | Indicates whether the specified object has a | >   |
| tatus` | ring | Legal Hold in place. Valid Values: ON/OFF    | Yes |
+--------+------+----------------------------------------------+-----+