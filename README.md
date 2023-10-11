# Expression Testing

[![license](https://img.shields.io/github/license/interlok-testing/testing_expression.svg)](https://github.com/interlok-testing/testing_expression/blob/develop/LICENSE)
[![Actions Status](https://github.com/interlok-testing/testing_expression/actions/workflows/gradle-build.yml/badge.svg)](https://github.com/interlok-testing/testing_expression/actions/workflows/gradle-build.yml)

Project tests interlok-expressions features

## What it does

This project contains various workflows that make up a basic/simple calculator API.

Each workflow is made up of:
* a jetty-message-consumer that consumes parameters from a given uri path
* a expression-service or freeform-expression-service that does a given algorithm and sets the result in metadata 'expressionResult'
* a metadata-to-payload that sets the payload from the metadata key 'expressionResult'
* a jetty-standard-response-producer that returns the payload result back to the requester

![workflow diagram](/workflow-diagram.png "workflow diagram")
 
## Getting started

* `./gradlew clean build`
* `(cd ./build/distribution && java -jar lib/interlok-boot.jar)`

Now you can do various api calls:

### Addition (using expression-service)
```xml
<algorithm>($1 + $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/add?num1=10&num2=25"
35
```

### Subtraction (using expression-service)
```xml
<algorithm>($1 - $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/minus?num1=10&num2=25"
-15
```
### Division (using expression-service)
```xml
<algorithm>($1 / $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/divide?num1=10&num2=2"
5
```

### Multiplication (using expression-service)
```xml
<algorithm>($1 * $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/multiply?num1=10&num2=25"
250
```

### Ggreater than (using expression-service)
```xml
<algorithm>($1 > $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/greater-than?num1=10&num2=25"
false
```

```
$ curl -s "http://localhost:8081/greater-than?num1=105&num2=25"
true
```

### Less than or equal to (using expression-service)
```xml
<algorithm>($1 <= $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/less-than-or-equal-to?num1=105&num2=25"
false
```

```
$ curl -s "http://localhost:8081/less-than-or-equal-to?num1=105&num2=250"
true
```

```
$ curl -s "http://localhost:8081/less-than-or-equal-to?num1=105&num2=105"
true
```

### Equal to (using expression-service)
```xml
<algorithm>($1.equals($2))</algorithm>
```

```
$ curl -s "http://localhost:8081/equal-to?num1=105&num2=105"
true
```

```
$ curl -s "http://localhost:8081/equal-to?num1=105&num2=1053"
false
```

### Multiplication (using freeform-expression-service)
```xml
<algorithm>(%message{num1} * %message{num2} * %message{num3})</algorithm>
```

```
$ curl -s "http://localhost:8081/multiply-three?num1=10&num2=5&num3=2"
100
```
