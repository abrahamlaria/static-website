---
title: "Architecting for the Enterprise: Single Responsability Principle"
date: 2018-07-22T10:10:21-07:00
draft: false
image: "uploads/Architecture.jpg"
type: "post"
tags: [
    "software architecture",
    "solid",
    "single responsability principle",
]
categories: [
    "architecture",
]
---
A class should have one, and only one, reason to change.
<!--more-->
# Intro

In object-oriented computer programming, the term SOLID is an acronym for five design principles intended to make software designs more understandable, flexible and maintainable. The principles are a subset of many principles promoted by **Robert C. Martin**. The theory of **SOLID** principles was introduced by Martin in his 2000 paper Design Principles and Design Patterns, although the SOLID acronym itself was introduced later by **Michael Feathers**.
## Single Responsibility Principle (SRP)

A responsibility is a reason to change. The principle says:

> A class should have one, and only one, reason to change.

The idea is that each class should be built around one core task. Let’s say a class has methods A () and B (). A single change to method A () would require a recompile of method B () which hasn’t been changed. 

A common visual example when explaining SRP is a Swiss Knife. It has tools for everything but if for some reason one of the tools needs to be replaced you have to dismantle the whole set.

Consider the following code:

~~~csharp
public class BarberShop
{
    public void OpenDoor()
    {
        //Open the door if the time is equal to 9AM
    }
 
    public void ServiceClient(Client client)
    {
        //Check if the shop is opened and then
        //service a client if there’s any
    }
 
    public void CloseDoor()
    {
        //Close the door at 5:30PM
    }
}
~~~

The above code is violating the SRP by mixing the OpenDoor and CloseDoor responsibility with the core ServiceClient functionality.

A better implementation would be abstracting the OpenDoor and CloseDoor to an IDoor interface and inject that interface to the BarberShop controller. By doing that you can fix the SRP violation and also you are complying with the Dependency Inversion Principle (DIP). I’m going to address DIP in another post.

The new implementation is similar to the code below these lines. Granted, it is longer and somehow more verbose than the first one. But who said that good software is easy to write?

~~~csharp
public class BarberShop
{
    IDoor _door;

    public BarberShop(IDoor door)
    {
        _door = door;
    }

    public void OpenShop()
    {
        _door.OpenDoor();
    }

    public void ServiceClient()
    {
        //Check if the shop is opened and then
        //service a client if there’s any
    }

    public void CloseShop()
    {
        _door.CloseDoor();
    }
}

public interface IDoor
{
    void OpenDoor();
    void CloseDoor();
}

public class Door : IDoor
{
    public void OpenDoor()
    {
        //Open the door if the time is equal to 9AM
    }

    public void CloseDoor()
    {
        //Close the door at 5:30PM
    }
}
~~~

Now that you understand the SRP I'll give you a word of caution, SRP should be taken to the limit. Yes, your classes should be as simple as possible and focus on a main core task. But you still need places to accommodate all the logic that the system requires. Avoid creating classes that are all properties with little or no behavior.

Hopefully this post helped you to better understand the S part of the SOLID word. Let me know your opinion.

***

<span style="font-size: 12px; line-height: normal;">**References:**</span></br>
<span style="font-size: 12px; line-height: normal;">Dino Esposito, Andrea Saltarello, **_Microsoft .Net:_** _Architecting Applications for the Enterprise_, 2014, Pg 65, Microsoft Press.</span></br>
<span style="font-size: 12px; line-height: normal;">**Wikipedia:**<a href="https://en.wikipedia.org/wiki/SOLID"> _SOLID_</a></span>

