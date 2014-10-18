# Mock FileFog Provider


**For testing purposes only:**  
A [Filefog](https://github.com/filefog/filefog) adapter that returns randomly generated results. 

## Install

Install is through NPM.

```bash
$ npm install https://github.com/NitroLabs/filefog-mock.git
```

## Configuration

The following config options are required:

```javascript
config: {};
```

##Methods
###download(identifier)
Download a file from the cloud, and return it as a buffer
(The mock provider just pipes a local file)
@identifier can either be the fileId or a file metadata object as returned by any of the other methods.


###searchFiles(filters,options)
It is possible to search through all files on the storage drive using the searchFiles method. The filter parameter provides a way to filter
the returned results. Not all filters are supported by each cloud service.
Filters include:
- filters.title - Filter results by file title
- filters.mimeType - Filter results by mimeType
- filters.parentFolder - Filter results by the parent folder identifier

The options parameter provide to alter the request that is sent
to the cloud service. Options include:
- options.fields - The fields that each file object should have
- options.pageToken - Used to retrieve the next page of results 
- options.maxResults - The maximum number of files returned

```javascript
var google = filefog.client("mock", {
    access_token: '...',
    refresh_token: '...'
})
.then(function (client) {
    var fields = ["id","title","mimeType"];
    return client.searchFiles({mimeType:'audio/mpeg'},{fields:fields});
}).then(function (response) {
    // Prints the first 100 mpeg files in the drive
    console.log(response);
});
```


## Testing

Test are written with mocha. Integration tests are handled by the [filefog-provider-tests](https://github.com/filefog/filefog-provider-tests) project, which tests provider methods against the latest FileFog API.

To run tests:

```bash
$ npm test
```

## About FileFog

FileFog is a cloud agnostic file API.  It provides a uniform API for accessing stuff from different kinds of cloud providers and file systems.  That means you write the same code to manipulate files, whether they live in google drive, dropbox, box.net, or your local file system.

To learn more visit the project on GitHub at [FileFog](https://github.com/filefog/filefog).