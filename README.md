
# Dominant Cycle Adaptive Filter Bank (DCA Filters)

A high-performance, adaptive technical analysis indicator written in **Pine Script v6**. The **Dominant Cycle Adaptive Filter Bank (DCA Filters)** dynamically tracks the primary cyclical frequency of market price action and tunes a network of lag-reduced filters to that specific frequency in real-time.

Unlike traditional moving averages that use rigid, static lookback periods, this indicator actively warps its parameters to match changing market conditions, offering an elegant balance between noise reduction and structural responsiveness.

---

## Acknowledgments & Theoretical Foundation

This indicator is heavily indebted to the pioneering work of **John F. Ehlers** in the field of Digital Signal Processing (DSP) applied to financial markets.

Ehlers introduced to the trading world: Homodyne Discriminator, MESA (Maximum Entropy Spectral Analysis), and autocorrelation-based cycle measurement. His research showed that financial time series are composed of variable cycles buried in non-stationary noise.

The core cycle engine in this indicator uses an **Autocorrelation Periodogram** derived from Ehlers' principles and optimized by developer *mihakralj* (QuanTAlib). This script builds upon that foundation by constructing a multi-phase adaptive filter bank using Ehlers' **SuperSmoother** filter architecture.

---

## For Traders & End Users

### What it Does

Traditional indicators like the Simple Moving Average (SMA) or Exponential Moving Average (EMA) suffer from a fatal flaw: if you set them to a short period, they generate whipsaws during market consolidations; if you set them to a long period, they lag significantly behind major turning points.

The **DCA Filter Bank** solves this by dynamically calculating the **Dominant Cycle** (the current rhythmic heartbeat of the market) and automatically tuning three interconnected smoothing layers to it.

### Key Visual Components

The indicator plots up to three structural lines directly on your chart:

* **Fast Line (Default: Visible):** Acts as the ultra-responsive core. It uses a fraction of the dominant cycle length to capture near-immediate momentum shifts.
* **Mid Line (Default: Visible):** The anchor line. It is tuned exactly to the measured dominant cycle period, filtering out noise smaller than the current cycle length.
* **Slow Line (Default: Hidden):** A macroeconomic/structural baseline. Tuned to a multiple of the dominant cycle, it filters out noise and intermediate fluctuations to reveal the underlying macro trend.

```
                  ▲ BULLISH MOMENTUM
  ───────────────── [Fast Line] (Responsive Trend)
   ░░░░░░░░░░░░░░░
  ───────────────── [Mid Line]  (Dominant Cycle Anchor)
   ░░░░░░░░░░░░░░░
  ───────────────── [Slow Line] (Macro Baseline)
                  ▼ BEARISH MOMENTUM

```

### Strategic Applications

1. **Dynamic Support & Resistance:** The cloud areas (shaded zones between the lines) act as self-adjusting cushion zones where price often tests and rejects during healthy trends.
2. **Trend Alignment:** When the **Fast Line** is above the **Mid Line** and the cloud is expanding, it indicates a strong, cycle-backed bullish expansion. The reverse is true for a bearish expansion.
3. **Adaptive Crossovers:** Using the Fast and Mid line crossovers yields much higher quality signals than standard MA crosses because the system naturally widens during highly volatile, long-cycle regimes and compresses during quiet, short-cycle regimes.

---

## Quick-Start Usage Guide

1. Copy the source script.
2. Open **TradingView**, navigate to the **Pine Editor** tab at the right of your screen.
3. Paste the code into a new indicator document and click **Add to Chart**.
4. Adjust the **Phase Spacing (k)** configuration to customize your strategy profile:
* Set to `1.414` (Square root of 2) for an **Octave-Harmonic** spacing profile (Balanced).
* Set to `2.0` for a **Full Octave Shift** (Slower, structural trend following).
* Set to `1.26` for a tight **Third-Octave Shift** (Aggressive scalping/momentum trading).
* Set to `1.618` for a **Golden Ratio Shift** (Highly organic spacing based on fractal market geometry).
