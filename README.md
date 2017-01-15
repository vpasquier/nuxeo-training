# Getting Started - Day 1 & 2

## Setup

Distribution and Dev mode setup:
- Get a nuxeo distribution.
- Go to `NUXEO_HOME/bin` folder.
- Execute `./nuxeoctl register`.
- Install Web UI at `./nuxeoctl mp-install nuxeo-web-ui`.
- Install JSF UI at `./nuxeoctl mp-install nuxeo-jsf-ui`.
- Open `NUXEO_HOME/bin/nuxeo.conf` file.
- Remove the line `wizard.done=false`.
- Download `nuxeo-elasticsearch-core-8.10.jar` from this repository to `NUXEO_HOME/nxserver/bundles` in your server to deactivate CORS on elasticsearch. (click yes to replace)
- Execute `./nuxeoctl console`.

# API REST - Day 3

## Setup

- Checkout this project and open restapi.js (only file to code within).
- Install the Nuxeo chrome extension.
- Stop Nuxeo server.
- Uncomment `org.nuxeo.dev=true`.
- Disable CORS in a new file `cors-config.xml` into `NUXEO_HOME/nxserver/config` folder with the following contribution:

```
<?xml version="1.0"?>
<component name="org.nuxeo.cors">
  <extension target="org.nuxeo.ecm.platform.web.common.requestcontroller.service.RequestControllerService" point="corsConfig">
    <corsConfig name="foobar" allowOrigin="*" supportedMethods="GET, POST, PUT, DELETE, HEAD, OPTIONS">
      <pattern>.*</pattern>
    </corsConfig>
  </extension>
</component>
```

Nuxeo Execution and Studio custom bundle setup:
- Execute `./nuxeoctl console`.
- Create into your project one document type:
  - Named `Meeting`
  - With one metadata `participants` String multivalued
  - And one metadata `meetingPublisher` complex containing `firstName` and `lastName` String
- Hotreload

## Initialization

#### Create and return a Client in `RestAPI.config = function ()`

To be able to make API calls on a Nuxeo server, you need to create a `Client` object:

```javascript
var nuxeo = new Nuxeo({
  baseURL: 'http://localhost:8080/nuxeo/',
  restPath: 'site/api/v1/',
  automationPath: 'site/automation/',
  auth: {
    method: 'basic',
    username: Administrator,
    password: Administrator
  },
  timeout: 3000
});

  nuxeo.schemas(["dublincore"]);
  nuxeo.timeout(3000);
  return nuxeo;
```

#### Nuxeo Methods

**nuxeo.timeout(timeout)**
Sets the common timeout in ms to be used for the requests.

**nuxeo.header(name, value)**

**nuxeo.headers(headers)**

**nuxeo.repositoryName(repositoryName)**

**nuxeo.schema(schema)**

**nuxeo.schemas(schemas)** (`X-NXDocumentProperties` header)

-----------

### 1) Get Administrator user in `RestAPI.getCurrentUser = function ()`

Use `this.nuxeo` to get `nuxeo` for all examples now.

####Request Object

Fetching vpasquier user: (using `user/{userName}` endpoint)

```javascript
this.nuxeo.request('user/vpasquier').get()
.then(function(response){
  callbackCurrentUser(null, response);
})
.catch(function(error) {
  callbackCurrentUser(error, null);
});
```
Calling endpoint `path/`

```javascript
var request = this.nuxeo.request('path/')....
```

You can have access to the following methods.

https://nuxeo.github.io/nuxeo-js-client/latest/Request.html

### 2) Execute Query in `RestAPI.executeQuery = function (query)`

Use GET method and `query` endpoint with `?query=SELECT * .....` path parameter.

### 3) Get Root Children in `RestAPI.getRootChildren = function ()`

To display the grid listing fetch all the children of a root document.

You can have access to the following methods:

https://nuxeo.github.io/nuxeo-js-client/latest/Operation.html

### 4) Fetch Document in `RestAPI.fetchDocument = function (id)`

To display the metadata on the right, fetch the document selected in the grid.

You can have access to the following methods: https://nuxeo.github.io/nuxeo-js-client/latest/Document.html

(Use content enricher with `X-NXContext-Category` header = "acls".)

### 5) Create Document in `RestAPI.createDocument = function (map)`

Hint:
```
properties: {
"dc:title": map["dc:title"],
"dc:description": map["dc:description"],
"dc:nature": map["dc:nature"],
"dc:language": map["dc:language"]
}
```

### 6) Update Document in `RestAPI.updateDocument = function (map)`

Use **document.set(properties)** and **document.save(callback)**
with `this.currentDocument`

### 7) Delete Document in `RestAPI.deleteDocument = function ()`

Check the repository API.

### Uploader API

To be able to import file or attach a blob in the interface you can see the following methods:

https://nuxeo.github.io/nuxeo-js-client/latest/BatchUpload.html

### 8) Import file by filling `RestAPI.importFile = function (file)`

Use `FileManager.Import` operation.

### 9) Attach file by filling `RestAPI.attachBlob = function (file)`

Use `Blob.Attach` operation.
