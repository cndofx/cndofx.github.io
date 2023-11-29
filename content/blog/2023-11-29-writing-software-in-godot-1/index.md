+++
title = "Writing Software in Godot (Part 1 / Planning and UI Layout)"
date = 2023-11-29
[taxonomies]
  series = ["Writing Software in Godot"]
+++

## Introduction

- [source code](https://github.com/cndofx/defenders-quest-mod-editor)

I want to make a mod editor for [Defender's Quest](https://store.steampowered.com/app/218410/Defenders_Quest_Valley_of_the_Forgotten_DX_edition/).
The game includes a mod editor already, but the UI is a mess, it's buggy,
and it doesn't run natively on linux. More importantly, I want experience
using godot to write non-game software and with godot in general. 
I also just want a project I can write about. 
I'll be using [godot v4.1](https://docs.godotengine.org/en/4.1/).

## The Plan

The mod editor needs to include an item editor and a map editor, along with
the ability to read and write the XML documents that the game uses for it's data.

In this part, I want to get the basic UI laid out for the main page and the item editor.
The map editor will be much more complex so I'll worry about that later.

In part 2, I want to write a basic XML reader and writer in GDScript. Godot
has an [XMLParser](https://docs.godotengine.org/en/stable/classes/class_xmlparser.html)
class built in, but it's not very ergonomic and doesn't do quite what I want.
It also doesnt have support for writing XML files, so I'll just try to come
up with something that can do both. XML is a complex format, but the files
I need to work with seem pretty basic, so a simple implementation shouldn't
be too hard.

In part 3, I'll get the UI functionality all hooked up and hopefully have the 
item editor at least partially working. This part will really test my knowledge
of godot design patterns, as there's a lot of moving parts and a lot of state
to manage. I plan on using [RefCounted](https://docs.godotengine.org/en/stable/classes/class_refcounted.html)
objects to store my data in memory and just having methods to convert those objects
to and from XML, but I'll see about that when I get there.

After all that, I want to make a map editor, but it's not part of the plan yet
as I don't know how complex it'll be. I want to look into how
[Pixelorama](https://github.com/Orama-Interactive/Pixelorama) (a pixel sprite editor made in godot)
works, and maybe see how some other godot developers have implemented a level editor in their games.

## Main UI

UI layout isn't particularly interesting so I don't have too much to write about,
but I do have some progress to show and a few important points to note.

- For all UI made in godot, but especially in software like this, it's important
to make use of godot's containers and anchors to lay out the controls rather 
than manually position controls so that everything plays nicely when the window is resized.
MarginContainer, VBoxContainer, HBoxContainer, and GridContainer are all very commonly used.

- Godot has a `application/run/low_processor_mode` property under project settings that 
prevents the screen from being redrawn if nothing visual has changed.

This is what the original mod editor looks like:

![original mod editor](original_mod_editor.png)

This is what mine looks like:

![my mod editor](my_mod_editor.png)

And this is what the scene tree currently looks like:

![godot scene tree](scene_tree.png)

Currently, only the ItemList and BattleList nodes (highlighted)
are separated into their own scenes. They are going to have very
similar functionality but don't share anything right now, so 
this will be changed later. 

I'm keeping most things all in the same scene for now as I don't know
how I'll be hooking everything up yet. Once I get to the code, I'll
revisit my structure.

## Item Editor UI

todo

## Useful Resources

- [Godot UI Basics](https://www.youtube.com/watch?v=1_OFJLyqlXI) by Godotneers
- [Every Control Node Used and Explained](https://www.youtube.com/watch?v=sb6xe87RUE4) by SDG Games