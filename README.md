# Cheat Sheet for the CIPM Program

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
    1. COnduct as Participants in CFA Institute Programs
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

Notional return = (Total margin receipt + notional income) / Actual economic exposure

For notional return calculation, the denominator is always positive regaredless the futures are long or short.

#### Forwards

The value of a long forward investment at time $t_1$

```math
    (F_{t_1} - F_{t_0}) \frac{1}{(1 + r_{fin})^{T-t_1}}
```

Notional return: Similar to futures, but the value need to be discounted.

#### Options

```math
    NE = \text{Sign} \times \delta \times \text{Number of contracts} \times \text{Contract value multiplier} \times \text{Price underlying}
```

Notional cash expsoure is the difference between the cost and notional exposure of the options.

Covered interest rate parity

```math
    F_0 = S_0\frac{1+r_{FC}}{1+r_{DC}}
```
where $F_0$ and $S_0$ are quoted in $\frac{FC}{DC}$.

#### Cost of hedging

- Spot currency return = $\frac{S_1}{S_0} - 1$
- Forward return = $\frac{S_1}{F_0} - 1$
- Forward currency premium = $\frac{F_0}{S_0} - 1$

Note: Positive forward currency trades at a premium, and forward return is worse than spot return if interest rates in the "nominator" currency is higher.

- Base currency return = $\frac{MV / S_1}{MV / S_0} - 1$
- Currency overlay return = $\frac{MV / F_0 - MV / S_1}{MV / S_0}$
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

1. Accuracy: avoid doubl counting, discretionary status, change/move
2. Completeness: data, details on discretion and disclosure, why not assigned
3. COnformity: CIPS standard oversight committee
4. Timeliness: assign, disclosure

## Performance Attribution

Valid benchmark "SAMURAI"

1. Specified in advance
2. Appropriate
3. Measurable
4. Unambiguous
5. Reflective of current investment opinions
6. Accountable
7. Investible

- Published benchmark-centered (PBC): P = M + A, (B = M)
- Manager strategy (MS): P = M + S + A

### Topics in Return Attribution

#### Brinson-Fachler Arithmetic Attribution

- Allocation $A_i = (w_i - W_i)(B- B_i)$, where $B = \sum^n_{i=1}W_iB_i$
- Selection $S_i = w_i(R_i - B_i)$

#### Options

- Total portfolio return = (Stock PnL + Option PnL + Gain on cash) / Total portfolio before adjustment
- Equity return = (Stock PnL + Option PnL + Interest on notional cash) / Combined equity exposure

Note: Interest on notional cash = Notional asset x Cash return. It can be negative in notional asset is negative.

#### Karnosky and Singer Multi-currency Attribution

Step 1
```math
    R = \sum_{i=1}^n{w_i(R_{Li}-I_i)} + \sum_{i=1}^n{(w_i + \tilde{w_i})(C_i+I_i)}
```
```math
    B = \underbrace{\sum_{i=1}^n{W_i(B_{Li}-I_i)}}_{B_L} + \underbrace{\sum_{i=1}^n{(W_i + \tilde{W_i})(C_i+I_i)}}_{C}
```
Step 2

Allocation
```math
    A_i = (w_i - W_i)(B_{Li} - I - B_L)
```

Selection
```math
    S_i = w_i(R_{Li} - B_{Li})
```

Currency allocation
```math
    CA_i = [(w_i + \tilde{w_i}) - (W_i + \tilde{W_i}))] \times (C_{i} + I - C)
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

- Allocation = $(W_{p,DB} - W_{b,DB}) \times R_{b,GDB}$
  - Total Interest Rate Allocation = Duration Effect + Curve Effect
  - Duration Effect = $\text{Duration return}_{p,DB} \times W_{p,DB} - \text{Duration return}_{b,DB} \times W_{b,DB}$
    - Duration Return = Zero-duration RFR + (Duration x Excess return per year)
- Sector allocation = ${(W_{ps} - W_{bs}) \times (R_{b,SDB} - R_{b,GDB})}$, always zero for government bonds
- Bond selection = $W_{ps} \times (R_{p,SDB} - R_{b,SDB})$, for both government and corporate bonds

#### Yield Curve Decomposition - Duration Based

- Passage of time
  - Initial yield = $Y \times \Delta t$
  - Roll down = $-D \times \Delta Y^{Roll} + \frac{1}{2} \times C \times (\Delta Y^{Roll})^2$
- Curve variation
  - Shift = $-D \times \Delta Y^{Shift} + \frac{1}{2} \times C \times (\Delta Y^{Shift})^2$
  - Slope = $-D \times \Delta Y^{Slope} + \frac{1}{2} \times C \times (\Delta Y^{Slope})^2$
  - Curvation = $-D \times \Delta Y^{Shape} + \frac{1}{2} \times C \times (\Delta Y^{Shape})^2$
- Spread variation
  - Sector = $-D \times \Delta Y^{Systematic} + \frac{1}{2} \times C \times (\Delta Y^{Systematic})^2$
  - Specific = $-D \times \Delta Y^{Specific} + \frac{1}{2} \times C \times (\Delta Y^{Specific})^2$

Note: Residual = Actual return - Estimated return

#### Yield Curve Decomposition - Full Repricing

- Passage of time
  - Coupon: $Return = \frac{Coupon}{P_T}$
  - Amortization: Using the same set of spot rates, less time to maturity
    - For bonds priced at a prmium (i.e. coupon rates are higher than market rates), prices converge (i.e. drop) toward par value as time goes by.
  - Roll down: Using the same set of spot rates but rolled down to **lower discount rates**
- Yield curve movements
  - Shift
  - Slope
  - Curvation
- Spread variation
  - Systematic
  - Specific

Note: No residual

## Performance Appraisal

## Manager Selection

## Investment Performance Presentation



## GIPS Standard