# Projektseite "Snake Game"

## Spieler

```lua


```

## Spielfeld

Der meiste Code des Spielfeldes ist für die Darstellung des Julia-Menge. Er stammt aus diesem Repository [Link](https://github.com/tinmanjuggernaut/godot-fractal-art). Ich habe den Code nur leicht angepasst, um ihn passend einsetzten zu können.

![](snake.gif)

Jetzt wird der Hintergrund des Spielfeldes immer geändert, wenn der Spieler bewegt wird.


## Punkteanzeige

```lua
extends RichTextLabel

var Punkte = 0

func score(menge = 1):
	Punkte += menge
	set_text("Punkte: " + str(Punkte))
```

Die Punkteanzeige ist ein RichTextLabel und hat somit einen Text, der angezeigt wird. Sie hat nur eine Funktion mit der die Punktanzahl erhöht wird und der Text mit der neuen Zahl aktualisiert wird.

## Sammelbares

Die Objekte mit denen der Spieler kollidieren kann, bestehen aus einer Textur und einer Kollisionsbox. Die Hauptklasse fügt die Funktion Kollision hinzu, bei der das Objekt gelöscht wird.

```lua
extends KinematicBody2D

func Kollision():
	queue_free()
```

## Feind

```lua
extends "res://pickup.gd"

func Kollision():
	get_tree().quit()
```

Kollidiert man mit einem Feind, wird das Spiel beendet.