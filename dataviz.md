In your bower.json:

```
{
  "name": "aws-app",
  "private": true,
  "dependencies": {
    "alloyeditor": "0.7.5",
    "iron-elements": "PolymerElements/iron-elements#^1.0.0",
    "jsPlumb": "2.0.4",
    "marked-element": "PolymerElements/marked-element#1.1.1",
    "moment": "2.10.6",
    "nuxeo-elements": "nuxeo/nuxeo-elements#master",
    "nuxeo-ui-elements": "nuxeo/nuxeo-ui-elements#master",
    "nuxeo-dataviz-elements": "nuxeo/nuxeo-dataviz-elements#master",
    "page": "nuxeo/page.js#1.6.6",
    "paper-elements": "PolymerElements/paper-elements#^1.0.1",
    "polymer": "Polymer/polymer#^1.1.0",
    "chart-elements": "nuxeo/chart-elements#3.1.0",
    "Chart.js": "2.1.6",
    "iron-list": "PolymerElements/iron-list#1.3.9"
  },
  "devDependencies": {
    "web-component-tester": "^4.0.0"
  },
  "resolutions": {
    "nuxeo": "0.25.0",
    "nuxeo-elements": "master"
  }
}
```


In your elements.html:

```
<!-- My custom element -->
<link rel="import" href="aws-app.html">

<!-- Nuxeo Dataviz elements -->
<link rel="import" href="../bower_components/nuxeo-dataviz-elements/nuxeo-audit-data.html">
<link rel="import" href="../bower_components/nuxeo-dataviz-elements/nuxeo-repository-data.html">
<link rel="import" href="../bower_components/nuxeo-dataviz-elements/nuxeo-search-data.html">
<link rel="import" href="../bower_components/nuxeo-dataviz-elements/nuxeo-workflow-data.html">

<!-- Chart elements -->
<link rel="import" href="../bower_components/chart-elements/chart-bar.html">
<link rel="import" href="../bower_components/chart-elements/chart-line.html">
<link rel="import" href="../bower_components/chart-elements/chart-pie.html">

<!-- Nuxeo Elements -->
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-connection.html">
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-document.html">
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-operation.html">
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-page-provider.html">
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-document-history-page-provider.html">
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-resource.html">
<link rel="import" href="../bower_components/nuxeo-elements/nuxeo-search.html">
```
