# CMIS 1.1 JSON REST API  #

## cmis type with versioning(not sure)##
```
cmisbook:album
cmisbook:audio
cmisbook:image
cmisbook:lyrics
cmisbook:media
cmisbook:note
cmisbook:officeDocument
cmisbook:pdf
cmisbook:poem
cmisbook:taggable
cmisbook:text
cmisbook:video
```

## browse the repo##
* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}
```

* http_method:

```url
get
```

## create new docuemnt##
* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={object_id}
```
* http_method:

```url
post
```

* http_header:

```url
Authorization: Basic {encoded_message_of("username:password")}
```

* multipart/formdata:

```url
{--multipart-boundary}
Content-Disposition: form-data; name="propertyId[0]"
Content-Type: text/plain; charset=utf-8

cmis:name

{--multipart-boundary}
Content-Disposition: form-data; name="propertyId[1]"
Content-Type: text/plain; charset=utf-8

cmis:objectTypeId

{--multipart-boundary}
Content-Disposition: form-data; name="propertyValue[0]"
Content-Type: text/plain; charset=utf-8

{filename}

{--multipart-boundary}
Content-Disposition: form-data; name="propertyValue[1]"
Content-Type: text/plain; charset=utf-8

{cmisbook:type}

{--multipart-boundary}
Content-Disposition: form-data; name="cmisaction"
Content-Type: text/plain; charset=utf-8

createDocument

{--multipart-boundary}
Content-Disposition: form-data; name="Browse..."; filename={filename}
Content-Type: text/plain
Content-Transfer-Encoding: binary

{file content string or binary code}

{--multipart-boundary}
```


## get all versions by object id##
* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={object_id}&cmisselector=versions
```

* http_methods:

```url
get
```



* examples:

```url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root?objectId=186&cmisselector=versions
```

## create new version of a document##

###step 1:###

`upload with checkout version action:`

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={object_id}
```

* http_header:

```url
Authorization: Basic {encoded_message_of("username:password")}
```

* http_method:

```url
post
```
* form_body_data:

```url
cmisaction=checkOut&succinct=true
```

`example:`

```url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root?objectId=185
```

###step 2###

`use the objectId return from step 1`

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={object_id}
```

* http_method:

```url
post
```

* http_header:

```url
Authorization: Basic dGVzdDo=
```

* multipart/formdata:

```url
{--multipart-boundary}
Content-Disposition: form-data; name="cmisaction"
Content-Type: text/plain; charset=utf-8

checkIn
{--multipart-boundary}
Content-Disposition: form-data; name="major"
Content-Type: text/plain; charset=utf-8

false
{--multipart-boundary}
Content-Disposition: form-data; name="checkinComment"
Content-Type: text/plain; charset=utf-8

{your check in comment}
{--multipart-boundary}
Content-Disposition: form-data; name="succinct"
Content-Type: text/plain; charset=utf-8

true
{--multipart-boundary}
Content-Disposition: form-data; name="content"; filename={filename}
Content-Type: text/plain
Content-Transfer-Encoding: binary

{file content string or binary code}

{--multipart-boundary}
```

`example:`

```url
http://173.39.194.161:8081/inmemory/browser/A1/root?objectId=186
```

* http_method:

```url
post
```

* multipart/formdata:

```url

--aPacHeCheMIStryoPEncmiS2c3ecc4dcheckIn14e9a3d59677ce39b6f
Content-Disposition: form-data; name="cmisaction"
Content-Type: text/plain; charset=utf-8

checkIn
--aPacHeCheMIStryoPEncmiS2c3ecc4dcheckIn14e9a3d59677ce39b6f
Content-Disposition: form-data; name="major"
Content-Type: text/plain; charset=utf-8

false
--aPacHeCheMIStryoPEncmiS2c3ecc4dcheckIn14e9a3d59677ce39b6f
Content-Disposition: form-data; name="checkinComment"
Content-Type: text/plain; charset=utf-8

