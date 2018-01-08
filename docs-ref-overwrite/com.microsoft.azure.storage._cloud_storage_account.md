---
uid: com.microsoft.azure.storage._cloud_storage_account
remarks: *content
---

Represents an [Azure Storage account](/azure/storage/common/storage-account-options) created from credentials. Use CloudStorageAccount client creation methods like `createBlobClient` to generate objects that access specific Azure Storage types.

```java
// Parse the connection string and create a blob client to interact with Blob storage
storageAccount = CloudStorageAccount.parse(storageConnectionString);
blobClient = storageAccount.createCloudBlobClient();
```