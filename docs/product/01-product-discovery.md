# Product Discovery

## 1. Product Vision

AssetOps is a personal digital asset portfolio and trade management application designed to provide a centralized and structured way to manage the complete trading lifecycle, from portfolio monitoring and trade analysis to transaction planning and execution.

The product aims to reduce the manual effort and operational friction involved in managing digital asset trades, improve visibility into portfolio positions and their evolution over time, and enable faster execution of trading strategies based on reliable account, transaction, fee, and market data.

In its current implementation, AssetOps is built on ServiceNow and integrated with Mercado Bitcoin for personal use. The product concept, however, is independent from this implementation architecture and could evolve to support a broader audience through a different technology stack.

AssetOps combines three core product areas: portfolio management, trade management, and trade planning and analysis.

The initial product will focus on consolidating information, supporting analysis, and improving the management of trading activities. Future capabilities may introduce user-defined rule-based automation, allowing AssetOps to execute predetermined actions when explicitly configured conditions are met.

In a longer-term horizon, autonomous decision-making based on market conditions and risk analysis may be explored. This remains a future product hypothesis and is not part of the current product scope.

---

## 2. Problem Statement

The primary user performs recurring buy and sell operations on Mercado Bitcoin with the goal of achieving a positive net result across each trade cycle.

To plan a trade, the user needs to understand the complete financial context of the operation, including the effective acquisition cost, available asset quantity, trading fees, potential residual balances (dust), target selling price, and expected net result after the transaction.

Although the trading activity itself takes place on Mercado Bitcoin, the information required to evaluate the complete trade cycle is not currently available to the user in a sufficiently consolidated and actionable view. As a result, the user relies on a manually maintained spreadsheet to combine transaction data and perform the calculations required to plan and evaluate trades.

This fragmented process makes it difficult to confidently determine the expected net result of a transaction before executing it. The manual process requires the user to maintain transaction data and calculations outside the exchange. This creates additional reconciliation effort and introduces potential risks of outdated information, calculation errors, and differences between expected and actual results after fees, quantity adjustments, precision, and rounding are considered.

The core problem is therefore not simply the amount of manual work involved, but the **lack of a consolidated and reliable view of the information required to evaluate and manage a complete trade cycle with confidence.**

---

## 3. Target User

### 3.1 Primary User

The initial primary user of AssetOps is the product creator herself, an active Mercado Bitcoin user who is currently learning and experimenting with short-term digital asset trading.

The current implementation is designed around this user's personal workflow and should not assume that the same behaviors, needs, or trading practices apply to all Mercado Bitcoin users or digital asset traders.

A broader target audience may be explored in the future if the product evolves beyond its current personal-use and ServiceNow-based implementation.

### 3.2 Trading Behavior

The user monitors the market daily and performs recurring buy and sell operations, primarily using limit orders with post-only execution in an attempt to reduce trading fees.

The user currently experiments with short-term price movements by observing recent and historical price ranges and positioning buy and sell orders based on her interpretation of those movements.

After completing a sell transaction, the user commonly continues trading the same asset by considering a new buy order, creating recurring trade cycles.

Order execution notifications received by email currently act as the main trigger for reviewing the completed transaction and planning the next action.

### 3.3 Goals and Decision-Making Context

The user seeks to achieve a positive net result after trading fees and attempts to maximize the return of each trade when market conditions allow.

In the current workflow, even a small positive net result may be considered acceptable. The user reports that recent trades commonly involve relatively small returns, often around 1–2%, although this is an observed behavior rather than a fixed product requirement or guaranteed outcome.

The user does not currently follow a formal or validated methodology for selecting assets or determining entry points. Initial asset purchases have largely been exploratory. Current decisions are informed by observing price charts, recent price movements, and historical minimum and maximum values.

Once capital has been allocated to an asset, the user commonly continues buying and selling that same asset across subsequent trade cycles.

### 3.4 Primary User Need

During a trade cycle, the user needs to evaluate market conditions and understand how different entry and exit prices affect the expected net result of the operation so that she can choose where to position buy and sell orders with greater confidence.

This requires visibility into the financial context of the trade, including asset quantities, acquisition costs, trading fees, expected proceeds, and the potential net result of different transaction scenarios.

---

## 4. Current Workflow (As-Is)

The user's current trading workflow is a recurring process distributed across Mercado Bitcoin, email notifications, and a manually maintained spreadsheet.

The spreadsheet is used primarily for planning, estimating, and recording trades. It is not considered a fully reliable source of truth for transaction values because calculated values may differ from those presented by Mercado Bitcoin.

When differences are identified before submitting an order, the user generally treats the values presented by Mercado Bitcoin as authoritative and manually transfers them back into the spreadsheet.

### 4.1 Market Observation and Buy Planning

Before creating a buy order, the user reviews the asset's price chart across multiple time horizons.

The user typically observes:

- Months.
- Weeks.
- Days.
- Three-hour intervals.
- One-hour intervals.
- Fifteen-minute intervals.
- One-minute intervals.

Particular attention is given to recent price oscillations and perceived local lows and highs.

The user does not currently use a formal or validated methodology to determine an entry price. Chart observation is used as an informal decision-support process for choosing a potential buy price.

Once a potential buy price has been selected, the user creates a planned buy transaction in the spreadsheet before submitting the actual order to Mercado Bitcoin.

### 4.2 Buy Calculation and Order Creation

The user currently experiments with predetermined BRL transaction amounts.

Recent experiments have involved progressively increasing transaction amounts over fixed periods, such as approximately BRL 1, BRL 2, and potentially BRL 3 per transaction.

These amounts represent the user's current experimental trading behavior and are not fixed business rules.

Using the intended BRL amount and selected asset price, the user uses spreadsheet calculations to estimate:

- Asset quantity.
- Trading fee.
- Total transaction value.
- Other calculated values required to represent the planned purchase.

The resulting values may contain multiple decimal places and may not exactly reproduce the values accepted or calculated by Mercado Bitcoin.

The user then creates the corresponding order in Mercado Bitcoin, normally using:

- Limit Order.
- Post Only.

Post-only execution is currently preferred in an attempt to obtain the applicable maker fee rather than a higher-cost execution type.

Before confirming the order, the user compares the values calculated in the spreadsheet with those displayed by Mercado Bitcoin.

Potential differences may occur in:

- Price.
- Asset quantity.
- Trading fee.
- Total transaction value.
- Decimal precision.

When a difference is identified, the user manually copies the value presented by Mercado Bitcoin into the spreadsheet before submitting the order.

The exact cause of these differences has not yet been validated.

### 4.3 Buy Order Execution

After the buy order has been submitted, the user waits for execution.

An email notification from Mercado Bitcoin currently acts as the primary trigger informing the user that the order has completed.

After receiving the notification, the user:

1. Opens the previously created buy row in the spreadsheet.
2. Changes the transaction status to executed.
3. Records the execution date.

Price, quantity, fee, and total transaction values were generally already recorded during order planning and reconciliation before the order was submitted.

The user does not currently perform a systematic post-execution reconciliation of all spreadsheet values against actual execution data.

### 4.4 Sell Planning

After a buy order has executed, the user creates a new planned sell row in the spreadsheet.

The spreadsheet uses information from the corresponding purchase as the starting point for estimating a potential sale.

The current calculation process is approximately:

1. Start with the asset quantity associated with the purchase.
2. Subtract the asset-denominated buy fee to estimate the quantity available for sale.
3. Use the resulting quantity as the planned sell quantity.
4. Initially use the purchase price as a reference sell price.
5. Estimate the BRL-denominated selling fee.
6. Calculate the estimated total proceeds from the sale.
7. Compare the estimated sale proceeds with the total BRL cost of the purchase.
8. Calculate the estimated monetary result.
9. Calculate the estimated percentage result.
10. Incrementally increase the proposed selling price until the spreadsheet estimates at least a small positive net result.

The user may select a higher target selling price when current market conditions appear to support a larger potential return.

The spreadsheet therefore acts as a scenario and estimation tool rather than an authoritative representation of the final transaction.

### 4.5 Sell Order Creation and Quantity Reconciliation

The user generally intends to sell 100% of the available position associated with the trade.

However, the quantity calculated by the spreadsheet after subtracting the estimated or recorded purchase fee does not always match the quantity that Mercado Bitcoin presents when the user selects 100% of the available asset balance.

When this occurs, the user:

1. Selects 100% of the available balance in Mercado Bitcoin.
2. Copies the resulting quantity into the spreadsheet.
3. Allows the spreadsheet to recalculate the estimated fees, proceeds, and result.
4. Continues comparing values between the spreadsheet and Mercado Bitcoin.
5. Uses Mercado Bitcoin values when the two sources cannot be reconciled.

The user has observed residual-balance and quantity discrepancies but does not currently have a validated explanation for their cause.

Potential causes such as precision, rounding, fees, or exchange rules remain hypotheses to be investigated separately.

### 4.6 Sell Order Execution

After submitting the sell order, the user waits for execution.

When the execution email is received, the user:

1. Opens the corresponding sell row in the spreadsheet.
2. Records the execution date.
3. Changes the transaction status to executed.
4. Creates a new planned buy row for the same asset.
5. Begins observing the market again to determine a potential new entry price.

The spreadsheet calculates an estimated monetary and percentage result for the completed trade cycle.

However, the user does not currently have an independent and reliable method for reconciling the spreadsheet's calculated result against the actual complete financial result of the trade.

The user therefore cannot currently confirm with confidence whether the calculated net result exactly matches the realized result after all exchange calculations, fees, quantity adjustments, precision, and rounding are considered.

### 4.7 Open Order Reassessment and Replacement

If an order remains open longer than expected, the user may reassess it.

There is currently no fixed time threshold or formal rule that determines when an order should be cancelled.

The decision is based on a combination of:

- How long the order has remained open.
- Current and recent asset prices.
- Chart observation.
- The originally targeted return.
- Previous executions at similar target returns.
- The user's judgment.

For a sell order, the user may return to the spreadsheet and reduce the expected profit margin while still attempting to maintain a positive estimated result.

The user then:

1. Recalculates the trade scenario in the spreadsheet.
2. Cancels the existing Mercado Bitcoin order.
3. Creates a replacement order using the revised values.

The relationship between cancelled and replacement orders is not currently formally tracked beyond the spreadsheet workflow.

### 4.8 Partial Executions

The user has observed a partial execution at least once.

In that case, no manual intervention was performed.

The order remained in an executing state and the user waited until the remaining quantity was executed.

Because the user's current transaction amounts are small, partial executions have not yet been a frequent part of the observed workflow.

The user does not currently have a defined process for handling an order that remains partially executed for an extended period.

### 4.9 Current Trade Cycle

The current end-to-end process can therefore be represented as:

Market Observation  
→ Buy Price Selection  
→ Planned Buy in Spreadsheet  
→ Buy Calculation  
→ Mercado Bitcoin Order Configuration  
→ Spreadsheet / Exchange Reconciliation  
→ Limit + Post-Only Buy Order  
→ Wait for Execution  
→ Email Notification  
→ Spreadsheet Status / Date Update  
→ Planned Sell Creation  
→ Sell Scenario Calculation  
→ Sell Quantity Reconciliation  
→ Mercado Bitcoin Order Configuration  
→ Limit + Post-Only Sell Order  
→ Wait for Execution  
→ Email Notification  
→ Spreadsheet Status / Date Update  
→ Estimated Trade Result  
→ New Buy Planning  
→ Repeat

Open orders may branch into:

Open Order  
→ Market Reassessment  
→ Spreadsheet Recalculation  
→ Cancellation  
→ Replacement Order

