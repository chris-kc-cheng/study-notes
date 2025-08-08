## Return Measurement




## Topics in Data Integrity

vs Custodian
1. Pricing: source
2. Missing trades: cutoff time
3. Corporate action
4. Exchange rate: time
5. OTC derivatives: missing terms, currency forward not priced by vendor
6. Expense & fees
7. Timing difference: settlement vs trade date
Action: Identify, document, implement control to alert, communicate

NAV-based and End-of-day time-weighted performance

1. Timing difference: price, FX, holdings
2. Fees: accrual frequency

Composite

## Topics in Return Attribution

Total Excess Return

```math
    \underbrace{\frac{1+R_L}{1+B_{SL}}}_{\text{Selection}}\times
    \underbrace{\frac{1+B_{SL}}{1+B_L}}_{\text{Allocation}}\times
    \underbrace{\frac{1+R}{1+R_L} \times \frac{1+B_L}{1+B}}_{\text{Naive Currency Allocation}} - 1
```


```math
    \underbrace{\frac{1+R_L}{1+B_{SL}}}_{\text{Selection}}\times
    \underbrace{\frac{1+B_{SL}}{1+B_L}}_{\text{Allocation}}\times
    \underbrace{\frac{1+R'_C}{1+B'_C}}_{\text{Currency Overlay}}\times
    \underbrace{\frac{1+R_C}{1+R'_C} \times \frac{1+B'_C}{1+B_C}}_{\text{Compounding}} - 1
```

## Fixed Income Attribution

1. Exposure Decomposition - Duration Based
2. Yield Curve Decomposition - Duration Based
3. Yield Curve Decomposition - Full Repricing