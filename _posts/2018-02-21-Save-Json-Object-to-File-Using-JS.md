---
layout: default
title: Save Json object to files, using JS
comments: true
---

1. Create Object
```
var obj = {
	"foo": "bar"
}
```

2. Convert object to string
```
// mim version json file.
var json = JSON.stringify(obj);

// readable json file
var json = JSON.stringify(messageJson, null, "\t");
```

3. Save to file
```
var fs = require('fs');
fs.writeFile('jsonfile.json', json, 'utf8', function(err) {
	if(err) {
		console.log(err)
	}else {
		console.log("*** File saved ***")
	}
});
```