Partial executions currently branch into:

Partial Execution  
→ Wait for Remaining Execution  
→ Full Execution

### 4.10 Systems Currently Used

The workflow currently depends on three systems:

**Mercado Bitcoin**

Used for:

- Market and chart observation.
- Actual order configuration.
- Order submission.
- Order cancellation.
- Available-balance verification.
- Final pre-submission transaction values.
- Order execution.

When spreadsheet estimates and Mercado Bitcoin values differ during order creation, the user currently treats Mercado Bitcoin's displayed values as authoritative.

**Email**

Used primarily as the trigger informing the user that an order has executed and that the next step in the trade cycle should begin.

**Spreadsheet**

Used for:

- Planned transaction creation.
- Buy and sell calculations.
- Fee estimation.
- Quantity estimation.
- Transaction status tracking.
- Execution-date recording.
- Sell-price scenario analysis.
- Estimated profit calculation.
- Percentage-return estimation.
- Historical trade-cycle tracking.

The spreadsheet is currently a planning and tracking tool rather than a fully reliable source of truth for actual exchange calculations.

---

## 5. User Pain Points

The following pain points are based on the user's current documented workflow and direct user feedback.

Severity represents how disruptive each pain point currently feels to the user. It should not be interpreted as product priority, since the importance of the underlying outcome may differ from the perceived operational friction.

### 5.1 Lack of Confidence in Realized Trade Results

**Severity: Medium**  
**Outcome importance: High**

The spreadsheet calculates an estimated monetary and percentage result for completed trade cycles, but the user does not currently have an independent and reliable way to confirm that this calculation matches the actual net result of the operation.

The user therefore lacks confidence in determining whether a completed trade produced the positive net result indicated by the spreadsheet after all applicable fees, quantities, precision, and rounding effects are considered.

The primary concern is not guaranteeing profitable trades, but being able to determine accurately whether a completed trade was profitable or unprofitable and by how much.

This is currently the most important outcome identified by the user.

### 5.2 Spreadsheet and Mercado Bitcoin Value Discrepancies

**Severity: Medium**

Values calculated in the spreadsheet do not always match the values displayed or accepted by Mercado Bitcoin during order configuration.

Observed discrepancies may affect fields such as:

- Asset quantity.
- Trading fee.
- Total transaction value.
- Decimal representation.

When discrepancies occur, the user generally replaces spreadsheet estimates with values displayed by Mercado Bitcoin.

The exact causes of these discrepancies have not yet been validated. Precision, rounding, fee calculation, and exchange-specific rules remain possible explanations rather than confirmed causes.

### 5.3 Manual Reconciliation Between Spreadsheet and Exchange

**Severity: High**

The user repeatedly compares spreadsheet calculations with values displayed by Mercado Bitcoin while preparing transactions.

When the values differ, information must be manually transferred from Mercado Bitcoin back into the spreadsheet, after which spreadsheet formulas recalculate dependent values.

This creates repeated reconciliation work during trade planning and makes the spreadsheet dependent on manual corrections to remain aligned with the exchange.

### 5.4 Uncertainty About Sellable Asset Quantity

**Severity: High**

The user attempts to estimate the quantity available for sale by subtracting the asset-denominated purchase fee from the purchased quantity.

However, this estimated quantity does not always match the quantity presented when 100% of the available asset balance is selected in Mercado Bitcoin.

As a result, the user cannot currently determine with confidence, using the spreadsheet alone, the exact quantity that will be available for a subsequent sale.

The cause of this discrepancy has not yet been validated.

### 5.5 Trial-and-Error Trade Planning

**Severity: High**

Determining transaction targets currently requires repeated manual experimentation.

When planning a sale, the user incrementally adjusts the proposed selling price in the spreadsheet until the estimated result reaches an acceptable positive value. The target may then be adjusted again based on current market observations.

When planning a new purchase after a completed sale, the user does not currently follow a formal or validated methodology for determining the next entry price.

Trade planning therefore combines spreadsheet experimentation, chart observation, and user judgment rather than a consistently defined decision process.

### 5.6 Fragmented Workflow

**Severity: Low**

The current trade cycle requires the user to move between Mercado Bitcoin, email notifications, and the spreadsheet.

Although this fragmentation contributes to the overall workflow complexity, the user currently considers switching between systems to be a relatively low-severity pain point.

The more significant friction comes from reconciling values and understanding the financial result of transactions rather than from the number of systems itself.

### 5.7 Risks and Unvalidated Hypotheses

The following should not currently be treated as confirmed user pain points:

- The spreadsheet may contain calculation errors.
- Manual entry may result in missing or outdated transaction information.
- Precision or rounding rules may explain discrepancies between systems.
- Fee calculation differences may explain discrepancies between systems.
- Residual balances may be caused by exchange precision or fee rules.
- Portfolio allocation visibility may represent a significant user problem.

These items are risks, possible causes, or hypotheses that require further validation.

They should remain separate from directly observed pain points until supporting evidence is available.

---

## 6. Existing Solutions

The primary user currently relies on a combination of Mercado Bitcoin and a custom spreadsheet to execute, plan, track, and analyze trading activity.

These tools address different parts of the workflow but do not currently provide the user with a single reliable way to evaluate the complete financial result of a trade cycle.

### 6.1 Mercado Bitcoin

Mercado Bitcoin is the exchange currently used by the primary user to perform digital asset transactions.

In the user's current workflow, the platform is used for:

- Market and price-chart observation.
- Buy and sell order configuration.
- Limit orders.
- Post-only order configuration.
- Order submission and cancellation.
- Balance and available-quantity verification.
- Order execution.
- Order-history consultation.
- Transaction and account information.
- CSV statement export.

The user primarily uses the Pro trading interface on the web because she perceives it as providing the information and order controls most appropriate for her current trading workflow.

Mercado Bitcoin therefore fulfills the operational role of executing and recording the actual exchange transactions.

#### Observed User Experience Gaps

For the user's current workflow, accessing and interpreting historical trading information requires significant navigation across the platform.

The user also considers the available CSV statement insufficiently detailed for independently reconstructing and evaluating complete trade cycles using her current process.

Most importantly, the user has not found a sufficiently clear way within her current use of the platform to associate purchases and subsequent sales into trade cycles and determine the resulting net monetary and percentage outcome after applicable transaction costs.

The user would also like better historical portfolio visualization on the web interface. Some portfolio visualization is available in the mobile experience, but the user currently considers the mobile interface less suitable for configuring and executing her trades.

These observations describe the user's current experience with the platform and should not be interpreted as a comprehensive assessment of all Mercado Bitcoin capabilities.

### 6.2 Custom Spreadsheet

The user created a custom spreadsheet as a workaround for analytical and planning needs that were not being sufficiently addressed by her existing Mercado Bitcoin workflow.

The spreadsheet is currently used to:

- Record planned and executed buy and sell transactions.
- Associate transaction information across recurring trade cycles.
- Estimate trading fees.
- Estimate transaction totals.
- Calculate potential selling prices.
- Estimate monetary trade results.
- Estimate percentage returns.
- Maintain a custom transaction history.
- Generate charts and aggregated views.
- Observe metrics such as estimated return percentages and average results across recorded transactions.

The spreadsheet provides analytical flexibility that the user has not found in her current exchange workflow.

However, it depends on manually maintained data and formulas.

Spreadsheet calculations do not always reproduce the values displayed by Mercado Bitcoin, requiring manual reconciliation between the two systems.

As a result, the spreadsheet is useful for planning and estimation but does not currently provide the user with complete confidence that its calculated trade-cycle result matches the actual realized financial result.

### 6.3 Current Solution Gap

The user's current solution can be summarized as:

Mercado Bitcoin  
→ authoritative operational environment for configuring and executing trades

Custom Spreadsheet  
→ user-created planning, calculation, tracking, and analysis workaround

Email  
→ execution notification and workflow trigger

The main gap exists between reliable transaction execution and reliable trade-cycle analysis.

The exchange contains the operational transaction data, while the spreadsheet provides the customized calculations and analytical structure the user needs. The user currently reconciles these two contexts manually.

This combination does not fully satisfy the user's most important identified outcome: confidently determining the actual net result of a completed trade cycle.

### 6.4 Alternative Solutions

The primary user has not yet evaluated alternative exchanges, portfolio-management applications, trading-analysis tools, crypto calculators, or other specialized products as potential solutions to the identified problem.

Therefore, the current discovery does not support the conclusion that the identified need represents a broader market gap or that no existing product already addresses it.

A broader competitive or alternative-solution analysis may be conducted later if required by the product strategy.

The current conclusion is limited to the user's existing workflow:

**The current combination of Mercado Bitcoin and a custom spreadsheet does not fully satisfy the primary user's identified need for reliable trade-cycle analysis.**

---

## 7. Product Opportunity

The primary product opportunity is to provide the user with a reliable way to understand and analyze the complete financial lifecycle of her trading activity, from individual transactions to trade cycles, assets, and overall portfolio performance.

The current workflow separates reliable exchange execution data from the customized calculations and analytical context maintained in the user's spreadsheet. This creates an opportunity to bring these contexts together so that trading results can be evaluated using reliable transaction information while preserving the analytical capabilities required by the user.

### 7.1 Trade Cycle Intelligence

The strongest opportunity identified during discovery is improving the user's ability to understand the actual financial result of a complete trade cycle.

The user's current priorities are:

1. Determine with confidence the realized net result of completed trades.
2. Understand related buy and sell transactions as complete trade cycles.
3. Evaluate the expected result of potential trades before execution.
4. Reduce the manual reconciliation required between exchange data and external calculations.

The opportunity is therefore not simply to automate the existing spreadsheet workflow.

It is to establish a reliable analytical representation of trading activity that distinguishes planned, estimated, and actual transaction results and allows the user to understand how each completed trade cycle affected her capital.

### 7.2 Asset-Level Intelligence

The user currently trades more than 30 digital assets.

Reliable trade-cycle information creates an opportunity to aggregate results by asset and help the user understand how different assets contribute to her overall trading performance.

Relevant questions include:

- Which assets have generated the highest and lowest realized results?
- How many trade cycles have been completed for each asset?
- What is the average realized result by asset?
- How much capital has been allocated to each asset?
- How do trading activity and results differ across assets?

These analytical needs depend on reliable transaction and trade-cycle information and should not be treated independently from the core trade-cycle problem.

### 7.3 Portfolio Intelligence

Once reliable transaction, trade-cycle, and asset-level information is available, there is an opportunity to provide a higher-level view of portfolio and capital evolution.

The user wants to understand how her overall holdings and trading results evolve over time and whether her trading activity is moving her portfolio toward her personally defined performance objectives.

The user currently has a personal goal of evaluating whether her trading activity can achieve an average daily portfolio growth target of 1%.

This target represents a user-defined performance objective, not a product promise, expected investment return, or guaranteed outcome.

The product opportunity is to enable accurate measurement and comparison against user-defined objectives, regardless of whether actual performance is positive, negative, or below the target.

### 7.4 Trade Planning and Scenario Analysis

After reliable actual trade results can be established, there is an additional opportunity to improve pre-trade analysis.

The user currently experiments with potential buy and sell prices through spreadsheet calculations and market observation.

A better analytical process could allow different transaction scenarios to be evaluated using known costs, quantities, fee structures, and other validated exchange rules.

The opportunity is to improve the information available for decision-making rather than to predict future market prices or guarantee profitable trades.

### 7.5 Operational Efficiency

Reducing manual reconciliation between exchange information and external calculations represents an additional opportunity.

