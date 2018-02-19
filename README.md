# Week5-6 Checkpoint

DGM6410 Game Design Tech Lab

This repository contains:


-  Inquiry
-  Research notes
-  Research Demo (PARTLY, online preview at <a href="https://appleseed0910.github.io/week5-6/week5-6demo" target="_blank">here</a>.
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

(there's another kind of hook, **_Hidden hooks_**, which could be called by **_(show:$keyName)_**) I think it could be used powerfully in some certain occasions such as reading secret message or invisiable ink, some tricks like that, but not as popular/common as former two main kinds of hooks. So I didn't write it here. [Link to the reference page](https://twine2.neocities.org/#markup_hidden-hook).

- Display macro

```
(display:"passageName")
```
This macro is quite staightforward for both understanding and learning. In my view, display macro is very suitable for some status or inventory passages. Some special game states which "stand" out from the formal game process.

### 2. Items or Variables, Inventory or Array

Although I've already picked these two topics in the last checkpoint, for further goal of building a demo contains **collection puzzle** and some more intermediate mechanics, I'm sorting some notes here for clarity. (Since my last checkpoint doesn't help so much.)

- Set variables
```
(set: $variableName to variableValue) // var a = num/boolean.
```
- Check operator
```
+, -, *, /, <=, >=, is, is not
```
- Conditional statement
```
(if: $variableName is "check opponent")[hook text](else:)
```
Here if we want to use something like "if variable is 5, set the variable to 7." It could be written in
```
(if: $a is 5)[(set: $a to $a+2)]
```
Becasue a macro should be using with a hook, so make sure putting the following macro inside a hook.
- Print macro
```
(pring: $variableName)
```
- History macro
```
(history:)
```
this macro shows all the passage names that the player has ever been.

In the book, the author used the array macro to render an inventory, it does make sense.
- Some related macros
```
Common structure:
(set: $bag to (array:))                      //create an empty array
(set: $bag to $bag + (array:"sleepyPotion")) //add an item to the array
(set: $bag to $bag - (array:"sleepyPotion")) //remove an item from the array
(if: $bag's length is 0)                     //check array length
(if: $bag contains "sleepyPotion")           //check belongings

For simplier structure:
(set: $haveSleepypotion to true)             //after or before somewhere that the player just picked up the item
(if: $haveSleepypotion is true)              //check belongings
```
- Count macro
Huge thank to the author (and to the creator of Twine of course!) As she mentioned in the book, there's the other useful macro inTwine called Count, whihc could help us with sorting the inventory when the item list gets really long or big.
```
(count: $bag, "sleepyPotion")         //return the amount of sleepyPotion in the bag
```

### 3. Character Stat
Before we start building up real combat in Twine, there's one more important thing need to do.

No matter it's on game design level or story design level, building up a detailed character stat is necessary. 

Here we're going to use Datamap macro.
```
(set: $character1 to (datamap:))                              //declare a stat datamap for the character1
(set: $character1 to it + (datamap:"Class", "Sleepyworm"))    //add property to the character datamap
// here we use the shortcut 'it' to represent $character1

(move: $character1's "Class" into $trashCan)                  //remove a certain property from the datamap
```
Besides, we still missed the most important one! Customized unique character name. To create a customized name, we use prompt and put macro.
```
(put: (prompt: "What's your name?", "") into $character1's "Name")
```
Changine variable's name is unwise to do but we could store the "Name" as a new property inside the datamap. When we need, we could simply use print macro to call it.
```
(set: $character1 to (datamap: "Name",""))                    //set a new character
(put: (prompt: "Name what?","") into $character1's "Name")    //ask name from the player
(print: $character1's "Name")                                 //print out the name when we need
```
Okay! With these LEGO pieces, we could bulid up a some what cool small demo.

## Research Demo
For this checkpoint, I created a small demo of a mystery with some techniques that I mentioned above.

Blueprint for this demo, the player would have the chance to customize their character's name and status.
<br>An inventory with some collectable items which would help them with solving simple puzzles.
<br>The final goal of this demo is to examine the house and try to escape.
<br>Also some combats would be added.

For this checkpoint, I finished the first little part.
Please check it out [here](https://appleseed0910.github.io/week5-6/week5-6demo)

## Reference
https://www.gamasutra.com/view/news/293930/7_works_of_interactive_fiction_that_every_developer_should_study.php
<br>https://twine2.neocities.org/
<br>http://glitch.camp/how_to_publish_a_website_using_github_pages/index.html
