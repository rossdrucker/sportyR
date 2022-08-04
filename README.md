
<!-- README.md is generated from README.Rmd. Please edit that file -->

# sportyR <img src="https://raw.githubusercontent.com/rossdrucker/sportyR/main/logos/sportyr-logo-hex.png" align="right" width="120"/>

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/sportyR)](https://CRAN.R-project.org/package=sportyR)
[![R-CMD-check](https://github.com/rossdrucker/sportyR/workflows/R-CMD-check/badge.svg)](https://github.com/rossdrucker/sportyR/actions)
[![](https://img.shields.io/badge/devel%20version-2.0.0-blue.svg)](https://github.com/rossdrucker/sportyR)
[![Test
Coverage](https://github.com/rossdrucker/sportyR/workflows/test-coverage/badge.svg)](https://github.com/rossdrucker/sportyR/actions)
[![codecov](https://codecov.io/gh/rossdrucker/sportyR/branch/master/graph/badge.svg)](https://codecov.io/gh/rossdrucker/sportyR)
[![License:
MIT](https://img.shields.io/badge/License-MIT-orange.svg)](https://opensource.org/licenses/MIT)
[![](http://cranlogs.r-pkg.org/badges/grand-total/sportyR?color=blue)](https://cran.r-project.org/package=sportyR)
<!-- badges: end -->

As the field of sports analytics evolve, there’s a growing need for
methods to both track and visualize players throughout the game. This
package aims to make this easy regardless of sport needed to be plotted.

## Installation

The most recent release of `sportyR` is available on
[CRAN](https://cran.r-project.org/web/packages/sportyR/index.html), and
it can be installed directly via:

``` r
# Install released version from CRAN
install.packages("sportyR")
```

The development version of `sportyR` can be installed from
[GitHub](https://github.com/rossdrucker/sportyR) with:

``` r
# Install development version from GitHub
devtools::install_github("rossdrucker/sportyR")
```

Once the library is installed, be sure to load it into the working
environment.

``` r
# Required to use package
library(sportyR)

# Not required directly for utilization of sportyR, but useful to add more data
# to plots and create animations
library(ggplot2)
library(gganimate)
```

## Plotting Functions

All plotting functions in this library are named as `geom_{sport}()`,
and take the following arguments:

-   `league`: the league code for the sport. In all functions, this will
    ***NOT*** have a default value. The supplied league is
    **case-insensitive**. Future iterations of this package may allow
    the full league name to be supplied if desired
    (e.g. `league = 'National Basketball Associaton'` instead of
    `league = 'NBA'`), but this feature is not currently available.

-   `display_range`: This automatically “zooms” in on the area of the
    plot you’re interested in. Valid ranges here vary by sport, but can
    be found by calling `?geom_{sport}` and reading about the display
    ranges

-   `x_trans` and `y_trans`: By default, the origin of the coordinate
    system *always* lies at the center of the plot. For example,
    `(0, 0)` on a basketball court lies along the division line and on
    the line that connects the center of each basket. If you want to
    shift the origin (and therefore the entire plot), use `x_trans` and
    `y_trans` to do so

-   `{surface_type}_updates`: A list of updates to the parameters that
    define the surface. I’ll demo how to use this to change a hockey
    rink in a different vignette, but I’ll call this out here

-   `color_updates`: A list that contains updates to the features’
    colors on the plot. These are named by what the feature is, using
    `snake_case` to specify the names. To get the list of color names
    you can change, try running `cani_color_league_features()` with your
    desired league

-   `rotation`: An angle (in degrees) that you’d like to rotate the plot
    by, where +is counterclockwise

-   `xlims` and `ylims`: Any limits you’d like to put on the plot in the
    x and y direction. These will overwrite anything set by the
    `display_range` parameter

-   `{surface}_units`: If your data is in units that are different than
    how the rule book of the league specifies the units (e.g. you’ve got
    NHL data in inches, but the rule book describes the rink in feet),
    change this parameter to match the units you’ve got your data in.
    You’re welcome to change the units of the data as well, but this is
    provided for convenience

## Plot Units

Each plot function has a standardized unit of measure in which the plot
is created, and is standardized by the primary units specified in their
respective rule books. They are as follows (and any explanation is in
parentheses):

|   Sport    |              League              | Primary Plotting Unit |
|:----------:|:--------------------------------:|:---------------------:|
|  Baseball  |          Little League           |         `ft`          |
|  Baseball  |               MiLB               |         `ft`          |
|  Baseball  |               MLB                |         `ft`          |
|  Baseball  |               NCAA               |         `ft`          |
|  Baseball  |        NFHS (High School)        |         `ft`          |
|  Baseball  |               Pony               |         `ft`          |
| Basketball |               FIBA               |          `m`          |
| Basketball |               NBA                |         `ft`          |
| Basketball |           NBA G League           |         `ft`          |
| Basketball |               NCAA               |         `ft`          |
| Basketball |               NFHS               |         `ft`          |
| Basketball |               WNBA               |         `ft`          |
|  Football  |               CFL                |         `yd`          |
|  Football  |               NCAA               |         `yd`          |
|  Football  | NFHS11 (High School, 11 players) |         `yd`          |
|  Football  |  NFHS6 (High School, 6 players)  |         `yd`          |
|  Football  |  NFHS8 (High School, 8 players)  |         `yd`          |
|  Football  |  NFHS9 (High School, 9 players)  |         `yd`          |
|  Football  |               NFL                |         `yd`          |
|   Hockey   |               AHL                |         `ft`          |
|   Hockey   |               ECHL               |         `ft`          |
|   Hockey   |               IIHF               |          `m`          |
|   Hockey   |               NCAA               |         `ft`          |
|   Hockey   |               NHL                |         `ft`          |
|   Hockey   |               NWHL               |         `ft`          |
|   Hockey   |               OHL                |         `ft`          |
|   Hockey   |               PHF                |         `ft`          |
|   Hockey   |              QMJHL               |         `ft`          |
|   Hockey   |               USHL               |         `ft`          |
|   Soccer   |               EPL                |          `m`          |
|   Soccer   |               FIFA               |          `m`          |
|   Soccer   |               MLS                |         `yd`          |
|   Soccer   |               NCAA               |         `yd`          |
|   Soccer   |               NWSL               |         `yd`          |
|   Tennis   |               ATP                |         `ft`          |
|   Tennis   |               ITA                |         `ft`          |
|   Tennis   |               ITF                |         `ft`          |
|   Tennis   |               NCAA               |         `ft`          |
|   Tennis   |               USTA               |         `ft`          |
|   Tennis   |               WTA                |         `ft`          |

However, since the data that is supplied may come in various units of
measure, the plots are able to be generated in the data’s units. This is
done via the `unit` argument in `geom_{sport}()`. The features
themselves will look visually identical, but the underlying coordinate
grid will change.

Additionally, the `convert_units()` function can be called on a data
frame to convert from the data’s arguments to the plot’s. For example,
if soccer data is given in yards, but is desirable to be plotted in
meters, calling
`convert_units(tracking_data, 'yd', 'm', conversion_columns = c('x', 'y'))`
will convert the x and y coordinates from yards to meters.

As mentioned [above](#plotting-functions), the `geom_{sport}()` family
of functions allow for rotations of surfaces via the `rotate` argument.
To make this easy, `sportyR` also allows for the rotation of data
frames’ coordinates ***so long as they contain an*** `x` ***and*** `y`
***column*** via the `rotate_coords()` function. Translation and
reflection of coordinates are also possible through `translate()` and
`reflect()` functions respectively.

## Surface Examples

Most playing surfaces are standard in size, so they can be rendered via
a call to the proper `geom_{sport}()` function like so:

``` r
# Draw a basic MLB field plot
geom_baseball("mlb")
```

<img src="man/figures/README-mlb-example-1.png" width="100%" />

``` r
# Create a 100m by 75m FIFA pitch
geom_soccer(
  "fifa",
  pitch_updates = list(
    pitch_length = 100,
    pitch_width = 75
  )
)
```

<img src="man/figures/README-fifa-example-1.png" width="100%" />

It’s also possible to plot parital surfaces and rotated surfaces:

``` r
# Draw half of a rotated NBA court
geom_basketball("nba", display_range = "offense", rotation = 270)
```

<img src="man/figures/README-nhl-example-1.png" width="100%" />

Creating a realistic, customized output plot is also possible by
supplying the proper arguments to recolor. More information on how to
customize is in the [next section](#cani-Functions). ***NOTE**: not all
of the arguments below are needed, however all are shown to display the
flexibility with which the plots can be customized.*

``` r
# Create a totally customized NCAA basketball court
geom_basketball(
  league = "ncaa",
  color_updates = list(
    offensive_half_court = "#e8e0d7",
    defensive_half_court = "#e8e0d7",
    court_apron = "#e84a27",
    two_point_range = c("#e8e0d7", "#ffffff66"),
    center_circle_fill = "#e8e0d7",
    painted_area = c("#e84a27", "#ffffff00"),
    free_throw_circle_fill = "#e8e0d7",
    sideline = "#13294b",
    endline = "#13294b",
    division_line = "#13294b",
    center_circle_outline = "#13294b",
    lane_boundary = c("#ffffff", "#ffffff00"),
    three_point_line = c("#13294b", "#ffffff"),
    free_throw_circle_outline = "#ffffff",
    lane_space_mark = "#ffffff",
    restricted_arc = "#13294b",
    backboard = "#13294b"
  )
)
```

<img src="man/figures/README-custom-ncaa-bb-example-1.png" width="100%" />

Want a blue college football field? Here’s how:

``` r
# Create a blue football field
geom_football(
  "ncaa",
  color_updates = list(
    field_apron = "#2e4597",
    field_border = "#2e4597",
    offensive_endzone = "#2e4597",
    defensive_endzone = "#2e4597",
    offensive_half = "#2e4597",
    defensive_half = "#2e4597",
    team_bench_area = "#2e4597"
  )
)
```

<img src="man/figures/README-custom-ncaa-football-plot-1.png" width="100%" />

## `cani` Functions

The main functionality of plotting is intended to be straightforward and
easy to use, but questions are sure to arise about what can and can’t be
plotted and customized in the current version of the package. The
`cani_` family of functions are here to help answer those questions
directly. Their syntax is meant to resemble a question like

> Can I plot a football field?

or

> Can `sportyR` make a baseball plot?

and message back the answer. Here’s how they work:

``` r
cani_plot_league("mlb")
#> A plot for MLB can be created via the geom_baseball() function
```

``` r
cani_color_league_features("nba")
#> Here are the viable plotting features to color for NBA basketball:
#> 
#> plot_background
#> defensive_half_court
#> offensive_half_court
#> court_apron
#> center_circle_outline
#> center_circle_fill
#> division_line
#> endline
#> sideline
#> two_point_range
#> three_point_line
#> painted_area
#> lane_boundary
#> free_throw_circle_outline
#> free_throw_circle_fill
#> free_throw_circle_dash
#> lane_space_mark
#> inbounding_line
#> substitution_line
#> baseline_lower_defensive_box
#> lane_lower_defensive_box
#> team_bench_line
#> restricted_arc
#> backboard
#> basket_ring
#> net
```

For more information, call `?cani_plot_league`, `?cani_plot_sport`, or
`?cani_color_league_features`.

## Adding Tracking Data

Because this package is an extension of the `ggplot2` package, data can
be added much the same way on top of the surface plot that
`geom_{sport}()` creates. Although tracking data isn’t widely publicly
available yet, there are a few examples to use. The data sources for the
following examples are below.

`sportyR` makes shot charts in all sports significantly easier. Here’s a
look at a shot chart from an NWHL game between the Minnesota Whitecaps
and the Boston Pride (data provided for the [Big Data Cup -
2021](https://github.com/bigdatacup/Big-Data-Cup-2021)):

``` r
# Read data from the Big Data Cup
bdc_data <- read.csv(
  glue::glue(
    "https://raw.githubusercontent.com/bigdatacup/Big-Data-Cup-2021",
    "/main/hackathon_nwhl.csv"
  )
)

# Change names of X.Coordinate and Y.coordinate to x and y respectively
names(bdc_data)[13:14] <- c("x", "y")

# Subset to only be shots from the game on 2021-01-23 between the Minnesota
# White Caps and Boston Pride
bdc_shots <- bdc_data[(bdc_data$Event == "Shot") &
                        (bdc_data$Home.Team == "Minnesota Whitecaps") &
                        (bdc_data$game_date == "2021-01-23"), ]

# Separate shots by team
whitecaps_shots <- bdc_shots[bdc_shots$Team == "Minnesota Whitecaps", ]
pride_shots <- bdc_shots[bdc_shots$Team == "Boston Pride", ]

# Correct the shot location
whitecaps_shots["x"] <- 200 - whitecaps_shots["x"]
whitecaps_shots["y"] <- 85 - whitecaps_shots["y"]

# Draw the rink
phf_rink <- geom_hockey("phf", x_trans = 100, y_trans = 42.5)

# Add the shot locations
phf_rink +
  geom_point(data = whitecaps_shots, aes(x, y), color = "#2251b8") +
  geom_point(data = pride_shots, aes(x, y), color = "#fec52e")
```

<img src="man/figures/README-bdc-example-1.png" width="100%" />

The functionality of `sportyR` also makes gif-making via `gganimate`
much easier as well. This is a play from Week 15 of the 2018 NFL season
between the Chicago Bears and Green Bay Packers. Data made available for
the [Big Data Bowl
2021](https://www.kaggle.com/c/nfl-big-data-bowl-2021) Kaggle
competition.

``` r
# Load the play data
example_nfl_play <- read.csv("data-raw/example-pbp-data.csv")

# Prep data for plotting
example_nfl_play[example_nfl_play["team"] == "home", "color"] <- "#c83803"
example_nfl_play[example_nfl_play["team"] == "away", "color"] <- "#ffb612"
example_nfl_play[example_nfl_play["team"] == "football", "color"] <- "#624a2e"

# Create the field
nfl_field <- geom_football("nfl", x_trans = 50, y_trans = 26.6667)

# Add the points on the field
play_anim <- nfl_field +
  geom_point(
    data = example_nfl_play, aes(x, y),
    color = example_nfl_play$color
  ) +
  transition_time(example_nfl_play$frameId)

# Show the animation
play_anim
```

<img src="man/figures/README-bdb-example-1.gif" width="100%" />

## License

This package is released under the [MIT
License](https://github.com/rossdrucker/sportyR/blob/master/LICENSE.md).

## Contributions

### League Office

The package maintainers and functional engineers

-   [Ross Drucker](https://github.com/rossdrucker) - `sportyR`
    Commissioner

### General Managers

Contribute by adding a new sport and become its general manager. Current
general managers (and their sports) are:

-   [Ross Drucker](https://github.com/rossdrucker) - Baseball
-   [Ross Drucker](https://github.com/rossdrucker) - Basketball
-   [Ross Drucker](https://github.com/rossdrucker) - Football
-   [Ross Drucker](https://github.com/rossdrucker) - Hockey
-   [Ross Drucker](https://github.com/rossdrucker) - Soccer
-   [Ross Drucker](https://github.com/rossdrucker) - Tennis

### Coaching Staffs

Notice something for a sport that already exists, but isn’t quite right?
Join that sport’s coaching staff!

### Scout Team

By regularly reporting issues, making very slight modifications, fixing
typos, or just helping others navigate their own issues, you’re able to
join the Scout Team!

### `sportyR`tist

The `sportyR` logo was created by Lindsey Kelso. Check her out on
[Instagram](http://Instagram.com/kelsokreationsbylindsey) or her [online
shop](http://kelsokreationsbylindsey.bigcartel.com)!
