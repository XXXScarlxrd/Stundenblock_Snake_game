# Projektseite "Snake Game"

## Spieler

```lua
extends KinematicBody2D

var Grundgeschwindigkeit = 200

var Bewegung = Vector2()

func _physics_process(_delta):
	var MausPosition = get_global_mouse_position()
	look_at(MausPosition) # Rotiert den Spieler
	Bewegung = Vector2(Grundgeschwindigkeit, 0).rotated(rotation)
	move_and_slide(Bewegung)
	var Kollision = get_slide_collision(0)
	if(Kollision):
		Kollision.collider.Kollision()
```

Hier ist die Bewegung des Spielers programmiert. Er hat eine Grundgeschwindigkeit von 200 Einheiten, ist also immer in Bewegung. Außerdem soll er sich immer zu Maus hin ausrichten, damit er sich dorthin bewegen kann. Am Ende findet noch eine Kollisionsabfrage statt. Wenn das if(Kollision) erfüllt ist, rufen wir die Kollisions-Funktion für die sammelbaren Objekte auf.

## Spielfeld

Der meiste Code des Spielfeldes ist für die Darstellung des Julia-Menge. Er stammt aus diesem Repository [Link](https://github.com/tinmanjuggernaut/godot-fractal-art). Ich habe den Code nur leicht angepasst, um ihn passend einsetzten zu können.

![](snake.gif)

Jetzt wird der Hintergrund des Spielfeldes immer geändert, wenn der Spieler bewegt wird.

```lua

```

## Punkteanzeige

```lua
extends RichTextLabel

var Punkte = 0

func score(menge = 1):
	Punkte += menge
	set_text("Punkte: " + str(Punkte))
```

Die Punkteanzeige ist ein RichTextLabel und hat somit einen Text, der angezeigt wird. Sie hat nur eine Funktion mit der die Punktanzahl erhöht wird und der Text mit der neuen Zahl aktualisiert wird.

## "Sammelbares"

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

Kollidiert man mit einem Feind, wird das Spiel beendet. Er wird mit einer roten Box dargestellt.

## Punkt

Die Punkte sind das wichtigste sammelbare Objekt. Sie sorgen dafür, dass die Spielerkette vergrößert wird. Die Logik dafür befindet sich allerdings im Spieler. Hier sorgen wir nur dafür, dass die Punktezahl erhöht wird und das Objekt gelöscht wird.

```lua
extends "res://pickup.gd"

func Kollision():
	get_node(@"/root/G/RichTextLabel").score(1)
	get_node("..").queue_free()
```

## "Powerup"

Das Powerup ist nicht wirklich hilfreich, aber es sieht cool es, wenn es den Hintergrund verändert. Es hat eine blaue Box als Textur.

```lua

```