## EUR Receivable FX Hedge – Technical Specification

**Created by:** [Kristy Chung]  
**Date Created:** November 6, 2025  
**Version:** 1.0  
**LLM Used:** Claude Sonnet 4.5 (specification structure)

**Role:** Treasury Analyst  
**Audience:** CFO and Director of Treasury

**Purpose:** Provide a professional, quantitative specification outlining the analytical structure for evaluating FX hedging alternatives for a EUR 5,000,000 receivable due March 15, 2026.

---

## 1. Problem Statement

Our firm will receive **EUR 5,000,000** on **March 15, 2026** (129 days forward) as payment for delivered consulting services. This creates foreign exchange exposure: if the EUR/USD exchange rate depreciates between now and the payment date, the dollar value of our receivable will decline, potentially reducing realized revenue by hundreds of thousands of dollars.

**Exposure type:** EUR-denominated receivable  
**Time horizon:** 129 days (approximately 4.3 months)  
**Objective:** Evaluate three hedging strategies to determine the optimal approach for protecting USD value while considering cost, flexibility, and potential upside participation  
**Decision context:** Corporate treasury seeks a data-driven recommendation to present to the CFO for approval

This specification outlines the analytical framework for quantifying, comparing, and visualizing alternative hedging strategies—forward contract, money market hedge, and currency option—against an unhedged baseline. The analysis will support a management decision that balances downside protection with economic efficiency.

---

## 2. Inputs (Known Variables)

| Variable | Description | Unit | Value | Source |
|----------|-------------|------|-------|--------|
| **FC_AMT** | EUR receivable amount | EUR | 5,000,000 | Contract documentation |
| **PAY_DATE** | Payment due date | Date | March 15, 2026 | Contract documentation |
| **DAYS** | Days to maturity | Days | 129 | Calculated from today |
| **S0** | Current EUR/USD spot rate | USD/EUR | 1.0850 | Market data (Nov 6, 2025) |
| **r_USD** | USD interest rate (p.a.) | % | 4.75 | US interbank rate (FRED) |
| **r_EUR** | EUR interest rate (p.a.) | % | 3.25 | Eurozone interbank rate (ECB) |
| **FWD_PTS** | Forward points | Basis points | -25 | FX dealer quote |
| **K_CALL** | EUR call strike price | USD/EUR | 1.0850 | Set at current spot (ATM) |
| **PREM_CALL** | EUR call option premium | USD/EUR | 0.0180 | Options market quote |

**Notes:**
- All interest rates assume simple interest convention, actual/360 day-count
- Forward points represent dealer quote for 129-day forward contract
- EUR call option (equivalent to USD put) provides downside protection
- Option premium is paid upfront in USD

---

## 3. Assumptions & Constraints

To ensure clarity and reproducibility, this analysis adopts the following conventions:

1. **Interest rate basis:** Simple interest calculation using actual/360 day-count convention
2. **Interest rate parity:** Forward rate derived from spot rate and interest rate differential; assumes market efficiency
3. **Money market access:** Firm can borrow EUR and invest USD at quoted interbank rates without credit spread or margin requirements
4. **Option structure:** European-style EUR call option exercisable only at maturity; premium paid upfront in USD
5. **Exchange rate convention:** All rates expressed as USD per EUR (direct quote from US perspective)
6. **Transaction costs excluded:** Analysis excludes bid-ask spreads, broker commissions, and administrative fees
7. **Single evaluation date:** Outcomes measured only at payment date (March 15, 2026); no interim mark-to-market analysis
8. **Tax neutrality:** Hedge gains and losses treated identically for corporate tax purposes
9. **No credit risk:** Assumes all counterparties (banks, dealers) fulfill contractual obligations

These assumptions allow for analytical clarity while noting that real-world implementation would require adjustment for transaction costs and credit considerations.

---

## 4. Calculation Flow

The analysis follows a four-strategy comparison structure, each with distinct logic:

### **4.1 Forward Contract Hedge**

