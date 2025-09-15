# Cheat Sheet for the CIPM Program Level II

## Ethical and Professional Standards

1. Professionalism
    1. Knowledge of the Law
    2. Independence and Objectivity
    3. Misrepresentation
    4. Misconduct
    5. Competence
2. Integrity of Capital Markets
    1. Material Nonpublic Information
    2. Market Manipulation
3. Duties to Clients
    1. Loyalty, Prudence, and Care
    2. Fair Dealing
    3. Suitability
    4. Performance Presentation
    5. Preservation of Confidentiality
4. Duties to Employers
    1. Loyalty
    2. Additional Compensation Arrangements
    3. Responsibilities of Supervisors
5. Investment Analysis, Recommendations, and Actions
    1. Diligence and Reasonable Basis
    2. Communication with Clients and Prospective Clients
6. Conflicts of Interest
    1. Avoid of Disclose Conflicts
    2. Priority of Transactions
    3. Referral Fees
7. Responsibilities as a CFA Institute Member or CFA Candidate
    1. Conduct as Participants in CFA Institute Programs
    2. Reference to CFA Institute, the CFA Designation, and the CFA Program

## Performance Measurement

### Return Measurement

Weights must add up to 100%

```math
    F_t = (B_t - \frac{E}{(1+r_{fin})^{\tilde{t}-t}})(1+r_{fin})^{T-t}
```

#### Futures

Notional exposure of futures contracts:

```math
    NE = \text{Sign} \times \text{Number of contracts} \times \text{Contract value multiplier} \times \text{Price underlying}
```

Use price of the underlying (i.e. Spot price) instead of futures price. Otherwise, the equity exposure will be overestimated if the futures price trades at a premium.

**Notional return** = (Total margin receipt + notional income) / Actual economic exposure

Note: Same formula for regardless future is long or short.

For notional return calculation, the denominator is always positive regaredless the futures are long or short.

#### Forwards

The value of a long forward investment at time $t_1$

```math
    (F_{t_1} - F_{t_0}) \frac{1}{(1 + r_{fin})^{T-t_1}}
```

Notional return: Similar to futures, but the value need to be discounted.

```math
    \text{Return} = \frac{\text{Multiplier} \times (F_{t_1} - F_{t_0}) \times (1 + r_{fin})^{-(T-t_1)} + \text{Notional cash} \times \text{Discount rate}}{\text{Notional exposure}}
```

#### Options

```math
    NE = \text{Sign} \times \delta \times \text{Number of contracts} \times \text{Contract value multiplier} \times \text{Price underlying}
```

Notional cash expsoure is the difference between the cost and notional exposure of the options.

#### Swap

```math
    \text{Return} = \frac{(Holding_{Current} - Holding_{Previous}) - (Exposure_{Current} - Exposure_{Previous}) + \text{Bond Interest} +\text{Swap Interest}}{Holding_{Previous} + Exposure_{Previous}}
```

#### Covered interest rate parity

```math
    F_0 = S_0\frac{1+r_{FC}}{1+r_{DC}}
```
where $F_0$ and $S_0$ are quoted in $\frac{FC}{DC}$.

#### Cost of hedging

- Spot currency return = $\frac{S_1}{S_0} - 1$
- Forward return = $\frac{S_1}{F_0} - 1$
- Forward currency premium = $\frac{F_0}{S_0} - 1$

Note: Forward currency trades at a premium, and forward return is worse than spot return if interest rates in the "nominator" currency is higher (should depreciate based or covered interest rate parity).

#### Hedged Return

Calculate in 3 steps:

- Base currency return = $\frac{MV_1 / S_1}{MV_0 / S_0} - 1$
- Currency overlay return = $\frac{MV_0 / F_0 - MV_0 / S_1}{MV_0 / S_0}$
- Hedged return = Base currency return + Currency overlay return

Note: MV is quoted in FC. $F_t$ and $S_t$ are quoted in $\frac{FC}{DC}$

Hedged return is less than perfectly hedged return if the position is overhedged (portfolio fell in value) and FC is appreciating against DC.

### Data Integrity

#### Investment manager and custodian

