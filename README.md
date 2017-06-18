# xStoragePool

The xStoragePool Module is intended to manage storage pools. In the first release, only a storage pool with a stripe set can be created using selected physical disks. In the near future, extra DSC resources will be added to the module.

# Description

The xStoragePool module contains the xStripeSet DSC Resource.

# Resources

* xStripeSet: creates a storage pool, a virtual disk and formats the created volume

# xStripeSet

* diskNumbers: DeviceID of the selected disks
* storagePoolName: Name for the Storage Pool that will be created
* virtualDiskName: Name of the virtual Disk that will be created
* driveLetter: Driveletter that will be assigned to the volume

# Versions

### 1.0.0.1
* Update of the xStripeSet DSC Resource
    * Completed all tests in the DSC test-step
    * Changed set-step so a configuration van be completed when parts already exist (e.g. Storage Pool was already created in a previous run, but something went wrong in one of the next steps.)

### 1.0.0.0
* Initial release with the following resources:
  * xStripeSet
  
# Examples

Create a stripe set using physical disk 1 and 2 and assign driveletter F to it.

```PowerShell
Configuration StoragePool
{
    Import-DscResource -ModuleName xStoragePool

    node localhost
    {
        xStripeSet SQLStoragePool
        {
            diskNumbers = 1,2
            storagePoolName = "StoragePool"
            virtualDiskName = "vDisk"
            driveLetter = "F"
        }
    }
}
```

To find out the DeviceID of the disks, you can use the following command:

```PowerShell
Get-PhysicalDisk | Select FriendlyName, DeviceId
```

