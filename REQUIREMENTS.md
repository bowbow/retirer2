## Project Overview

This project is an interactive retirement planning tool. Its purpose is to help a person:

- **Understand when they can retire** given their income, savings, and spending.
- **Estimate how their assets can grow** over time under different assumptions.
- **Plan withdrawals in retirement** to see whether their money will likely last.

This document is an initial guess at requirements and is expected to change as we learn more from the actual user.

## Target Users

- **Primary user – individual saver**
  - Has one or more investment or savings accounts.
  - Wants to know if they are "on track" for retirement.
  - Comfortable entering simple financial data but **not** a finance expert.
- **Secondary user – advisor / helper**
  - May sit with the primary user and help plug in numbers.
  - Needs simple, clear outputs they can explain quickly.

## High-Level Goals

- **Clarity**: Explain results in plain language and simple visuals.
- **Exploration**: Make it easy to tweak assumptions and immediately see the impact.
- **Reality-based**: Use reasonable financial modeling assumptions (inflation, taxes, returns), but keep them understandable.

## Core Concepts

- **Working / accumulation phase**: Time before retirement when the user is earning income and adding to savings.
- **Retirement / decumulation phase**: Time after retirement when the user is withdrawing from savings.
- **Assets**: Accounts where the user saves/invests (e.g., brokerage, 401(k), IRA, savings).
- **Contributions**: How much the user adds to assets over time (monthly/yearly).
- **Withdrawal strategy**: How much the user takes out in retirement (fixed amount, % of portfolio, etc.).
- **Assumptions**: Investment returns, inflation, tax rate, life expectancy, and any safety margins.

## Functional Requirements

### 1. User Inputs – Personal & Timeline

- **Age and timing**
  - **Current age** (or current year and birth year).
  - **Planned retirement age** (or allow the tool to suggest one).
  - **Life expectancy assumption** (default, e.g. 90; editable).
- **Income & savings behavior**
  - Current **annual gross income** (optional but useful).
  - **Savings rate** (percentage of income or fixed amount per year/month).
  - Option to model **changes over time** (e.g., savings increase every year by inflation or by a set amount).

### 2. User Inputs – Assets & Accounts

- Allow the user to define one or more **accounts**, each with:
  - **Name** (e.g., "401(k)", "Brokerage", "Cash savings").
  - **Current balance**.
  - **Expected annual return** (before or after inflation; we should be explicit).
  - **Contribution pattern**:
    - Amount contributed (per month or per year).
    - Start and end age or year (e.g., contributions stop at retirement).
  - Optional **tax treatment flag** (e.g., tax-deferred vs taxable) for future enhancement.

### 3. User Inputs – Assumptions

- Global assumptions (with sensible defaults and explanations):
  - **Inflation rate**.
  - **Real vs nominal returns** (clarify which one is being entered).
  - **Safe withdrawal rate** (e.g., 3.5–4% rule).
  - **Tax rate** (simple, flat effective rate for now).
- Ability to set **scenario presets** (e.g., conservative / moderate / aggressive) that adjust return and inflation assumptions.

### 4. Projections – Accumulation Phase

The tool should:

- **Simulate year-by-year balances** from now until the user’s planned retirement age (or suggested age).
- For each year:
  - Add contributions.
  - Apply investment returns.
  - Adjust for inflation as needed (depending on whether we present results in real or nominal terms).
- Allow the user to see:
  - **Total projected portfolio value at retirement**.
  - **Per-account balances at retirement** (if we model multiple accounts).
  - Simple **chart of balance over time** leading up to retirement.

### 5. Projections – Retirement Withdrawals

- Given a **starting portfolio at retirement** and a **withdrawal strategy**, project balances from retirement age through life expectancy.
- Required capabilities:
  - Model a **fixed real withdrawal** (e.g., \$X per year adjusted for inflation).
  - Model a **percentage-based withdrawal** (e.g., Y% of starting balance or Y% of current balance each year).
  - Show whether the portfolio:
    - **Lasts through life expectancy**.
    - **Runs out early**, including when (age/year).
  - Show simple charts:
    - Portfolio value vs. age in retirement.
    - Withdrawals vs. age.

### 6. Retirement Feasibility & "Can I Retire?" View

- Provide a clear summary answer such as:
  - **"You can retire at age N with a X% success margin under current assumptions."**
  - Or: **"With your current plan, your savings are projected to run out at age M (before your target age L)."**
- Allow the tool to:
  - Recommend a **later retirement age** to meet basic feasibility.
  - Recommend **higher savings rate** or **lower retirement spending** targets.
- Show simple **trade-off exploration**:
  - "If you retire at age R-2 / R / R+2, here’s how long your money is projected to last."

### 7. Scenario Comparison

- Allow the user to create and save **named scenarios**:
  - e.g., "Baseline", "Early retirement", "More aggressive returns".
- For each scenario, store:
  - Inputs (ages, contributions, returns, inflation, withdrawal rate).
  - Key outputs (portfolio at retirement, how long money lasts, success/failure).
- Provide a simple **comparison view**:
  - Table of scenarios with key metrics side by side.

### 8. UX & Interaction

- The tool should:
  - **Validate inputs** (e.g., ages are reasonable, percentages between 0–100).
  - Provide **inline explanations/tooltips** for financial terms.
  - Make it easy to **reset to defaults** or **duplicate a scenario**.
- Favor **sliders + text inputs** for key parameters (withdrawal rate, retirement age, savings rate), so users can quickly experiment.

## Non-Functional Requirements (Initial)

- **Performance**
  - Calculations for typical timelines (e.g., ages 25–95) should feel instant.
  - Support frequent recomputation as the user drags sliders or changes assumptions.
- **Usability**
  - Use plain language; avoid jargon where possible.
  - Focus on a small number of primary outputs rather than overwhelming the user.
- **Transparency**
  - Make it clear which assumptions are being used.
  - Provide an optional "details" view that explains the math or shows a table of year-by-year values.
- **Extensibility**
  - Design models and data structures so that later additions are easy, e.g.:
    - Social Security / pension income.
    - One-time events (buying a house, inheritance, large medical cost).
    - More detailed tax modeling.

## Out of Scope (For Now)

These may be added later, but are **not required** in the initial version:

- Detailed tax optimization (e.g., specific US tax brackets, Roth conversion strategies).
- Asset allocation recommendations (e.g., which funds/stocks to buy).
- Monte Carlo simulations and probability-of-success analytics (initial version may use deterministic assumptions only).
- Currency conversion / multi-country tax rules.

## Open Questions to Refine Later

- How realistic/complex should the financial model be vs. keeping the tool simple?
- Which country’s tax and retirement rules (if any) should the tool reflect, or should it stay generic?
- Do we need explicit modeling of Social Security / government pensions / employer pensions?
- How much historical data or backtesting (if any) do we want to include?
- Should the tool be web-only, or is there a CLI/desktop mode expected as well?

These questions should be revisited as soon as we have a real user or clearer product vision.