1. Pricing: source
2. Missing trades: cutoff time
3. Mistimed cash flow: settlement vs trade date
4. Corporate action
5. Exchange rate: time
6. OTC derivatives: missing terms, currency forward not priced by vendor
7. Expense & fees

Action: Identify, document, implement control to alert, communicate

#### NAV-based and End-of-day time-weighted performance

1. Timing difference: price, FX, holdings
2. Fees: accrual frequency

#### Composite

1. Accuracy: avoid double counting, discretionary status, change/move
2. Completeness: data, details on discretion and disclosure, why not assigned
3. Conformity: GIPS standard oversight committee
4. Timeliness: assign, disclosure

Note: Comprehensive composite definition = too broad

## Performance Attribution

Valid benchmark "SAMURAI"

1. Specified in advance
2. Appropriate
3. Measurable
4. Unambiguous
5. Reflective of current investment opinions
6. Accountable
7. Investible

- S: Style exposure, A: Active position
- Published benchmark-centered (PBC): P = M + A, (B = M)
- Manager strategy (MS): P = M + S + A
- Risk band should serve as extreme boundaries around a neutral weight

### Topics in Return Attribution

#### Brinson-Fachler Arithmetic Attribution

- Allocation $A_i = (w_i - W_i)(B_i - B)$, where $B = \sum^n_{i=1}W_iB_i$
- Selection $S_i = w_i(R_i - B_i)$

#### Options

- Total portfolio return before adjustment = (Stock PnL + Option PnL + Gain on cash) / Total portfolio before adjustment
- Equity return = (Stock PnL + Option PnL + Interest on notional cash) / Combined equity exposure

Note: Interest on notional cash = Notional asset x Cash return. It can be negative if notional asset is negative.

#### Karnosky and Singer Multi-currency Attribution

Use continuously compounded (or log) returns, which is additive.

Step 1 - Calculate equity risk premium $B_L$ and foreign cash return converted to base currency $C$
```math
    R = \sum_{i=1}^n{w_i(R_{Li}-I_i)} + \sum_{i=1}^n{(w_i + \tilde{w_i})(C_i+I_i)}
```
```math
    B = \underbrace{\sum_{i=1}^n{W_i(B_{Li}-I_i)}}_{B_L} + \underbrace{\sum_{i=1}^n{(W_i + \tilde{W_i})(C_i+I_i)}}_{C}
```
Step 2 - Calculate the 3 effects

Allocation
```math
    A_i = (w_i - W_i)[(B_{Li} - I_i) - B_L]
```

Selection
```math
    S_i = w_i(R_{Li} - B_{Li})
```

Currency allocation
```math
    CA_i = [(w_i + \tilde{w_i}) - (W_i + \tilde{W_i}))] \times [(C_{i} + I_i) - C]
```

#### Geometric Multi-Currency Attribution

Total Excess Return

```math
    \underbrace{\frac{1+R_L}{1+B_{SL}}}_{\text{Selection}}\times
    \underbrace{\frac{1+B_{SL}}{1+B_L}}_{\text{Allocation}}\times
    \underbrace{\frac{1+R}{1+R_L} \times \frac{1+B_L}{1+B}}_{\text{Naive Currency Allocation}} - 1
```

```math
    \underbrace{\frac{1+R_L}{1+B_{SL}}}_{\text{Selection}}\times
    \underbrace{\frac{1+B_{SL}}{1+B_L}}_{\text{Allocation}}\times
    \underbrace{\frac{R_C}{B_C}}_{\text{Naive Currency Allocation}} - 1
```
where $R_C=\frac{1 + R}{1 + R_L} - 1$, and $B_C=\frac{1 + B}{1 + B_L} - 1$

Isolating the compounding effects

```math
    \underbrace{\frac{1+R_L}{1+B_{SL}}}_{\text{Selection}}\times
    \underbrace{\frac{1+B_{SL}}{1+B_L}}_{\text{Allocation}}\times
    \underbrace{\frac{1+R'_C}{1+B'_C}}_{\text{Currency Overlay}}\times
    \underbrace{\frac{1+R_C}{1+R'_C} \times \frac{1+B'_C}{1+B_C}}_{\text{Compounding}} - 1
```