However, discovery indicates that operational efficiency is not currently the user's highest-value outcome.

The primary value lies in confidence and visibility:

**first understand the result correctly, then reduce the effort required to obtain that understanding.**

### 7.6 Opportunity Boundaries

The opportunity identified during current discovery does not imply that:

- Profitable trades can be guaranteed.
- Future market prices can be predicted reliably.
- A particular asset can be guaranteed to produce better returns.
- A user-defined performance target will be achieved.
- Automated trading decisions are required to solve the current problem.
- AssetOps or ServiceNow is the only possible solution.
- No existing third-party product already addresses these needs.

Alternative exchanges and specialized portfolio or trading-analysis products have not yet been evaluated.

The current opportunity is therefore based on the unmet needs observed in the primary user's existing workflow rather than on a validated broader market gap.

### 7.7 Opportunity Summary

The opportunity can be summarized as:

**Enable the user to move from isolated transaction data and manually reconciled estimates to reliable trade-cycle intelligence, and use that foundation to understand asset-level and portfolio-level performance over time.**

The intended progression of value is:

Transaction Data  
→ Trade Cycle Intelligence  
→ Asset-Level Intelligence  
→ Portfolio Intelligence  
→ Better-Informed Trade Planning
---

## 8. Product Assumptions

The following assumptions represent beliefs that have not yet been fully validated.

They are intentionally separated from validated user evidence and should be tested through product, business, integration, architecture, and technical discovery.

Assumptions are classified according to the potential impact on the current product direction if they prove to be false.

### 8.1 Critical Product Viability Assumptions

#### PA-01 — Sufficient Exchange Data Is Available

**Assumption:** Mercado Bitcoin provides, through accessible platform data, APIs, statements, or other reliable sources, sufficient information to determine the actual financial result of relevant trading operations.

**Impact if false: Critical**

The primary product opportunity depends on establishing reliable trade-cycle intelligence from actual transaction information.

If the required data cannot be obtained with sufficient completeness and reliability, the product would not be able to satisfy its most important identified user outcome.

This assumption requires technical and integration validation.

#### PA-02 — Exchange Calculations Can Be Reliably Reconciled

**Assumption:** The rules that materially affect transaction results, including applicable fees, asset quantities, precision, rounding, and execution values, can be understood and reproduced or reconciled with sufficient accuracy outside the exchange.

**Impact if false: Critical**

AssetOps does not need to reproduce irrelevant internal exchange calculations, but it must be able to determine financial results with sufficient reliability to reconcile them against the actual realized transaction outcome.

If material differences cannot be explained or reconciled, the user would continue to lack confidence in the calculated trade result.

This assumption requires business-rule, integration, and technical validation.

### 8.2 Trade-Cycle Modeling Assumptions

#### PA-03 — Trading Activity Can Be Represented as Meaningful Trade Cycles

**Assumption:** Buy and sell activity can be associated using a consistent methodology that allows the user to evaluate meaningful trade cycles.

**Impact if false: Medium to High**

Simple one-buy/one-sell scenarios may be straightforward, but trading activity may include:

- Multiple purchases of the same asset.
- Partial sales.
- Additional purchases before a position is fully sold.
- Partial executions.
- Cancelled and replacement orders.

A methodology for associating acquisition and disposal activity has not yet been defined.

Possible approaches may include system-defined allocation methodologies or explicit user association. These alternatives require further business analysis before a rule is selected.

The product may remain viable if automatic association is not possible, provided that a sufficiently reliable alternative can be established.

### 8.3 Historical Data Assumptions

#### PA-04 — Existing Trading History Can Be Reconstructed

**Assumption:** Sufficient historical information may be available to reconstruct some or all trading activity performed before AssetOps begins collecting data.

**Impact if false: Low**

Historical reconstruction would improve portfolio and performance analysis, but it is not required for the core product concept to remain viable.

If historical information proves insufficient, AssetOps could begin establishing reliable trade-cycle and portfolio information prospectively from a defined starting point.

The completeness of available historical information requires validation.

### 8.4 Portfolio Intelligence Assumptions

#### PA-05 — Reliable Trade-Cycle Data Can Be Aggregated by Asset

**Assumption:** Once individual transaction and trade-cycle results are reliable, they can be aggregated meaningfully at the asset level.

This could allow the user to evaluate how trading activity and realized results differ across the more than 30 assets currently traded.

**Impact if false: Medium**

Asset-level analysis contributes to the broader Portfolio Intelligence opportunity but is secondary to reliable individual trade-cycle results.

#### PA-06 — Asset-Level Results Can Support Portfolio-Level Analysis

**Assumption:** Reliable transaction and asset-level information can be aggregated into meaningful views of portfolio and capital evolution over time.

**Impact if false: Medium**

Portfolio Intelligence represents an important higher-level user need, but the core Trade Cycle Intelligence opportunity could remain valuable independently.

### 8.5 Trade Planning Assumptions

#### PA-07 — Validated Transaction Rules Can Support Pre-Trade Scenario Analysis

**Assumption:** Once applicable fee, quantity, precision, and calculation rules are understood, they can be used to estimate the financial result of hypothetical buy and sell scenarios before an order is executed.

**Impact if false: Medium**

Pre-trade scenario analysis is valuable to the user but is lower priority than determining the actual result of completed trades.

The product could therefore retain significant value even if scenario calculations require additional limitations or cannot initially reproduce every execution condition.

### 8.6 Integration Assumptions

#### PA-08 — Required Mercado Bitcoin Data Can Be Accessed Programmatically

**Assumption:** Mercado Bitcoin provides APIs or other appropriate integration mechanisms through which the data required by the product can be retrieved with sufficient reliability.

**Impact if false: High to Critical for the current implementation**

The specific data availability, authentication mechanisms, endpoint coverage, pagination, rate limits, historical availability, and execution information have not yet been validated.

This assumption requires dedicated integration discovery.

#### PA-09 — Order Execution State Can Be Obtained Without Email as the Authoritative Source

**Assumption:** Order and execution status can be obtained from exchange data or integration mechanisms without depending on execution-notification emails as the authoritative transaction source.

**Impact if false: Medium to High**

Email currently acts as a workflow trigger but is not assumed to be the preferred source of financial transaction truth.

This requires integration validation.

### 8.7 Platform and Architecture Assumptions

#### PA-10 — ServiceNow Can Support the Current Implementation

**Assumption:** ServiceNow can store, process, calculate, secure, and present the data required for the current AssetOps implementation with sufficient precision, performance, and reliability.

**Impact if false: Medium for the current project; Low for the product concept**

ServiceNow is the technology selected for the current implementation and portfolio project.

It is not considered part of the fundamental product definition.

If ServiceNow proves unsuitable for critical product requirements, the product concept may remain valid while requiring a different implementation architecture.

This assumption requires architecture and technical validation.

### 8.8 Security Assumptions

#### PA-11 — Exchange Integration Can Be Implemented Securely

**Assumption:** Required exchange credentials and account access can be managed without exposing sensitive information and with permissions appropriate to the capabilities being implemented.

**Impact if false: High**

The current product direction assumes that required data access can be implemented without introducing unacceptable credential or account-security risks.

Authentication, credential storage, permissions, logging, and repository hygiene require dedicated security validation.

### 8.9 User and Product Value Assumptions

Discovery has already provided direct user evidence that:

- Confidence in realized trade results is highly important to the primary user.
- Complete trade-cycle visibility is valuable.
- Pre-trade analysis is valuable.
- Portfolio and asset-level performance visibility is desired.
- Manual reconciliation is a significant operational pain point.

These findings should not be treated as completely untested assumptions for the current primary user.

However, whether the same needs and priorities apply to a broader population of digital asset traders remains unvalidated.

#### PA-12 — The Problem Extends Beyond the Primary User

**Assumption:** Other digital asset traders may experience sufficiently similar problems for AssetOps to provide value beyond its current primary user.

**Impact if false: Low for the current personal-use product; High for future market expansion**

No broader user research has yet been conducted.

The current discovery therefore supports the product for the primary user's workflow but does not establish broader product-market demand.

### 8.10 Assumption Prioritization

The assumptions that should receive the earliest validation are:

1. **PA-01 — Sufficient Exchange Data Is Available**
2. **PA-02 — Exchange Calculations Can Be Reliably Reconciled**
3. **PA-08 — Required Mercado Bitcoin Data Can Be Accessed Programmatically**
4. **PA-03 — Trading Activity Can Be Represented as Meaningful Trade Cycles**
5. **PA-11 — Exchange Integration Can Be Implemented Securely**

These assumptions have the greatest potential to invalidate or materially change the current product direction.

Other assumptions may be validated progressively as the product moves through business analysis, integration discovery, architecture, implementation, and product validation.

---

## 9. Discovery Questions

The following questions represent important unknowns that require further investigation before related product decisions can be considered validated.

Questions are prioritized according to their potential impact on product viability and are expected to be answered progressively through product discovery, business analysis, integration research, architecture, security analysis, implementation, and validation.

### 9.1 P0 — Product Viability

- **DQ-01:** What exchange data is required to determine the realized net result of a completed trade?
- **DQ-02:** Does Mercado Bitcoin make all required data available through sufficiently reliable sources?
- **DQ-03:** Which of the required data is available programmatically through Mercado Bitcoin APIs?
- **DQ-04:** Are actual execution fees available directly, or must any fees be derived?
- **DQ-05:** What precision and rounding rules materially affect quantities, fees, transaction totals, and realized results?
- **DQ-06:** Can external calculations be reconciled with Mercado Bitcoin transaction results with sufficient reliability?
- **DQ-07:** Can the required exchange access be implemented with acceptable security and permissions?

### 9.2 P1 — Trade Cycle Intelligence

- **DQ-08:** What constitutes a trade cycle for the purposes of AssetOps analysis?
- **DQ-09:** How should multiple purchases of the same asset be handled when subsequent sales occur?
- **DQ-10:** How should partial sales be associated with previous purchases?
- **DQ-11:** How should an additional purchase made before an existing position is fully sold affect the trade cycle?
- **DQ-12:** How should partial executions be represented?
- **DQ-13:** How should cancelled and replacement orders be represented and related?
- **DQ-14:** Which values should be considered planned, estimated, executed, and realized?
- **DQ-15:** Which source should be authoritative for each transaction attribute?
- **DQ-16:** What level of numerical reconciliation is required for a trade result to be considered reliable?

### 9.3 P1 — Portfolio Intelligence

- **DQ-17:** How should realized results from multiple trade cycles be aggregated by asset?
- **DQ-18:** What information is required to represent the user's current position in each asset?
- **DQ-19:** How should realized and unrealized results be distinguished?
- **DQ-20:** How should portfolio value and its evolution over time be calculated?
- **DQ-21:** Which asset-level metrics help the user evaluate where trading activity, capital, and attention are producing results?
- **DQ-22:** Which portfolio-level metrics are required to evaluate performance against user-defined objectives?
- **DQ-23:** How should realized trading performance be calculated over a defined period?
- **DQ-24:** How should total portfolio value and portfolio value performance be calculated over a defined period?
- **DQ-25:** How should realized and unrealized performance be presented separately to avoid double counting or misinterpretation?
- **DQ-26:** What should define the beginning and ending portfolio value for daily performance measurement?
- **DQ-27:** How should deposits, withdrawals, transfers, and other external capital movements be distinguished from investment performance?
- **DQ-28:** How should user-defined performance targets be evaluated independently against realized trading performance and total portfolio value performance?

### 9.4 P2 — Trade Planning

