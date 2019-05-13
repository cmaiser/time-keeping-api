# Time Keeping API for Chris Maiser
## Data Model
[Entity Relationship Diagram](TimeEventDataModel.pdf)
### Summary
The API allows CRUD operation for "time events" which represent actions a user would make on a time card.  Actions are stored in a reference  table ACTION with names such as "Clock In", "Clock Out", etc.  The relationships are as follows:
* An employee (EMPLOYEE) can have 0-to-many pay periods (PAY_PERIOD)
* A pay period can have 0-to-many time card events (TIME_EVENT)
* Different time event types are represented via FK TIME_EVENT.ACTION_KEY
* Internal logic will handle inserting new PAY_PERIOD records based on pre-defined thresholds and associating time events with the appropriate (probably current) pay period.  

## API Documentation
[Documentation](http://htmlpreview.github.com/?https://github.com/cmaiser/time-keeping-api/blob/master/TimeEventApi.html)

## Example Usage
### API has been mocked in SwaggerHub and is currently live
Clock in for an employee (Assume action with value 2 corresponds to "Clock In")  
* curl -X POST "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"eventKey\": 1, \"employeeId\": 42, \"action\": 2, \"time\": {}, \"approve\": \"Y\"}"  

Clock out for an employee (Assume action with value 3 correponds to "Clock Out")  
* curl -X POST "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"eventKey\": 1, \"employeeId\": 42, \"action\": 3, \"time\": {}, \"approve\": \"Y\"}"  

Edit time for an employee  
* curl -X PUT "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"eventKey\": 1, \"employeeId\": 42, \"action\": 2, \"time\": \"2019-08-29T09:12:33.001Z\", \"approve\": \"N\"}"  

Delete a time for an employee  
* curl -X DELETE "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents?timeEventKey=1" -H "accept: application/json"  

Get all times for an employee
* curl -X GET "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents?employeeKey=1" -H "accept: application/json"  

Get a specific day for an employee  
* curl -X GET "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents?date=2019-08-29" -H "accept: application/json"  

Get times for a pay period  
* curl -X GET "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents?payPeriod=2" -H "accept: application/json"  

Approve time for an employee  
* curl -X PUT "https://virtserver.swaggerhub.com/chrismaiser/TimeEventTracker/1.0.0/timeEvents" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"eventKey\": 1, \"employeeId\": 42, \"action\": 2, \"time\": \"2019-08-29T09:12:33.001Z\", \"approve\": \"Y\"}"  