where $R'_C=\sum_{i=1}^{n}w_iC_i$, and $B'_C=\sum_{i=1}^{n}W_iC_i$

Note: Please refer to p.359 for revised country allocation

#### Multi-Period Attribution

- Smoothing
  - Carino and Menchero
- Linking
  - Frongello and GRAP, algorithms are order dependent

### Fixed Income Attribution

#### Exposure Decomposition - Duration Based (Brinson-Hood-Beebower)

- Top down, benchmark-relative, transactional
- intuitive, simple data requirement, good for marketing/client reports, not well-versed for quantitative analysis

| Factor | Return | Notes |
|:-------|:------:|-------|
| **Allocation** | $(W_{p,DB} - W_{b,DB}) \times R_{b,GDB}$ | Duration Effect + Curve Effect
| &nbsp; Duration Effect | $\text{Duration return}_{\text{p,DB}} \times W_{p,DB} - \text{Duration return}_{\text{b,DB}} \times W_{b,DB}$
| &nbsp; Duration Return | Zero-duration RFR + (Duration x Excess return per year)
| **Sector allocation** | ${(W_{ps} - W_{bs}) \times (R_{b,SDB} - R_{b,GDB})}$, always zero for government bonds
| **Bond selection** | $W_{ps} \times (R_{p,SDB} - R_{b,SDB})$, for both government and corporate bonds

#### Yield Curve Decomposition - Duration Based

- Either top-down (group by portfolio or bucket-level) or buttom-up (security level), buy-and-hold
- Can be applied separately to portfolios and benchmarks. Difference between the two is the effect of active portfolio management decisions.
- Requires more data, better suited to decision makers, summary version can be used for marketing/client reports
- Break down when instruments have embedded options or large movements in market yield (Solution: Use effective duration instead of Modified duration)

| Factor | Return | Notes |
|:-------|:------:|-------|
| **Passage of time**   |
| &nbsp; Initial yield         |$Y \times \Delta t$ | from coupon and amortization
| &nbsp; Roll down             |$-D \times \Delta Y^{\text{Roll}} + \frac{1}{2} \times C \times (\Delta Y^{\text{Roll}})^2$ | bond will trade at a lower YTM as it approaches maturity
| **Curve variation**
| &nbsp; Shift                 | $-D \times \Delta Y^{\text{Shift}} + \frac{1}{2} \times C \times (\Delta Y^{\text{Shift}})^2$
| &nbsp; Slope                 | $-D \times \Delta Y^{\text{Slope}} + \frac{1}{2} \times C \times (\Delta Y^{\text{Slope}})^2$
| &nbsp; Curvature             | $-D \times \Delta Y^{\text{Shape}} + \frac{1}{2} \times C \times (\Delta Y^{\text{Shape}})^2$
| **Spread variation**
| &nbsp; Sector                | $-D \times \Delta Y^{\text{Systematic}} + \frac{1}{2} \times C \times (\Delta Y^{\text{Systematic}})^2$
| &nbsp; Specific              |$-D \times \Delta Y^{\text{Specific}} + \frac{1}{2} \times C \times (\Delta Y^{\text{Specific}})^2$

Note: Residual = Actual return - Estimated return

#### Yield Curve Decomposition - Full Repricing

- Bottom-up security repricing, buy-n-hold
- Can deal with a broader range of instrument ypes and yield changes
- Greater variety of quantitative modeling outside of attribution e.g. ex ante risk

