# Utilita Payments System
-------------------------
  
  
## Infrastructure Overview

![Payments System Block Flow](Utilita-Block-Flow2-With-Payment-Success.svg 'Block Flow Payments System')
  

**Front-end Service** - Used by WebClient - displays gets current Vending status allow customer to make payments

### Flow
  - Customer hits **Front-end Service** - where payment can be made and Rcurrent vending service is shown if applicable (ie payment added)
  - Payment Attempted (**Payments Servive**) - Front-end Service calls Payments service
  - Payment Success (**Payments Servive**) - Payment services puts message in `PaymentSuccess` MessageQ and inserts row in DB record, notifies customer that it is now attempting to update meter.
  - Payment Failure (**Payments Servive**) -  Payment services puts message in `PaymentFaliure` MessageQ including reason, notifies customer via Front-end Service and inserts row in DB record. 
  

