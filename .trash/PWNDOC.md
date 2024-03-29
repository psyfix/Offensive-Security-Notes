#### Contributing to API.

1. Create a model and schema to be added to the database. (pwndoc-main\\pwndoc-main\\backend\\src\\models)
```
var mongoose = require('mongoose');//.set('debug', true);
var Schema = mongoose.Schema;

var TestSchema = new Schema({
    name:               {type: String, required: true},
    test_title:             String,
    test_name:              String,
    test_description:       String,
    test_severity:          String
})

var Test = mongoose.model('Test', TestSchema);
module.exports = Test;
```

2. Create a route. (pwndoc-main\\pwndoc-main\\backend\\src\\routes)
```
module.exports = function(app) {

    var Response = require('../lib/httpResponse');
    var Test = require('mongoose').model('Test');

    // Get test api
    app.get("/api/tests", function(req, res) {
        // Assuming acl.hasPermission('tests:read') checks permissions
        Test.find({})
            .then(tests => {
                Response.Ok(res, tests);
            })
            .catch(err => {
                console.error(err);
                Response.Internal(res, "Internal Server Error");
            });
    });
}
```

3. Import the route and model into the main app.js server file. (pwndoc-main\\pwndoc-main\\backend\\src\\app.js)

#### Contributing

```
1. Install docker desktop for windows first.
2. Clone down the latest version of PWNDOC.
3. Open a windows powershell terminal.
	docker-compose -f backend/docker-compose.dev.yml up -d --build
	docker-compose -f frontend/docker-compose.dev.yml up -d --build
4. Open up the docker windows gui application.
5. Manage the built containers from there you can restart and see logs.
```


### DEV DASHBOARD
A dashboard that loads by api requests returning a bunch of data from the db and dynamically loading it into the dashboard.
```
Features
1. API GET REQUEST to: /api/audits
2. Then pull all the audits (company names to create companies column)
3. Then pull all the audit findings
4. Then calculate the cvss scores for each finding using (CVSS31.calculateCVSSFromVector)
5. Then convert scores to severities and enter in chart.
```
![[Pasted image 20240308124232.png]]