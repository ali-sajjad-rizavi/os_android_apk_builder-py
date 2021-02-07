Introduction
------------

This module will create an Android APK/App Bundle programmatically (dynamically), from an Android project, faster and without Android Studio.

## Installation
Install via pip:

```python 
pip install os-android-apk-builder
```

## Usage       
    
First, define your KeyStore and version properties:


```python
from os_android_apk_builder.objs.KeyStoreProperties import KeyStoreProperties
from os_android_apk_builder.objs.VersionProperties import VersionProperties


# set your KeyStore properties
key_store_props = KeyStoreProperties(key_store_file_path='/path/to/keystore/file.jks',
                                     store_password='StorePassword123',
                                     key_alias='alias name',
                                     key_password='KeyPassword123',
                                     v1_signing_enabled=True,
                                     v2_signing_enabled=True)

# set the version properties (version code and version name)
version_props = VersionProperties(new_version_code=VersionProperties.RAISE_VERSION_BY_ONE,
new_version_name="1.0.3")
```

Now, generate an apk or app bundle below:
    
# Generate APK
```python
from os_android_apk_builder import apk_builder

apk_builder.build_apk(project_path='/path/to/android/project',
                      apk_dst_dir_path='/path/to/apk/output/directory',
                      key_store_properties=key_store_props,
                      version_properties=version_props)
```

# Generate AppBundle
```python
from os_android_apk_builder import apk_builder

apk_builder.build_app_bundle(project_path='/path/to/android/project',
                             app_bundle_dst_dir_path='/path/to/app/bundle/output/directory',
                             key_store_properties=key_store_props,
                             version_properties=version_props)
```

## Advanced Usage
You can save your Key Store properties in a file, to avoid supplying them again with each binary build.

Todo so, create a json file (or copy this [sign_in_example.json](os_android_apk_builder/examples/properties_example.json) file): 
```json
{
  "storeFile": "path/to/keystore_file.keystore",
  "storePassword": "myCoolKeyStorePass",
  "keyAlias": "myAliasName",
  "keyPassword": "myAliasPassword",
  "v1SigningEnabled": true,
  "v2SigningEnabled": true
}
```

Then build the KeyStoreProperties base on the link to the file: 

```python
key_store_props = KeyStoreProperties.build_from_file(file_path= 'path/to/json/file.xml')
```    

Furthermore, if the gradle wrapper isn't good enough, you can run the gradle from your system. Just supply it's path when creating the apk/app bundle with the argument: 
    
    gradle_path='path/to/gradle'

(you can write just 'gradle' if it's already recognized by your environment variables).


## Licence
MIT