- **DQ-29:** Which inputs are required to evaluate a hypothetical buy or sell scenario?
- **DQ-30:** Can applicable fees and exchange rules be incorporated reliably into pre-trade estimates?
- **DQ-31:** Which differences between estimated and actual execution results are unavoidable?
- **DQ-32:** What information does the user need when comparing alternative buy or sell prices?
- **DQ-33:** How should user-defined target returns be represented without implying that the target will be achieved?

### 9.5 P2 — Historical Data

- **DQ-34:** How much historical transaction and execution data is available?
- **DQ-35:** Can historical transactions be reconstructed with sufficient information to calculate reliable results?
- **DQ-36:** If complete historical reconstruction is not possible, what should define the starting point for reliable AssetOps data?

### 9.6 P2 — Current Workflow and User Experience

- **DQ-37:** Which steps in the current workflow consume the most time or require the most repeated reconciliation?
- **DQ-38:** Which information currently requires the most navigation to retrieve?
- **DQ-39:** Which analytical views are currently most useful in the user's spreadsheet?
- **DQ-40:** Which portfolio and performance visualizations would materially improve the user's ability to understand trading results?

### 9.7 P3 — Market and Alternative Solutions

- **DQ-41:** Which alternative exchanges are relevant to the user's current trading behavior?
- **DQ-42:** How do relevant alternatives compare in trading fees, supported order types, execution capabilities, data availability, and usability?
- **DQ-43:** Do existing portfolio or crypto trade-analysis products already provide reliable trade-cycle analysis for the user's workflow?
- **DQ-44:** Would an existing product or alternative exchange solve the identified problem without requiring a custom application?
- **DQ-45:** Do other digital asset traders experience sufficiently similar problems to justify exploring AssetOps beyond the current primary user?

### 9.8 Discovery Priority

The earliest discovery effort should focus on the P0 questions because negative findings may invalidate or materially change the current product direction.

P1 questions define how the core Trade Cycle Intelligence and Portfolio Intelligence opportunities should work conceptually.

P2 questions influence planning, historical reconstruction, operational efficiency, and user experience but are not currently considered fundamental to initial product viability.

P3 questions concern broader alternatives and potential market expansion. They are important for determining whether AssetOps represents a broader product opportunity but do not currently block validation of the personal-use product concept.

Discovery questions should remain open until supported by sufficient evidence. Proposed answers should not be treated as validated product requirements until the corresponding investigation has been completed.

---

## 10. Problem Hypotheses

The following hypotheses describe the current understanding of the primary user's problem and the relationships believed to exist between its causes, symptoms, and desired outcomes.

These hypotheses are based on the discovery completed so far but should remain open to validation or rejection as additional evidence becomes available.

### PH-01 — Reliable Trade Result Is the Core User Problem

**Hypothesis**

The primary user's most important difficulty is not executing digital asset trades, but determining with confidence the actual net financial result of her trading activity after execution.

The current spreadsheet provides an estimated result, but the user cannot independently confirm that the calculation fully reflects actual execution values, fees, quantities, precision, rounding, and other applicable exchange rules.

**Expected evidence**

This hypothesis is strengthened if:

- The user continues to identify realized-result confidence as a high-importance outcome.
- Material differences exist between externally calculated and actual exchange values.
- Existing exchange information does not provide the user with a sufficiently clear representation of the complete realized result.

**Potential disconfirmation**

This hypothesis would be weakened if reliable realized results are already readily available to the user through an existing solution or if further investigation shows that result confidence is not materially important to the user's workflow.

### PH-02 — Manual Reconciliation Contributes to Result Uncertainty

**Hypothesis**

The separation between authoritative exchange information and externally maintained spreadsheet calculations contributes to the user's uncertainty about transaction and trading results.

The problem is not primarily the existence of multiple systems.

Instead, the user must manually reconcile information between those systems because the spreadsheet provides the customized analytical context while Mercado Bitcoin provides the authoritative operational values.

**Expected evidence**

This hypothesis is strengthened if:

- Reconciliation is repeatedly required during the current workflow.
- Spreadsheet values differ materially from exchange values.
- Manual corrections are necessary for spreadsheet calculations to remain aligned with the exchange.
- Reliable use of authoritative transaction information reduces uncertainty in calculated results.

**Potential disconfirmation**

This hypothesis would be weakened if reconciliation can be shown to have little relationship with result uncertainty or if the spreadsheet already reproduces actual results reliably without meaningful reconciliation.

### PH-03 — Position and Trade-Cycle Context Is More Useful Than Isolated Transactions

**Hypothesis**

Analyzing isolated orders is insufficient for the user's current analytical needs.

The user requires relationships between acquisition activity, asset positions, subsequent disposals, applicable costs, and realized results in order to understand trading performance.

For simple scenarios, this may resemble a direct buy-to-sell trade cycle.

For more complex scenarios involving multiple purchases or partial sales, the user's current mental model favors treating purchases of the same asset as contributing to an aggregated position from which subsequent sales reduce quantity and realize results.

The financial methodology used to calculate the cost and result of these aggregated positions has not yet been defined or validated.

**Expected evidence**

This hypothesis is strengthened if:

- The user consistently evaluates performance across related buying and selling activity rather than individual orders.
- Multiple purchases and partial sales occur in actual trading activity.
- Position-level context improves the user's ability to interpret realized and remaining value.
- A consistent allocation methodology can be established for complex transaction sequences.

**Potential disconfirmation**

This hypothesis would be weakened if individual exchange transactions already provide sufficient analytical context or if meaningful relationships between acquisitions, positions, and disposals cannot be established reliably.

### PH-04 — Reliable Transaction Foundations Enable Higher-Level Performance Intelligence

**Hypothesis**

Reliable transaction and position information can provide the foundation for progressively higher levels of analysis:

Transaction Data  
→ Position and Trade-Cycle Intelligence  
→ Asset-Level Intelligence  
→ Portfolio Intelligence

If underlying transaction quantities, costs, fees, and realized results are reliable, those results may be aggregated to help the user understand performance by asset and across the overall portfolio.

**Expected evidence**

This hypothesis is strengthened if:

- Transaction-level results can be reconciled reliably.
- Position and realized-result calculations remain consistent across multiple transaction patterns.
- Asset-level aggregation produces meaningful and interpretable performance information.
- Portfolio-level metrics can be calculated without introducing double counting or confusing realized and unrealized performance.

**Potential disconfirmation**

This hypothesis would be weakened if reliable transaction information cannot be established or if aggregating transaction results does not produce meaningful asset-level or portfolio-level analysis.

### PH-05 — Reliable Performance Information Improves Decision Support

**Hypothesis**

Providing reliable historical results, position information, asset-level performance, and portfolio-level performance will give the user better information for evaluating her trading activity and planning future operations.

The expected value is improved visibility and decision support rather than guaranteed improvement in investment returns.

**Expected evidence**

This hypothesis is strengthened if the user can use reliable performance information to answer questions such as:

- Which assets have contributed most or least to realized results?
- How have open positions changed in value?
- How has total portfolio value evolved?
- How does realized performance compare with portfolio-value performance?
- How does actual performance compare with user-defined objectives?
- Which historical information is relevant when evaluating future trade scenarios?

**Potential disconfirmation**

This hypothesis would be weakened if the resulting information does not materially affect the user's understanding, evaluation, or planning process.

### 10.1 Hypothesis Relationship

The current problem model can be summarized as:

Authoritative Exchange Data
        +
External Analytical Calculations
        ↓
Manual Reconciliation
        ↓
Uncertainty About Reliable Results
        ↓
Need for Position and Trade-Cycle Intelligence
        ↓
Asset-Level Performance Understanding
        ↓
Portfolio-Level Performance Understanding
        ↓
Better-Informed User Decision-Making

The hypotheses do not assume that better information will produce profitable trades or improve investment returns.

They propose that more reliable and appropriately structured information may improve the user's ability to understand and evaluate her own trading activity.

### 10.2 Remaining Uncertainty

Several elements of this hypothesis model remain unvalidated, including:

- Whether all required exchange data can be obtained.
- Whether external calculations can be reconciled with sufficient reliability.
- Which methodology should be used to calculate the cost of aggregated asset positions.
- How partial sales should realize results against an aggregated position.
- How realized and unrealized performance should be calculated and presented.
- Whether reliable transaction information can be aggregated into meaningful portfolio-level metrics.
- Whether existing third-party solutions already address these needs.

These uncertainties should be investigated before the corresponding product behavior is treated as validated.

---
## 11. Evidence, Assumptions, Hypotheses, and Unknowns

This section provides an explicit classification of the current discovery findings.

The purpose is to prevent user observations, product assumptions, proposed explanations, and externally verifiable facts from being treated as equivalent forms of evidence.

### 11.1 Evidence Classification

Evidence collected during the current discovery is primarily based on direct description and observation of the primary user's own workflow.

Unless explicitly stated otherwise, these findings should be interpreted as **user-reported or workflow-observed evidence**, not as independently verified claims about Mercado Bitcoin, financial methodology, exchange behavior, or the broader digital asset market.

#### E-01 — The User Performs Recurring Trading Activity

**Classification:** User-reported evidence

The primary user performs recurring buy and sell operations using Mercado Bitcoin and currently trades across more than 30 digital assets.

#### E-02 — Mercado Bitcoin Is the Current Execution Environment

**Classification:** User-reported / workflow evidence

The user currently uses Mercado Bitcoin to observe market information, configure orders, submit and cancel orders, verify available quantities, and execute transactions.

Within the current workflow, values presented by Mercado Bitcoin are treated by the user as authoritative when they differ from spreadsheet estimates.

This does not independently validate the correctness or completeness of every Mercado Bitcoin value or calculation.

#### E-03 — A Custom Spreadsheet Is Used for Planning and Analysis

**Classification:** Direct workflow evidence

The user created and maintains a spreadsheet to support activities including:

- Transaction planning.
- Quantity and fee estimation.
- Buy and sell calculations.
- Sell-price scenario analysis.
- Estimated trade-result calculations.
- Percentage-return calculations.
- Transaction tracking.
- Historical analysis.
- Charts and aggregated metrics.

#### E-04 — Manual Reconciliation Occurs

**Classification:** Direct workflow evidence

The user compares spreadsheet estimates with values displayed by Mercado Bitcoin during transaction preparation.

When differences are identified, the user manually transfers Mercado Bitcoin values into the spreadsheet and allows dependent calculations to update.

#### E-05 — Value Discrepancies Have Been Observed

**Classification:** User-reported evidence

The user has observed differences between spreadsheet calculations and values displayed by Mercado Bitcoin.

Observed differences may involve:

- Asset quantities.
- Fees.
- Transaction totals.
- Decimal representation.

The causes of these differences have not been established.

#### E-06 — Sellable Quantity Discrepancies Have Been Observed

**Classification:** User-reported evidence

The quantity estimated by the user's spreadsheet does not always match the quantity displayed when the user attempts to sell 100% of the available asset balance.

The user currently resolves this by using the quantity displayed by Mercado Bitcoin.

The cause remains unknown.

#### E-07 — Realized-Result Confidence Is the Highest-Importance Outcome

**Classification:** Direct user evidence

The user identified the ability to determine with confidence whether completed trading activity produced a positive or negative net result as the most important current outcome.

This outcome is more important to the user than eliminating manual reconciliation itself.

#### E-08 — Complete Trade Context Is Valuable

**Classification:** Direct user evidence

The user wants to understand related buying and selling activity as a meaningful financial context rather than evaluating only isolated orders.

For more complex scenarios involving multiple purchases, the user's current mental model favors an aggregated asset position that can later be partially or fully reduced through sales.

