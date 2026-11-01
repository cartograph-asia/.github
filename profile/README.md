# Cartograph

**A photo survey of Asia, one plot at a time.**

Cartograph is a community game with a simple, very large goal: a photograph for every plot of land in South, Southeast and East Asia – from Pakistan to Japan, from Mongolia to Indonesia.

The map is divided into hexagonal plots. Every plot starts blank. Surveyors go out, take a photo, and claim the plot. Over time, the blank map fills with pictures of what Asia actually looks like from the ground – not from satellites, not from postcards, but from the people walking it.

> Status: pre-alpha. Concept settled, prototype in progress. Nothing to play yet.

---

## How it works

**Plots.** The map uses [H3](https://h3geo.org/) hexagons at resolution 8 – roughly 0.74 km² per plot, about 1 km across. That is close to a classic kilometre square, small enough that a village has several plots and large enough that each one holds a real piece of landscape. Across the whole region there are tens of millions of them.

**Surveying.** A Surveyor uploads a photo taken inside a plot. The first photo claims the plot: it turns from blank to surveyed and carries the Surveyor's name as its first surveyor, permanently – like an explorer's name on an old map. Further photos add to the plot but do not replace the claim.

**Ranks.** Every member is a Surveyor. Ranks are earned globally and are the same everywhere:

Apprentice → Surveyor → Senior Surveyor → Master Surveyor → Cartographer

**Leaderboards** are local. Asia is too large for one list, so standings are kept per country and per province. Anyone can be the top Surveyor of their own corner. Country titles ("Surveyor of Thailand") are awarded on reaching a threshold in that country, and collecting them across several countries is a goal of its own.

**Territories.** Provinces, islands and cities are closable areas with a coverage percentage. Completing one is an achievement.

**Seasons.** Monsoon and dry season change the landscape. A plot can be surveyed in both, which is a second trophy – and, in the long run, an archive of how Asia changes through the year.

**Later: "Where was this?"** Once a region holds enough photos, a second game mode opens: guess where a photo was taken, scored by distance. Good guessers earn points; photographers earn points when their photos are recognised (landmarks) and when they are not (hidden places). Same account, same Surveyor, two ways to play.

## What it is not

Not an OpenStreetMap editor, not a stock photo site, not a travel guide. The point is coverage: going to the plot that nobody has photographed yet.

## Inspiration

The idea of photographing every grid square of a country comes from [Geograph](https://www.geograph.org.uk/), which has been doing this for Britain and Ireland since 2005 and has collected millions of images. Cartograph is an independent project with its own name, grid, rules and code – no affiliation.

## Stack (planned)

| Layer | Choice | Why |
|---|---|---|
| Grid | H3, resolution 8 | Uniform cells worldwide, hierarchical, libraries in every language |
| Base map | OpenStreetMap → PMTiles via Planetiler, self-hosted | One archive file, served by HTTP range requests, no tile server to run |
| Map rendering | MapLibre GL JS | Open, fast, vector |
| Plot layer | Client-side via h3-js at high zoom; aggregated MVT from PostGIS at low zoom | The grid is maths, not tiles; coverage changes constantly |
| Database | PostgreSQL + PostGIS + H3 extension | Spatial queries and hex hierarchy in one place |
| Photo storage | S3-compatible object storage (MinIO for the prototype, Hetzner Object Storage in production), served under img.cartograph.asia | Swappable behind one URL |
| Hosting | Hetzner | |

## Open decisions

- **Photo licence.** Leaning towards a Creative Commons licence so the archive is useful beyond the game. Which one (BY, BY-SA) is not settled.
- **Scoring details.** What a first survey is worth, how remoteness is weighted, what counts as a valid photo (and what does not – drive-by shots, screenshots, duplicates).
- **Country boundaries.** Leaderboards per country mean choosing boundaries. Default is to follow OpenStreetMap as-is and say so; neutral regions (provinces, islands) are the alternative.
- **Starting area.** Thailand first, then Southeast Asia, then the rest.

## Roadmap

1. Thailand prototype: base map, plot overlay, upload a photo into a plot.
2. Accounts, ranks, provincial leaderboards.
3. Southeast Asia base map; public beta.
4. Full region. "Where was this?" mode.

## Links

- Website: [cartograph.asia](https://cartograph.asia)
- X: [@cartographasia](https://x.com/cartographasia)
- Instagram: [@cartograph.asia](https://instagram.com/cartograph.asia)
