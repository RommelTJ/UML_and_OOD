# UML Basics and Fundamental Diagram Types

## What's UML?

* Unified Modeling Language
* Graphical notation used to communicate the design of software systems
* Diagram Types
  * Use-Case Diagrams (functional diagrams)
  * Class Diagrams (structural diagrams)
  * Sequence Diagrams (dynamic/behavioral diagrams)
* It's independent of any programming language
* Diagramming lets you gain a deeper understanding of what should be implemented
* Helps us communicate ideas with other developers effectively
* Detailed diagrams are often required for Waterfall projects

## Use Case Diagrams

* Its purpose is to visualize the functional requirements of the system.
* They show groups of related use cases.
* To represent a use case, we draw an oval and put the title of the use case in it.
  * Examples: Create Trip Entry, Edit Trip, Export App Database
* We use stick figures to represent the Actors
  * Actors are human beings or other systems that interact with our system
  * Note: `actor` in mermaidjs only exist in sequence diagrams
  * Primary actors are typically labeled on the left side of the use-case diagram
  * Secondary actors are typically labeled on the right side of the use-case diagram
* We draw lines to represent interactions between actors and the ovals
* System boundaries are represented by rectangular frames
* Use case diagrams provide a clear way to communicate the high-level features and the scope of the system
  * But they don't replace use-case descriptions
    * These include more information so that important details are not missed.

```mermaid
flowchart TD;
   %% Trigger event
   TRIGGER([The user asks the system to log them in])-->S1;
 
   %% Main success scenario
   S1[The system renders the login screen<br /> and asks the user to provide their credentials]-->S2;
   S2[/"The user provides its credentials (email and password)<br /> and asks the system to log them in"/]-->S3;
   S3[The system asks the backend API to verify users credentials]-->S4;
   S4{The backend API confirms that<br /> the provided credentials are valid?};
   S4--Yes-->S5;
   S5{The backend API confirms that<br /> the user has an active subscription?};
   S5--Yes-->SUCCESS
  
   %% Extension 2a: The user authenticates via 3rd party system (Google, Facebook)
   S1-->EXT2a1;
   EXT2a1["The user asks the system to authenticate it<br /> via 3rd party authentication system <br />(Google or Facebook)"]-->EXT2a2;
   EXT2a2[The system redirects the user to the<br /> appropriate 3rd party authentication system]-->EXT2a3;
   EXT2a3{The user successfully authenticates <br />using 3rd party authentication system?};
   EXT2a3--Yes-->EXT2a4;
   EXT2a3--No-->EXT4a2;
   EXT2a4[the 3rd party authentication system<br /> provides the system with the user's<br /> identification information]-->EXT2a5;
   EXT2a5[The system asks the backend system to confirm<br /> that the user has a valid subscription]-->EXT2a6;
   EXT2a6{The backend API confirms that<br /> the user has an active subscription?};
   EXT2a6--Yes-->EXT2a7;
   EXT2a6--No-->EXT5a2;
   EXT2a7[The backend system provides the system<br /> with the appropriate authentication token]-->SUCCESS;
 
   %% Extension 4a: The user does not have a valid account
   S4--No-->EXT4a1;
   EXT4a1[The backend system determines<br /> that the user does not have a valid account<br /> and informs the System of that fact]-->EXT4a2;
   EXT4a2[The system informs the user that<br /> their credentials are not valid];
   EXT4a2-->S1;
 
   %% Extension 5a: The user does not have a valid account
   S5--No-->EXT5a1;
   EXT5a1[The backend system determines<br /> that the user does have an account but <br />does not have a valid subscription<br /> and informs the System of that fact]-->EXT5a2;
   EXT5a2[The system informs the user that <br />it does not have a valid subscription]-->EXT5a3;
   EXT5a3[The system instructs the user to </br />go to the web to buy a subscription];
   EXT5a3-->FAILURE;   
 
   SUCCESS([System logs the user in]);
   style SUCCESS fill:#cfc
 
   FAILURE(Login flow terminates);
   style FAILURE fill:#fcc
```

Elevator Challenge:  
- What actors interact with the elevator?
- What are its main functions?
- Elevators are on duty 24/7
- Maintenance and repair is required

User role:  
```mermaid
flowchart LR
  TRIGGER([The user enters the elevator])-->S1
  TRIGGER([The user enters the elevator])-->S2
  TRIGGER([The user enters the elevator])-->S3
  TRIGGER([The user enters the elevator])-->S4
  TRIGGER([The user enters the elevator])-->S5
  
  %% Main success scenario %%
  subgraph Elevator
    S1[Call Elevator]
    S2[Select Floor]
    S3[Ride Elevator]
    S4[Operate Doors]
    S5[Trigger Emergency]
  end
```

Technician Role:  
```mermaid
flowchart LR
  TRIGGER([The technician enters the elevator])-->S1
  TRIGGER([The technician enters the elevator])-->S2
  TRIGGER([The technician enters the elevator])-->S3
  TRIGGER([The technician enters the elevator])-->S4
  TRIGGER([The technician enters the elevator])-->S5
  TRIGGER([The technician enters the elevator])-->S6
  TRIGGER([The technician enters the elevator])-->S7
  TRIGGER([The technician enters the elevator])-->S8
  
  %% Main success scenario %%
  subgraph Elevator
    S1[Call Elevator]
    S2[Select Floor]
    S3[Ride Elevator]
    S4[Operate Doors]
    S5[Trigger Emergency]
    S6[Inspect Elevator]
    S7[Service Elevator]
    S8[Repair Elevator]
  end
```

## Class Diagrams

* The most frequently used UML diagram type.
* First, identify all the entities that represent the system.
* A class is represented as a rectangle with 3 compartments.
  * Class Name
    * Standard: Name should be in upper camel-case.
  * Attributes
    * Should be concise
    * Should be in lower camel-case.
    * Should include the data type.
  * Operations
    * Should be verbs in lower camer-case.
    * Can specify method arguments.
    * Can specify a return type.  

Class Diagram Challenge:  
* Create a class diagram of an elevator maintenance robot.
  * Robot must have an unique identifier
  * Robot can diagnose, service, and repair the elevator
  * Keep it simple

## Visibility: Public, Private, Protected, Package

## Associations

## Generalization

## Dependency, Aggregation, Composition and Realization

## Sequence Diagrams

## Activity Diagrams

## Statechart Diagrams

