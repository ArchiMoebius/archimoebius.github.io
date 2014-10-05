---
layout: post
title: Model Exploration
categories:
- Software Engineering
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---

<p>
    For the past thirty some odd years software engineer‘s have needed some set method by which to develop applications. The need for a set methodology for application architecture creation and maintenance gave birth to many development ground rules which have evolved over the years. A more concise definition of the basic steps that go into software engineering are: analysis, design, implementation and testing. These are the basic building blocks for different models which are employed to produce dependable software. The models which we will be discussing are waterfall, incremental, and prototype. First we will explore what Extreme programming is. Extreme programming (XP) is one of the newest additions to the software engineer‘s arsenal of development styles. However, XP is not right for every project. Only projects which are no more than median in size should have the XP model applied to them. XP entails rapid design, development, debugging and deployment on an extremely tight, evolutionary but iterative schedule. In the words of Martin Fowler “(XP) challenges many of the common assumptions about software development. Of these one of the most controversial is its rejection of significant effort in up-front design, in favor of a more evolutionary approach”. To summarize, simple design and an evolutionary code base are quintessentially XP.
</p>

<p>
    According to Kent Beck, XP can be broken down and defined by the following four categories of development analysis, design, implementation, and testing. Analysis involves project planning, small releases and metaphor. Design entails simplicity, re-factoring and continuous integration. Implementation is where pair programming and collective ownership come into play. The last phase of development, testing, is applicable to every stage of the software’s life span.
</p>

<p>
    The first stage is project planning. Programmers give time estimates which reflect the required time that each story release will incur. Each iteration (life cycle) of an application only implements those stories which the customer wants or those that are needed to ascertain a milestone which is required for a release. Releases are made any time from daily to monthly and start as soon as possible. Before ‘finalising’ a design the programmers crank out as much of the product as possible. This is done for a couple of reasons. These reasons are expedition of error catching and design refinement as well as dynamic requirements integration. The customer is king under the XP process. Without good communication, however, the translation of requirements between the customer and the development team can be horribly misconstrued. Communication is a huge barrier which XP overcomes through the use of metaphors. Once the customer and the team have defined a set of metaphors, communication of requirements is made much cleaner and misinterpretations are minimised.
</p>

<p>
    Secondly comes design. Simplicity in design is a must for the XP model. If you don’t require it don’t put it in the design, keep it DRY (Don’t Repeat Yourself). The design is the conceptual representation of a perception for a how a system should operate. It is not the final product. It should not try to address every conceivable issue and should be used as a guideline which can be redrafted. Without a dynamic perspective on design, the XP model will lose it‘s adaptive nature in respect to updated requirements. Re-factoring is a must. The design will evolve on its own after more requirements are put into place and all of its tests are created. As a system‘s design evolves, the code must reflect these changes and be able to adapt to the new requirements while still passing all previous test cases. Development continues even when design changes occur. Continuous integration is key for XP. For each iteration to proceed, all tests must pass or the new code will be scrapped and the process restarts. In short, design for today and let tomorrow come.
</p>

<p>
    Third is implementation. In most of the conventional development methodologies everyone cranks out their own code which is later integrated. Surprisingly, XP uses a method called paired programming for all production code. As the name implies, paired programming means that the programmers share the same mouse/keyboard/screen while writing or integrating the production code. Although much research has been done in regards to the cost benefit of such a method, results are inconclusive as to whether or not this method is worthwhile. One positive result that pair programming produces is collective ownership of the whole project. This lends to the longevity of the project in the event of an employee’s termination. Pair programming is used more like a security blanket for the project. If one of the main developers leaves, there will be someone who knows how the code works and precious time will not be wasted trying to understand what was created by the ex-employee. Aside from paired programming, XP‘s implementation phase also includes testing. Programmers write more tests than actual code. Only after the program passes all functionality tests can the customer receive the product per release of complete iteration.
</p>

<p>
    In review, XP incorporates an open-ended design approach which allows customers to update requirements enabling quick product evolution and short iterative life cycles. This allows for quick integration, testing and state releases. Although XP is a great model for applications which are mid sized and smaller, XP has not been applied to larger projects and as such it would not be wise to do so until it stands the test of time. XP should be used for production of RIA (Rich Internet Applications) and any type of project which does not rely on many critical systems or the use of a language without a large compile time overhead. XP projects are more apt to succeed when the systems environment is more forgiving. For example, if one were to use XP for construction of a missile’s guidance system the results would be disastrous. If you used XP perhaps you would miss a test case and forget to test for changes in sea level. Then you would lose the missile and be forced to start over. On the other hand if the project is to create a system to render animations for a video game company, a quick moving development team which could respond to dynamic requirements would work well. Essentially, the type of project which is going to be completed dictates what methodology should be used. Fortunately this is where other models come into play.
</p>

<p>
    When it comes to other models used in software engineering, the waterfall method ensures that something is created and it will work most of the time. This work-flow is used mainly by larger companies who can handle the exponential costs involved with altering initial requirement specifications to accommodate new requests or unseen needs. XP on the other-hand has flexibility built in which minimizes the costs associated with design alterations. Using the waterfall method, one must try to foresee all issues which could possibly arise. Whereas, using XP you design what you can and let the evolution of the code and the clients request finalize the system. With a limited sequential life cycle which doesn’t allow for flexible or evolving designs the applications for the use of the waterfall method are limited. From this limitation came the incremental model.
</p>

<p>
    Iteration is what XP is all about! Well the incremental model is one of XP’s roots. With the incremental model all requirement analysis is done in one step and is not visited again. After which the system enters the iterative steps of design, implementation, and testing. The incremental model is similar to the XP model in that each complete iteration produces a release product which the customer can use to measure progress. However, using the incremental model entails that all requirements for the system have to be gathered upfront. The incremental model is not nearly as flexible as the XP model when it comes to changing requirements and should be used with projects which have a clear and concise project scope. Although a great concept, most projects don’t have well defined scopes and need to be tested a lot so that the customer can decide upon which they like the most. Since most customers don’t know what they want their product to look like we have our next model, the prototype model.
</p>

<p>
    The idea behind the prototype model is much like painting a portrait many times and then only taking the appreciated aspects and incorporating them into a final picture. Requirements are gathered, a prototype is designed and built, analysis of the prototype gathers which components should stay and which should be redesigned. After deciding on a competent prototype, requirements are finalized the systems is designed, implemented, tested, and finally released. Like the XP method the prototype model lets the customer see tangible evidence of progress and is able to refine their requirements while deciding upon how the system should work. When compared to XP, however, this method lacks the speed at which a system can be built because it is focused upon eliciting requirements more than implementing them.
</p>

<p>
     Ultimately the XP process is basically a streamlined version of all the waterfall, incremental, and prototype models. XP entails the mitigation of static requirements and the creation of an adaptive, evolving design method. This allows the stakeholders to alter requirements and view the effects with a minimal impact to time and cost factors. Overall the extreme programming model is an innovative methodology which can be employed to develop median sized applications in a cost and time efficient manner.
</p>

Works cited:

Martin Fowler. “Is design Dead”, in Proceedings of the International Conference on
eXtreme Programming and Agile Processes in Software Engineering, pages 3-17, 2000.
URL: http://martinfowler.com/articles/designDead.html

 
Kent Beck. “Embracing Change with Extreme Programming”. 
IEEE Computer, issue 32, no. 10, pages 70 — 77, 1999. 