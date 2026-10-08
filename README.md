# MLS Elo Ratings Dataset

Historical and up-to-date Elo ratings for Major League Soccer (MLS), covering every regular-season and playoff match from the league's inaugural 1996 season to the present.
### Content

- `results.csv` — every included MLS match, with pre-match and post-match Elo ratings for both teams
- `teams.csv` — each team's current Elo rating and when it was last updated
- `home_advantage.csv` — the current home-field advantage parameter used in the model

`results.csv` columns:

- `date` — match date (`YYYY-MM-DD`)
- `home_team` / `away_team` — team names (current naming used throughout)
- `home_elo_current` / `away_elo_current` — each team's Elo rating going into the match
- `home_score` / `away_score` — full-time score
- `result` — match outcome from the home team's perspective (`H`/`D`/`A`)
- `neutral` — whether the match was played at a neutral venue
- `home_elo_update` / `away_elo_update` — each team's Elo rating after the match

**Note on team names**: Team names are unified to each club's *current* name throughout the dataset, including for historical matches. For example, matches played by the "MetroStars" in the 1990s are listed under the team's current name, New York Red Bulls. This is done so a team's full history and stats can be tracked under a single, consistent name.

### Methodology of the Dataset

The model follows the standard Elo methodology used across most football Elo implementations:

- **Scope**: Only MLS league matches are included — from the first MLS match in 1996 through the most recent match played. Cup competitions (e.g., U.S. Open Cup, Leagues Cup) and continental competitions (e.g., CONCACAF Champions Cup) are **not** included.
- **Initial rating**: Every team starts at an Elo of **1,500**.
- **Match weighting**: All matches are weighted equally — there is no additional weight for playoffs, rivalries, or other match types.
- **Margin of victory**: The Elo update accounts for goal difference — a team that wins by a larger margin gains more Elo than a team that wins narrowly.
- **Everything else** (400-point ratings scale, home-field advantage adjustment, etc.) follows conventional Elo methodology.
- **Two-legged playoff rounds (2003–2018)**: Some Conference Semifinals/Finals during this period were decided over two legs (aggregate score). For these ties, the two legs are combined into a single aggregate result and treated as one neutral-site match for Elo purposes, rather than as two separate updates.
- **Extra time**: Some historical playoff matches may include extra-time scores. Going forward, updates will only use the regulation-time (90-minute) score.
Data compiled from publicly available match results.



#Methodology of the Analyses

The methodology was primarily ran by Jacob Kepes, with some of the base code taken from online sources. Analyses were written in R Studio and Quarto.
I created the columns of goals scored, goals against, goal differential, and the points at each month in the season. Because matchweeks and games don't always occur on the same day, I wanted to aggregate by month.
The analyses were only based after 2020 because I wanted to capture a more recent period of time that captures how large the league has grown and the nunber of teams that have been added.
I then ran a random forest model with 500 trees.