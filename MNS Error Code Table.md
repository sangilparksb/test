# Basic OSS concepts
This section introduces the basic concepts of OSS.

## Object
An object (also known as a file) is a discrete unit of data. 

An object is composed of:
- Metadata, known as Object Meta, which is a key-value pair that expresses the object's attributes, such as its last modification time and size, as well as user-defined information 
- User data, known as Data 
- A unique object name, known as a Key 

The size of an object will vary depending on the upload method. Multipart Upload supports objects of up to 48.8 TB. Other upload methods only support objects of up to 5 GB.

An object's lifecycle starts from when it has been successfully uploaded, and ends when it has been deleted. During an object's lifecycle, its information cannot be changed. If you upload an object with a duplicate name in a bucket, it will overwrite the existing one. Therefore, unlike the file system, OSS does not allow users to modify only part of an object.

OSS provides the [Append Upload](~~31851~~) function, which allows users to continually append data to the end of an object.

The name of an object must comply with the following rules: 
- It must use UTF-8 encoding.
- It must be between 1-1023 bytes in length.
- It cannot start with a backslash "/" or forward slash "\".

>**NOTE:** Object names are case sensitive. 

##Bucket
A bucket is a virtual division of object storage that, unlike file systems, manages objects in a flat structure. 

Bucket properties are as follows:
- All objects must belong to a bucket, and during an object's lifecycle it remains directly affiliated with the corresponding bucket.
- A user can have multiple buckets, with each bucket able to contain an unlimited number of objects.
- You can set and modify the attributes of a bucket for region and object access control and object lifecycle management. These attributes apply to all objects in the bucket. 
- You can create different buckets to perform different management functions. 

The name of a bucket must comply with the following rules:
- It can only contain lower-case letters, digits, and hyphens (-). 
- It must start and end with a lower-case letter or number.
- It must be between 3-63 bytes in length.
- It must be globally unique within the OSS. 

