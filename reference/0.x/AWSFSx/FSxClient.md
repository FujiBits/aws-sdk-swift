# FSxClient

``` swift
public class FSxClient 
```

## Inheritance

[`FSxClientProtocol`](/aws-sdk-swift/reference/0.x/AWSFSx/FSxClientProtocol)

## Initializers

### `init(config:)`

``` swift
public init(config: AWSClientRuntime.AWSClientConfiguration) 
```

### `init(region:)`

``` swift
public convenience init(region: Swift.String? = nil) throws 
```

## Properties

### `clientName`

``` swift
public static let clientName = "FSxClient"
```

## Methods

### `associateFileSystemAliases(input:completion:)`

Use this action to associate one or more Domain Name Server (DNS) aliases with an existing Amazon FSx for Windows File Server file system. A file system can have a maximum of 50 DNS aliases associated with it at any one time. If you try to associate a DNS alias that is already associated with the file system, FSx takes no action on that alias in the request. For more information, see [Working with DNS Aliases](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/managing-dns-aliases.html) and [Walkthrough 5: Using DNS aliases to access your file system](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/walkthrough05-file-system-custom-CNAME.html), including additional steps you must take to be able to access your file system using a DNS alias. The system response shows the DNS aliases that Amazon FSx is attempting to associate with the file system. Use the API operation to monitor the status of the aliases Amazon FSx is associating with the file system.

``` swift
public func associateFileSystemAliases(input: AssociateFileSystemAliasesInput, completion: @escaping (ClientRuntime.SdkResult<AssociateFileSystemAliasesOutputResponse, AssociateFileSystemAliasesOutputError>) -> Void)
```

### `cancelDataRepositoryTask(input:completion:)`

Cancels an existing Amazon FSx for Lustre data repository task if that task is in either the PENDING or EXECUTING state. When you cancel a task, Amazon FSx does the following.

``` swift
public func cancelDataRepositoryTask(input: CancelDataRepositoryTaskInput, completion: @escaping (ClientRuntime.SdkResult<CancelDataRepositoryTaskOutputResponse, CancelDataRepositoryTaskOutputError>) -> Void)
```

  - Any files that FSx has already exported are not reverted.

  - FSx continues to export any files that are "in-flight" when the cancel operation is received.

  - FSx does not export any files that have not yet been exported.

### `copyBackup(input:completion:)`

Copies an existing backup within the same Amazon Web Services account to another Amazon Web Services Region (cross-Region copy) or within the same Amazon Web Services Region (in-Region copy). You can have up to five backup copy requests in progress to a single destination Region per account. You can use cross-Region backup copies for cross-region disaster recovery. You periodically take backups and copy them to another Region so that in the event of a disaster in the primary Region, you can restore from backup and recover availability quickly in the other Region. You can make cross-Region copies only within your Amazon Web Services partition. You can also use backup copies to clone your file data set to another Region or within the same Region. You can use the SourceRegion parameter to specify the Amazon Web Services Region from which the backup will be copied. For example, if you make the call from the us-west-1 Region and want to copy a backup from the us-east-2 Region, you specify us-east-2 in the SourceRegion parameter to make a cross-Region copy. If you don't specify a Region, the backup copy is created in the same Region where the request is sent from (in-Region copy). For more information on creating backup copies, see [ Copying backups](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/using-backups.html#copy-backups) in the Amazon FSx for Windows User Guide and [Copying backups](https://docs.aws.amazon.com/fsx/latest/LustreGuide/using-backups-fsx.html#copy-backups) in the Amazon FSx for Lustre User Guide.

``` swift
public func copyBackup(input: CopyBackupInput, completion: @escaping (ClientRuntime.SdkResult<CopyBackupOutputResponse, CopyBackupOutputError>) -> Void)
```

### `createBackup(input:completion:)`

Creates a backup of an existing Amazon FSx for Windows File Server or Amazon FSx for Lustre file system, or of an Amazon FSx for NetApp ONTAP volume. Creating regular backups is a best practice, enabling you to restore a file system or volume from a backup if an issue arises with the original file system or volume. For Amazon FSx for Lustre file systems, you can create a backup only for file systems with the following configuration:

``` swift
public func createBackup(input: CreateBackupInput, completion: @escaping (ClientRuntime.SdkResult<CreateBackupOutputResponse, CreateBackupOutputError>) -> Void)
```

  - a Persistent deployment type

  - is not linked to a data repository.

