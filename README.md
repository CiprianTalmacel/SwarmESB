###Hello visitors: These days we are refactoring SwarmESB repository to prepare SwarmESb2.0 release. For a few days just look directly in SwarmCore module to start working with Swarms. Still, the main documentation is here! 

#SwarmESB central repository. Refactoring and master plan:
This is the new version of SwarmESB, based on [SwarmCore] (https://github.com/salboaie/swarmcore "SwarmCore") that adds:  
 - default load distribution between Adapters
 - new broadcast primitive
 - "do" syntax to describe guaranteed message delivery (at least once)  
 - allows creation of personalised/custom ESBs that can use other middleware than Redis
 - refactoring in progress to grow it around a DI container for better stability (semnatic-firewall module)
 - based on a new powerful ACl module (acl-magic module)
 - deployment support for docker containers
 - UI with system monitoring (work in progress)
 - better logging (work in progress) 
 - support for typed persistence and complex custom type representation ("apersistence" module) 
 - support for executable choreography (work in progress based on PubSubChor module)
 - distributed transactions mechanisms (work in progress)
 - support for representation of long living processes (work in progress)

## What is SwarmESB ?

Swarm communication is a micro-services architecture based on a new message communication pattern we call "swarms" 
It offers an starting architecture for cloud and enterprise systems. 
The usual method of doing message passing is to have relatively intelligent processes, objects or actors sending and receiving dumb messages. 
Thinking to messages as relatively smart beings visiting relatively non intelligent places, we noticed a positive effect on the quality of the code and a new path for 
decomposing complex applications in small services. 
SwarmESB is using swarm communication for creating an easy to grow Enterprise Service Bus. 
You add your own microservices (we call adapters) and describe how  microservices get composed for your usecases in a coupling free DSL (swarm descriptions).


Presentation:  https://docs.google.com/presentation/d/1xn1L9bbiD1TUY7ku5d0V_zF7SBkH3ANQ2uN8AxAXaA8/

![Overview](http://salboaie.github.com/images/swarmDiagram.png "SwarmESB")


A "swarm" is a set of related messages with some basic intelligence and is based on an intuitive point of view:
 computer processes communicating by asynchronous messages are more like "dumb trees/flowers" visited by "smart 
swarms of bees" than "smart people" communicating by "dumb messages".
This intuition have a powerful effect on reducing complexity of many distributed systems (already proved by SOA)
Service orchestration with SwarmESB is elegant, there is no need to learn new languages and difficult new concepts: just use Java Script code and a few simple concepts.


 SwarmESB is an open source project implementing a new approach: "Swarming architecture" that you could reuse
for your new multi-tenant systems that will transparently acquire the benefits of scalability, high availability, highly
parallel computing and loose coupling usually obtained with asynchronous messages, message queues, pub/sub channels and
using a message or service bus. While this project is build using Node.js and Redis, this project will present "swarming"
as a new fundamental concept, comparable, but from the code maintainability perspective a lot simpler than direct 
usage of Enterprise Integration Patterns or the Actor model used in Scala and Erlang.


Imagine, Swarms can be for SOA's orchestration what REST is for SOAP!

## Examples
    
A swarm description is written in Java Script and is composed from:  variable declarations (for defaults),
constructors (functions that get called on the adapter that starts a swarm) and phases (code that get executed
remotely, usually in another node) 
    
The swarm described bellow will magically get executed without any other programming efforts in 3 nodes (processes):

            vars:{
                message:"Hello World",
            },
            start:function(){ //constructor  that can be executed in any adapter
                        this.swarm("concat");  // swarm is a "primitive" used to invoke execution in a phase
                    },
            concat:{ // phase that get executed in "Core" adapter
                node:"Core",
                code : function (){
                        this.message = this.message + " The swarming has begun! ";
                        this.swarm("print");    //move again
                    }
            },
            print:{ //print phase executed in "Logger" adapter
            node:"Logger",
            code : function (){
                cprint(this.message);    //use of some api, specific to the Logger node
                },
            }
 

Waw: each node could be on a different continent!  Check other swarms for parallel execution examples.



## Easy and fun! 
        
    Check our wiki: https://github.com/salboaie/SwarmESB/wiki

    Technologies: node.js, Redis, PUB/SUB
    
SwarmESB ca be used as a light, open source, ESB (or Message Bus) for your enterprise applications.
Instead of message oriented communication or web services, you describe your communication between "nodes" in what
we call "swarm descriptions" or simple "swarms".
"Nodes" can be adapters to various servers or clients connected to the "swarming middleware": SwarmESB.

Your adapters can use web services as a particular case of providing existing APIs in a node.


## Installation:  https://github.com/salboaie/SwarmESB/wiki/Install-guide

## Conclusions:

    1. Maintainable code: Open/closed principle, no threads get abused (ever), simple
    2. High performance: We are using node.js and his asynchronous capabilities revealed no throughput degradation in
    our benchmarks. Network latency have no effect in capability of the system to execute things in parallel.
    3. Scalability: Load balancing and sharding (research) can be implemented using swarming concepts
    4. High availability: Still at the research level but looks promising


    
## Project SWARM

    SwarmESB is part of the open source project "Swarm project" together with:
    
* SwarmShape: https://github.com/salboaie/SwarmShape : a MVVM framework with swarm based persistence
* WSSearmClient: https://github.com/salboaie/WSSearmClient : swarm client for web sockets
* SwarmCore https://github.com/salboaie/SwarmCore : a reusable node.js module containing the SwarmESB implementation 
    
   
    
#Copyright
(c) Axiologic Research & Alboaie Sînică. 
Code License: LGPL or MIT 
The content of the README and of the wiki is Public Domain

Commercial versions derived from this project are allowed. However, it would be desirable that all ESBs developed around swarm communication idea to get identical APIs and compatible programming styles.
Contact salboaie@gmail.com for details. 


#Supporters
![WebStorm, the best IDE for node.js and JS](http://www.jetbrains.com/img/logos/webstorm_logo142x29.gif) 

* http://www.jetbrains.com