| Factor | Return | Notes |
|:-------|:------:|-------|
|**Passage of time**
| Coupon                | $$\frac{Coupon}{\text{Price}_T}$$
| Amortization          | $$\frac{\text{Price}_{\text{Amori}} - \text{Price}_T}{\text{Price}_T}$$ | Using the same set of spot rates, less time to maturity. For bonds priced at a premium (i.e. coupon rates are higher than market rates), prices converge (i.e. drop) toward par value as time goes by. |
| Roll down             | $$\frac{\text{Price}_{\text{Roll}} - \text{Price}_\text{Amori}}{\text{Price}_T}$$ | Using the same set of spot rates but rolled down to **lower discount rates**
| **Yield curve movements** |
| Shift                 | $$\frac{\text{Price}_{\text{Shift}} - \text{Price}_\text{Roll}}{\text{Price}_T}$$
| Slope                 | $$\frac{\text{Price}_{\text{Slope}} - \text{Price}_\text{Shift}}{\text{Price}_T}$$
| Curvature             | $$\frac{\text{Price}_{\text{Curvature}} - \text{Price}_\text{Slope}}{\text{Price}_T}$$
| **Spread variation**  |
| Systematic            | $$\frac{\text{Price}_{\text{Systematic}} - \text{Price}_\text{Curvature}}{\text{Price}_T}$$
| Specific              | $$\frac{\text{Price}_{T+1} - \text{Price}_\text{Systematic}}{\text{Price}_T}$$

No residual

## Performance Appraisal

### Topics
- Managers' skill should be sufficient to overcome fee and trading costs
- Gross-of-fee analysis maybe useful for asset owners with sufficient scale to negotiate
- t-statistic is the ratio of the estimated intercept to its standard error. e.g. $t=\frac{\alpha}{s/\sqrt{n}}$
- Type I error: Hiring (or retaining) an unskilled manager, error of commission
- Type II error: Not hiring (or firing) a skilled manager
- There is a tradeoff between Type I and Type II error, unless more data is used
- 3 principles:
  1. Appropriate benchmark
  2. Appropriate estimation model
  3. Validate the model fit
- 14 common pitfalls
  1. Noise, use quality control chart
  2. Past return is not reliable indicator of future performance, should also assess firm, process and sfaff
  3. Benchmark, should represent the process, risk factor, investible with proper treatment of cash
  4. Appraisal measure, context matters - standalone vs total portfolio
  5. Scalability of risk, if there is restriction in leverage or hedging
  6. Synthesized exposure, off-benchmark risk that should be penalized and it can be exposed through factor analysis
  7. Effect of total AUM across multiple products, market impact cost
  8. Constraints, e.g. country, market cap, ESG, legal/regulatory
  9. Benchmark and risk-free rate are the opportunity cost\
     Note: High volatility dampens the geometric return but not arithmetic return, resulting in double jeopardy
  10. Portfolio or utility, appraisal ratio to determine the marginal benefit of a new manager
  11. Convexity or Tactical Asset Allocation, factor analysis is unable to detect
  12. Valuable information is lost if track record is truncated
  13. Serial correlation, smoothed return
  14. Selection biases e.g. backfill

Factor-based benchmarks
- Carhart four-factor mode: RMRF, SMB (Size), HML (Value), WML (Momentum)
- Elton and Gruber: RMRF, FIRF (Excess return of Bloomberg Barclays Aggregate Bond Index), TERM (10Y vs 30d yield), DEFAULT (Baa - Treasury yield), OPTION (Bloomberg Barclays GNMA - government bond w/ same duration)

...

Addition to Current Portfolio
```math
    \alpha = r_{new} - \beta_{new}(r_p) \\
    \beta_{new} = \frac{cov_{new,p}}{\sigma^2_p} = \rho\frac{\sigma_{new}}{\sigma_p} \\
    \sigma^2_{\varepsilon,new} = \sigma^2_{new} - \beta^2\sigma^2_p
```
 
 - Fung and Hsieh: RMRF, SMB, TREAS10YR (Constant maturity yield), CREDIT (Baa - Treasury yield), BONDPTFS, CURRPTFS, COMMPTFS (3 primitive trend-following strategies)
 - Treynor-Mazuy: RMRF, $(RMRF_t)^2$
 - Henriksson-Merton: RMRF, $(RMRF_t)^+$

### Equity Style Analysis: Beyond Performance Measurement

1. Traditional growth vs cyclical opportunities?
    - Long Term Growth IBES Means (Forecast, premium) vs EPS Growth - 5 Years (Historical)
    - **High** historical earning growth coupled with high forecasted earnings = Buying high secular growth, Exhibit greater earnings **consistency**
    - **Low** historical earning growth coupled with high forecasted earnings = Focused on expected changes in earnings, invest in highly **cyclical** companies and have more economically sensitive performance    
