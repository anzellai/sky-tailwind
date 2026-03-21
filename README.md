# Sky Tailwind

A type-safe, Tailwind CSS-inspired utility library for the [Sky](https://github.com/anzellai/sky) programming language.

Every Tailwind class becomes a Sky function — typos are compiler errors, autocomplete shows all available utilities, and all CSS is baked into the binary at compile time with zero runtime cost.

## Installation

Add `sky-tailwind` as a dependency in your project's `sky.toml`:

```toml
[dependencies]
"github.com/anzellai/sky-tailwind" = "latest"
```

Then install:

```bash
sky install
```

## Quick Start

```elm
module Main exposing (main)

import Github.Com.Anzellai.SkyTailwind.Tailwind as Tw
import Std.Html exposing (..)
import Std.Html.Attributes exposing (..)

view model =
    div []
        [ Tw.styles    -- inject CSS once at the top of your view
        , div
            [ Tw.tw
                [ Tw.maxW7xl
                , Tw.mxAuto
                , Tw.p8
                ]
            ]
            [ h1
                [ Tw.tw [ Tw.text4xl, Tw.fontBold, Tw.textGray900 ] ]
                [ text "Hello, Sky Tailwind!" ]
            , p
                [ Tw.tw [ Tw.mt4, Tw.textLg, Tw.textGray600 ] ]
                [ text "Type-safe styling for Sky apps." ]
            , button
                [ Tw.tw
                    [ Tw.bgBlue600
                    , Tw.textWhite
                    , Tw.px6
                    , Tw.py3
                    , Tw.roundedLg
                    , Tw.fontSemibold
                    , Tw.shadow
                    , Tw.hover Tw.bgBlue700
                    , Tw.transition
                    ]
                ]
                [ text "Get Started" ]
            ]
        ]
```

### Key concepts

1. **`Tw.styles`** — a `VNode` that injects all CSS rules. Place it once at the top level of your view.
2. **`Tw.tw`** — takes a `List (String, String)` of utilities and merges them into a single `class` attribute.
3. **`Tw.twWith`** — same as `tw` but also accepts additional custom class names as a `String`.

## Available Modules

You can import the main module for everything, or import individual modules for granularity:

| Module                   | What it provides                                                         |
| ------------------------ | ------------------------------------------------------------------------ |
| `SkyTailwind`            | Core functions (`tw`, `twWith`, `styles`) + re-exports all utilities     |
| `SkyTailwind.Spacing`    | Padding (`p0`..`p24`), margin (`m0`..`m24`), gap (`gap0`..`gap12`)       |
| `SkyTailwind.Typography` | Font size, weight, family, text color, alignment, decoration, transforms |
| `SkyTailwind.Layout`     | Display, position, sizing (`w*`, `h*`), overflow, z-index                |
| `SkyTailwind.Flex`       | Flex direction, wrap, justify, align, order, grow/shrink                 |
| `SkyTailwind.Grid`       | Grid columns/rows, span, flow, place content/items/self                  |
| `SkyTailwind.Background` | Background colors, size, position, repeat                                |
| `SkyTailwind.Border`     | Border width, color, style, radius, rings                                |
| `SkyTailwind.Effects`    | Shadows, opacity, transitions, transforms, cursor                        |
| `SkyTailwind.Responsive` | Breakpoint wrappers: `sm`, `md`, `lg`, `xl`, `xxl`                       |
| `SkyTailwind.State`      | State variants: `hover`, `focus`, `active`, `disabled`                   |

## Responsive Design

Wrap any utility with a breakpoint function:

```elm
div
    [ Tw.tw
        [ Tw.gridCols1                -- 1 column on mobile
        , Tw.md Tw.gridCols2          -- 2 columns at 768px+
        , Tw.lg Tw.gridCols3          -- 3 columns at 1024px+
        ]
    ]
    [ ... ]
```

Breakpoints: `sm` (640px), `md` (768px), `lg` (1024px), `xl` (1280px), `xxl` (1536px).

## State Variants

Wrap utilities with state functions for interactive styles:

```elm
button
    [ Tw.tw
        [ Tw.bgBlue600
        , Tw.hover Tw.bgBlue700       -- darker on hover
        , Tw.focus Tw.ringBlue500      -- ring on focus
        , Tw.active Tw.bgBlue800       -- darkest on click
        , Tw.transition
        ]
    ]
    [ text "Click me" ]
```

Available states: `hover`, `focus`, `active`, `disabled`, `firstChild`, `lastChild`, `odd`, `even`.

## Conditional Styling

Since utilities are just list items, use standard Sky list operations:

```elm
let
    base =
        [ Tw.px4, Tw.py2, Tw.rounded, Tw.fontSemibold ]

    variant =
        if isPrimary then
            [ Tw.bgBlue600, Tw.textWhite ]
        else
            [ Tw.bgGray200, Tw.textGray800 ]
in
button [ Tw.tw (base ++ variant) ] [ text label ]
```

## Mixing with Custom Classes

Use `twWith` to combine utilities with custom class names:

```elm
div
    [ Tw.twWith "my-custom-class another-class"
        [ Tw.p4, Tw.bgWhite ]
    ]
    [ ... ]
```

## Running the Showcase

This repository includes an interactive landing page that demonstrates all available utilities, a component gallery, and a getting-started guide.

```bash
# Build and run
sky run src/Main.sky

# Or use watch mode for development
sky dev src/Main.sky
```

Then open [http://localhost:4000](http://localhost:4000) in your browser.

The showcase includes:

- **Home** — feature overview, live interactive demo, and quick reference
- **Getting Started** — step-by-step usage guide
- **Components** — gallery of buttons, cards, alerts, badges, forms, and more

## License

MIT
