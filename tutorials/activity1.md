```ghost
namespace SpriteKind {
    export const invis = SpriteKind.create()
    export const Van = SpriteKind.create()
}
scene.onOverlapTile(SpriteKind.Van, assets.tile`ash`, function (sprite, location) {
    if (Math.percentChance(30)) {
        tiles.setTileAt(location, assets.tile`heavy_ash`)
        number_high_concentration += 1
    } else {
        tiles.setTileAt(location, assets.tile`light_ash`)
        number_low_concentration += 1
    }
    info.changeScoreBy(-1)
})
scene.onOverlapTile(SpriteKind.Van, assets.tile`data_receiver`, function (sprite, location) {
    if (info.score() != 0) {
        game.showLongText("We need more data to make a decision", DialogLayout.Bottom)
        last_score_message = info.score()
    } else {
        // we need to add logic to calculate the concentration.
        high_concetration_fraction = Math.round(number_high_concentration / (number_high_concentration + number_low_concentration) * 100)
        // we need to calculate  what the number of high concentration cells actualy is, put in a message and then put in to the game end conditional statement
        game.showLongText("Your data shows ash levels are " + convertToText(high_concetration_fraction) + ("%. For levels above " + convertToText(ash_decision_threshold) + "% we recommend closing the airport."), DialogLayout.Center)
        if (game.ask("Close the airport?", "Yes (A=OK) No (B=Cancel)")) {
            if (high_concetration_fraction > ash_decision_threshold) {
                game.showLongText("Airport closed, you have kept everyone safe, well done!", DialogLayout.Bottom)
                game.reset()
            } else {
                game.showLongText("Airport closed, but levels were not high. People are safe, but this has cost airlines a lot of money.", DialogLayout.Bottom)
                game.reset()
            }
        } else {
            if (high_concetration_fraction > ash_decision_threshold) {
                game.showLongText("Flights continued, but high ash levels damaged planes, this cost the airlines money and put people in danger.", DialogLayout.Bottom)
                game.reset()
            } else {
                game.showLongText("Flights continued safely, well done!", DialogLayout.Bottom)
                game.reset()
            }
        }
    }
})
let high_concetration_fraction = 0
let last_score_message = 0
let number_low_concentration = 0
let number_high_concentration = 0
let ash_decision_threshold = 0
tiles.setCurrentTilemap(tilemap`level1`)
let van = sprites.create(img`
    . . . 2 . . . . . . . . . . . . 
    . . . 2 . . . . . . . . . . . . 
    . . . 2 . . . . . . . . . . . . 
    . . . 2 . . . . . . . . . . . . 
    . f 1 d 1 f . . . . . . . . . . 
    . f 1 d 1 f . . . . . . . . . . 
    . f 1 1 1 f . f f f . 8 8 8 . . 
    . f f f f f . f 1 f . 8 8 8 8 . 
    . . f . f . . f d f . 8 8 1 8 8 
    . f f f f f . f f f . 8 8 1 1 8 
    8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 
    4 8 8 8 8 8 8 8 8 8 8 8 8 8 8 5 
    4 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 
    . . f f f . . . . . . f f f . . 
    . . f b f . . . . . . f b f . . 
    . . f f f . . . . . . f f f . . 
    `, SpriteKind.Van)
tiles.placeOnTile(van, tiles.getTileLocation(2, 3))
info.setScore(tiles.getTilesByType(assets.tile`ash`).length)
scene.cameraFollowSprite(van)
controller.moveSprite(van)
effects.blizzard.startScreenEffect(500000000000000000)
ash_decision_threshold = 25
```

## Introduction @unplugged

![Psyched Monkey](/static/skillmap/interface/monkey.png "Psyched Monkey is Ready!" )

**We have an emergency! A volcano has erupted, and we need to gather air quality data and send it back to the Met Office for processing.**

Complete this tutorial to explore the game which introduces:
Our quest has three main aspects to it: 

- Gathering the data, 
- Sending the data to the Met Office, 
- Decide whether to shut the airport, based on the data collected.

## step 1 

**⭐Welcome⭐**

You've just discovered the most important part of following a tutorial — reading instructions!

If you can't see all of the instructions, click **[v More...]** below to expand the box.

---

When you're ready to move to the next step, click **[ >  Next]** to continue.  


## step 2

This box is where you'll find information for each step. 

If you don't find all of the info you need, 
click the lightbulb to the right for an extra hint.

#### ~ tutorialhint 
```
**You found the hints!**
```


## Using the workspace