The calculation methodology for this model has not yet been validated.

#### E-09 — Portfolio and Asset-Level Performance Are Important

**Classification:** Direct user evidence

The user wants to understand:

- Performance by asset.
- Which assets contribute more or less to realized results.
- Portfolio-value evolution.
- Realized trading performance.
- Unrealized changes in open positions.

The user wants realized trading performance and total portfolio-value performance to be measured separately.

#### E-10 — The User Has a Personal Performance Objective

**Classification:** Direct user evidence

The user currently uses a 1% daily performance target as a personal objective.

The user considers the objective reached if either realized trading performance or total portfolio-value performance independently reaches the target.

This target represents user context only.

It is not evidence that the target is achievable, sustainable, appropriate, or attributable to the product.

#### E-11 — The User Has Not Evaluated Alternative Solutions

**Classification:** Direct user evidence

The primary user has not yet evaluated other exchanges, portfolio-management applications, crypto-analysis tools, or specialized trading-analysis products as alternatives to the current Mercado Bitcoin and spreadsheet workflow.

Therefore, no conclusion about a broader market gap is currently supported.

### 11.2 Assumptions

The following remain assumptions rather than validated evidence:

- Sufficient exchange data exists to calculate reliable realized results.
- Required data can be accessed programmatically.
- Applicable fee rules can be identified correctly.
- Precision and rounding rules can be understood sufficiently.
- External calculations can be reconciled with actual exchange outcomes.
- Trading activity can be modeled consistently across complex position scenarios.
- Historical transactions can be reconstructed sufficiently.
- Reliable trade results can be aggregated meaningfully by asset.
- Asset-level information can support reliable portfolio-level analysis.
- Pre-trade scenarios can be estimated reliably from validated transaction rules.
- ServiceNow can support the required precision, reliability, security, and performance.
- Exchange integration can be implemented securely.
- Similar needs exist among users beyond the current primary user.

These assumptions are detailed and prioritized in the Product Assumptions section.

### 11.3 Problem Hypotheses

The current discovery also contains hypotheses about relationships between observed problems:

- Reliable trade-result determination is the central user problem.
- Manual reconciliation contributes to result uncertainty.
- Position and trade-cycle context provides more analytical value than isolated transactions.
- Reliable transaction information enables progressively higher levels of asset and portfolio intelligence.
- Reliable performance information improves the user's ability to evaluate and plan trading activity.

These hypotheses are supported to different degrees by current user evidence but remain open to further validation or disconfirmation.

They are detailed in the Problem Hypotheses section.

### 11.4 Unknowns

The following remain explicitly unknown:

- The complete set of exchange data required to calculate realized results.
- Whether all required data is available from Mercado Bitcoin.
- Which required data is available through APIs.
- The exact applicable fee rules for relevant transaction scenarios.
- The precision and rounding rules that explain observed discrepancies.
- The appropriate financial methodology for aggregated positions, multiple purchases, and partial sales.
- The appropriate treatment of partial executions.
- The required reconciliation tolerance for reliable financial calculations.
- The completeness of historical exchange data.
- The appropriate methodology for realized versus unrealized performance.
- The treatment of deposits, withdrawals, transfers, and other external capital movements in performance calculations.
- Whether existing third-party products already solve the identified problem.
- Whether the problem generalizes to a broader user population.

These unknowns are represented by the prioritized Discovery Questions and should not be converted into product requirements until investigated.

### 11.5 External Validation Boundary

Current discovery evidence primarily validates the **primary user's experience and needs**.

It does not yet independently validate:

- Mercado Bitcoin's complete product capabilities.
- Mercado Bitcoin's internal calculation methodology.
- Current Mercado Bitcoin API coverage.
- Current Mercado Bitcoin fee structures.
- Exchange precision and rounding rules.
- Financial or accounting methodologies.
- Competitor capabilities.
- Broader market demand.
- The feasibility of the proposed technical implementation.

Claims in these areas require appropriate external, technical, business-rule, or market evidence before being treated as validated facts.

### 11.6 Traceability Principle

The project should maintain the following distinction throughout subsequent phases:

Evidence  
→ supports or challenges assumptions and hypotheses

Assumptions  
→ identify beliefs that require validation

Hypotheses  
→ describe testable explanations or relationships

Discovery Questions  
→ define what must be investigated

Validated Findings  
→ may become inputs to product decisions and requirements

Product Requirements  
→ should not be created solely from unvalidated assumptions

This distinction should remain visible as AssetOps moves from discovery into business analysis, technical discovery, architecture, design, implementation, and validation.

---

## 11. Current Spreadsheet Data Model

The user's current spreadsheet contains the following fields.

### 11.1 Execution Date

Date on which the order was executed.

### 11.2 Asset / Currency

Trading pair associated with the transaction.

Example:

`CHZ/BRL`

### 11.3 Order Type

Identifies the transaction side and order type.

Examples:

- Buy Limit Post Only.
- Sell Limit Post Only.

### 11.4 Price (BRL)

Unit price of the asset used by the order.

### 11.5 Asset Quantity

Quantity of the asset purchased or sold.

### 11.6 Asset Fee

Fee represented in terms of asset quantity when applicable.

The current spreadsheet estimates this fee using the applicable trading fee rate.

Current calculation:

`Asset Quantity × Trading Fee Rate`

The actual fee behavior, amount, precision, and currency must be validated against Mercado Bitcoin execution data.

### 11.7 Total (BRL)

Total BRL value associated with the transaction.

The current calculation differs depending on whether the transaction is a buy or sell and how trading fees are applied.

The exact calculation must be validated against actual Mercado Bitcoin execution data before being implemented in AssetOps.

### 11.8 Fee (BRL)

Trading fee represented in BRL when applicable.

The current spreadsheet estimates this value using the transaction value and expected trading fee rate.

The actual fee should be obtained from Mercado Bitcoin execution data whenever available.

### 11.9 Status

Current spreadsheet statuses:

- **Not Published:** a planned transaction used to estimate a future buy or sell order.
- **Open:** an order has been submitted to Mercado Bitcoin but has not yet been fully executed.
- **Executed:** the order has been executed.

These statuses represent both planned transactions and real exchange orders and may need to be expanded to accurately represent Mercado Bitcoin order states, including partial executions and cancellations.

### 11.10 Profit After Sale

Current calculation:

`Net Sale Total - Purchase Total`

This represents the monetary result associated with completing a buy/sell cycle.

The calculation must be reviewed to ensure all applicable trading costs are included.

### 11.11 Profit Percentage

Current calculation:

`Profit After Sale / Purchase Total`

This represents the percentage return calculated for a completed buy/sell cycle.

---

## 12. Problem Validation Criteria

Problem validation determines whether the identified user problem is sufficiently supported by evidence to justify continued product investigation.

It does not validate AssetOps as the solution, confirm technical feasibility, establish a broader market opportunity, or prove that the proposed product can improve investment performance.

The current validation scope is limited to the primary user's documented workflow.

### 12.1 PVC-01 — The Problem Is Observable

**Criterion**

The primary user must demonstrate or describe a recurring situation in which she cannot determine the complete financial result of her trading activity with sufficient confidence using her current workflow.

**Current evidence**

The user currently relies on a custom spreadsheet to calculate estimated trading results and has reported that these calculations cannot be independently reconciled with complete confidence against actual exchange outcomes.

**Current status: Supported**

### 12.2 PVC-02 — The Problem Is Important to the User

**Criterion**

Reliable understanding of realized trading results must represent a meaningful user outcome rather than a minor convenience.

**Current evidence**

The user identified confidence in realized trade results as the most important outcome among the currently identified needs.

The user wants to understand whether trading activity produced a positive or negative result and by how much.

**Current status: Supported**

### 12.3 PVC-03 — The Current Workflow Requires a Workaround

**Criterion**

The user's current behavior should demonstrate that additional effort is already being invested to compensate for the identified problem.

**Current evidence**

The user created and maintains a custom spreadsheet for transaction planning, calculations, estimated trade results, historical tracking, and analytical views that are not sufficiently addressed by her current exchange workflow.

The spreadsheet therefore represents an existing user-created workaround.

**Current status: Supported**

### 12.4 PVC-04 — The Current Solution Does Not Fully Satisfy the Need

**Criterion**

The combination of solutions currently used by the primary user must leave a meaningful portion of the identified need unresolved.

**Current evidence**

Mercado Bitcoin provides the operational environment for trading, while the spreadsheet provides customized planning and analysis.

The user currently reconciles information between these contexts manually and still cannot confirm the complete realized trade result with the desired level of confidence.

**Current status: Supported for the current workflow**

This criterion does not establish that no existing third-party product or alternative exchange already addresses the problem.

### 12.5 PVC-05 — The Problem Produces Meaningful Consequences

**Criterion**

The problem should create observable consequences in the user's current workflow or ability to evaluate trading activity.

**Current evidence**

Observed consequences include:

- Repeated manual reconciliation.
- Uncertainty about sellable quantities.
- Difficulty confirming realized results.
- Trial-and-error transaction planning.
- Limited ability to evaluate results across assets.
- Limited ability to understand realized and portfolio-value performance over time.

**Current status: Supported**

### 12.6 Problem Validation Boundary

The following are not required to establish that the current primary-user problem exists:

- Confirmation that Mercado Bitcoin APIs provide all required data.
- Selection of a trade-position cost methodology.
- Validation of fee, precision, or rounding rules.
- Confirmation that ServiceNow is technically suitable.
- Confirmation that AssetOps can solve the problem.
- Evidence that other traders experience the same problem.
- Evidence that no competing product already solves the problem.
- Evidence that better information will increase investment returns.

These questions concern solution viability, technical feasibility, business rules, or market validation and should be evaluated separately.

### 12.7 Decision Criteria

Based on the current discovery scope, the problem-validation decision should use three possible outcomes.

#### Proceed

Proceed when:

- The problem is observable.
- The problem is meaningful to the primary user.
- Current behavior demonstrates an existing workaround.
- The current workflow does not fully satisfy the identified need.
- The problem creates meaningful consequences.

A Proceed decision means that further investigation of possible solutions is justified.

It does not authorize implementation or imply that the current proposed solution is viable.

#### Pivot

Pivot the problem definition when additional evidence shows that:

- The originally identified core problem is primarily a symptom of another problem.
- Another user outcome is materially more important.
- The current framing does not accurately represent the user's behavior.
- New evidence substantially changes the understanding of the problem.

#### Stop

Stop further investigation of this problem when evidence demonstrates that:

- The user can already satisfy the identified need with sufficient confidence and acceptable effort.
- The problem is not meaningful enough to justify further investigation.
- The observed workaround is unrelated to the proposed problem.
- The problem no longer occurs or has been incorrectly characterized.

Technical inability to implement AssetOps alone should not be interpreted as evidence that the user problem does not exist.

### 12.8 Current Problem Validation Assessment

Based on the discovery conducted with the current primary user:

| Validation Criterion | Current Assessment |
| --- | --- |
| PVC-01 — Problem is observable | Supported |
| PVC-02 — Problem is important | Supported |
| PVC-03 — Workaround exists | Supported |
| PVC-04 — Current solution is insufficient | Supported for current workflow |
| PVC-05 — Meaningful consequences exist | Supported |

**Current decision: PROCEED with further discovery and solution validation.**

This decision validates continued investigation of the problem for the current primary user.

It does not yet validate:

- AssetOps as the correct solution.
- ServiceNow as the correct implementation platform.
- Mercado Bitcoin integration feasibility.
- Calculation correctness.
- Product-market fit.
- Commercial viability.
- Broader market demand.

