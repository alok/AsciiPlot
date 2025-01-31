# AsciiPlot

An ASCII plotting library for Lean 4, designed for creating beautiful terminal-based visualizations with a composable, type-safe API.

## Features

- [ ] 🎯 Pure functional design with strong type safety
- [ ] 📊 Basic plotting primitives (points, lines, scatter plots)
- [ ] 📐 Automatic scaling and axis generation
- [ ] 🧩 Composable plot elements
- [ ] 🎨 Customizable plot styles (characters, borders)
- [x] 📏 Flexible canvas sizing

## Installation

Add to your `lakefile.toml`:

```toml
[[require]]
name = "AsciiPlot"
url = "https://github.com/username/AsciiPlot.git"
```

## Quick Start

```lean
import AsciiPlot

/-- Compare linear and quadratic functions with axis labels -/
def compareLinQuad : AsciiPlot.AsciiPlot :=
    let sinPoints := Array.range 100 |>.map fun x =>
        let x := x.toFloat / 10
        (x, Float.sin x)
    let cosPoints := Array.range 100 |>.map fun x =>
        let x := x.toFloat / 10
        (x, Float.cos x)
    
    {
      title := "Linear vs Quadratic",
      series := #[
        { label := "y = x",
          points := sinPoints,
          marker := '+' },
        { label := "y = x²",
          points := cosPoints,
          marker := '*' }
      ],
      width := 50,
      height := 20,
      axisConfig := {
        xLabel := "x",
        yLabel := "f(x)",
        xTicks := 5,
        yTicks := 4,
        showTickValues := true
      }
  }

#eval compareLinQuad -- Prints a plot in the infoview.
```

Which renders as

```text
                  Linear vs Quadratic                   

│*─────────────────────────────────────────────────│
│ *                                               *│
│  *                                             * │
│   *                                           *  │
│    *                                         *   │
│     *                                       *    │
│                                                  │
│      *                                     *     │
│       **                                 **      │
│         *                               *        │
│          *                             *         │
│           *                           *          │
│            **                       **           │
│              **                   **        +++++│
│                **               **   +++++++     │
│                  ***         ***+++++            │
│                     *********                    │
│               ++++++++                           │
│        +++++++                                   │
│++++++++                                          │
│                                                  │
│+───────────+───────────+───────────+────────────+│
          -5.00      -2.55      -0.10       2.35       4.80   
                          x
Legend:

+ y = x
* y = x²
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## Acknowledgments

Inspired by:
- R's ggplot2
- Julia's UnicodePlots
