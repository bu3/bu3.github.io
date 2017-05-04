---
layout: default
title:  "Team leaders are bottle necks"
categories: 
    - experience
---
# Team leaders are bottle necks

In the last project I worked on I had to face a very strong company culture.
This company was moving its first steps into the agile methodology so they asked my company to help them.
 
This company has been focused on what their IT department could or could not achieve instead of focusing on 
what their customers need, so they developed a kind of Engineering Team Leader cult.

In this context the TL validates all the decisions during each phase of the project.<br/>
He is in charge of:
 * approving business decisions with Product Managers
 * making decisions in behalf of the developers, wherever they are related to technologies, languages and design
 * reviewing code compliance
 * defining and promoting conventions

This culture brought the developers to look for TL approval for any decisions they might have to take and 
they didn't feel it as an imposition, but actually as a best practice to follow for achieving the best result.

As I could see that set up brings to a ***bottle neck*** that slows down the product development and release, because everything has to pass through the TL approval.

 
### Who is this guy? 

I tried to put my self in TL's shoes and I guess I understood why he wants:
 * to be aware of everything
 * to design everything upfront
 * to use only technologies certified by someone else in the company
 * to not risk anything

**It's the fear of failing.**

He used to ask questions like:
* *What if tomorrow we find out that this framework does not suit anymore our project?*
* *What if tomorrow we find out that this design pattern does not apply anymore to our project?*
* *What if tomorrow we find out that the model does not work anymore?*

Is it fear? I guess so.


The way I tried to help that team and that TL was pushing back their culture, promoting individuals ideas and trying to keep them focused 
on the stories provided by Product Managers instead of designing big solutions upfront.

That's what we strongly believe in my company:
 * do what works
 * fail fast
 * get feedback 
 * make it better.

We constantly iterate through this mantra.

So I encouraged them:
 * to make their own decisions
 * to improve and increase the use of TDD
 * to make baby steps instead of huge design upfront
 * to write code fast, release, validate and than refactor it

### Why TDD? 

Using TDD makes the team free to experimenting new possibilities, technologies, patterns and refactoring with no fear of their code.

### What does it mean making baby steps? 

Let's consider a scenario where your application is supposed to integrate with another system that accepts multiple kind of requests and returns different responses.
Probably at the beginning you don't have any clue on how to manage that.
So instead of trying to manage all the possible scenarios in one story, I usually prefer to spread them in multiple stories.
Using that approach, the first story should be hard but should give a better understanding of the complexity.
The second one should clarify even more and probably you might have a better understanding on how to move forward and hopefully refactoring the previous version of your code.<br/>
And so on till all the scenarios are covered. 
 
### Why small stories?

Having small stories helps the team in getting feedback from the user, because for example the Product managers might show the new features to the customers and
change the priority of next feature to be implemented.
<br/>Also releasing often it's very rewarding for developers and it helps a lot to keep the team mood up.
 
### How did it go? 

The TL was very interested in this approach, even though he was expecting us to have a silver bullet for smoothing their challenges out.
<br/>He spent some time trying to get our secret recipe, but after a while he found very uncomfortable to avoid designing everything upfront,
having meetings for any further possible step, analysing any possible side effect of a decision.
<br/>Many times during the weekly planning meeting, he showed a lot of frustration while the team was trying to stay focused on small stories and he kept asking always the same questions.

So after a while he started to find side ways for avoiding this approach and he fell in his own way of doing things, where he thought he might control the beast.
<br/>So he ended up on having meetings at developers desk, endless discussion about side effects, working on multiple scenarios at the same time.

On his defence, I have to say that I'm guilty for pushing a lot on them for using this approach, mainly because of the very short engagement period, and this has created a wall between me and the TL. 
Sadly after a while even his sidekicks fell entitled to push back my counseling because their TL was doing it already.

On my defence I have to say that this approach worked very well with the junior developers on the team, because still not totally corrupted by the TL cult, they gave this approach a chance.

I'm happy because before leaving the project we tackled some important challenges and we got some important results, but the team was completely divided.

The objective successful result is that I made their use of TDD much better and hopefully they'll bring the lesson learnt in other projects as well.


I felt it like a personal failure and if I would ever have to face the same culture I will use a different approach. ***Maybe***.







