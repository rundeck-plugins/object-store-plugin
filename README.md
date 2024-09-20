**NOTE**: this repo is not used, the code for this plugin exists in https://github.com/rundeck/rundeck


# Object Store Plugin

Save Rundeck data in an Amazon S3 compliant object store. 

### Configuring the plugin

The Object Store plugin can be configured by using the following pattern in the `rundeck-config.properties` file.

Example configuration using a Minio server

    rundeck.storage.provider.1.type=object
    rundeck.storage.provider.1.path=keys
    rundeck.storage.provider.1.config.bucket=key-storage-bucket
    rundeck.storage.provider.1.config.objectStoreUrl=http://x.x.x.x:9000
    rundeck.storage.provider.1.config.secretKey=<Your Minio Secret Key>
    rundeck.storage.provider.1.config.accessKey=<Your Minio Access Key>
    
#### Object lookup details

By default the plugin will cache the directory structure of the objects in the store in memory. 
This makes lookup operations much faster. However, if your object store is being written to by
multiple sources the plugin may get out of sync regarding the object that are actually in the store.
If you would like to use uncached lookups, you can set the property:

    rundeck.storage.provider.1.config.uncachedObjectLookup=true
    
This may incure a significant performance penalty because the plugin will query the object store every
time it needs to do a lookup operation, but it will allow you to access objects written by other sources. 