**Step 1:** Calculate the forward exchange rate using interest rate parity
- Multiply current spot rate by (1 + r_USD × days/360)
- Divide by (1 + r_EUR × days/360)
- This gives the no-arbitrage forward rate for the 129-day horizon

**Step 2:** Lock in USD proceeds
- Multiply EUR receivable amount by the calculated forward rate
- This represents guaranteed USD proceeds regardless of future spot rate

**Step 3:** Compare against spot scenarios
- Calculate what USD proceeds would be at various future spot rates
- Identify the "opportunity cost" if EUR strengthens beyond forward rate

**Step 4:** Document certainty benefit
- Forward eliminates all FX risk but also removes upside potential

### **4.2 Money Market Hedge**

**Step 1:** Calculate present value of EUR receivable
- Discount EUR 5,000,000 using EUR interest rate over 129 days
- Formula: EUR_AMT / (1 + r_EUR × days/360)
- This determines how much EUR to borrow today

**Step 2:** Borrow EUR today
- Borrow the PV amount calculated in Step 1 at EUR interest rate
- At maturity, the EUR 5,000,000 receivable will exactly repay this loan

**Step 3:** Convert borrowed EUR to USD immediately
- Exchange the borrowed EUR at current spot rate (S0)
- This locks in today's exchange rate for the synthetic hedge

**Step 4:** Invest USD proceeds
- Invest converted USD at USD interest rate for 129 days
- Calculate maturity value: USD_invested × (1 + r_USD × days/360)

**Step 5:** Verify at maturity
- EUR receivable pays off EUR loan (principal + interest = EUR 5,000,000)
- USD investment matures to final proceeds
- Confirm this matches forward hedge outcome (validates IRP)

### **4.3 Currency Option Hedge**

**Step 1:** Purchase EUR call option (USD put equivalent)
- Strike price: 1.0850 (at-the-money, equal to current spot)
- Premium: 0.0180 USD per EUR
- Total premium cost: EUR 5,000,000 × 0.0180 = USD 90,000

**Step 2:** Pay premium upfront
- Premium paid today reduces net proceeds regardless of outcome
- This is the "insurance cost" for downside protection

**Step 3:** Evaluate at maturity based on realized spot rate (S_T)
- **If S_T < 1.0850 (EUR weakens):** Exercise option
  - Convert EUR at protected strike rate of 1.0850
  - USD proceeds = EUR 5,000,000 × 1.0850 = USD 5,425,000
- **If S_T ≥ 1.0850 (EUR strengthens):** Let option expire
  - Convert EUR at favorable market spot rate S_T
  - USD proceeds = EUR 5,000,000 × S_T
  - Capture upside while protected on downside

**Step 4:** Calculate net proceeds
- Subtract upfront premium from conversion proceeds
- Net USD = Gross conversion proceeds - USD 90,000

**Step 5:** Determine breakeven spot rate
- Find S_T where option hedge net proceeds equal unhedged proceeds
- Breakeven occurs when upside gain offsets premium cost

### **4.4 Unhedged Baseline**

**Step 1:** Wait until payment date (March 15, 2026)
- Take no hedging action today
- Accept full exposure to spot rate movements

**Step 2:** Convert at realized spot rate
- USD proceeds = EUR 5,000,000 × S_T (whatever the future spot rate is)
- Maximum upside potential but also maximum downside risk

**Step 3:** Use as benchmark
- Compare all hedged outcomes against this unhedged result
- Quantifies the value (or cost) of each hedging strategy

**Sequencing note:** All calculations reference the same base inputs. Option and money market hedges are compared against the forward contract to assess relative value and trade-offs.

---

## 5. Outputs

The model will generate the following decision-support outputs:

