## Changing requirements ##
- changing is hard
- some changes are impossible
- cost of change
- correctness of the change

>**the Goal is to make the cost of change as low as possible** 

## Solutions ##
- test
- Design

> We can create some tests for the functions that we have created to see if the change has any issue or not.

> We have to design the system so that we will be able to develop it more and more in the future.

## Agility ##
- Market and competitors
- فیدبک لوپ کوتاه (providing features to users and getting feedback from them)
- technical debt (We do some thing wrong technically to provide the app faster and then we will fix the technical issue later)
## Maintenance 
- The software has to work for years
- New people may get added to the project
- New features may get added
- Evolvability, modifiability, changing the system has to be easy
- updating the versions
> Refactoring: Upgrading the quality of the code

## Complicated large Business Logic
- Too many features
- Millions lines of code
- Too many developers working on the project
## Microservice
> Breaking the projects to some services
- Microservices act independently, they have separate databases for themselves
- A Microservice has some APIs so that other microservices can get data from it

>**Monolithic is the opposite of Microservice (One Project and a Super Service)**

>`coupling:` Coupling is when A microservice is dependent to other one.

> The languages of microservices are not necessarily the same.
> We choose the language of each microservice according to the need of that service to have the best performance.

## Scale  مقیاس
- Growth rate of users
- users management
The number of users can suddenly get increased.
We have to be careful about the growth rate of users in special hours.
#### Solutions ####
- `scalability`: 
increasing the usage of resources as much as the requests increase (usually in a linear manner)
>We have to know what we are going to be scalable about
- `Monitoring`:
Monitoring is one of the important things in a software.‌ It tells us the status of the whole system, things like:
- Request rate of some apis
- response time and etc...

## Performance
- user experience
#### solutions
- Monitoring
- Databse Selection: Choosing the right DBMS according to our need
- Databse Optimization
---
# Session 3
