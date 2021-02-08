# technologyconsulting-showcase-manufacturedomain
manufacturedomain is a part of a showcase implementation which is running on a open liberty instance. It is structured right now like this

- **manufacturedomainParent** Parent maven module
    - **manufacturedomainDTO** - contains all classes used in the rest controllers
    - **manufacturedomainWAR** - contains the rest controllers and all EJB classes and entities
    - **manufacturedomainEAR** - contains the war module
and could be found under the src folder

## The project consists of the following packages

- **de.novatec.showcase.manufacture.dto** - with all related order domain dto's
- **de.novatec.showcase.manufacture.ejb.entity** - with all related order domain entities
- **de.novatec.showcase.manufacture.ejb.session** - with the order domain EJB session beans
- **de.novatec.showcase.manufacture.controller** - with corresponding REST controllers for Item, Customer and Order
- **de.novatec.showcase.manufacture.mapper** - with orika mapper fro dto/entity mapping


## build, run and stop manufacturedomain on an open liberty server
- **build:** mvn clean install
- **run:** mvn liberty:run
- **stop:** mvn liberty:stop
- **run open liberty in development mode:** mvn liberty:dev

All commands have to be executed from the manufacturedomainEAR folder. In development mode you can run the the integration tests (*IT.java classes) by pressing RETURN/ENTER when the server is up. Code changes in the IT tests are hot replaced.

## Smoketest
There is a little script smoketest.sh in the manufacturedomainParent\resources\smoketest folder which could be used to test if the very basic functionality works after staring the open liberty server with the manufacturedomain as EAR. Be careful this smoketest.sh could be run only once!!!

- create three components (parts)
- create 21 assemblies
- create bill of material (bom) 
    - with three components and two assemblies
    - assembly 1 is build up from part 1,2,3 and 
    - assembly 2 is build up only from part 1 and 2
    - assembly 3 to 21 is build up only from part 1 and 3
- create the inventories for 
    - three components and 
    - 21 assemblies
- create/schedule a workorder
- deliver (ComponentDemand) parts
- move workorder through the workorder states
    - **STAGE1**
    - **STAGE2**
    - **STAGE3**
- complete workorder/ set workorder in state **COMPLETE**
- create second workorder
- cancel the second workorder / set workorder in state **CANCELED**

The smoketest.sh script consist of two sub scripts - the setup-db.sh and business-calls.sh script. The first one setup the database of the orderdomain via some REST calls. The data for the calls could be found in the folder ./resources/smoketest/data. The smoketest script additionally starts/stops a mockserver which is used for emulating the manufature domain in the business calls. The exceptations for the calls could also be found in data folder. All three scripts have the optional parameters -h for setting the host and -p for setting the port of the domain which is called. The host defaults to localhost and port to 9080.

## openAPI
check [openAPI](http://localhost:9080/api/explorer/) if the server is running for the API documentation of the manufacture domain

