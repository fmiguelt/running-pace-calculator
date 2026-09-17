# Running Pace Calculator

A single-file, dependency-free HTML tool for runners who need to move between **speed (km/h)** and **pace (min/km)**, and to work out the averages of a run made up of several segments.

Everything runs locally in the browser — no build step, no network requests, no data leaves the page.

## Getting started

Open `running_pace_calculator.html` in any modern browser:

```bash
open running_pace_calculator.html      # macOS
xdg-open running_pace_calculator.html  # Linux
```

That's it. There is nothing to install.

## Features

### 1. Convert speed to pace
Enter a speed in km/h and get the equivalent pace in `mm:ss` per kilometre.

> 12 km/h → 5:00 min/km

### 2. Convert pace to speed
Enter a pace as `mm:ss` and get the equivalent speed in km/h.

> 5:30 min/km → 10.91 km/h

### 3. Multi-segment run calculator
Add one entry per segment, each with its **distance (km)** and **speed (km/h)**. The calculator returns:

- total distance
- total time
- average speed
- average pace

The average is **distance-weighted** (total distance ÷ total time), not a naive mean of the segment speeds — so a long slow segment correctly outweighs a short fast one.

Use **Add Segment** to append entries and **Remove** to drop one.

### 4. Average pace from 1K segments
Built for reading splits straight off a watch. Enter the pace of each kilometre as `mm:ss` and get a per-km breakdown table plus the total distance, total time, average pace, and average speed.

The **8K** and **10K** buttons pre-create that many segment rows in one click (this clears any rows already present). **Add 1K Segment** appends a single extra row.

Because every segment is exactly 1 km, the average here is a straight mean of the split times.

### 5. Pace & speed reference table
A static lookup table generated on page load, covering paces from **6:30 down to 3:00 min/km** in 10-second steps (22 rows), filtered to speeds between 8 and 20 km/h and sorted by ascending speed.

## Input formats

| Field | Format | Example |
|---|---|---|
| Speed | Decimal number, km/h | `11.5` |
| Pace | `mm:ss` | `5:30` |
| Distance | Decimal number, km | `2.5` |

Invalid input (missing values, non-numeric entries, seconds outside `0`–`59`, or a pace not in `mm:ss` form) raises a browser alert and the calculation is aborted.

## How it works

The maths is a single relationship, applied in both directions:

```
pace (min/km) = 60 / speed (km/h)
speed (km/h)  = 60 / pace (min/km)
```

For the multi-segment calculator, each segment's time is derived as `distance / speed`, times are summed, and the average speed is `total distance / total time`.

## Project structure

```
running_pace_calculator.html   # markup, styles and logic in one file
README.md                      # this file
```

The page is responsive: the two converters sit side by side on desktop and stack into a single column below 768px.

## Browser support

Any browser with ES6 template literals and `String.prototype.padStart` — Chrome, Firefox, Safari and Edge in current versions all qualify.
