## FX Hedge Model Technical Specification

**Prepared by:** [Kristy Chung]  
**Date:** November 6, 2025  
**Subject:** EUR Receivable Hedge Analysis – Technical Specification

---

## 1. Problem Statement

Our firm will receive **EUR 5,000,000** on **March 15, 2026** (129 days forward) as payment for delivered consulting services. This exposure creates FX risk: if the EUR/USD exchange rate depreciates between today and the payment date, the dollar value of our receivable will decline. Management seeks to evaluate three hedging strategies—forward contract, money market hedge, and currency option—to determine the optimal approach for locking in value while considering cost, flexibility, and downside protection.

The model must quantify expected USD proceeds, breakeven exchange rates, and net outcomes across a range of future spot rates to support a data-driven hedging decision.

---

## 2. Inputs (Known Variables)

| Variable | Value | Unit | Source |
|----------|-------|------|--------|
| **Exposure amount** | 5,000,000 | EUR | Contract documentation |
| **Payment date** | March 15, 2026 | Date | Contract documentation |
| **Current spot rate** | 1.0850 | USD/EUR | Market data (Nov 6, 2025) |
| **Days to maturity** | 129 | Days | Calculated |
| **EUR interest rate** | 3.25% | % per annum | Eurozone interbank rate (ECB) |
| **USD interest rate** | 4.75% | % per annum | US interbank rate (FRED) |
| **Forward points** | -25 | Basis points | FX dealer quote |
| **Call option premium** | 0.0180 | USD per EUR | Options market quote |
| **Option strike price** | 1.0850 | USD/EUR | At-the-money (ATM) strike |

All interest rates assume simple interest convention for consistency with short-term money market instruments. Transaction costs (e.g., bid-ask spreads, commissions) are excluded for analytical clarity but noted as a limitation.

---

## 3. Assumptions & Constraints

- **Interest rate basis:** Simple interest, actual/360 day-count convention
- **Forward rate calculation:** Interest rate parity holds; forward rate = spot × (1 + r_USD × days/360) / (1 + r_EUR × days/360)
- **Money market execution:** Firm can borrow EUR and invest USD at quoted interbank rates with no credit spread
- **Option mechanics:** European-style call option (exercisable only at maturity); premium paid upfront in USD
- **No transaction costs:** Excludes bid-ask spreads, broker fees, and margin requirements
- **Single scenario horizon:** Model evaluates outcomes at payment date only; no interim mark-to-market or early termination scenarios
- **Tax neutrality:** Hedge gains/losses treated identically for tax purposes

---

## 4. Calculation Flow

### **4.1 Forward Contract Hedge**
1. Calculate forward rate using interest rate parity formula
2. Lock in USD proceeds = EUR amount × forward rate
3. Compare locked proceeds to unhedged outcome at various future spot rates
4. Compute opportunity cost if EUR strengthens beyond forward rate

### **4.2 Money Market Hedge**
1. Determine present value of EUR receivable by discounting at EUR interest rate
2. Borrow this PV amount in EUR today at EUR interest rate
3. Convert borrowed EUR to USD at current spot rate
4. Invest USD proceeds at USD interest rate until payment date
5. At maturity: EUR receivable repays EUR loan principal + interest; USD investment matures
6. Calculate net USD proceeds and compare to forward hedge

### **4.3 Currency Option Hedge**
1. Purchase EUR call option (USD put) at ATM strike equal to current spot rate
2. Pay upfront premium in USD (EUR amount × premium per unit)
3. At maturity, evaluate intrinsic value:
   - If spot > strike: exercise option, convert at strike rate
   - If spot ≤ strike: let option expire, convert at spot rate
4. Calculate net USD proceeds = conversion proceeds - option premium cost
5. Determine breakeven spot rate where option hedge equals unhedged outcome

### **4.4 Unhedged Baseline**
1. Convert EUR receivable at future spot rate on payment date
2. USD proceeds = EUR amount × future spot rate
3. Serves as benchmark for evaluating hedge effectiveness

---

## 5. Outputs

### **5.1 Summary Metrics Table**
- **Hedged USD proceeds** for each strategy
- **Effective exchange rate** (USD proceeds / EUR amount)
- **Cost of hedge** (premium paid or opportunity cost vs. unhedged)
- **Breakeven exchange rates** for option strategy

### **5.2 Scenario Analysis Table**
- Future spot rates ranging from 1.0000 to 1.1500 (50-pip increments)
- USD proceeds for each strategy at each spot rate
- Best-performing strategy identified per scenario

### **5.3 Visualizations**
- **Payoff diagram:** Line chart showing USD proceeds (y-axis) vs. future spot rate (x-axis) for all four strategies
- **Hedge effectiveness:** Bar chart comparing locked-in proceeds across strategies
- **Downside protection comparison:** Highlighting floor values and upside participation

### **5.4 Decision Matrix**
- Rank strategies by: (1) downside protection, (2) cost efficiency, (3) flexibility
- Management recommendation with supporting rationale

---

## 6. Sensitivity Plan

### **6.1 Exchange Rate Scenarios**
Test model across 12 future spot rates (1.0000 to 1.1500 in 50-pip increments) to capture:
- **Worst-case depreciation** (EUR weakens to 1.0000)
- **Expected case** (forward rate as unbiased predictor)
- **Best-case appreciation** (EUR strengthens to 1.1500)

### **6.2 Interest Rate Sensitivity**
Secondary analysis: adjust EUR and USD rates by ±50 bps to assess impact on forward rate and money market hedge outcomes.

### **6.3 Option Premium Sensitivity**
Test option hedge viability if premium increases by 20% or 50% to reflect volatility shocks.

### **6.4 Visualization Approach**
- **Primary chart:** Overlay all four strategies on single payoff diagram with future spot rate on x-axis (1.00–1.15) and USD proceeds on y-axis
- **Annotation:** Mark forward rate, current spot, and breakeven points
- **Color coding:** Distinct colors for each strategy with legend

---

## 7. Limitations & Next Steps

### **7.1 Limitations**
- **Transaction costs excluded:** Real-world bid-ask spreads (typically 1-3 pips for EUR/USD) would reduce net proceeds by approximately $5,000-$15,000
- **Counterparty risk ignored:** Model assumes dealers fulfill forward and option contracts without default
- **Static analysis:** No consideration of dynamic hedging, portfolio effects, or hedging in tranches
- **Simplified option structure:** American options, exotic structures (collars, range forwards), and volatility surfaces not evaluated
- **Single time horizon:** Interim cash flow needs and mark-to-market P&L not modeled

### **7.2 Stage 3 Excel Build Preview**
The Stage 3 deliverable will operationalize this specification by:
1. Building a dynamic Excel model with input cells for all variables
2. Implementing formulas for each calculation flow section
3. Creating scenario analysis with data tables
4. Generating publication-quality charts for the payoff diagram
5. Adding conditional formatting to highlight optimal strategies by scenario

This specification provides the blueprint for constructing a hedge evaluation tool that treasury can use for recurring FX exposures.

---

**End of Specification**
