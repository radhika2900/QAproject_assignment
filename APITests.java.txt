package com.api.tests;

import org.testng.Assert;
import org.testng.annotations.Test;

import io.restassured.RestAssured;
import io.restassured.response.Response;
import static io.restassured.RestAssured.given;

public class APITests {
   
    @Test
    public void testAddPets() {
        RestAssured.baseURI = "https://petstore.swagger.io/v2&quot;;
       
        String jsonbody = "{"
                + "  \"id\": 0,"
                + "  \"category\": {"
                + "    \"id\": 0,"
                + "    \"name\": \"string\""
                + "  },"
                + "  \"name\": \"doggie\","
                + "  \"photoUrls\": ["
                + "    \"string\""
                + "  ],"
                + "  \"tags\": ["
                + "    {"
                + "      \"id\": 0,"
                + "      \"name\": \"string\""
                + "    }"
                + "  ],"
                + "  \"status\": \"available\""
                + "}";
       
        Response response = given().header("accept", "application/json").header("Content-Type" , "application/json" )
                .body(jsonbody).when().post("/pet");
       
        System.out.println(response.prettyPrint());
        response.then().statusCode(200).and().contentType("application/json");
       
       
    }
   
    @Test
    public void testUpdatePets() {
        RestAssured.baseURI = "https://petstore.swagger.io/v2&quot;;
       
        String jsonbody = "{"
                + "  \"id\": 0,"
                + "  \"category\": {"
                + "    \"id\": 0,"
                + "    \"name\": \"string\""
                + "  },"
                + "  \"name\": \"doggie\","
                + "  \"photoUrls\": ["
                + "    \"string\""
                + "  ],"
                + "  \"tags\": ["
                + "    {"
                + "      \"id\": 0,"
                + "      \"name\": \"string\""
                + "    }"
                + "  ],"
                + "  \"status\": \"available\""
                + "}";
       
        Response response = given().header("accept", "application/json").header("Content-Type" , "application/json" )
                .body(jsonbody).when().put("/pet");
       
        System.out.println(response.prettyPrint());
        Assert.assertEquals(response.statusCode(), 200);
        Assert.assertEquals(response.contentType(), "application/json");
       
        response.then().statusCode(200).and().contentType("application/json");        
    }

    @Test
    public void getPets() {
        RestAssured.baseURI = "https://petstore.swagger.io/v2&quot;;
        Response response = given().header("accept", "application/json").when().get("/pet/findByStatus?status=pending");
   
        System.out.println(response.prettyPrint());
        response.then().statusCode(200).and().contentType("application/json");        
    }
   
    @Test
    public void getPetsById() {
        RestAssured.baseURI = "https://petstore.swagger.io/v2&quot;;
        Response response = given().header("accept", "application/json").when().get("/pet/9223372036854026608");
   
        //System.out.println(response.prettyPrint());
        response.then().statusCode(200).and().contentType("application/json");        
    }
   
    @Test
    public void deletePets() {
        RestAssured.baseURI = "https://petstore.swagger.io/v2&quot;;
        Response response = given().header("accept", "application/json").when().delete("/pet/9223372036854026422");
   
        //System.out.println(response.prettyPrint());
        response.then().statusCode(200).and().contentType("application/json");        
    }
   
}