Made a minor change
--aPacHeCheMIStryoPEncmiS2c3ecc4dcheckIn14e9a3d59677ce39b6f
Content-Disposition: form-data; name="succinct"
Content-Type: text/plain; charset=utf-8

true
--aPacHeCheMIStryoPEncmiS2c3ecc4dcheckIn14e9a3d59677ce39b6f
Content-Disposition: form-data; name="content"; filename=DockerUp.txt
Content-Type: text/plain
Content-Transfer-Encoding: binary

yum install docker-io

--aPacHeCheMIStryoPEncmiS2c3ecc4dcheckIn14e9a3d59677ce39b6f--

```

## copy object##

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={target_folder_id}&sourceId={original_object_id}
```

* http_method:

```url
post
```

`example: `

```url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root?objectId=101&cmisaction=createDocumentFromSource&major=true&sourceId=161
```

## create folder##

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}
```

* http_method:

```url
post
```

* http_content_type:

```url
application/x-www-form-urlencoded
```

* http_form_data(decoded):

```
propertyValue[0]={folder_name}
propertyValue[1]=cmis:folder
propertyId[0]=cmis:name
propertyId[1]=cmis:objectTypeId
cmisaction=createFolder
```

* http_form_data(encoded):

```
propertyValue%5B0%5D={folder_name}&propertyValue%5B1%5D=cmis%3Afolder&propertyId%5B0%5D=cmis%3Aname&propertyId%5B1%5D=cmis%3AobjectTypeId&cmisaction=createFolder
```

`example:`

* url:

```url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root
```

* form_data:

```url
propertyValue%5B0%5D=123123&propertyValue%5B1%5D=cmis%3Afolder&propertyId%5B0%5D=cmis%3Aname&propertyId%5B1%5D=cmis%3AobjectTypeId&cmisaction=createFolder
```

## update object name##

* http_url:

```url
http://{cmis_host}:{cmis_port}/inmemory/browser/{folder_path}
```

* http_method:

```url
post
```

* form_data(decoded):

```url
propertyId[0]=cmis:name
propertyValue[0]={object_id}
cmisaction=update
```

* form_data(encoded):

```url
propertyId%5B0%5D=cmis%3Aname&propertyValue%5B0%5D={object_id}&cmisaction=update
```

## delete object##

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={cmis_object_id}&cmisselector=content&cmisaction=delete&allVersions=true
```

* http_method: 

```url
post
```

`example:`

``` url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root?objectId=164&cmisselector=content&cmisaction=delete
```


## delete folder including its descendents##

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={cmis_object_id}&cmisselector=content&cmisaction=deleteTree&allVersions=true
```

* http_method: 

```url
post
```

`example:`

``` url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root?objectId=164&cmisselector=content&cmisaction=deleteTree
```

## batch move##

* http_url:

```url
http://{cmis_host}:{cmis_port}/{cmis_app_name}/browser/{folder_path}?objectId={cmis_object_id}&cmisselector=content&cmisaction=move&sourceFolderId={source_folder_id}&targetFolderId={target_folder_id}
```

* http_method: 

```url
post
```

`example:`

```url
http://{cmis_host}:{cmis_port}/inmemory/browser/A1/root?objectId=173&cmisselector=content&cmisaction=move&sourceFolderId=100&targetFolderId=174
```

## references file##

* [project code repo url](https://github.com/apache/chemistry-opencmis)

* [accessing http-method references for cmis-action-api](https://github.com/apache/chemistry-opencmis/blob/3c255935f9ec82e63e96ca767cda32004ed291c4/chemistry-opencmis-server/chemistry-opencmis-server-bindings/src/main/java/org/apache/chemistry/opencmis/server/impl/browser/CmisBrowserBindingServlet.java)

# accessing action key references for cmis-action-api:

* [action key references](https://github.com/apache/chemistry-opencmis/blob/trunk/chemistry-opencmis-commons/chemistry-opencmis-commons-impl/src/main/java/org/apache/chemistry/opencmis/commons/impl/Constants.java)

