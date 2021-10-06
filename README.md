# boto3_digitalOcean_s3_compatibility
Note! -> This repository contains all the working code which i'm using in my project: apkfuel.com

This repository contains the below functionalities:

(1): Upload data to digital ocean space on root directory or to sub-directory of space/bucket

import os

import boto3

import sys

from boto3.session import Session

from io import BytesIO

#file_name is the desired file name to upload on digital ocean space

file_name = 'my_file.txt'

session = boto3.session.Session()

#access key and secret is to be generated from digital ocean api page: https://cloud.digitalocean.com/account/api/

#session.client parameters: 

                           # region_name = enter region name like sfo3 which means your space is in the 'San Francisco' datacenter)
                           
                           # endpint_url = https://*.digitaloceanspaces.com -> add sfo3 in place of * if your space datacenter is 'San Francisco'
                           
                           # aws_access_key_id = generate access key from api page
                           
                           # aws_secret_accesss_key = copy the secret from api page
                           
client = session.client('s3',
                        region_name='sfo3',
                        endpoint_url='https://sfo3.digitaloceanspaces.com',
                        aws_access_key_id='enter_your_access_key',
                        aws_secret_access_key='enter_your_secret_key')
                      

#client.upload_file() parameters: 
                          # path: for example '/home/apkfuel/public_html/apk-downloader/user_content/apk_data/'
                          
                          # bucket-name: for example 'play.savegoogle.com'
                          
                          # final_name_of_file: for example 'subfolder/' + file_name -> DONT use subfolder i.e 'subfolder/' if you want to upload your file in the main directory, hence the main directory upload code line will become: file_name
                          
                          # ExtraArgs: for making the file public -> dont use this line if you want our file to be private
                          
client.upload_file(
    '/path/' + file_name, 'bucket-name', 'final_name_of_file_with_extention',
    
    ExtraArgs={'ACL': 'public-read'}
    
)
