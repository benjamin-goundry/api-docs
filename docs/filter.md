# # MR(API) Documentation - Filter


## Basic `Filter` usage

When you make a request to our API you typically get a response like this.


```plaintext
GET api/maps
```
```json
[
  {
    "name": "Yggdrasill Path",
    "full_name": "Yggdrasill Path - Yggsgard",
    "location": "Yggsgard",
    "id": 1032,
    "description": "Beneath the sky-shutting canopy of the World Tree, Yggdrasill, lies the golden glory of Asgard, realm of the gods, now overgrown with the roots and flora. However, the throne-seizing scheme of Loki, god of mischief, threatens the ever-lasting prosperity of this kingdom and all of the Ten Realms.",
    "images": [
      "https://mrapi.org/assets/maps/yggdrasill-path-1.png",
      "https://mrapi.org/assets/maps/yggdrasill-path-2.png",
      "https://mrapi.org/assets/maps/yggdrasill-path-3.png"
    ],
    "is_competitve": false,
    "gamemode": "convoy"
  },
  {
    "name": "Shin-Shibuya",
    "full_name": "Shin-Shibuya - Tokyo 2099",
    "location": "Tokyo 2099",
    "id": 1034,
    "description": "Another world has emerged from the Timestream Entanglement! It's time to have some ramen and sushi after that nature walk! I'm thrilled that these foods still retain their classic flavors even in Tokyo of 2099! But it is a pity that there aren't any Kaiju or giant robots fighting in the city anymore...",
    "images": [
      "https://mrapi.org/assets/maps/shin-shibuya-mission.png",
      "https://mrapi.org/assets/maps/shin-shibuya-1.png",
      "https://mrapi.org/assets/maps/shin-shibuya-2.png"
    ],
    "is_competitve": false,
    "gamemode": "convergence"
  },
  {
    "name": "Hall of Djalia",
    "full_name": "Hall of Djalia - Intergalactic Empire of Wakanda",
    "location": "Intergalactic Empire of Wakanda",
    "id": 1101,
    "description": null,
    "images": [
      "https://mrapi.org/assets/maps/hall-of-djalia-mission.png",
      "https://mrapi.org/assets/maps/hall-of-djalia-1.png",
      "https://mrapi.org/assets/maps/hall-of-djalia-2.png"
    ],
    "is_competitve": false,
    "gamemode": "convergence"
  },
```


This is a lot of information to process. What if we could only get a fraction of this?

This is where `filter` comes to save us. Lets only get the `name` and `gamemode`.
We pass `name` and `gamemode` separated by a `,`


```plaintext
GET /api/maps?filter=name,gamemode
```
```json
[
  {
    "name": "Yggdrasill Path",
    "gamemode": "convoy"
  },
  {
    "name": "Shin-Shibuya",
    "gamemode": "convergence"
  },
  {
    "name": "Hall of Djalia",
    "gamemode": "convergence"
  },
]
```

Look how much less data we have with just a simple use of the `filter` parameter.

---

## Returned a JSON array

If you request a resource and get returned a JSON array, `filter` has to be tweaked a small bit.

```plaintext
GET /api/heroes-stats/pc
```
```json
{
  "quickPlay": [
    {
      "name": "Hulk",
      "role": "Vanguard",
      "pickRate": "9.78%",
      "winRate": "51.45%"
    },
    {
      "name": "Doctor Strange",
      "role": "Vanguard",
      "pickRate": "12.52%",
      "winRate": "49.05%"
    },
    {
      "name": "Captain America",
      "role": "Vanguard",
      "pickRate": "10.33%",
      "winRate": "52.24%"
    }
  ]
}
```

The objects we want to access are embedded within the `quickPlay` array.

In this case, we can use the `.` to show we only wanted the `name` and `pickRate` from inside of the `quickPlay` JSON array. As such we pass in `quickPlay.name` and `quickPlay.pickRate`.


```plaintext
GET /api/heroes-stats/pc?filter=quickPlay.name,quickPlay.pickRate
```
```json
{
    "quickPlay": [
    {
      "name": "Hulk",
      "pickRate": "9.78%",
    },
    {
      "name": "Doctor Strange",
      "pickRate": "12.52%"
    },
    {
      "name": "Captain America",
      "pickRate": "10.33%"
    }
  ]
}
```


