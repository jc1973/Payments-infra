# Utilita Payments System
-------------------------
  
  
## Infrastructure Overview

![Payments System Block Flow](Utilita-Block-Flow2-With-Payment-Success.svg 'Block Flow Payments System')
  

**Front-end Service** - Used by WebClient - displays gets current Vending status allow customer to make payments

### Flow
  - Customer hits Front-end Service - where payment can be made and Rcurrent vending service is shown if applicable (ie payment added)
  - Payment Attempted - Front-end Service calls Payments service
  - Payment Success - Payment services puts message in `PaymentSuccess` MessageQ and inserts row in DB record, notifies customer that attempted to update meter.
  - Payment Failure -  Payment services puts message in `PaymentSuccess` MessageQ including reason
 

