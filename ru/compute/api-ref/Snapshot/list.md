---
editable: false
sourcePath: en/_api-ref/compute/api-ref/Snapshot/list.md
---


# Method list
Retrieves the list of Snapshot resources in the specified folder.
 

 
## HTTP request {#https-request}
```
GET https://compute.api.cloud.yandex.net/compute/v1/snapshots
```
 
## Query parameters {#query_params}
 
Parameter | Description
--- | ---
folderId | Required. ID of the folder to list snapshots in. To get the folder ID, use a [list](/docs/resource-manager/api-ref/Folder/list) request.  The maximum string length in characters is 50.
pageSize | The maximum number of results per page to return. If the number of available results is larger than [pageSize](/docs/compute/api-ref/Snapshot/list#query_params), the service returns a [nextPageToken](/docs/compute/api-ref/Snapshot/list#responses) that can be used to get the next page of results in subsequent list requests.  The maximum value is 1000.
pageToken | Page token. To get the next page of results, set [pageToken](/docs/compute/api-ref/Snapshot/list#query_params) to the [nextPageToken](/docs/compute/api-ref/Snapshot/list#responses) returned by a previous list request.  The maximum string length in characters is 100.
filter | A filter expression that filters resources listed in the response. The expression must specify: 1. The field name. Currently you can use filtering only on the [Snapshot.name](/docs/compute/api-ref/Snapshot#representation) field. 2. An `=` operator. 3. The value in double quotes (`"`). Must be 3-63 characters long and match the regular expression `[a-z]([-a-z0-9]{,61}[a-z0-9])?`.  The maximum string length in characters is 1000.
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "snapshots": [
    {
      "id": "string",
      "folderId": "string",
      "createdAt": "string",
      "name": "string",
      "description": "string",
      "labels": "object",
      "storageSize": "string",
      "diskSize": "string",
      "productIds": [
        "string"
      ],
      "status": "string",
      "sourceDiskId": "string"
    }
  ],
  "nextPageToken": "string"
}
```

 
Field | Description
--- | ---
snapshots[] | **object**<br><p>A Snapshot resource. For more information, see <a href="/docs/compute/concepts/snapshot">Snapshots</a>.</p> 
snapshots[].<br>id | **string**<br><p>ID of the snapshot.</p> 
snapshots[].<br>folderId | **string**<br><p>ID of the folder that the snapshot belongs to.</p> 
snapshots[].<br>createdAt | **string** (date-time)<br><p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
snapshots[].<br>name | **string**<br><p>Name of the snapshot. 1-63 characters long.</p> 
snapshots[].<br>description | **string**<br><p>Description of the snapshot. 0-256 characters long.</p> 
snapshots[].<br>labels | **object**<br><p>Resource labels as ``key:value`` pairs. Maximum of 64 per resource.</p> 
snapshots[].<br>storageSize | **string** (int64)<br><p>Size of the snapshot, specified in bytes.</p> 
snapshots[].<br>diskSize | **string** (int64)<br><p>Size of the disk when the snapshot was created, specified in bytes.</p> 
snapshots[].<br>productIds[] | **string**<br><p>License IDs that indicate which licenses are attached to this resource. License IDs are used to calculate additional charges for the use of the virtual machine.</p> <p>The correct license ID is generated by Yandex.Cloud. IDs are inherited by new resources created from this resource.</p> <p>If you know the license IDs, specify them when you create the image. For example, if you create a disk image using a third-party utility and load it into Yandex Object Storage, the license IDs will be lost. You can specify them in the <a href="/docs/compute/api-ref/Image/create">create</a> request.</p> 
snapshots[].<br>status | **string**<br><p>Current status of the snapshot.</p> <ul> <li>CREATING: Snapshot is being created.</li> <li>READY: Snapshot is ready to use.</li> <li>ERROR: Snapshot encountered a problem and cannot operate.</li> <li>DELETING: Snapshot is being deleted.</li> </ul> 
snapshots[].<br>sourceDiskId | **string**<br><p>ID of the source disk used to create this snapshot.</p> 
nextPageToken | **string**<br><p>This token allows you to get the next page of results for list requests. If the number of results is larger than <a href="/docs/compute/api-ref/Snapshot/list#query_params">pageSize</a>, use the <a href="/docs/compute/api-ref/Snapshot/list#responses">nextPageToken</a> as the value for the <a href="/docs/compute/api-ref/Snapshot/list#query_params">pageToken</a> query parameter in the next list request. Each subsequent list request will have its own <a href="/docs/compute/api-ref/Snapshot/list#responses">nextPageToken</a> to continue paging through the results.</p> 