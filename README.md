# Introduction
Welcome to the API testing suite for the thetestingworldapi.com API. This repository contains a Postman collection and environment designed to facilitate API testing for various functionalities related to booking. The API allows operations such as login, set booking, get booking, edit booking, delete. 

# Summery    
I have Completed an API test of login, set booking, get booking, edit booking, delete
https://restful-booker.herokuapp.com  
<p align="center">
  <img src="https://github.com/asaha12/cricket_19_keyboard/assets/113898640/8393cd4a-c9ed-402e-82b6-e08111601610" />
</p>
 

Here in this API student details viewed and different tests were performed like GET, POST, PUT, DELETE.

**Summary:** Test Scripts 4 and Total 8 assertions were done. All of them passed with 0 skipped tests. The number of iteration was 1.



# Requirements  
**Java**  
https://www.oracle.com/java/technologies/downloads/   
**Postman**   
https://www.postman.com/   
**Node JS**   
https://nodejs.org/en/    



# Assertions Details    
#### Get_Booking
**Test Script**
```bash
var statuscode = pm.response.code
if(statuscode==200)
{
        pm.test("Status code is 200", function () {
            pm.response.to.have.status(200);
        });

        var jsonData = pm.response.json()
        pm.test("First Name Validation", function(){
            pm.expect(jsonData.firstname).to.eql(pm.environment.get("firstname"))
        })  
        pm.test("Last Name Validation", function(){
            pm.expect(jsonData.lastname).to.eql(pm.environment.get("lastname"))
        })
        pm.test("Total Price Validation", function(){
            pm.expect(jsonData.totalprice).to.eql(pm.environment.get("totalprice"))
        })
        pm.test("Deposit paid Validation", function(){
            pm.expect(String(jsonData.depositpaid)).to.eql(pm.environment.get("depositpaid"))
        })
        pm.test("Checkin Validation", function(){
            pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("checkin"))
        })
        pm.test("Checkout Validation", function(){
            pm.expect(jsonData.bookingdates.checkout).to.eql(pm.environment.get("checkout"))
        })
}

else if(statuscode==404)
{
    pm.test("Not Found", function () {
            pm.response.to.have.status(404);
        });
}

else if(statuscode==403)
{
    pm.test("Forbidden", function () {
            pm.response.to.have.status(403);
        });
}

else
{
    pm.test("Something Wrong");
}

```
#### Delete Booking
**Body**
```bash   
var statuscode = pm.response.code
if(statuscode==201)
{
     pm.test("User Deleted", function () {
            pm.response.to.have.status(201);
        });   
}

else if(statuscode==404)
{
    pm.test("Not Found", function () {
            pm.response.to.have.status(404);
        });
}

else if(statuscode==403)
{
    pm.test("Forbidden: Expired Token", function () {
            pm.response.to.have.status(403);
        });
}

else
{
    pm.test("Something Wrong");
}


```
#### Set Bookking
**Pre-Request Scripts**

```bash   
var firstname = pm. variables. replaceIn("{{$randomFirstName}}")
pm.environment.set("firstname", firstname)

var lastname = pm. variables. replaceIn("{{$randomLastName}}")
pm.environment.set("lastname", lastname)

var t = pm. variables. replaceIn("{{$randomPrice}}")
var totalprice = parseInt(t, 10);
pm.environment.set("totalprice", totalprice)

var depositpaid = pm. variables. replaceIn("{{$randomBoolean}}")
pm.environment.set("depositpaid", depositpaid)

// Get the random recent date as a string
var a = pm.variables.replaceIn("{{$randomDatePast}}");
var randomDateRecent = new Date(a);
var checkin = randomDateRecent.toISOString().split('T')[0];
pm.environment.set("checkin", checkin);


// Get the random recent date as a string
var b = pm.variables.replaceIn("{{$randomDateFuture}}");
var randomDate = new Date(a);
var checkout = randomDate.toISOString().split('T')[0];
pm.environment.set("checkout", checkout);
```



# Create Test Suites   

### Using Newman   


  Newman is a command-line Collection Runner for Postman. It enables you to run and test a Postman Collection directly from the command line.
#### Install Command    
```bash
npm install -g newman    
```
#### Run Command    
- newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
- newman run “Collection Link” -e “Path”/EnvironmentName.json    

#### Create HTML Report  
 
#### Install Command      
```bash
npm install -g newman-reporter-html
```
**or**   
```bash
npm install -g newman-reporter-htmlextra    
```
#### Run Command      
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,html    
**or**    
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,htmlextra

- #### Newman File htmlextra
 <p align="center">
  <img src="https://github.com/asaha12/cricket_19_keyboard/assets/113898640/5ed484ce-2967-4a4e-942d-9e58049471d6"/></p>