For more information about backups, see the following:

  - For Amazon FSx for Lustre, see [Working with FSx for Lustre backups](https://docs.aws.amazon.com/fsx/latest/LustreGuide/using-backups-fsx.html).

  - For Amazon FSx for Windows, see [Working with FSx for Windows backups](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/using-backups.html).

  - For Amazon FSx for NetApp ONTAP, see [Working with FSx for NetApp ONTAP backups](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/using-backups.html).

If a backup with the specified client request token exists, and the parameters match, this operation returns the description of the existing backup. If a backup specified client request token exists, and the parameters don't match, this operation returns IncompatibleParameterError. If a backup with the specified client request token doesn't exist, CreateBackup does the following:

  - Creates a new Amazon FSx backup with an assigned ID, and an initial lifecycle state of CREATING.

  - Returns the description of the backup.

By using the idempotent operation, you can retry a CreateBackup operation without the risk of creating an extra backup. This approach can be useful when an initial call fails in a way that makes it unclear whether a backup was created. If you use the same client request token and the initial call created a backup, the operation returns a successful result because all the parameters are the same. The CreateBackup operation returns while the backup's lifecycle state is still CREATING. You can check the backup creation status by calling the \[DescribeBackups\] operation, which returns the backup state along with other information.

### `createDataRepositoryTask(input:completion:)`

Creates an Amazon FSx for Lustre data repository task. You use data repository tasks to perform bulk operations between your Amazon FSx file system and its linked data repository. An example of a data repository task is exporting any data and metadata changes, including POSIX metadata, to files, directories, and symbolic links (symlinks) from your FSx file system to its linked data repository. A CreateDataRepositoryTask operation will fail if a data repository is not linked to the FSx file system. To learn more about data repository tasks, see [Data Repository Tasks](https://docs.aws.amazon.com/fsx/latest/LustreGuide/data-repository-tasks.html). To learn more about linking a data repository to your file system, see [Linking your file system to an S3 bucket](https://docs.aws.amazon.com/fsx/latest/LustreGuide/create-fs-linked-data-repo.html).

``` swift
public func createDataRepositoryTask(input: CreateDataRepositoryTaskInput, completion: @escaping (ClientRuntime.SdkResult<CreateDataRepositoryTaskOutputResponse, CreateDataRepositoryTaskOutputError>) -> Void)
```

### `createFileSystem(input:completion:)`

Creates a new, empty Amazon FSx file system. If a file system with the specified client request token exists and the parameters match, CreateFileSystem returns the description of the existing file system. If a file system specified client request token exists and the parameters don't match, this call returns IncompatibleParameterError. If a file system with the specified client request token doesn't exist, CreateFileSystem does the following:

``` swift
public func createFileSystem(input: CreateFileSystemInput, completion: @escaping (ClientRuntime.SdkResult<CreateFileSystemOutputResponse, CreateFileSystemOutputError>) -> Void)
```

  - Creates a new, empty Amazon FSx file system with an assigned ID, and an initial lifecycle state of CREATING.

  - Returns the description of the file system.

This operation requires a client request token in the request that Amazon FSx uses to ensure idempotent creation. This means that calling the operation multiple times with the same client request token has no effect. By using the idempotent operation, you can retry a CreateFileSystem operation without the risk of creating an extra file system. This approach can be useful when an initial call fails in a way that makes it unclear whether a file system was created. Examples are if a transport level timeout occurred, or your connection was reset. If you use the same client request token and the initial call created a file system, the client receives success as long as the parameters are the same. The CreateFileSystem call returns while the file system's lifecycle state is still CREATING. You can check the file-system creation status by calling the \[DescribeFileSystems\] operation, which returns the file system state along with other information.

### `createFileSystemFromBackup(input:completion:)`

Creates a new Amazon FSx for Lustre or Amazon FSx for Windows File Server file system from an existing Amazon FSx backup. If a file system with the specified client request token exists and the parameters match, this operation returns the description of the file system. If a client request token specified by the file system exists and the parameters don't match, this call returns IncompatibleParameterError. If a file system with the specified client request token doesn't exist, this operation does the following:

``` swift
public func createFileSystemFromBackup(input: CreateFileSystemFromBackupInput, completion: @escaping (ClientRuntime.SdkResult<CreateFileSystemFromBackupOutputResponse, CreateFileSystemFromBackupOutputError>) -> Void)
```

  - Creates a new Amazon FSx file system from backup with an assigned ID, and an initial lifecycle state of CREATING.

  - Returns the description of the file system.

Parameters like Active Directory, default share name, automatic backup, and backup settings default to the parameters of the file system that was backed up, unless overridden. You can explicitly supply other settings. By using the idempotent operation, you can retry a CreateFileSystemFromBackup call without the risk of creating an extra file system. This approach can be useful when an initial call fails in a way that makes it unclear whether a file system was created. Examples are if a transport level timeout occurred, or your connection was reset. If you use the same client request token and the initial call created a file system, the client receives success as long as the parameters are the same. The CreateFileSystemFromBackup call returns while the file system's lifecycle state is still CREATING. You can check the file-system creation status by calling the \[DescribeFileSystems\] operation, which returns the file system state along with other information.

### `createStorageVirtualMachine(input:completion:)`

Creates a storage virtual machine (SVM) for an Amazon FSx for ONTAP file system.

``` swift
public func createStorageVirtualMachine(input: CreateStorageVirtualMachineInput, completion: @escaping (ClientRuntime.SdkResult<CreateStorageVirtualMachineOutputResponse, CreateStorageVirtualMachineOutputError>) -> Void)
```

### `createVolume(input:completion:)`

Creates an Amazon FSx for NetApp ONTAP storage volume.

``` swift
public func createVolume(input: CreateVolumeInput, completion: @escaping (ClientRuntime.SdkResult<CreateVolumeOutputResponse, CreateVolumeOutputError>) -> Void)
```

### `createVolumeFromBackup(input:completion:)`

Creates a new Amazon FSx for NetApp ONTAP volume from an existing Amazon FSx volume backup.

``` swift
public func createVolumeFromBackup(input: CreateVolumeFromBackupInput, completion: @escaping (ClientRuntime.SdkResult<CreateVolumeFromBackupOutputResponse, CreateVolumeFromBackupOutputError>) -> Void)
```

### `deleteBackup(input:completion:)`

Deletes an Amazon FSx backup, deleting its contents. After deletion, the backup no longer exists, and its data is gone. The DeleteBackup call returns instantly. The backup will not show up in later DescribeBackups calls. The data in a deleted backup is also deleted and can't be recovered by any means.

``` swift
public func deleteBackup(input: DeleteBackupInput, completion: @escaping (ClientRuntime.SdkResult<DeleteBackupOutputResponse, DeleteBackupOutputError>) -> Void)
```

### `deleteFileSystem(input:completion:)`

Deletes a file system, deleting its contents. After deletion, the file system no longer exists, and its data is gone. Any existing automatic backups will also be deleted. To delete an Amazon FSx for NetApp ONTAP file system, first delete all the volumes and SVMs on the file system. Then provide a FileSystemId value to the DeleFileSystem operation. By default, when you delete an Amazon FSx for Windows File Server file system, a final backup is created upon deletion. This final backup is not subject to the file system's retention policy, and must be manually deleted. The DeleteFileSystem action returns while the file system has the DELETING status. You can check the file system deletion status by calling the \[DescribeFileSystems\] action, which returns a list of file systems in your account. If you pass the file system ID for a deleted file system, the \[DescribeFileSystems\] returns a FileSystemNotFound error. Deleting an Amazon FSx for Lustre file system will fail with a 400 BadRequest if a data repository task is in a PENDING or EXECUTING state. The data in a deleted file system is also deleted and can't be recovered by any means.

``` swift
public func deleteFileSystem(input: DeleteFileSystemInput, completion: @escaping (ClientRuntime.SdkResult<DeleteFileSystemOutputResponse, DeleteFileSystemOutputError>) -> Void)
```

### `deleteStorageVirtualMachine(input:completion:)`

Deletes an existing Amazon FSx for ONTAP storage virtual machine (SVM). Prior to deleting an SVM, you must delete all non-root volumes in the SVM, otherwise the operation will fail.

``` swift
public func deleteStorageVirtualMachine(input: DeleteStorageVirtualMachineInput, completion: @escaping (ClientRuntime.SdkResult<DeleteStorageVirtualMachineOutputResponse, DeleteStorageVirtualMachineOutputError>) -> Void)
```

### `deleteVolume(input:completion:)`

Deletes an Amazon FSx for NetApp ONTAP volume. When deleting a volume, you have the option of creating a final backup. If you create a final backup, you have the option to apply Tags to the backup. You need to have fsx:TagResource permission in order to apply tags to the backup.

``` swift
public func deleteVolume(input: DeleteVolumeInput, completion: @escaping (ClientRuntime.SdkResult<DeleteVolumeOutputResponse, DeleteVolumeOutputError>) -> Void)
```

### `describeBackups(input:completion:)`

Returns the description of specific Amazon FSx backups, if a BackupIds value is provided for that backup. Otherwise, it returns all backups owned by your Amazon Web Services account in the Amazon Web Services Region of the endpoint that you're calling. When retrieving all backups, you can optionally specify the MaxResults parameter to limit the number of backups in a response. If more backups remain, Amazon FSx returns a NextToken value in the response. In this case, send a later request with the NextToken request parameter set to the value of NextToken from the last response. This action is used in an iterative process to retrieve a list of your backups. DescribeBackups is called first without a NextTokenvalue. Then the action continues to be called with the NextToken parameter set to the value of the last NextToken value until a response has no NextToken. When using this action, keep the following in mind:

``` swift
public func describeBackups(input: DescribeBackupsInput, completion: @escaping (ClientRuntime.SdkResult<DescribeBackupsOutputResponse, DescribeBackupsOutputError>) -> Void)
```

  - The implementation might return fewer than MaxResults backup descriptions while still including a NextToken value.

  - The order of backups returned in the response of one DescribeBackups call and the order of backups returned across the responses of a multi-call iteration is unspecified.

### `describeDataRepositoryTasks(input:completion:)`

Returns the description of specific Amazon FSx for Lustre data repository tasks, if one or more TaskIds values are provided in the request, or if filters are used in the request. You can use filters to narrow the response to include just tasks for specific file systems, or tasks in a specific lifecycle state. Otherwise, it returns all data repository tasks owned by your Amazon Web Services account in the Amazon Web Services Region of the endpoint that you're calling. When retrieving all tasks, you can paginate the response by using the optional MaxResults parameter to limit the number of tasks returned in a response. If more tasks remain, Amazon FSx returns a NextToken value in the response. In this case, send a later request with the NextToken request parameter set to the value of NextToken from the last response.

``` swift
public func describeDataRepositoryTasks(input: DescribeDataRepositoryTasksInput, completion: @escaping (ClientRuntime.SdkResult<DescribeDataRepositoryTasksOutputResponse, DescribeDataRepositoryTasksOutputError>) -> Void)
```

### `describeFileSystemAliases(input:completion:)`

Returns the DNS aliases that are associated with the specified Amazon FSx for Windows File Server file system. A history of all DNS aliases that have been associated with and disassociated from the file system is available in the list of \[AdministrativeAction\] provided in the \[DescribeFileSystems\] operation response.

``` swift
public func describeFileSystemAliases(input: DescribeFileSystemAliasesInput, completion: @escaping (ClientRuntime.SdkResult<DescribeFileSystemAliasesOutputResponse, DescribeFileSystemAliasesOutputError>) -> Void)
```

### `describeFileSystems(input:completion:)`

Returns the description of specific Amazon FSx file systems, if a FileSystemIds value is provided for that file system. Otherwise, it returns descriptions of all file systems owned by your Amazon Web Services account in the Amazon Web Services Region of the endpoint that you're calling. When retrieving all file system descriptions, you can optionally specify the MaxResults parameter to limit the number of descriptions in a response. If more file system descriptions remain, Amazon FSx returns a NextToken value in the response. In this case, send a later request with the NextToken request parameter set to the value of NextToken from the last response. This action is used in an iterative process to retrieve a list of your file system descriptions. DescribeFileSystems is called first without a NextTokenvalue. Then the action continues to be called with the NextToken parameter set to the value of the last NextToken value until a response has no NextToken. When using this action, keep the following in mind:

``` swift
public func describeFileSystems(input: DescribeFileSystemsInput, completion: @escaping (ClientRuntime.SdkResult<DescribeFileSystemsOutputResponse, DescribeFileSystemsOutputError>) -> Void)
```

  - The implementation might return fewer than MaxResults file system descriptions while still including a NextToken value.

  - The order of file systems returned in the response of one DescribeFileSystems call and the order of file systems returned across the responses of a multicall iteration is unspecified.

### `describeStorageVirtualMachines(input:completion:)`

Describes one or more Amazon FSx for NetApp ONTAP storage virtual machines (SVMs).

``` swift
public func describeStorageVirtualMachines(input: DescribeStorageVirtualMachinesInput, completion: @escaping (ClientRuntime.SdkResult<DescribeStorageVirtualMachinesOutputResponse, DescribeStorageVirtualMachinesOutputError>) -> Void)
```

### `describeVolumes(input:completion:)`

Describes one or more Amazon FSx for NetApp ONTAP volumes.

``` swift
public func describeVolumes(input: DescribeVolumesInput, completion: @escaping (ClientRuntime.SdkResult<DescribeVolumesOutputResponse, DescribeVolumesOutputError>) -> Void)
```

### `disassociateFileSystemAliases(input:completion:)`

Use this action to disassociate, or remove, one or more Domain Name Service (DNS) aliases from an Amazon FSx for Windows File Server file system. If you attempt to disassociate a DNS alias that is not associated with the file system, Amazon FSx responds with a 400 Bad Request. For more information, see [Working with DNS Aliases](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/managing-dns-aliases.html). The system generated response showing the DNS aliases that Amazon FSx is attempting to disassociate from the file system. Use the API operation to monitor the status of the aliases Amazon FSx is disassociating with the file system.

``` swift
public func disassociateFileSystemAliases(input: DisassociateFileSystemAliasesInput, completion: @escaping (ClientRuntime.SdkResult<DisassociateFileSystemAliasesOutputResponse, DisassociateFileSystemAliasesOutputError>) -> Void)
```

### `listTagsForResource(input:completion:)`

Lists tags for an Amazon FSx file systems and backups in the case of Amazon FSx for Windows File Server. When retrieving all tags, you can optionally specify the MaxResults parameter to limit the number of tags in a response. If more tags remain, Amazon FSx returns a NextToken value in the response. In this case, send a later request with the NextToken request parameter set to the value of NextToken from the last response. This action is used in an iterative process to retrieve a list of your tags. ListTagsForResource is called first without a NextTokenvalue. Then the action continues to be called with the NextToken parameter set to the value of the last NextToken value until a response has no NextToken. When using this action, keep the following in mind:

``` swift
public func listTagsForResource(input: ListTagsForResourceInput, completion: @escaping (ClientRuntime.SdkResult<ListTagsForResourceOutputResponse, ListTagsForResourceOutputError>) -> Void)
```

  - The implementation might return fewer than MaxResults file system descriptions while still including a NextToken value.

  - The order of tags returned in the response of one ListTagsForResource call and the order of tags returned across the responses of a multi-call iteration is unspecified.

### `tagResource(input:completion:)`

Tags an Amazon FSx resource.

``` swift
public func tagResource(input: TagResourceInput, completion: @escaping (ClientRuntime.SdkResult<TagResourceOutputResponse, TagResourceOutputError>) -> Void)
```

### `untagResource(input:completion:)`

This action removes a tag from an Amazon FSx resource.

``` swift
public func untagResource(input: UntagResourceInput, completion: @escaping (ClientRuntime.SdkResult<UntagResourceOutputResponse, UntagResourceOutputError>) -> Void)
```

### `updateFileSystem(input:completion:)`

Use this operation to update the configuration of an existing Amazon FSx file system. You can update multiple properties in a single request. For Amazon FSx for Windows File Server file systems, you can update the following properties:

``` swift
public func updateFileSystem(input: UpdateFileSystemInput, completion: @escaping (ClientRuntime.SdkResult<UpdateFileSystemOutputResponse, UpdateFileSystemOutputError>) -> Void)
```

  - AuditLogConfiguration

  - AutomaticBackupRetentionDays

  - DailyAutomaticBackupStartTime

  - SelfManagedActiveDirectoryConfiguration

  - StorageCapacity

  - ThroughputCapacity

  - WeeklyMaintenanceStartTime

For Amazon FSx for Lustre file systems, you can update the following properties:

  - AutoImportPolicy

  - AutomaticBackupRetentionDays

  - DailyAutomaticBackupStartTime

  - DataCompressionType

  - StorageCapacity

  - WeeklyMaintenanceStartTime

For Amazon FSx for NetApp ONTAP file systems, you can update the following properties:

  - AutomaticBackupRetentionDays

  - DailyAutomaticBackupStartTime

  - FsxAdminPassword

  - WeeklyMaintenanceStartTime

### `updateStorageVirtualMachine(input:completion:)`

Updates an Amazon FSx for ONTAP storage virtual machine (SVM).

``` swift
public func updateStorageVirtualMachine(input: UpdateStorageVirtualMachineInput, completion: @escaping (ClientRuntime.SdkResult<UpdateStorageVirtualMachineOutputResponse, UpdateStorageVirtualMachineOutputError>) -> Void)
```

### `updateVolume(input:completion:)`

Updates an Amazon FSx for NetApp ONTAP volume's configuration.

``` swift
public func updateVolume(input: UpdateVolumeInput, completion: @escaping (ClientRuntime.SdkResult<UpdateVolumeOutputResponse, UpdateVolumeOutputError>) -> Void)
```
