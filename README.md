# sb-cordova-plugin-downloadmanager

This plugin provides all the support needed for downloading files. Plugin defines a global object called `downloadManager`. 

## Installation

With Cordova:

`cordova plugin add sb-cordova-plugin-downloadmanager`

With Ionic:

`ionic cordova plugin add sb-cordova-plugin-downloadmanager`

### enqueue
This method download the file from the provided uri. You need to pass the `downloadRequest` object with details mentioned below.
```js
const downloadRequest = {
  uri: <fileUri>,
  title: <title>,
  description: 'Display description',
  mimeType: 'application/pdf',
  visibleInDownloadsUi: true,
  notificationVisibility: 1,
  destinationInExternalPublicDir: {
    dirType: 'Download',
    subPath: `/${fileName}`
  }
};
downloadManager.enqueue(downloadRequest, (err, id: string) => {
  if (err) {
    console.log({ reason: 'download-failed' });
  }
  console.log('error occured while downloading');
});
```

### query
This method provided the donload progress of ongoing donwnload. Pass the download ID received from `enqueue` as array.
```js
downloadManager.query(
  {
    ids: [downloadId]
  }, (err, downloadpProgress) => {
    if(err) {
      console.log('Failed');
      return false;
    }

    console.log('Success ', downloadpProgress);
});
```

### remove
To cancel ongoing download, call this method with argument as Array of download ID's of those doenloads which need to be canceled.
```js
downloadManager.remove(
[downloadId!],
(err, cancelCount) => {
  if (err) {
    console.log('Error while canceling download');
  }
  
  console.log('Total download canceled ' , cancelCount);
});
```

### fetchSpeedLog
This methods provides the download speed details from the network, along with other details about the network and downloading speed.
```js
downloadManager.fetchSpeedLog((_, downloadSpeedLogs) => {
  console.log('Download speed details ', downloadSpeedLogs);
}, error => {
  console.log('Error while fetching download speed);
});
```