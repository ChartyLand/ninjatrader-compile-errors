# `'DashStyleHelper' does not exist in the current context`

## Cause

`DashStyleHelper` is declared in the **`NinjaTrader.Gui`** namespace. The NinjaScript wizards for indicators and strategies write `using NinjaTrader.NinjaScript.DrawingTools;` into new files, because that is where `Draw.*` lives. `DashStyleHelper` is not in `DrawingTools`.

## Fix

Add the namespace to the `using` block at the top of the file:

```csharp
using NinjaTrader.Gui;
```

`DashStyleHelper` is then available to `Draw.Line`, `Draw.Ray`, `Draw.HorizontalLine`, and every other `Draw` overload that takes a dash style:

```csharp
Draw.Line(this, "tag", false, 10, Low[10], 0, Low[0],
          Brushes.Orange, DashStyleHelper.Dash, 2);
```

## Why the error is confusing

The IntelliSense suggestion list offers `NinjaTrader.NinjaScript.DrawingTools` because that is the namespace already imported by the wizard, and it does not contain the type. Adding a `using` for the namespace that does contain it is the whole fix.

## Evidence

- NinjaScript reference index: https://docs.ninjatrader.com/ninjascript/llms.txt
- Forum threads where this is the accepted answer: discourse.ninjatrader.com topics 7038 and 2964
