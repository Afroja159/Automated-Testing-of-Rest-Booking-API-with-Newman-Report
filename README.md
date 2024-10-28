### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- https://documenter.getpostman.com/view/26561979/2sAY4uBNUt
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/Afroja159/Automated-Testing-of-Rest-Booking-API-with-Newman-Report.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
    // first name
    var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
    console.log(firstName)
    pm.environment.set("firstName", firstName)

    // last name 
    var lastName = pm.variables.replaceIn("{{$randomLastName}}")
    console.log(lastName)
    pm.environment.set("lastName", lastName)

    // total price
    var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
    console.log(totalPrice)
    pm.environment.set("totalPrice", totalPrice)

    // deposit paid
    var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
    console.log(depositPaid)
    pm.environment.set("depositPaid", depositPaid)

    // date
    const moment = require('moment')
    const today = moment()
    console.log(today)
    console.log(today.add(5, 'd').add(2, 'M').add(1, 'Y').format("YYYY-MM-DD"))
    console.log(today.subtract(3, 'd').subtract(2, 'M').subtract(2, 'Y'))

    // checkin
    var checkIn = today.add(2, 'd').add(1, 'M').format("YYYY-MM-DD")
    pm.environment.set("checkIn", checkIn)

    // checkout
    var checkOut = today.add(7, 'd').add(2, 'M').format("YYYY-MM-DD")
    pm.environment.set("checkOut", checkOut)

    // additional needs
    var additionalNeeds = pm.variables.replaceIn("{{$randomLoremWord}}")
    console.log(additionalNeeds)
    pm.environment.set("additionalNeeds", additionalNeeds)
```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{checkIn}}",
    	"checkout" : "{{checkOut}}"
	},
	"additionalneeds" : "{{additionalNeeds}}"
 }

```
  **Response Body:**
 ```console 
  {
      "bookingid": 4334,
      "booking": {
          "firstname": "Joelle",
          "lastname": "Krajcik",
          "totalprice": 266,
          "depositpaid": true,
          "bookingdates": {
              "checkin": "2024-03-15",
              "checkout": "2024-03-20"
          },
          "additionalneeds": "monitor"
      }
  }
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "D'angelo",
    "lastname": "Feeney",
    "totalprice": 757,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-03-15",
        "checkout": "2024-03-20"
    },
    "additionalneeds": "hard drive"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "06eb798bf6f2caa"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
    // update first name
    var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
    console.log(firstName)
    pm.environment.set("updated_firstName", firstName)

    // update last name
    var lastName = pm.variables.replaceIn("{{$randomLastName}}")
    console.log(lastName)
    pm.environment.set("updated_lastName", lastName)

    // update total price
    var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
    console.log(totalPrice)
    pm.environment.set("updated_totalPrice", totalPrice)

    // update deposit paid
    var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
    console.log(depositPaid)
    pm.environment.set("updated_depositPaid", depositPaid)

    // date format
    const moment = require('moment')
    const today = moment()
    console.log(today.add(2, 'd').add(1, 'M').add(2, 'Y').format("YYYY-MM-DD"))
    console.log(today.subtract(1, 'd').format("YYYY- MM-DD"))

    // update check in
    var checkIn = today.add(2, 'd').add(1, 'M').format("YYYY-MM-DD")
    pm.environment.set("updated_checkIn", checkIn)

    // update check out
    var checkOut = today.add(9, 'd').add(3, 'M').add(1, 'Y').format("YYYY-MM-DD")
    pm.environment.set("updated_checkOut", checkOut)

    // update additional needs
    var additionalNeeds = pm.variables.replaceIn("{{$randomLoremWord}}")
    console.log(additionalNeeds)
    pm.environment.set("updated_additionalNeeds", additionalNeeds)
```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{updated_firstName}}",
	"lastname" : "{{updated_lastName}}",
	"totalprice" : {{updated_totalPrice}},
	"depositpaid" : {{updated_depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{updated_checkIn}}",
    	"checkout" : "{{updated_checkOut}}"
	},
	"additionalneeds" : "{{updated_additionalNeeds}}"
 }

```
  **Response Body:**
 ```console 
  {
      "bookingid": 4334,
      "booking": {
          "firstname": "Joelle",
          "lastname": "Krajcik",
          "totalprice": 266,
          "depositpaid": true,
          "bookingdates": {
              "checkin": "2024-03-15",
              "checkout": "2024-03-20"
          },
          "additionalneeds": "monitor"
      }
  }
```

 ## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run Booking_System_Practice.postman_collection.json -e Booking_System_Practice.postman_environment.json 
```
- Run Command for Report: 
```console 
newman run Booking_System_Practice.postman_collection.json -e Booking_System_Practice.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:
![image](https://github.com/user-attachments/assets/afa44f6a-888f-4bf2-9870-6830ebcca582)
![image](https://github.com/user-attachments/assets/91cb7c04-112d-4f84-b9f6-31c012e0ee84)
![image](https://github.com/user-attachments/assets/c03c4b6f-25f7-46b6-803d-8754263ec3c0)
![image](https://github.com/user-attachments/assets/856a7e34-1f40-4501-9235-c8624060dc9f)




