# Expression Testing

Project tests interlok-expressions features

## What it does

This project contains various workflows that make up a basic/simple calculator API.

Each workflow is made up of:
* a jetty-message-consumer that consumes parameters from a given uri path
* a expression-service or freeform-expression-service that does a given algorithm and sets the result in metadata 'expressionResult'
* a metadata-to-payload that sets the payload from the metadata key 'expressionResult'
* a jetty-standard-response-producer that returns the payload result back to the requester

## Getting started

* `./gradlew clean build`
* `(cd ./build/distribution && java -jar lib/interlok-boot.jar)`

Now you can do various api calls:

### addition
```xml
<expression-service>
    <unique-id>add-two-numbers</unique-id>
    <algorithm>($1 + $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/add?num1=10&num2=25"
35
```

### subtraction
```xml
<expression-service>
    <unique-id>minus-two-numbers</unique-id>
    <algorithm>($1 - $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/minus?num1=10&num2=25"
-15
```
### division
```xml
<expression-service>
    <unique-id>divide-two-numbers</unique-id>
    <algorithm>($1 / $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/divide?num1=10&num2=2"
5
```

### multiplication
```xml
<expression-service>
    <unique-id>multiply-two-numbers</unique-id>
    <algorithm>($1 * $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/multiply?num1=10&num2=25"
250
```

### greater than
```xml
<expression-service>
    <unique-id>is-number1-greater-than-number2</unique-id>
    <algorithm>($1 &gt; $2)</algorithm>
```

```
$ curl -s "http://localhost:8081/greater-than?num1=10&num2=25"
false
```

```
$ curl -s "http://localhost:8081/greater-than?num1=105&num2=25"
true
```

### less than or equal to
```xml
<expression-service>
    <unique-id>is-number1-less-than-or-equal-to-number2</unique-id>
    <algorithm>($1 &lt;= $2)</algorithm>
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

### equal to
```xml
<expression-service>
    <unique-id>is-number1-equal-to-number2</unique-id>
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

### multiplication (using a freeform-expression-service)
```xml
<freeform-expression-service>
    <unique-id>multiply-three-numbers</unique-id>
    <algorithm>(%message{num1} * %message{num2} * %message{num3})</algorithm>
```

```
$ curl -s "http://localhost:8081/multiply-three?num1=10&num2=5&num3=2"
100
```
