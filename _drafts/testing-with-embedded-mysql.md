---
layout: default
title:  "Running integration tests with an embedded MySql"
comments: true
categories: 
    - experience
---

# Running integration tests with an embedded MySql

Last project I was working on was a Spring REST API for storing and retrieving data from a data storage. 
Nothing special so far.

It got much more interesting when one of the field in the payload became a JSON string content.

Something like this:
```json
{
  "key" : "value",
  "data" : "{ \"prop\" : \"value\" }"
}
```
Clients of my REST API are allowed to store whatever JSON content they need and they can perform search against this field using a JSON path expression.
For doing that my pair and I ended up using MySql that support JSON field since v5.7.

Before this new feature we used H2 for running the acceptance/integration tests but H2 has no support fot JSON field yet,
so we needed to have a MySql instance for testing.

We didn't like the idea of having am instance of MySql on our machine because it's annoying to take care of it any time you need to run your test. 
Like dropping the schema, creating if again and so on. We wanted something as handy as H2.

We found this amazing [library](https://github.com/wix/wix-embedded-mysql){:target="_blank"} from Wix on Github.

We changed our **build.gradle** to using it 
```groovy
buildscript {
	/* other stuff */
	dependencies {
		/* other dependencies */
		classpath('com.wix:wix-embedded-mysql:3.0.0')
	}
	/* other stuff */
}
``` 
than we added to new tasks for starting and stopping MySql
```groovy
def mysql
task startMysql {
	mysql = EmbeddedMysql.anEmbeddedMysql(Version.v5_7_latest)
			.addSchema("acme")
			.start()
}

task stopMysql {
	doLast {
		if(mysql != null) {
			mysql.stop()
		}
	}
}
```

We configure **test** task to run **startMysql** before and **stopMysql** after.
```groovy

test.dependsOn startMysql
test.finalizedBy stopMysql
``` 
 Now running **./gradlew test** will automatically start and stop a fresh new instance of MySql every time.
 
 Super handy if you need to go native on your JPA code.