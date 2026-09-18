# Some Background


**Source File:**

None


**Word Count:**

None



---

Topic 31

Topic 31

You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. Joe Armstrong

You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.

You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.

Joe Armstrong

Joe Armstrong

Do you program in an object-oriented language? Do you use inheritance?

If so, stop! It probably isn’t what you want to do.

Let’s see why.

Inheritance first appeared in Simula 67 in 1969. It was an elegant solution to the problem of queuing multiple types of events on the same list. The Simula approach was to use something called prefix classes . You could write something like this:

prefix classes

The link is a prefix class that adds the functionality of linked lists. This lets you add both cars and bicycles to the list of things waiting at (say) a traffic light. In current terminology, link would be a parent class.

link

link

The mental model used by Simula programmers was that the instance data and implementation of class link was prepended to the implementation of classes car and bicycle . The link part was almost viewed as being a container that carried around cars and bicycles. This gave them a form of polymorphism: cars and bicycles both implemented the link interface because they both contained the link code.

link

car

bicycle

link

container

link

link

After Simula came Smalltalk. Alan Kay, one of the creators of Smalltalk, describes in a 2019 Quora answer [44] why Smalltalk has inheritance:

why

So when I designed Smalltalk-72—and it was a lark for fun while thinking about Smalltalk-71—I thought it would be fun to use its Lisp-like dynamics to do experiments with “differential programming” (meaning: various ways to accomplish “this is like that except”).

This is subclassing purely for behavior.

These two styles of inheritance (which actually had a fair amount in common) developed over the following decades. The Simula approach, which suggested inheritance was a way of combining types, continued in languages such as C++ and Java. The Smalltalk school, where inheritance was a dynamic organization of behaviors, was seen in languages such as Ruby and JavaScript.

So, now we’re faced with a generation of OO developers who use inheritance for one of two reasons: they don’t like typing, or they like types.

Those who don’t like typing save their fingers by using inheritance to add common functionality from a base class into child classes: class User and class Product are both subclasses of ActiveRecord::Base .

User

Product

ActiveRecord::Base

Those who like types use inheritance to express the relationship between classes: a Car is-a-kind-of Vehicle .

Car

Vehicle

Unfortunately both kinds of inheritance have problems.

Inheritance is coupling. Not only is the child class coupled to the parent, the parent’s parent, and so on, but the code that uses the child is also coupled to all the ancestors. Here’s an example:

uses

When the top-level calls my_car.move_at , the method being invoked is in Vehicle , the parent of Car .

my_car.move_at

Vehicle

Car

Now the developer in charge of Vehicle changes the API, so move_at becomes set_velocity , and the instance variable @speed becomes @velocity .

Vehicle

move_at

set_velocity

@speed

@velocity

An API change is expected to break clients of Vehicle class. But the top-level is not: as far as it is concerned it is using a Car . What the Car class does in terms of implementation is not the concern of the top-level code, but it still breaks.

Vehicle

Car

Car

Similarly the name of an instance variable is purely an internal implementation detail, but when Vehicle changes it also (silently) breaks Car .

Vehicle

Car

So much coupling.

Some folks view inheritance as a way of defining new types. Their favorite design diagram shows class hierarchies. They view problems the way Victorian gentleman scientists viewed nature, as something to be broken down into categories.

Unfortunately, these diagrams soon grow into wall-covering monstrosities, layer-upon-layer added in order to express the smallest nuance of differentiation between classes. This added complexity can make the application more brittle, as changes can ripple up and down many layers.

Even worse, though, is the multiple inheritance issue. A Car may be a kind of Vehicle , but it can also be a kind of Asset , InsuredItem , LoanCollateral and so on. Modeling this correctly would need multiple inheritance.

Car

Vehicle

Asset

InsuredItem

LoanCollateral

C++ gave multiple inheritance a bad name in the 1990s because of some questionable disambiguation semantics. As a result, many current OO languages don’t offer it. So, even if you’re happy with complex type trees, you won’t be able to model your domain accurately anyway.

Let us suggest three techniques that mean you should never need to use inheritance again:

Interfaces and protocols

Delegation

Mixins and traits

Most OO languages allow you to specify that a class implements one or more sets of behaviors. You could say, for example, that a Car class implements the Drivable behavior and the Locatable behavior. The syntax used for doing this varies: in Java, it might look like this:

Car

Drivable

Locatable

Drivable and Locatable are what Java calls interfaces ; other languages call them protocols , and some call them traits (although this is not what we’ll be calling a trait later).

Drivable

Locatable

interfaces

protocols

traits

Interfaces are defined like this:

These declarations create no code: they simply say that any class that implements Drivable must implement the two methods getSpeed and stop , and a class that’s Locatable must implement getLocation and locationIsValid . This means that our previous class definition of Car will only be valid if it includes all four of these methods.

Drivable

getSpeed

stop

Locatable

getLocation

locationIsValid

Car

What makes interfaces and protocols so powerful is that we can use them as types, and any class that implements the appropriate interface will be compatible with that type. If Car and Phone both implement Locatable , we could store both in a list of locatable items:

Car

Phone

Locatable

We can then process that list, safe in the knowledge that every item has getLocation and locationIsValid :

getLocation

locationIsValid

Interfaces and protocols give us polymorphism without inheritance.

Inheritance encourages developers to create classes whose objects have large numbers of methods. If a parent class has 20 methods, and the subclass wants to make use of just two of them, its objects will still have the other 18 just lying around and callable. The class has lost control of its interface. This is a common problem—many persistence and UI frameworks insist that application components subclass some supplied base class:

The Account class now carries all of the persistence class’s API around with it. Instead, imagine an alternative using delegation, as in the following example:

Account

We now expose none of the framework API to the clients of our Account class: that coupling is now broken. But there’s more. Now that we’re no longer constrained by the API of the framework we’re using, we’re free to create the API we need. Yes, we could do that before, but we always ran the risk that the interface we wrote can be bypassed, and the persistence API used instead. Now we control everything.

none

Account

In fact, we can take this a step further. Why should an Account have to know how to persist itself? Isn’t its job to know and enforce the account business rules?

Account

Now we’re really decoupled, but it has come at a cost. We’re having to write more code, and typically some of it will be boilerplate: it’s likely that all our record classes will need a find method, for example.

find

Fortunately, that’s what mixins and traits do for us.

As an industry, we love to give things names. Quite often we’ll give the same thing many names. More is better, right?

That’s what we’re dealing with when we look at mixins. The basic idea is simple: we want to be able to extend classes and objects with new functionality without using inheritance. So we create a set of these functions, give that set a name, and then somehow extend a class or object with them. At that point, you’ve created a new class or object that combines the capabilities of the original and all its mixins. In most cases, you’ll be able to make this extension even if you don’t have access to the source code of the class you’re extending.

Now the implementation and name of this feature varies between languages. We’ll tend to call them mixins here, but we really want you to think of this as a language-agnostic feature. The important thing is the capability that all these implementations have: merging functionality between existing things and new things .

mixins

existing things

new things

As an example, let’s go back to our AccountRecord example. As we left it, an AccountRecord needed to know about both accounts and about our persistence framework. It also needed to delegate all the methods in the persistence layer that it wanted to expose to the outside world.

AccountRecord

AccountRecord

Mixins give us an alternative. First, we could write a mixin that implements (for example) two of three of the standard finder methods. We could then add them into AccountRecord as a mixin. And, as we write new classes for persisted things, we can add the mixin to them, too:

AccountRecord

We can take this a lot further. For example, we all know our business objects need validation code to prevent bad data from infiltrating our calculations. But exactly what do we mean by validation ?

validation

If we take an account, for example, there are probably many different layers of validation that could be applied:

Validating that a hashed password matches one entered by the user

Validating form data entered by the user when an account is created

Validating form data entered by an admin person updating the user details

Validating data added to the account by other system components

Validating data for consistency before it is persisted

A common (and we believe less-than-ideal) approach is to bundle all the validations into a single class (the business object/persistence object) and then add flags to control which fire in which circumstances.

We think a better way is to use mixins to create specialized classes for appropriate situations:

Here, both derived classes include validations common to all account objects. The customer variant also includes validations appropriate for the customer-facing APIs, while the admin variant contained (the presumably less restrictive) admin validations.

Now, by passing instances of AccountForCustomer or AccountForAdmin back and forth, our code automatically ensures the correct validation is applied.

AccountForCustomer

AccountForAdmin

automatically

We’ve had a quick look at three alternatives to traditional class inheritance:

Interfaces and protocols

Delegation

Mixins and traits

Each of these methods may be better for you in different circumstances, depending on whether your goal is sharing type information, adding functionality, or sharing methods. As with anything in programming, aim to use the technique that best expresses your intent.

And try not to drag the whole jungle along for the ride.

Topic 8, ​ The Essence of Good Design ​

Topic 10, ​ Orthogonality ​

Topic 28, ​ Decoupling ​

The next time you find yourself subclassing, take a minute to examine the options. Can you achieve what you want with interfaces, delegation, and/or mixins? Can you reduce coupling by doing so?