2. Avoid negative earnings surprise?
    - Long Term Growth IBES Means vs Negative Earnings Surprise (Earnings that fall below estimates)
    - Going extreme on high forecasted growth increased the likelihood of exposure to negative earnings surprise but also amplify the negative effects
3. **Justify** the price paid?
    - P/E (excl. negative earnings) vs Positive Earnings Surprise
    - High percentage of Negative Earnings Surprise at a given P/E ratio (no clear linear relationship) indicates the manager may be a poor judge at forecasting earnings
4. Earnings quality
    - Cash Flow 5 Yrs Growth vs EPS Growth - 5 Yrs
    - Cash Flow Growth should be close to or above its EPS Growth
5. Performance volatility
    - EPS Growth - 5 Years vs EPS Variability - 5 Years (correlated to general economic performance)
    - High EPS Variability likely suggests that performance will be highly correlated with general economic performance, and sensitive to earnings change
6. Different market environments
    - e.g. Rising/falling market, or periods that favor certain strategy
7. Multiple portfolio characteristics
8. Across multiple time periods

## Manager Selection

### Introduction

- The smaller the difference in sample size and distribution mean (doesn't make a difference whoever I hired/fired) AND the wider the dispersion of the distribution (easier to distinguish relative skill), the smaller the expected cost of Type I and Type II error.
- If manager performance is mean-reverting
    - Type I error: Reject null hypothesis of no skill
        - Hiring / retain (does not fire) a (no skill) strong performer only to see a reversion in performance        
    - Type II error: Not rejecting the null hypothesis
        - avoids hiring (skilled) managers with weak short-term track records
        - firing a poor performer only to see a reversion in performance
- Returns-based style analysis (RBSA), top-down, imprecise, not subject to window dressing
- Holdings-based style analysis (HBSA), bottom-up, style map
- Up/down capture ratio: use geometric average
- Batting average (Absolute: investment decisions, Relative: return relative to benchmark)
- Active share: $$ = \frac{1}{2}\sum_{i=1}^{N}{|w_i - W_i|}$$

### Topics


### Case Studies

### Setting Weights

- Two-step process: Investors accept beta risk, managers carry residual risk
- Risk in objective function can be: active return variance, SD, downside risk, beta, LPM
- Mean-lower partial moments (LPM): sum of squared differences below a target mean
- "Misfit" risk: delta between investor benchmarks and normal portfolio

... TODO: pure information ratio ??? ...

### Dimensions of Active Management

- Alpha forecasts can be backed out of the portfolio holdings, using reverse optimization

## Investment Performance Presentation

### GIPS Standard

- Applied on a firm-wide basis, held out to the public as a distinct business entity
- At least five-year period or since inception, build up to a minimum of 10 years
- Total firm assets:
    - Include non-discretionary (unable to fully implement) portfolio assets, and assets managed by sub-advisors that the firm has authority to select
    - NOT include advisory-only (no authority) assets, uncalled committed capital, or overlay exposure
- Prospective client (composite strategy)/investor (pooled fund): expressed interest, and qualified to invest
- May (not required) to use money-weighted return only if 1. has control over external cash flows, and 2a. portfolio is closed-end/fixed-life/fixed-commitment, or 2b. significant illiquid investments
- Composite
    - Asset-weighted average
    - May include non-fee-paying portfolios
    - NOT include non-discretionary
    - Carve-Outs: Must create a separate composite once the firm obtains standalone portfolios
    - Subscription line of credit: Not require to present returns w/o if principal was repaid within 120 days
    - Internal dispersion (high/low, interquartile range, 3Yr ann. SD), if there are 6+ portfolios
- Percentage of non-fee-paying portfolios
- Percentage of assets valued using subjective unobservable inputs
- Disclosure:
    - Significant Events: minimum of one year and as long as it is relevant to interpreting the track record
- Portability: Decision makers, process, records to support, and no break in the track record


## GIPS Standard for Firms

https://www.gipsstandards.org/wp-content/uploads/2021/03/2020_gips_standards_firms.pdf

??? The firm is not required to create a composite that includes only one or more pooled funds unless the firm offers the strategy as a segregated account.