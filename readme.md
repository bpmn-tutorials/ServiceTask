Repository to test Java Service Task in KIE Business Central
============================================================

> ### Important Note
> This repository uses *.jar artifact with Java Class from https://github.com/bpmn-tutorials/ServiceTaskTest

> ### Important Note 2
> Don't forget to install Work Item Handler of Service Task to your new project (it is already configured for this one)
> ![](./images/WorkItemHandlerRegistration.png) 

Repository contains  3 Business Processes to test:
* **JavaTask** Business Process - uses Java Service Task to greet multiple users inside of _Java Service Task_ using *Multiple Instance* property.
* **ServiceTaskInsideOfAdHocSubProcess** - uses Java Service Task for simple greetings one user at a time inside of AdHocSubprocess.
* **SLADueDateTestJavaServiceTask** - demonstrates how to use SLA for Java Service Tasks. Also demonstrate how to use Java Services Tasks Parameters with different data types than String.

## JavaTask

![](src/main/resources/com/myspace/servicetask/ServiceTask.JavaTask-svg.svg)

When you start this process you will be asked for list of names. Each of this names (up to 3, see parameters below) will be sent to Java Service Task and string "Hello, %name%" will be returned back to the process and all resulted strings will be printed in the Script task.

![](./images/TaskStartup.png)
  
### Used Parameters of _Java Service Task_
* **Implementation** - *Java* (Java class will be executed)
* **Interface** - *org.test.service.SimpleServiceTask* (FQN of the executed class)
* **Operation** - *sayHelloTo* (method name to invoke)
* **Multiple Instance** - *true* (Task will be executed as many times as many names will be provided in Process Variable _InputCollection_)
* **MI Collection input** - *InputCollection* (Array list provided during process start)
* **MI Data Input** - *Parameter* this is Input Data Assignment for Java Service task, it will be transferred to java class
* **MI Collection output** - *OutputCollection* (Array list where values returned from Java Task will be stored)
* **MI Data Output** - *Result* this is Output Data Assignment for Java Service Task, when class executed on the server this variable will store the result
* **MI Completion Condition (mvel)** - `OutputCollection.size() == 3` no more than three people will be greeted.

After execution following text will be printed in Server Log (*On Entry Action* and *On Exit Action* Properties of Java Service Task used to format Task Invocation data. At the end of the output you can see that all provided names are greeted by Service Task and result printed to the server log.)
```console
12:43:26,938 INFO  [stdout] (default task-18) ================================
12:43:26,938 INFO  [stdout] (default task-18) Java Service Task instance is about to be executed.
12:43:26,938 INFO  [stdout] (default task-18) Thread ID is: 2600
12:43:26,938 INFO  [stdout] (default task-18) Provided name = Jan
12:43:26,938 INFO  [stdout] (default task-18)
12:43:26,939 INFO  [stdout] (default task-18) Hello world from the Java Service Task.
12:43:26,940 INFO  [stdout] (default task-18)
12:43:26,940 INFO  [stdout] (default task-18) Java Service Task instance is about to finish it's work.
12:43:26,940 INFO  [stdout] (default task-18) Result returned by Java service is: Hello, Jan
12:43:26,940 INFO  [stdout] (default task-18) ================================
12:43:26,940 INFO  [stdout] (default task-18)
12:43:26,943 INFO  [stdout] (default task-18) ================================
12:43:26,943 INFO  [stdout] (default task-18) Java Service Task instance is about to be executed.
12:43:26,943 INFO  [stdout] (default task-18) Thread ID is: 2600
12:43:26,943 INFO  [stdout] (default task-18) Provided name = Ivan
12:43:26,943 INFO  [stdout] (default task-18)
12:43:26,944 INFO  [stdout] (default task-18) Hello world from the Java Service Task.
12:43:26,945 INFO  [stdout] (default task-18)
12:43:26,945 INFO  [stdout] (default task-18) Java Service Task instance is about to finish it's work.
12:43:26,945 INFO  [stdout] (default task-18) Result returned by Java service is: Hello, Ivan
12:43:26,945 INFO  [stdout] (default task-18) ================================
12:43:26,945 INFO  [stdout] (default task-18)
12:43:26,947 INFO  [stdout] (default task-18) ================================
12:43:26,947 INFO  [stdout] (default task-18) Java Service Task instance is about to be executed.
12:43:26,947 INFO  [stdout] (default task-18) Thread ID is: 2600
12:43:26,947 INFO  [stdout] (default task-18) Provided name = John
12:43:26,947 INFO  [stdout] (default task-18)
12:43:26,947 INFO  [stdout] (default task-18) Hello world from the Java Service Task.
12:43:26,948 INFO  [stdout] (default task-18)
12:43:26,948 INFO  [stdout] (default task-18) Java Service Task instance is about to finish it's work.
12:43:26,948 INFO  [stdout] (default task-18) Result returned by Java service is: Hello, John
12:43:26,948 INFO  [stdout] (default task-18) ================================
12:43:26,948 INFO  [stdout] (default task-18)
12:43:26,950 INFO  [stdout] (default task-18) Hello, Jan
12:43:26,950 INFO  [stdout] (default task-18) Hello, Ivan
12:43:26,950 INFO  [stdout] (default task-18) Hello, John
12:43:26,950 INFO  [stdout] (default task-18) Thread ID is: 2600
```
