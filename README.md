# Jenn's Challenge

## Screenshots taken from the game

### Level 001
![Jenn's Challenge](screenshots/jenns_challenge.png)

### Level 005
![Jenn's Challenge - Level 5](screenshots/jenn_level5.png)

### Level 008
![Jenn's Challenge - Level 8](screenshots/jenn_level8.png)

More levels can be added via the map editor, some levels have been faithfully recreated, some features still needs to be added to make the full experience a reality, for now this is half of the game in it's entirety which is more than enough to have fun. Enjoy!

### Jenn swimming
![Jenn's Challenge - Swimming Upwards](screenshots/jenn_swimming_upwards.png)

### Jenn walking
![Jenn's Challenge - Walking](screenshots/jenn_walking.png)

This build fixes authored waypoint movement for Spider and tile-linked custom monsters.

![Route caching works like this](screenshots/Flickans%20guide%20till%20route%20caching.png)

## Authored monster paths
- Continuous/loop authored paths automatically start from the monster's actual spawn/current position.
- Spiders use their authored waypoint controller when authored paths are enabled.
- Tile-linked custom monsters use the same controller when they have waypoint data and are in loop/rail/path mode.
- Custom monsters without authored paths do not enter the path controller, so they cannot freeze merely because they are custom.
- Spider A* remains available when authored paths are disabled.

![Route rebuilt after object or monster is in the custom monsters path](screenshots/När%20monsterets%20rutt%20byggs%20om.png)

## Path traversal performance
Authored waypoint monsters use a cached short-segment route. A route is calculated once and its directions are consumed one tile at a time. Long waypoint segments are broken into small route chunks, so traversal cost is independent of the full 992x992 map size during normal movement.

The following values are available through `CC_MONSTER_CONFIG` for tuning:
- `pathRouteChunkTiles` (default 32)
- `pathRouteMarginTiles` (default 10)
- `pathRouteMaxSteps` (default 128)

If another actor occupies the next cached step, the route is invalidated and rebuilt from the monster's current position.
