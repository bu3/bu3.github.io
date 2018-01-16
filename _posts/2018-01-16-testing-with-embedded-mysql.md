---
layout: default
title:  "Running integration tests with an embedded MySql"
comments: true
categories: test
tags: 
     - tdd
     - test 
     - mysql
---

# Running integration tests with an embedded MySql

Consider this scenario: 

you are working on a Spring application with JPA for persistence layer and suddenly a new story needs to use a MySql native function like for example JSON_SEARCH.

How this affect your tests?

In a regular scenario for running integration tests you could use H2 but in this scenario it's not possible, because H2 does not have any JSON support yet.

You could manage to run a MySql instance for running tests but you need to take care of some annoying steps like dropping data, tables and schemas right after each run.

Also you have to configure any machine where your tests are supposed to run for having a MySql instance.

Wouldn't it be nice to avoid all those steps and have a brand new MySql instance every time you run your tests instead?

My colleague [@Luis](https://github.com/lurraca) and I had to face this scenario and we ended up using an embedded MySql.

We found this amazing [library](https://github.com/wix/wix-embedded-mysql){:target="_blank"} from Wix on Github for downloading, configuring and starting a MySql instance on the fly.

We managed to add two tasks for starting and stopping MySql with Gradle.

Now before running our tests, another task sets up MySql and after tests another one stops it. 


Let's move to the code.


These are the entity and a repository using a native query for using MySql ***JSON_SEARCH*** function:  

```kotlin 

@Entity(name = "employees")
data class Employee(
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Id
    val id:Long,

    @Lob
    @Column
    val data: String

){
    constructor() : this(0, "")
}

interface DataRepository : CrudRepository<Employee, Long> {

    @Query("select id, data from employees e where JSON_SEARCH(e.data, 'all', ?2, NULL, ?1) is not null", nativeQuery = true)
    fun search(path:String, value: String): List<Employee>

}
```

The **data** field in the Employee entity is the json string I want to search against using ***JSON_SEARCH*** function.

The following ones are the small changes we applied to our **build.gradle**:

A build script dependency 
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
and two tasks for starting and stopping MySql
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

That's it.

If you want to take a look to the source code, you can find it [here](https://github.com/bu3/embedded-mysql)