| Output | Description | Format | Purpose |
|--------|-------------|--------|---------|
| **USD_FORWARD** | Locked USD proceeds from forward | Numeric | Certainty benchmark |
| **FWD_RATE** | Calculated forward exchange rate | Numeric | Validate IRP and dealer quote |
| **USD_MM** | USD proceeds from money market hedge | Numeric | Cross-check vs. forward |
| **USD_OPTION** | Net USD proceeds from option hedge | Table (by S_T) | Downside protection analysis |
| **USD_UNHEDGED** | Unhedged USD proceeds | Table (by S_T) | Baseline comparison |
| **BREAKEVEN_OPT** | Spot rate where option equals unhedged | Numeric | Decision threshold |
| **SCENARIO_TABLE** | Comparative proceeds across spot scenarios | Table | Side-by-side evaluation |
| **PAYOFF_CHART** | Hedge outcomes vs. future spot rate | Line chart | Visual strategy comparison |
| **SUMMARY_TABLE** | Strategy ranking by criteria | Matrix | Executive decision support |
| **RECOMMENDATION** | Written analysis with rationale | 2-3 paragraphs | CFO-ready summary |

**Visualization specifications:**
- **Payoff chart:** X-axis shows future spot rates from 1.0000 to 1.1500; Y-axis shows USD proceeds; four lines (forward, money market, option, unhedged)
- **Annotations:** Mark current spot, forward rate, and option breakeven point
- **Decision matrix:** Rank strategies by downside protection, cost, and flexibility

---

## 6. Sensitivity Plan

To assess hedge robustness across plausible FX scenarios, the model will test outcomes at varying future spot rates:

### **6.1 Primary Scenario Analysis**
- **Range:** Future spot rates (S_T) from 1.0000 to 1.1500 USD/EUR
- **Increment:** 0.0050 (50 basis points)
- **Total scenarios:** 11 discrete rate points
- **Coverage:** Captures ~8% depreciation to ~6% appreciation from current spot

**Scenario interpretation:**
- **1.0000 (worst case):** EUR depreciates ~7.8% → tests downside protection
- **1.0850 (neutral):** No change from current spot → baseline
- **1.1500 (best case):** EUR appreciates ~6.0% → tests upside participation

### **6.2 Secondary Sensitivities** (optional extensions)
- **Interest rate shock:** Adjust r_USD and r_EUR by ±50 bps to test forward rate sensitivity
- **Option premium variation:** Model option hedge if premium increases 20% or 50% (volatility spike scenario)
- **Time decay:** Illustrate option value erosion if decision delayed by 30 days

### **6.3 Visualization Approach**
1. Generate table showing USD proceeds for all four strategies across 11 spot scenarios
2. Create line chart overlaying all strategies with future spot on X-axis
3. Highlight regions where each strategy dominates
4. Add conditional formatting to identify optimal strategy per scenario

---

## 7. Limitations & Next Steps

### **7.1 Analytical Limitations**

This specification intentionally excludes certain factors to maintain analytical focus:

- **Transaction costs:** Bid-ask spreads (typically 1-3 pips for EUR/USD) would reduce proceeds by approximately $5,000-$15,000; excluded for strategy comparison clarity
- **Counterparty credit risk:** Assumes no dealer default; real hedges require credit assessment
- **Dynamic hedging:** Static analysis at maturity only; no adjustment strategy or interim rebalancing
- **Volatility surface:** Option pricing uses flat premium; actual pricing reflects strike and maturity structure
- **Alternative structures:** Collars, range forwards, and participating forwards not evaluated
- **Portfolio effects:** Single-transaction analysis; no consideration of natural hedges from other FX exposures
- **Accounting treatment:** GAAP hedge accounting qualification not addressed

### **7.2 Stage 3 Implementation Preview**

The next phase will construct an Excel-based decision model that operationalizes this specification:

1. **Input dashboard:** Centralized input cells for all variables in Section 2, enabling scenario updates
2. **Calculation engine:** Formulas implementing each hedge type per Section 4 logic
3. **Scenario generator:** Data table automatically computing proceeds across spot rate range
4. **Visualization suite:** Dynamic charts updating with input changes
5. **Decision output:** Summary table and recommendation text for management presentation

This specification provides the complete technical blueprint for building a production-ready FX hedge evaluation tool that treasury can deploy for recurring foreign currency exposures.

---

**End of Specification**
