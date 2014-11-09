rundeck-php
===========

PHP API to Access Rundeck API - control and create jobs

Based on documentation at http://rundeck.org/docs/api/index.html#

WARNING!!! This API is incomplete, not all functions implemented.

Requirements
============
None. Get yourself recent PHP 5.3+ and it will do.
Rundeck 2.1+ 

You might want to checkout my script to automatically install and
configure rundeck https://gist.github.com/huksley/ed30cd723128e4c36406

Invocation
==========

```php
require_once("Rundeck.class.php");

$s = new Rundeck();
$s->token = "MY_TOKEN_HERE";
$s->url = "http://rundeck-server:4440";
$s->project = "my-project";

// List of jobs on server (this are very slow).
// Returned instances only have name
$jobs = $s->jobs();

// Return complete job info, including scheduling (if any) and execution script
$job = $s->job($job[0]);

// Invoke job now
$execution = $s->run($job);

// Wait for job to complete
while ($s->status($job) == "running") {}

// All last executions of job
$executions = $s->last($job);

// Create new job, it will run automatically every 5 minutes
$newJob = new Job("my-new-job");
$newJob->schedule = "0/5 * * * *";
$newJob->exec = array("whoami");
$newJob = $s->create($newJob);
```

License
=======

Code is licensed under Apache License v.2
