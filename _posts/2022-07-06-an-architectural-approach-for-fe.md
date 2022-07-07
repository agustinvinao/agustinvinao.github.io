---
title: An Architectural Approach for FrontEnd Applications
published: true
---
An Architectural Approach for FrontEnd Applications
---

After more than 8 years of working with Angular (angularJS and angular), I'm putting together what I'm still trying to name as a framework or as a protocol for this part of a system.

Even when this will describe FE section of a system, with the necessary tweaks, it can be applied to Backend, devops systems, and others.

## The Problem

I will describe the problem I'm trying to solve using two different examples:

1. A new system
2. An existing system

We will use the same example for both.

Let's suppose you're a new member of a team, the system is the classic shopping cart for your company. You have a website to show your products, the features of this system are simple:

- add items to your shopping cart
- place an order
- create an account
- login in to your account
- check your orders
- access my profile

### 1. A new system

How should a team start working on a system in a way to have minimal well defined information? and how to avoid having too much documentation with the problems of mantain it?
Documentation, you will find people who love it, even more than code or anything else.

### 2. An existing system

A common problem I've found on existing systems is how to share knowledge with new devs.

How do new members understand the system with a holistic perspective and generate the necessary tools for starting contributing as soon as possible?

If I go and ask someone currently working in the system, I may get an opinionated point of view of what a system is doing at the moment. This view may have an excellent description of anything coded by who explains this but not the same level from other parts without the same dedication from this person. Nobody to blame, just about our expertise level on different sections. 

For example, if I was working on the shopping cart of the company's website, I know-how was built; but if I need to explain the profile section, I won't have the same expertise.

## Documentation, a hard balance between usefull and useless

Documentation can be your best friend or your worst nightmare. If the documentation is up to date, you will say "thank you" each time you have questions, but if it is not, you will lose your confidence quickly and stop looking at the documentation after a couple of times where this occurs.

How much it cost to mantain the documentation? Almost nobody ask. There is a false belief that documentation doesn't require maintenance. This is false, documentation is something that requires to be checked all the time.

Initial documentation of a system works as a blueprint. It reflects the intentions and a proposal about what it will be a system. 

An implementation of a blueprint may have diferences. Is the documentation the tools for verify. Based on the diferences, an action must be taked. Update the documentation or fixing our implemantation.

## The solution

I have a philosophy: I don't talk about a problem without trying to offer a solution -or something where to start-.

### a blueprint for the system

Anytime when we want to build something new or if we want to understand something that exists, having a blueprint is one of the best ways.

Having a single place where we can answer fundamental questions will help to share knowledge, have all people with a common understanding and don't repeat the same questions overtime with the risk of different answers.

I have a basic format for this blueprint, can be used for new or existing systems. In both cases as developers/architects we need to answer each item with what we want or what it exists in the system.

### an example for the blueprint

The following works as an example, the listed items in the blueprint must be agreed upon, but this is not a fixed list. It can change over time. Every change will go through the agile cycle to get an agreement and verify its content.


### App Overview
    Short description of the purpose of the application and keys requirements
    Anyone reading the overview will have an idea about the intentions of the system and the scope.
    Example: A shopping cart application for placing and tracking orders for the company products.

### App Features
    Most important features of the system. One line per feature, as a title.
    In our example, this will show like: shopping cart, profile view, and orders list.

### Domain Security
    What type of security will we use? Cookies, tokens? Both? How will it be implemented?

### Domain Rules
    List the most relevant domain rules of the system.
    Not all the domain rules must appear here. Using other documents for different features or subsections of the system can help. We must avoid having hard-to-maintain documentation, sometimes because of the extension of it.

### Logging
    What information about the system do we need to store for later evaluation? 
    Is the user behaviour tracked? What happens when an error happens?
    Is the application sending a report to an API endpoint for evaluation?
    Is an error going silent, and nobody else than the user will see it?

### Communication
    What is going to be used to communicate with data sources? One or more APIs? Websockets? Other?
    How does it manage the state?
    How is the external data flow in the application?

### Data Models
    What's the purpose of the models?
    Will it include logic? Or the application won't have any logic at all?
    Classes or interfaces?

### Components design
    Any component pattern strategy? example Container/Presenter pattern
    Most important components.

### Shared Functionality
    List of external libs.
    List of 3rd party libs.

### Testing
    What's the philosophy for testing? Unit test? e2e?
    What's the coverage value expected? What type of coverage? Line coverage? Statement coverage?

### Development Setup
    A detailed instructions how to setup a local environment to run the application for development.

### CD/CI
    Exists a CD/CI setup for the application?
    How is the CD triggered?
    Is any code change triggering a build?
    How can I access the results of a build or any errors on it?

## Final note

I see the previous example as a document living in the same repository as the project's code. It can be a markdown file, a wiki, or anything that helps to access this information.

Working on a project presents challenges overtime, it's never about what we thing today, it's about what is going to be in the future:

- How can we implement what we design?
- How can we verify if it is not possible to implement what we've designed?
- How can we explain what we've implemented to others? And to us in 6 months? In a year?
- How can we create a plan to extend our system? Is the plan affecting our implementation?

Finding answers to these questions will be easier if we have our blueprint up to date. It will help us to understand how things work and how anything new will need to interact without existing systems.