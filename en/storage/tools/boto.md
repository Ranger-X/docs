# boto3 and boto

[The boto3](https://github.com/boto/boto3) and [boto](https://github.com/boto/boto) development tools offer SDKs for the Python 2.x and 3.x programming languages. The SDKs are designed for working with AWS services.

## Before you start {#before-you-begin}

{% include [aws-tools-prepare](../../_includes/aws-tools/aws-tools-prepare.md) %}

## Installation {#installation}

{% include [install-boto](../../_includes/aws-tools/install-boto.md)%}

## Setup {#setup}

{% include [storage-sdk-setup](../_includes_service/storage-sdk-setup-storage-url.md) %}

## Example {#boto-example}

{% list tabs %}

- boto3

  ```python
  #!/usr/bin/env python
  #-*- coding: utf-8 -*-
  import boto3
  session = boto3.session.Session()
  s3 = session.client(
      service_name='s3',
      endpoint_url='https://{{ s3-storage-host }}'
  )
  
  # Creating a new bucket
  s3.create_bucket(Bucket='bucket-name')
  
  # Uploading objects into a bucket
  
  ## From a string
  s3.put_object(Bucket='bucket-name', Key='object_name', Body='TEST', StorageClass='COLD')
  
  ## From a file
  s3.upload_file('this_script.py', 'bucket-name', 'py_script.py')
  s3.upload_file('this_script.py', 'bucket-name', 'script/py_script.py')
  
  # Getting a list of objects in a bucket
  for key in s3.list_objects(Bucket='bucket-name')['Contents']:
      print(key['Key'])
  
  # Deleting multiple objects
  forDeletion = [{'Key':'object_name'}, {'Key':'script/py_script.py'}]
  response = s3.delete_objects(Bucket='bucket-name', Delete={'Objects': forDeletion})
  
  # Retrieving an object
  get_object_response = s3.get_object(Bucket='bucket-name',Key='py_script.py')
  print(get_object_response['Body'].read())
  ```

- boto

  ```python
  #!/usr/bin/env python
  #-*- coding: utf-8 -*-
  import os
  from boto.s3.key import Key
  from boto.s3.connection import S3Connection
  os.environ['S3_USE_SIGV4'] = 'True'
  conn = S3Connection(
      host='{{ s3-storage-host }}'
  )
  conn.auth_region_name = 'ru-central1'
  
  # Creating a new bucket
  conn.create_bucket('bucket-name')
  bucket = conn.get_bucket('bucket-name')
  
  # Uploading objects into a bucket
  
  ## From a string
  bucket.new_key('test-string').set_contents_from_string('TEST')
  
  ## From a file
  file_key_1 = Key(bucket)
  file_key_1.key = 'py_script.py'
  file_key_1.set_contents_from_filename('this_script.py')
  file_key_2 = Key(bucket)
  file_key_2.key = 'script/py_script.py'
  file_key_2.set_contents_from_filename('this_script.py')
  
  # Getting a list of objects in a bucket
  keys_list=bucket.list()
  for key in keys_list:
      print key.key
  
  # Deleting multiple objects
  response = bucket.delete_keys(['test-string', 'py_script.py'])
  
  # Retrieving an object
  key = bucket.get_key('script/py_script.py')
  print key.get_contents_as_string()
  ```

{% endlist %}

