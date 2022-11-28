# Utilita Payments System
-------------------------
  
  
## Infrastructure Overview

![Payments System Block Flow](Utilita-Block-Flow2-With-Payment-Success.svg 'Block Flow Payments System')
  

**Front-end Service** - Used by WebClient - displays gets current Vending status allow customer to make payments

### Flow
  - Customer hits **Front-end Service** - where payment can be made and Rcurrent vending service is shown if applicable (ie payment added)
  - Payment Attempted (**Payments Service**) - Front-end Service calls Payments service
  - Payment Success (**Payments Service**) - Payment services puts message in `PaymentSuccess` MessageQ, inserts row in DB, notifies customer that it is now attempting to update meter.
  - Payment Failure (**Payments Service**) -  Payment services puts message in `PaymentFaliure` MessageQ including reason, notifies customer via Front-end Service and inserts row in DB. 
  - **Meter Vending Service** - read messages from `PaymentSuccess` MessageQ and hit the 3rd Party Service to provide Vending
  - Vending Success (**Meter Vending Service**) - **Front-end Service** recieves message to notify customer of successful credit added, row inserted into DB
  - Vending Failure (**Meter Vending Service**) - **Front-end Service** recieves message to notify customer of attempting to add credit, **Meter Vending Service** retries 3rd Party Service to provide Vending, until Max attempts reached when: **Front-end Service** recieves notification and the Customer is alerted, on call operators are alerted, and message is inserted into the `VendingFailure` MessageQ
  
  
  
## Cloud Infrastructure


![AWS Infrastructure](Utilita-AWS-Solution-ECR.svg 'AWS Infrastructure')
