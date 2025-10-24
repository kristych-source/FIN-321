# MEMORANDUM: Foreign Exchange Hedging Strategy for EUR Receivable

**Created by:** Kristy Chung  
**Date Created:** October 23, 2025  
**Version:** 1.0  
**LLM Used:** Claude Sonnet 4.5

---

## Executive Summary

Our firm faces foreign exchange exposure on a €12,500,000 receivable due in one year. At the current spot rate of 1.1607 EURUSD, this translates to approximately $14.5 million. However, euro depreciation could significantly reduce our USD proceeds. I recommend we evaluate three hedging families—forward contracts, money market hedges, and options—to mitigate this risk. Preliminary analysis suggests a forward contract may provide the most cost-effective protection, though options offer greater flexibility if euro strengthening is anticipated. In Stages 2–3, I will build a quantitative model to compare these strategies and recommend an optimal hedge.

---

## Background & Objectives

Our firm expects to receive €12,500,000 from a European client in exactly one year. This creates **translation risk**: if the euro weakens against the dollar during this period, we will receive fewer USD than currently anticipated. Given current volatility in EUR/USD markets and diverging monetary policies between the Federal Reserve (policy rate: 4.25%) and the European Central Bank (deposit rate: 2.00%), this exposure warrants careful management.

**Primary Objective:** Determine the most cost-effective hedging strategy to lock in favorable USD proceeds while maintaining acceptable flexibility.

**Secondary Objective:** Build a replicable framework for evaluating future FX exposures across multiple currencies and time horizons.

---

## Methods

### **Exposure Details**
- **Currency:** EUR (euro)
- **Amount:** €12,500,000
- **Timing:** Payment due in 1 year (October 23, 2026)
- **Current Spot Rate:** 1.1607 EURUSD
- **Expected USD Proceeds (unhedged):** ~$14.5 million at current spot

### **Risk Assessment**
Without hedging, our USD proceeds are vulnerable to euro depreciation. If EURUSD falls to 1.05 (a 9.5% decline from current levels), we would receive only $13.1 million—a loss of $1.4 million relative to current expectations. Given the ECB's accommodative policy stance and potential eurozone growth concerns, downside risk is material.

### **Hedge Family Evaluation**

#### **1. Forward Contract**
Lock in the 1-year forward rate of 1.0910 EURUSD today, guaranteeing $13.64 million in proceeds.

**Pros:**
- Eliminates FX uncertainty entirely
- No upfront premium cost
- Simple execution and accounting treatment

**Cons:**
- Foregoes gains if euro strengthens above 1.0910
- No flexibility to capitalize on favorable movements

---

#### **2. Money Market Hedge**
Borrow EUR today at the euro interest rate (2.15%), convert to USD at spot (1.1607), and invest at the USD rate (3.55%) for one year.

**Pros:**
- Replicates forward contract economics synthetically
- May offer pricing advantages if forward markets are illiquid
- Creates natural hedge using balance sheet positions

**Cons:**
- Requires borrowing capacity and credit lines
- More complex execution with multiple transactions
- May incur transaction costs that erode value

---

#### **3. Currency Options (Put Option on EUR)**
Purchase a EUR put option with strike price at or near current forward rate (K = 1.0910), premium = $0.017 per EUR.

**Pros:**
- Provides downside protection while preserving upside participation
- Flexibility to let option expire if euro strengthens
- Useful if we expect euro volatility or potential appreciation

**Cons:**
- Upfront premium cost of $212,500 (€12.5M × $0.017)
- Reduces effective proceeds by premium amount
- More expensive than forward if euro depreciates as expected

---

## Limitations & Next Steps

**Limitations:**
- Analysis assumes rates and forward quotes remain stable; actual execution prices may differ
- Does not incorporate credit risk, counterparty risk, or accounting implications (FASB ASC 815)
- Options analysis simplified; actual strategy may require collars or risk reversals
- Excludes transaction costs, bid-ask spreads, and margin requirements

**Next Steps:**

1. **Technical Specification** (Stage 2): Develop a detailed spreadsheet model specification including:
   - Input parameters (spot rate, forward rate, interest rates, option strikes/premiums, receivable amount)
   - Calculation logic for each hedge strategy's USD proceeds under various EURUSD scenarios (range: 1.00 to 1.25)
   - Output metrics: net USD proceeds, opportunity cost, hedge effectiveness ratio

2. **Excel Model Build** (Stage 2): Implement the specification in Excel with scenario analysis, breakeven calculations, and sensitivity tables showing how each hedge performs across different spot rates at maturity.

3. **Prompt Engineering** (Stage 2): Create a natural language prompt that instructs an AI assistant to generate the hedge comparison model given only the key inputs, ensuring reproducibility for future FX exposures.

4. **Final Analysis & Recommendation** (Stage 3): Use the model to evaluate all three strategies under baseline, optimistic, and pessimistic EUR scenarios, then recommend the optimal hedge based on risk tolerance and cost-benefit analysis.

**Responsible Parties:** Treasury team (model development), CFO (final approval), Finance Operations (execution)

---

## References

- Federal Reserve H.15 Selected Interest Rates (October 23, 2025)
- European Central Bank Monetary Policy Decisions (September 11, 2025)
- Bloomberg FX Forward Quotes (October 23, 2025)
- FASB ASC Topic 815: Derivatives and Hedging (accounting guidance)
