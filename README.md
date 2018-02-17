# Week5-6 Checkpoint

DGM6410 Game Design Tech Lab

This repository contains:


-  Inquiry
-  Research notes
-  Research Demo
-  Futher Research expectations

In last two weeks, I kepet reading and learn from the book *Writing Interactive Fiction With Twine*. 

But based on last comment that I received, I'd take care of presenting the research process more clearly.

(I've also learned a bit about using GithubPages and Github formatting marks this week. Efficient tool and knowledge!)

## Research

### 1. Vitrual map and Puzzel Design 
I bind these two topics together not only because in the book the two chapters are connected, but also after I read them thoroughly, I think these two elements are highly relevant to each other. This concept is more on content level rather than detail technique level, I think. But still very important.

In multiple classic or popular CYOA games, setting decription usually relates to puzzles and provides hints for the puzzles.

Such as, in **Zork**, the setting is just the puzzle itself. Everything is presented in the game is useful for a certain goal. The puzzle for the players is to figure out how to correctly interact with these objects.

Whereas, Twine allows us to create choice branches instead. In some games that I've played such as [
Turing Trial](https://rtgrl.itch.io/turing-trial) and [Egress](https://thealeks.itch.io/egress), the map of the game is described with plain text, and player moves between locations through choices. It also reminds me some commercial games like **Lifeline series**. Although some of them don't have a *map* view, the players still have a clear memory or cognition of their locations.

In the book *chapter 3 Creating a Vivid setting*, the author picked the maze as an ultimate chanllenge, which means the setting itself would be a puzzle for the players. This smoothly switched the topic to the next *chapter 4 Designing Puzzles*. There is more deep and practical tips and knowledge need to pay attention here.

Not like some games with graphics, the puzzle that we could make in Twine more likely to be text. (We could insert imgs when we need, but hardly to make some interactions but a just plain picture, which declines fun of graphic puzzle I think.) In the book, the author sorted the puzzles in different genres such as **useful-item puzzle**, **Sequencing puzzle**, **Interacting-objects puzzle** etc.

These genre names could help us with brainstorming, but what more important I think is to make the puzzle **matters** with the story. Make the puzzle engage with the story or push story forward, meld with the story.

Some technique reviews for this part:

- Macro and Hook

As we all know in Twine, links could be eaisly create by square brackets such as
```
[[Link Text|Passage Name]] //not prefer
```
or
```
[[Link Text -> Passge Name]] [[Passage Name <- Link Text]] //recommend 
```
There is also the other useful link macro in Twine. It allow us to create a link inside the same passage, which means
```
(link-replace:"Link Text")[New text]  //Replace the link text with the new text
(link-reveal:"Link Text")[New text]   //Bind the link text with the new text
```
by using these macro, once the link is clicked, the new text would appear right behind the link. This is called **_anonymous hooks_**.

The other type of hook is **_named hooks_** which usually looks like
```
[Link text]<tagName|
(click: ?tagName)[New Text]
```
Here we actually use another click macro. "<tagName|" is the hook name. [Newtext] is the hook, (clcik: ?tagName) is the macro.

By using **_named hooks_**, we could put Link and the new text anywhere we want separately. Such as a letter, leaflet, or a note. The item itself need to appear in a setting decription, but the detailed content could go below all the body text.

- Display macro

```
(display:"passageName")
```
This marco is quite staightforward for both understanding and learning. In my view, display marco is very suitable for some status or inventory passages. Some special game states which "stand" out from the formal game process.

## Reference
https://www.gamasutra.com/view/news/293930/7_works_of_interactive_fiction_that_every_developer_should_study.php

https://twine2.neocities.org/