---

## 13. Research Findings

### 13.1 Research Scope

The current research focused on understanding the existing trading workflow, needs, behaviors, pain points, workarounds, and desired outcomes of AssetOps' initial primary user.

The research was qualitative and exploratory.

It was conducted through a structured discovery conversation in which the participant described her current trading behavior and walked through the process used to plan, execute, track, and evaluate digital asset transactions.

The investigation covered:

- Market observation and trade planning.
- Buy-order preparation and execution.
- Post-execution tracking.
- Sell planning and scenario analysis.
- Sellable-quantity reconciliation.
- Trade-result calculation.
- Open-order reassessment.
- Cancelled and replacement orders.
- Partial executions.
- Spreadsheet usage.
- Exchange usage.
- Portfolio-analysis needs.
- Performance objectives.
- Existing solution usage.
- Alternative solutions previously explored.

### 13.2 Participant Context

The current research includes one participant.

The participant is:

- The initial primary user of AssetOps.
- The creator of the current spreadsheet workaround.
- The creator of the AssetOps project.
- An active Mercado Bitcoin user.
- Currently learning and experimenting with short-term digital asset trading.
- Currently trading across more than 30 digital assets.

Because the participant is also the product creator, findings may be influenced by prior knowledge of the proposed product direction.

The research should therefore be interpreted as validation of the participant's own workflow and needs rather than validation of a broader market or user population.

### 13.3 Key Research Findings

#### RF-01 — The User Has Created an External Analytical Workaround

The participant created a custom spreadsheet because her existing exchange workflow did not provide the analytical context she needed to understand and evaluate her trading activity.

The spreadsheet is not used primarily as an alternative execution environment.

Instead, it acts as an external analytical layer for:

- Planning transactions.
- Estimating quantities and fees.
- Evaluating potential selling prices.
- Estimating trade results.
- Tracking transaction status.
- Maintaining historical information.
- Producing charts and aggregated metrics.

This behavior demonstrates that the participant is already investing effort in compensating for an unmet analytical need.

#### RF-02 — Confidence in Financial Results Is More Important Than Workflow Convenience

The participant identified confidence in realized trading results as the most important current outcome.

When asked to prioritize desired improvements, the participant ranked them as:

1. Confidence in the realized result.
2. Complete trade-cycle visibility.
3. Confidence during trade planning.
4. Reduction of manual reconciliation.

This indicates that reducing manual work alone would not address the participant's primary need.

The more important need is being able to understand and trust the financial result represented by the analytical process.

#### RF-03 — Isolated Orders Do Not Match the User's Full Analytical Context

The participant evaluates trading activity across related acquisition and disposal events rather than treating each order as analytically independent.

For simple transactions, this can resemble a buy followed by a sell.

For more complex activity involving multiple purchases and partial sales, the participant currently favors thinking in terms of an aggregated asset position that can later be reduced through sales.

This suggests that order-level history alone may not provide the analytical context required by the participant.

The appropriate financial methodology for representing aggregated positions has not yet been established.

#### RF-04 — Trade Planning Is an Iterative Analytical Process

The participant currently combines market observation with spreadsheet-based scenario calculations when deciding where to position orders.

For sell planning, potential selling prices may be adjusted repeatedly until the spreadsheet indicates an acceptable estimated result.

The participant may then adjust the target further based on current market conditions.

This demonstrates that the current workflow includes an iterative scenario-analysis process rather than only transaction execution.

The participant does not currently follow a formal or validated methodology for predicting market entry or exit points.

#### RF-05 — Portfolio Analysis Depends on Reliable Lower-Level Trading Information

The participant currently trades across more than 30 digital assets and wants to understand how different assets contribute to overall trading and portfolio performance.

Desired analytical understanding includes:

- Results by asset.
- Historical trading performance.
- Portfolio-value evolution.
- Realized trading performance.
- Unrealized changes in open positions.

The participant wants realized trading performance and total portfolio-value performance to remain analytically separate.

Reliable portfolio analysis therefore depends on trustworthy underlying transaction, position, and realized-result information.

#### RF-06 — Analytical Uncertainty Creates More Friction Than System Switching

The participant considers the fragmented use of Mercado Bitcoin, email, and the spreadsheet to be a relatively low-severity problem by itself.

Higher-severity friction is associated with:

- Manual reconciliation.
- Uncertainty about sellable quantities.
- Trial-and-error planning.
- Difficulty confirming financial results.

This indicates that consolidating systems into a single interface would not necessarily address the participant's primary problem unless the underlying information and calculations are sufficiently reliable.

#### RF-07 — Alternative Solutions Have Not Yet Been Explored

The participant has not evaluated other exchanges, portfolio-management applications, crypto-analysis tools, or specialized trading-analysis products as alternatives to the current workflow.

Current research therefore demonstrates an unmet need within the participant's existing combination of Mercado Bitcoin and a custom spreadsheet.

It does not demonstrate that the need is unmet by the broader market.

### 13.4 Research Limitations

The current research has several important limitations.

#### Single Participant

Research has been conducted with one primary participant.

Findings should not be generalized to digital asset traders as a broader population.

#### Participant and Product Creator Are the Same Person

The participant is also the creator of AssetOps.

This creates a potential confirmation-bias risk because the participant already has exposure to the proposed product concept and implementation direction.

#### Self-Reported Workflow

Much of the current evidence is based on the participant's description of her behavior and experience.

The complete workflow has not yet been independently observed through contextual inquiry or instrumented behavioral data.

#### Exchange Capabilities Have Not Been Independently Validated

Statements about Mercado Bitcoin primarily describe the participant's current experience with the platform.

The research has not yet independently verified the complete capabilities of the exchange, its APIs, fee methodology, precision rules, or alternative interfaces.

#### Alternative Products Have Not Been Evaluated

No competitive or alternative-solution research has yet established whether another product already addresses the identified need.

#### Financial Methodologies Remain Unvalidated

The research identified analytical needs involving positions, realized results, unrealized performance, partial sales, and multiple purchases.

The appropriate financial or accounting methodologies for these calculations have not yet been established.

#### No Outcome Measurement Yet

The current research establishes behaviors, needs, pain points, and desired outcomes.

It does not yet demonstrate that a proposed solution will reduce effort, improve calculation reliability, improve decision quality, or affect financial performance.

### 13.5 Research Implications

The research suggests that subsequent product investigation should prioritize:

1. **Reliability before convenience**  
   Any future solution direction should address confidence in financial results before focusing primarily on workflow consolidation or automation.

2. **Financial context beyond isolated orders**  
   Further investigation should determine how acquisition activity, positions, disposals, and realized results should be represented.

3. **Clear separation of estimated and actual information**  
   The current workflow mixes planning calculations with values later reconciled against the exchange. Future investigation should preserve a clear distinction between planned, estimated, executed, and realized information.

4. **Trade-level foundations before portfolio-level conclusions**  
   Asset and portfolio analysis should depend on sufficiently reliable underlying transaction and position information.

5. **Separate realized and portfolio-value performance**  
   These represent different analytical concepts for the participant and should not be combined into a single performance measure without appropriate methodology.

6. **Validate critical external dependencies early**  
   Exchange data availability, calculation rules, and integration feasibility materially affect whether the identified analytical needs can be addressed reliably.

7. **Avoid broader market claims**  
   Additional users and alternative solutions should be researched before treating AssetOps as a validated market opportunity.

### 13.6 Research Summary

Current research supports the conclusion that the primary user has a meaningful unmet need in her existing workflow around understanding and evaluating the financial results of recurring digital asset trading activity.

The strongest finding is that **reliability and interpretability of trading results matter more to the participant than simply reducing the number of manual steps or systems involved**.

The participant has already created a spreadsheet workaround, but the separation between exchange information and externally maintained calculations prevents her from achieving the desired level of confidence in the resulting analysis.

The research also indicates that the problem extends analytically beyond individual orders. The participant wants to understand positions, realized results, asset-level performance, and portfolio evolution while keeping realized trading performance distinct from changes in total portfolio value.

These findings are sufficient to support a Product Manager decision about whether further solution discovery is justified for the current primary user.

They are not sufficient to validate AssetOps as the solution or to establish broader product-market demand.

---

## 14. Discovery Gate Decision

### 14.1 Gate

**Gate:** Problem Discovery  
**Decision:** PROCEED WITH CONDITIONS  
**Decision Owner:** Product Manager  
**Inputs:** Problem Validation Criteria and Research Findings

### 14.2 Decision

The current discovery provides sufficient evidence to justify continued investigation of the AssetOps product opportunity for the current primary user.

The decision is therefore:

**PROCEED WITH CONDITIONS**

This decision confirms that the identified problem is sufficiently understood and meaningful to justify moving beyond problem discovery.

It does not validate AssetOps as the correct solution and does not authorize unrestricted implementation.

### 14.3 Decision Rationale

The decision is supported by the following findings:

1. **The problem is observable.**  
   The primary user currently cannot determine the complete realized financial result of her trading activity with the desired level of confidence using the existing workflow.

2. **The problem is meaningful.**  
   Confidence in realized trading results was identified as the user's highest-importance outcome.

3. **Existing behavior demonstrates demand for a solution.**  
   The user has already created and maintains a custom spreadsheet to compensate for analytical needs not sufficiently addressed by the current exchange workflow.

4. **The current workflow remains insufficient.**  
   Mercado Bitcoin provides the operational transaction environment while the spreadsheet provides customized analysis, requiring manual reconciliation between the two contexts.

5. **The problem produces observable consequences.**  
   These include manual reconciliation, uncertainty about quantities and results, iterative scenario calculations, and limited confidence in higher-level asset and portfolio analysis.

6. **The problem has been investigated beyond its initial framing.**  
   Discovery indicates that the core need is not simply workflow automation or interface consolidation. Reliability and interpretability of trading information represent the stronger user need.

7. **The analytical problem extends beyond isolated orders.**  
   Further investigation must consider transactions, positions, realized results, asset-level performance, and portfolio-level performance.

### 14.4 Conditions for Proceeding

The Proceed decision is conditional on validating several critical assumptions before the product direction is considered ready for implementation.

#### Condition 1 — Required Exchange Data

It must be demonstrated that sufficiently complete and reliable exchange data can be obtained to support the calculation of actual trading results.

Related assumptions:

- PA-01 — Sufficient Exchange Data Is Available.
- PA-08 — Required Mercado Bitcoin Data Can Be Accessed Programmatically.

#### Condition 2 — Financial Reconciliation

It must be demonstrated that material transaction calculations can be understood and reconciled with the exchange with sufficient reliability.

This includes investigation of:

- Fees.
- Quantities.
- Execution values.
- Precision.
- Rounding.
- Other exchange rules that materially affect realized results.

Related assumption:

- PA-02 — Exchange Calculations Can Be Reliably Reconciled.

#### Condition 3 — Position and Realized-Result Methodology

A consistent methodology must be established for representing trading activity involving:

- Multiple purchases.
- Aggregated positions.
- Partial sales.
- Partial executions.
- Additional purchases before a position is fully disposed.
- Cancelled and replacement orders.

Related assumption:

- PA-03 — Trading Activity Can Be Represented as Meaningful Trade Cycles.

#### Condition 4 — Secure Data Access

The required exchange integration must be achievable without unacceptable credential, account-access, or sensitive-data risks.

Related assumption:

- PA-11 — Exchange Integration Can Be Implemented Securely.

### 14.5 What This Gate Authorizes

This gate authorizes continued work on:

- Product definition.
- Business-rule discovery.
- Requirements analysis.
- Mercado Bitcoin integration discovery.
- Data investigation.
- Financial calculation validation.
- Position and trade-cycle modeling.
- UX exploration.
- Architecture investigation.
- Security analysis.
- Technical feasibility validation.
- MVP definition and prioritization, subject to validated findings.

The purpose of these activities is to determine whether a viable solution can be defined.

### 14.6 What This Gate Does Not Authorize

This gate does not yet authorize treating the proposed solution as validated.

Specifically, it does not establish that:

- AssetOps is the correct solution.
- ServiceNow is the correct long-term architecture.
- Mercado Bitcoin APIs provide all required information.
- Current spreadsheet formulas are correct.
- Required financial calculations can be reproduced reliably.
- A specific position-cost methodology has been selected.
- Automated trading should be implemented.
- The product can improve or guarantee investment returns.
- The product addresses a validated broader market.
- Development should begin before critical readiness conditions are satisfied.

### 14.7 Reconsideration Triggers

The Product Manager should reconsider the current product direction if subsequent discovery demonstrates that:

- Required transaction data cannot be obtained with sufficient completeness or reliability.
- Material financial results cannot be reconciled with the exchange with sufficient confidence.
- No viable methodology can represent positions and realized results for the user's trading behavior.
- Required account access introduces unacceptable security risks.
- An existing solution is identified that satisfies the user's needs sufficiently and materially changes the rationale for a custom solution.
- New evidence demonstrates that the current problem framing is materially incorrect.

Depending on the finding, the appropriate response may be:

**Proceed**  
Continue when critical assumptions are validated.

**Pivot**  
Change the solution direction, integration approach, product scope, analytical model, or architecture while preserving a validated underlying problem.

**Stop**  
Stop the current product direction if the core value proposition cannot be delivered reliably or the identified need no longer justifies a custom solution.

### 14.8 Scope of Validation

This gate applies only to the current primary-user problem discovery.

It does not represent:

- Market validation.
- Product-market fit.
- Commercial validation.
- Multi-user research validation.
- Solution validation.
- Technical readiness.
- Release readiness.

These require separate evidence and subsequent gates.

### 14.9 Gate Result

**DISCOVERY GATE: PROCEED WITH CONDITIONS**

The problem is sufficiently validated for the current primary user to justify continued product and solution discovery.

The next phase should focus on converting the validated problem understanding into a clearer product definition while prioritizing validation of the critical assumptions that could invalidate or materially change the proposed solution direction.

---

## 15. Current Trading Goals and Behaviors

The user currently follows a small-value trading strategy while learning and validating the process.

These goals describe the user's current behavior and should not be interpreted as guaranteed or expected investment returns provided by AssetOps.

### 15.1 Current Transaction Size

Typical transactions currently range between approximately BRL 1 and BRL 2.

The user intends to experiment with larger transaction values in the future after gaining confidence in the process and calculations.

### 15.2 Minimum Monetary Result

The user currently aims for a minimum positive result of approximately BRL 0.01 per completed buy/sell cycle after trading fees.

This is a user-defined target rather than a guaranteed outcome.

### 15.3 Target Return

The user would like to evaluate trading scenarios that produce positive returns while accounting for trading fees.

An exploratory daily return objective between approximately 0.5% and 3% has been identified by the user.

This is a user-defined objective and not a guaranteed or validated investment outcome.

AssetOps may calculate whether hypothetical or completed transactions meet a user-defined objective, but it should not represent such objectives as guaranteed future returns.

### 15.4 Order Placement Behavior

The user generally:

1. Attempts to place buy orders below the current market price.
2. Waits for the buy order to execute.
3. Calculates a higher target selling price.
4. Evaluates whether the estimated sale would produce an acceptable positive result after fees.
5. Places a limit sell order.
6. Waits for the sell order to execute.
7. Records the result.
8. Repeats the process.

If an order remains open for too long, the user may:

1. Cancel the existing order.
2. Re-evaluate the current market price.
3. Calculate another target price.
4. Re-evaluate the expected result after fees.
5. Submit a replacement order.

The user wants the expected result after fees to remain positive before submitting a replacement order.

### 15.5 Tax Considerations

The user recognizes that taxation may become relevant as transaction volumes and realized gains increase.

AssetOps may eventually need to support:

- Realized gain tracking.
- Acquisition cost tracking.
- Sale proceeds.
- Trading fees.
- Tax-relevant transaction history.
- Monthly summaries.
- Data export for tax calculation or reporting.

Brazilian tax rules applicable to crypto assets must be researched separately using authoritative sources before tax calculations are designed or implemented.

Tax rules must not be hard-coded based on assumptions.

---

## 16. Product Principles

The following principles define durable decision rules for AssetOps.

They are intended to guide product, design, business-rule, architecture, engineering, and prioritization decisions when multiple implementation or experience alternatives are possible.

The principles describe how the product should behave conceptually rather than defining specific features or technologies.

### 16.1 PP-01 — Reliability Before Convenience

AssetOps should prioritize the reliability and integrity of financial information over workflow convenience.

Reducing manual effort, navigation, or interaction cost is valuable, but not when doing so makes financial information less reliable, less understandable, or more difficult to reconcile.

When reliability and convenience conflict, reliability should take precedence.

**Decision implication:**  
A slower or more explicit workflow may be preferable to a simpler workflow that hides uncertainty or presents insufficiently validated information as authoritative.

### 16.2 PP-02 — Preserve the Meaning of Financial Information

AssetOps should maintain clear distinctions between information representing different stages of a transaction or analysis.

In particular:

- Planned values represent user intent.
- Estimated values represent calculated expectations.
- Executed values represent what occurred during exchange execution.
- Realized values represent the financial result derived from completed activity.

These concepts should not be silently substituted for one another.

**Decision implication:**  
When the system cannot determine an actual value reliably, it should communicate the appropriate information state rather than presenting an estimate as an actual result.

### 16.3 PP-03 — Results Should Be Explainable and Traceable

AssetOps should favor financial results that can be understood and traced to their underlying transaction data and applicable calculation rules.

A calculated result should not function only as an unexplained output.

Where appropriate, the user should be able to understand which quantities, costs, proceeds, fees, and other relevant inputs contributed to the result.

**Decision implication:**  
When choosing between a calculation that is easier to display and one that is sufficiently traceable and reconcilable, the product should favor the latter.

### 16.4 PP-04 — Build Intelligence From Reliable Foundations

Higher-level analysis should depend on sufficiently reliable lower-level information.

The current analytical hierarchy is:

Transaction Data  
→ Position and Trade-Cycle Intelligence  
→ Asset-Level Intelligence  
→ Portfolio Intelligence

Portfolio and asset-level conclusions should not create an impression of precision that is unsupported by the underlying transaction and position data.

**Decision implication:**  
A higher-level analytical capability may be deferred when its underlying data or calculation methodology has not yet reached the required level of reliability.

### 16.5 PP-05 — Support Decisions Without Pretending to Predict Outcomes

AssetOps should help the user understand historical results, current positions, financial scenarios, performance, and relevant information for planning future actions.

It should not represent uncertain market outcomes as known or guaranteed.

Scenario analysis represents what may happen under defined assumptions. It does not represent a prediction that those conditions will occur.

**Decision implication:**  
Product language and analytical outputs should distinguish calculated scenarios from predictions, recommendations, and guaranteed investment outcomes.

### 16.6 PP-06 — Validate Before Automating

AssetOps should not automate financial actions or decisions based on logic, data, or calculation rules that have not first been sufficiently understood and validated.

The intended progression is:

Understand  
→ Validate  
→ Support  
→ Automate

Future rule-based or autonomous capabilities should inherit the same reliability, traceability, security, and validation standards applied to manually initiated analytical processes.

**Decision implication:**  
Automation should be deferred when the product cannot yet reliably explain or validate the underlying decision logic or financial result.

### 16.7 Applying the Principles

Product principles should be used as decision criteria rather than absolute substitutes for judgment.

When evaluating a product or technical trade-off, the team should ask:

1. Does this preserve or improve the reliability of financial information?
2. Is the information state clear and correctly represented?
3. Can important financial results be explained and traced?
4. Are higher-level conclusions supported by reliable underlying information?
5. Are scenarios or uncertain outcomes represented honestly?
6. Has the underlying logic been sufficiently validated before automation is introduced?

If a proposed capability conflicts materially with these principles, the conflict should be made explicit and justified before proceeding.

## 17. Product Goals

The following product goals translate the validated problem, discovery findings, product opportunity, and product principles into outcomes that AssetOps should enable.

They describe what the product should help achieve without prescribing specific features, technologies, or implementation approaches.

These goals should guide subsequent MVP scope, prioritization, requirements, and product outcome definition.

### 17.1 PG-01 — Establish Reliable Trade Results

AssetOps should enable the user to determine with confidence the financial result of completed trading activity based on sufficiently reliable transaction data and validated calculation rules.

The product should make relevant quantities, costs, proceeds, fees, and other applicable financial inputs understandable and traceable when determining realized results.

**Intended outcome:**
The user can understand and reconcile whether completed trading activity produced a positive, negative, or neutral net financial result without depending on an unverified external reconstruction.

### 17.2 PG-02 — Provide Complete Position and Trade-Cycle Context

AssetOps should enable the user to understand trading activity as part of meaningful positions and trade cycles rather than only as isolated orders or transactions.

The product should preserve the relationships needed to understand how purchases, sales, partial activity, fees, and other relevant events affect an asset position and its financial result over time.

**Intended outcome:**
The user can evaluate the financial context of an asset position and related trading activity without manually reconstructing that context from disconnected records.

### 17.3 PG-03 — Enable Asset-Level Intelligence

AssetOps should enable the user to evaluate trading and position information at the individual asset level using sufficiently reliable underlying financial data.

Asset-level analysis should help the user understand how each asset contributes to trading results, current exposure, and relevant performance over time without overstating the precision of conclusions unsupported by the underlying data.

**Intended outcome:**
The user can compare and understand the financial behavior and contribution of individual assets to support decisions about where to focus attention and capital.

### 17.4 PG-04 — Enable Portfolio-Level Intelligence

AssetOps should enable the user to understand portfolio-level financial performance and composition using sufficiently reliable underlying position and asset-level information.

Portfolio analysis should preserve meaningful distinctions between realized trading performance and changes in total portfolio value, including the effects of open positions and external cash flows where applicable.

**Intended outcome:**
The user can evaluate portfolio evolution and performance without conflating realized trading results, unrealized changes, or external movements of capital.

### 17.5 PG-05 — Support Informed Trade Planning

AssetOps should enable the user to evaluate potential trading actions using reliable historical, position, and financial context together with clearly stated assumptions.

Planning and scenario analysis should help the user understand how different quantities, prices, fees, and other relevant variables may affect an expected financial result without representing uncertain market outcomes as predictions or guarantees.

**Intended outcome:**
The user can evaluate and compare potential trading scenarios with clearer financial context before deciding whether and how to act.

### 17.6 PG-06 — Reduce Dependence on Manual Reconciliation

AssetOps should reduce the manual effort required to reconstruct, compare, and reconcile financial information across the user's trading workflow.

This reduction should result from providing sufficiently reliable and connected financial context rather than from removing validation steps that are necessary for confidence in the information.

**Intended outcome:**
The user spends less effort manually reconstructing financial context while maintaining or improving confidence in the information used to understand and plan trading activity.

### 17.7 Applying the Product Goals

Product goals should guide product scope, prioritization, and subsequent definition of measurable outcomes.

When evaluating a proposed capability, the team should consider:

1. Which product goal does this capability support?
2. What user outcome is expected to improve?
3. Does the capability depend on a lower-level product goal that has not yet been sufficiently established?
4. Does it improve decision support without overstating certainty or expected investment outcomes?
5. Does it preserve the reliability and traceability required by the Product Principles?

A proposed capability that does not materially support a product goal should require explicit justification before being prioritized.

## 18. Detailed As-Is Process

This section describes the current trading process in operational detail based on the workflow observed and reported during discovery.

Its purpose is to make current activities, systems, decision points, manual calculations, information states, and known uncertainties explicit before defining a future-state process or formal business rules.

The process documented here represents current behavior rather than desired AssetOps behavior. Unvalidated calculations, assumptions, and unresolved exchange behavior should therefore remain identified as such.

### 18.1 Process Participants and Systems

The current process is performed by a single primary user and relies on three external components with different responsibilities.

#### User

The user performs market analysis, plans transactions, places and manages orders, updates the spreadsheet, interprets execution notifications, and decides when to continue, cancel, replace, or reassess trading activity.

#### Mercado Bitcoin

Mercado Bitcoin is the current execution environment for trading activity.

The user treats values presented by Mercado Bitcoin as operationally authoritative when they differ from spreadsheet estimates. The current discovery does not yet establish which specific exchange data should be considered authoritative for every financial attribute or calculation.

#### Spreadsheet

The spreadsheet is a user-created planning, estimation, and tracking tool.

It is used to prepare transactions, estimate quantities, fees and expected results, record execution-related information, and support analysis. Its formulas and reconstructed financial results have not yet been independently validated and should not be treated as authoritative business rules.

#### Email Notifications

Execution emails currently act as workflow triggers that inform the user that trading activity has executed and prompt the next manual step.

They are not currently established as the authoritative source of execution or financial data.

### 18.2 Pre-Buy Analysis and Buy Planning

Before placing a buy order, the user analyzes Mercado Bitcoin charts across multiple horizons to identify exploratory potential entry points.

The user then creates a planned line in the spreadsheet to represent the intended buy activity. This planning step includes estimated price, estimated value in BRL, estimated quantity, estimated fee, and precision.

The spreadsheet values are compared with the values presented by Mercado Bitcoin before confirmation. When there is a difference, the current discovery indicates that the user tends to use the values presented by the exchange.

At this stage, Planned should be understood as the user's intent to buy, while Estimated should be understood as the spreadsheet-based calculation or expectation before execution. These are distinct states in the current process.

### 18.3 Buy Order Placement and Execution

The predominant buy-order pattern currently observed is Limit + Post Only.

The user submits the order to Mercado Bitcoin and the order can remain open without a fixed timeout. While it remains open, the user may re-evaluate the chart and the margin, then maintain, cancel, recalculate, or replace the order.

Execution email notifications function as workflow triggers that signal completion and prompt the next manual step.

After a buy executes, the user updates the spreadsheet manually, including date and status. The current discovery does not establish a systematic post-execution reconciliation process for confirming all financial details against the exchange.

States or behaviors not yet observed should not be inferred here.

### 18.4 Sell Planning

Sell planning currently begins after the buy activity and is oriented toward selling 100% of the position or quantity related to the activity.

The spreadsheet estimates the quantity that can be sold after accounting for the buy fee. The current discovery indicates an unvalidated current-state assumption for the sell fee calculation of `quantity × sell price × 0.003`; this is not a business rule.

The spreadsheet also calculates total, profit, and percentage. The user iteratively adjusts the sell price until the expected result becomes positive and may increase the target price further if market conditions appear to support it.

The planned sell quantity is compared with the quantity that Mercado Bitcoin allows the user to sell at 100%. When there is a difference, the user currently copies the exchange value back into the spreadsheet.

At this stage, Planned should be understood as the user's intent to sell, while Estimated should be understood as the spreadsheet-based calculation or expectation before execution. These are distinct states in the current process.

### 18.5 Sell Order Placement and Execution

The sell order is submitted to Mercado Bitcoin after planning is complete.

If the sell order remains open, the current re-evaluation pattern is the same as for buys: the user may continue waiting, cancel, recalculate, or replace the order. No fixed timeout has been established.

Execution email notifications again function as workflow triggers and prompt manual update activity.

After a sell completes, the user updates the spreadsheet manually and then begins planning the next buy. The current discovery does not provide a verified and reliable independent reconstruction of the realized net result from the process as a whole.

### 18.6 Exceptional and Incomplete Order States

A partial fill was observed at least once, and in that instance the user waited for completion.

The current discovery does not establish a formal process for partial fills that remain open for an extended period.

Cancelled and replaced orders are part of current re-evaluation behavior, but their detailed rules are not yet formalized.

The current discovery does not justify assuming Mercado Bitcoin rules for partial execution, cancellation, replacement, fees, precision, or rounding beyond what has been observed.

These items should be treated as gaps or unknowns that require further analysis.

### 18.7 Current Information-State Flow

The current process can be described as a progression through four information states:

PLANNED → ESTIMATED → EXECUTED → REALIZED

Planned is the user's intention. Estimated is the calculation or expectation before execution. Executed is what actually occurred on the exchange. Realized is the financial result derived from completed activity.

The current process does not guarantee a reliable or reconciled transition across all of these states.

### 18.8 Manual Handoffs and Reconciliation Points

The key handoffs in the current process are Mercado Bitcoin → Spreadsheet, Email → User, User → Spreadsheet, Spreadsheet → Mercado Bitcoin during planning, and Mercado Bitcoin → Spreadsheet when values diverge.

The work of comparison, update, reconstruction, and financial interpretation is manual.

### 18.9 As-Is Gaps and Unresolved Rules

The discovery leaves several rules unresolved: authoritative source by financial attribute, actual fee determination, precision and rounding, sellable quantity, reliable realized-result calculation, multiple purchases, partial sales, partial executions, cancelled or replacement orders, position and trade-cycle methodology, historical reconstruction, and the current dependence on email as a workflow trigger.

These items should be distinguished as observed behavior, unvalidated current calculation or assumption, or unknown.

### 18.10 As-Is Process Summary

Analyze Market → Plan Buy → Estimate Values → Compare with Exchange → Place Buy Order → Wait/Reassess → Buy Executes → Update Spreadsheet → Plan Sell → Estimate Result → Compare Sellable Quantity → Place Sell Order → Wait/Reassess → Sell Executes → Update Spreadsheet → Start Next Cycle

Cancelled orders, replacements, and partial executions can interrupt or deviate from this flow, and their rules remain incomplete in the current discovery.

## 19. To-Be Process

This section describes the intended future process for AssetOps based only on the validated discovery findings, Product Principles, Product Goals, and documented As-Is process.

The To-Be process is meant to preserve reliable and traceable financial information, connect the full trading lifecycle, reduce manual reconstruction, and support decision-making without treating convenience as more important than reliability.

### 19.1 Future-State Process Objectives

The future-state process should preserve trustworthy financial information, maintain traceability from input to result, and connect the complete lifecycle of trading activity.

It should reduce the need for manual reconstruction by presenting connected context, validated calculations, and clear state transitions.

It should also provide enough context for the user to make informed trading decisions while keeping reliability and validation ahead of convenience.

### 19.2 Future-State Participants and Responsibilities

The future-state process should distinguish responsibilities among the user, AssetOps, and Mercado Bitcoin.

The user remains responsible for market judgment, trading decisions, and initiating actions.

Mercado Bitcoin remains the execution and data environment for available exchange-side information.

AssetOps consolidates, structures, calculates, reconciles, and presents information only when the necessary data and rules have been sufficiently validated. It should not present unvalidated calculations as authoritative.

Email should not be treated as an authoritative source in the future-state process. If it remains part of the workflow, it should function only as a notification or trigger input, not as the source of truth.

### 19.3 Information-State Lifecycle

The future-state process should preserve the lifecycle PLANNED → ESTIMATED → EXECUTED → REALIZED.

Planned represents the user's intent. Estimated represents the pre-execution calculation or scenario. Executed represents the known exchange-side outcome. Realized represents the financial result derived from completed activity when the necessary information and rules are sufficiently available.

A later state should not be inferred, displayed, or treated as authoritative without sufficient evidence and data support.

### 19.4 To-Be Buy Planning and Execution

The buy process should begin with observing context and analyzing the available information needed to plan a buy.

The user then forms a planned action, and AssetOps can calculate an estimated scenario once the required inputs and rules are sufficiently validated.

Before submission, the necessary inputs should be validated to the extent currently supported by reliable data and business rules.

The user makes the decision to proceed, after which the order is submitted and tracked, the execution state is captured, and the position and related financial context are updated.

This process should not invent exchange endpoints, fee structures, or order rules beyond what discovery has already established.

### 19.5 To-Be Sell Planning and Execution

The sell process should use the current position and sufficiently reliable financial context to define a sell scenario.

AssetOps should calculate estimated proceeds, fees, and expected result only according to validated rules and sufficient data.

The user then decides whether to proceed, the order is executed, actual data is captured, and the realized result is determined or reconciled when possible.

This process should remain dependent on validated data and rules rather than assuming any unverified exchange behavior.

### 19.6 Position and Trade-Cycle Evolution

The future-state process should represent buys, sells, and partial activity as events that may alter a position and its broader trade-cycle context.

The methodology used to derive position state or trade-cycle result should not assume average cost, FIFO, or any other accounting method that has not yet been validated.

That methodology remains a dependency for business-rule analysis.

### 19.7 Order State and Exception Handling

The future-state process should conceptually include open, pending, executed, partially executed, cancelled, replaced, and replaced-by-new-order states where applicable.

It should preserve the real known state of an order and avoid silently treating incomplete activity as complete.

The detailed order-state rules for Mercado Bitcoin remain dependent on further technical and integration discovery.

### 19.8 Reconciliation and Data Confidence

The future-state process should explicitly reconcile captured data, validated rules, and derived results.

Divergences should remain visible and unresolved rather than being silently replaced by estimates.

The process should clearly distinguish authoritative source, derived value, and user-entered or planned value.

### 19.9 Asset and Portfolio Intelligence

The future-state process should progress from transaction data to position and trade-cycle intelligence, then to asset-level intelligence, and then to portfolio intelligence.

Higher-level intelligence should depend on sufficiently reliable lower-level fundamentals.

The process should preserve the separation between realized trading performance, unrealized information, and portfolio value performance, including external cash flows when applicable.

### 19.10 Decision Support and Future Automation

Planning and scenario analysis should support decisions without predicting or guaranteeing outcomes.

The future-state model should follow the conceptual progression Understand → Validate → Support → Automate.

Future automation for financial actions should remain dependent on validated data, rules, security, and logic and should not be assumed as part of this initial To-Be process.

### 19.11 Remaining Dependencies and Decision Points

The future-state process still depends on several unresolved decision points: exchange/API data sufficiency, authoritative source per attribute, actual fees, precision and rounding, sellable quantity, partial execution behavior, cancellation and replacement behavior, position and trade-cycle methodology, realized-result methodology, historical reconstruction, security and authentication, and idempotency or synchronization where applicable.

These points should remain open for later analysis and not be resolved implicitly in this section.

### 19.12 To-Be Process Summary

Observe Context → Plan Action → Calculate Scenario → Validate Required Information → User Decision → Submit/Track Order → Capture Actual Execution → Update Position / Trade-Cycle Context → Reconcile Financial Result → Update Asset / Portfolio Intelligence → Support Next Decision

Exception states can redirect the process back to tracking, reconciliation, or a new user decision when the order or financial state is incomplete or unresolved.
