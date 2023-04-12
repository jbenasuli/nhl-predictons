# Feature Design Notes

## target

Objective: predict game winner
<!-- alternate target = total goals scored (actual goals) -->

Binary classification target:

- features data structured from perspective of 'home team'
  - stats collected are for and against home team
- home team won (in binary home team won = 1)
- field_id: W or wins

## Features

High multicolinearity due to the nature of sports statistics

- first attempts were overfit to 100%
- group features into sets of components for svm/xgboost/nn modeling
- evaluate if componenet sets should be defined for both teams or just the home team


### Feature component sets

5v5 Offense (adjusted)
- fenwick shots for
- xG for
- shooting %
- HDSC for %


5v5 Defense (adjusted)
- fenwick shots against
- xG against
- HDSC against %

PP (5v4 Offense)
- fenwick shots for
- xG for
- shooting %
- HDSC for %

PK (4v5 Defense)

- fenwick shots against
- xG against
- HDSC against %

Goaltending
- Sv%

Macro
- PP time
  - per 60 mins or rel to pk time


### Metadata features


### moneypuck box score

asdf

### NatStat box score

asdf

### Feature Notes/commentary

![Fenwick Based Variable Hierarchy](Users/jamesbenasuli/Desktop/nhl-predictons/references/fenwick-model.png)

Notes:

- Rates: TOI is presented as TOI/GP. For and against statistics are presented as the counts per 60 minutes of play
  - Rate version of any specific metric: (metric / toi) * 60
- Rolling windows available out of the box (only counts regular season games):
  - Full Season: season to date games played (GP)
  - Last 10 Games: each team last 10 GP
  - Last 25 Games: each team last 25 GP

Basis/descriptive stats to aid in feature engineering

- Home team name (align with nhl team name encoding)
- GP: games_played (dont think this will be predictive, but we may need it for derizing some new stats)
- TOI: time_on_ice (see GP above)
- Standandings points
  - would need to express as rate of GP/Possible Points aka points percentage
  - points per rolling window (would this only work for lopsided opponents with a big stats delta? or would it just be plain old noisy?)

Fenwick shot variables

- fenwick: any unblocked shot attempt (goals, shots on net and misses) outside of the shootout
- FF - Count of Fenwick for that team.
- FA - Count of Fenwick against that team.
- FF/60 - Rate of Fenwick for that team per 60 minutes of play. FF*60/TOI
- FA/60 - Rate of Fenwick against that team per 60 minutes of play. FA*60/TOI
- FF% - Percentage of total Fenwick in games that team played that are for that team. FF*100/(FF+FA)
  - xFF%: % of Fenwick against can be derived by taking 1-FF%
  
Goal Vars

Standard metrics

- Goals: Any goal, outside of the shootout.
- GF: Count of Goals for that team.
- GA: Count of Goals against that team.
- GF/60: Rate of Goals for that team per 60 minutes of play. GF*60/TOI
- GA/60: Rate of Goals against that team per 60 minutes of play. GA*60/TOI
- GF%: Percentage of total Goals in games that team played that are for that team. GF*100/(GF+GA)

Potential derived stats

- d
- d
- d
- 

#### min features needed for head to head?

Basic input list

- shots for
- shots against
- xG for
- xG against
- shooting %
- sv%

### Basic transformations

Adjust the following stats on a 'per60' basis i.e. divide individual skater stats by the # of games played

- shots for per60
- shots against
- xG for
- xG against

### dependents

## data to scrape

## data to download
