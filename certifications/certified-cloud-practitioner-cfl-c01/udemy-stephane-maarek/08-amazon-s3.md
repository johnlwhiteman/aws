# 08: Amazon S3

## Overview

* Infinite scaling storage
* AWS services use it

### Use Cases

* Backup and storage
* Disaster recovery
* Archive
* Hybrid cloud storage
* Application hosting
* Media hosting
* Data lakes & big data anlytics
* Software delivery
* Static websites
* Nasdaq stores 7 years of data into S3 Glacier

### S3 Buckets

* Stores objects (files) in "buckets" (directories)
* Buckets must have a globaly unique name (across all regions all accounts)
* Buckets are defined at the region level
* S3 looks like a global service but buckets are created in a region
* Naming convention
  * No uppercase, no underscore
  * 3-63 characters long
  * Not an IP
  * Must start with lowercase letter or number
  * Must NOT start with the prefix xn--
  * Must NOT end with the suffix --s3alias

### S3 Objects

* Objects (files) have a key
  * Keys are very long names that contain slashes ("/")
* The *key* is the FULL path:
  * s3://my-bucket/*my_file.txt*
  * s3://my-bucket/*my_folderI/another_foler/my_file.txt*
* The key is composed of prefix + object name
  * s3://my-bucket/*my_folder/another_folder/my_file.txt*
* There's not concept of "directories" within buckets
  * (although the UI will trick you to think otherwise)
* Object values are the content of the body
  * Max object size is 5TB (5000GB), must use "multi-part upload"
* Metadata (list of  text key / value pairs - system or user metadata)
* Tags (Unicode key / value pair - up to 10) -- useful for security / lifecycle
* Version ID (if versioning is enabled)





## References
