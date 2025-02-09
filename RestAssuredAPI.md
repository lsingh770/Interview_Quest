**RestAssured API Framework Interview Questions**:

---

### **Basic Level Questions**
#### **1. What is RestAssured? How does it help in API automation?**  
RestAssured is a Java library used for testing RESTful APIs. It simplifies API testing by providing a fluent and readable interface to send HTTP requests and validate responses. It eliminates the need to write extensive boilerplate code for API testing.

---

#### **2. How do you set up a basic RestAssured framework using Gradle/Maven?**  
**For Gradle:** Add the following dependencies in `build.gradle`:
```gradle
dependencies {
    testImplementation 'io.rest-assured:rest-assured:5.3.0'
    testImplementation 'org.testng:testng:7.7.1'
}
```
**For Maven:** Add this to `pom.xml`:
```xml
<dependencies>
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>rest-assured</artifactId>
        <version>5.3.0</version>
    </dependency>
</dependencies>
```
---

#### **3. How do you send a GET request using RestAssured?**  
```java
import io.restassured.RestAssured;
import io.restassured.response.Response;
import static io.restassured.RestAssured.*;

public class GetRequestExample {
    public static void main(String[] args) {
        Response response = given()
                .when().get("https://jsonplaceholder.typicode.com/posts/1")
                .then().statusCode(200)
                .extract().response();

        System.out.println(response.asString());
    }
}
```
---

#### **4. How do you send a POST request with a JSON payload in RestAssured?**  
```java
String requestBody = "{ \"title\": \"foo\", \"body\": \"bar\", \"userId\": 1 }";

Response response = given()
    .header("Content-Type", "application/json")
    .body(requestBody)
    .when().post("https://jsonplaceholder.typicode.com/posts")
    .then().statusCode(201)
    .extract().response();
```
---

#### **5. How do you validate response status codes using RestAssured?**  
```java
Response response = given().get("https://jsonplaceholder.typicode.com/posts/1");
Assert.assertEquals(response.getStatusCode(), 200);
```
---

#### **6. What is the difference between PUT and PATCH requests? How do you implement them in RestAssured?**  
- **PUT** updates the entire resource.  
- **PATCH** updates only specific fields.  

**PUT Request Example:**
```java
String putBody = "{ \"id\": 1, \"title\": \"Updated Title\", \"body\": \"Updated Body\", \"userId\": 1 }";
given().header("Content-Type", "application/json")
    .body(putBody)
    .when().put("https://jsonplaceholder.typicode.com/posts/1")
    .then().statusCode(200);
```
**PATCH Request Example:**
```java
String patchBody = "{ \"title\": \"Patched Title\" }";
given().header("Content-Type", "application/json")
    .body(patchBody)
    .when().patch("https://jsonplaceholder.typicode.com/posts/1")
    .then().statusCode(200);
```
---

#### **7. How do you pass query parameters in RestAssured?**  
```java
given().queryParam("userId", 1)
    .when().get("https://jsonplaceholder.typicode.com/posts")
    .then().statusCode(200);
```
---

#### **8. What is the difference between path parameters and query parameters in RestAssured?**  
- **Path parameters** are part of the URL (`/posts/{id}`)  
- **Query parameters** are appended to the URL (`/posts?userId=1`)  

Example:  
```java
given().pathParam("id", 1)
    .when().get("https://jsonplaceholder.typicode.com/posts/{id}")
    .then().statusCode(200);
```
---

#### **9. How do you add headers to a request in RestAssured?**  
```java
given().header("Authorization", "Bearer token")
    .when().get("https://api.example.com/data")
    .then().statusCode(200);
```
---

#### **10. How do you handle authentication in RestAssured?**  
**Basic Authentication:**
```java
given().auth().basic("username", "password")
    .when().get("https://api.example.com/data")
    .then().statusCode(200);
```
**Bearer Token Authentication:**
```java
given().header("Authorization", "Bearer your_token")
    .when().get("https://api.example.com/data")
    .then().statusCode(200);
```
---

### **Intermediate Level Questions**
#### **11. How do you validate JSON response body fields using RestAssured?**  
```java
given().when().get("https://jsonplaceholder.typicode.com/posts/1")
    .then().body("title", equalTo("sunt aut facere repellat provident occaecati excepturi optio reprehenderit"));
```
---

#### **12. How do you extract response values from RestAssured responses?**  
```java
Response response = given().get("https://jsonplaceholder.typicode.com/posts/1");
String title = response.jsonPath().getString("title");
System.out.println("Title: " + title);
```
---

#### **13. How do you log API request and response details in RestAssured?**  
```java
given().log().all()
    .when().get("https://jsonplaceholder.typicode.com/posts/1")
    .then().log().all();
```
---

#### **14. How do you handle response time validation in RestAssured?**  
```java
given().when().get("https://jsonplaceholder.typicode.com/posts/1")
    .then().time(lessThan(2000L));
```
---

#### **15. How do you integrate RestAssured with TestNG?**  
```java
import org.testng.annotations.Test;
import static io.restassured.RestAssured.*;

public class RestAssuredTest {
    @Test
    public void testGetAPI() {
        given().when().get("https://jsonplaceholder.typicode.com/posts/1")
            .then().statusCode(200);
    }
}
```
---

### **Advanced Level Questions**
#### **21. How do you implement API request chaining in RestAssured?**  
```java
Response postResponse = given()
    .body("{ \"title\": \"test\", \"body\": \"test body\", \"userId\": 1 }")
    .when().post("https://jsonplaceholder.typicode.com/posts");

int newId = postResponse.jsonPath().getInt("id");

given().when().get("https://jsonplaceholder.typicode.com/posts/" + newId)
    .then().statusCode(200);
```
---

#### **26. What are some common challenges while automating APIs using RestAssured?**  
- Handling **dynamic response data**  
- Managing **authentication tokens**  
- Dealing with **rate-limiting APIs**  
- **Parallel execution** challenges  
- Handling **schema validation and response structure changes**  

---

Would you like more answers or any specific code samples? 🚀
