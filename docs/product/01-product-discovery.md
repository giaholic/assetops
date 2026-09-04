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

## 9. Questions

The following questions need to be validated during discovery.

### 9.1 Product and Portfolio Questions

- Which portfolio information is most valuable to the user?
- How frequently should portfolio data be synchronized?
- Which historical information should be stored?
- How should portfolio performance be calculated?
- Which Mercado Bitcoin API endpoints are required?
- What limitations exist in the Mercado Bitcoin API?
- How should API failures and unavailable data be handled?
- What security controls are required for API credentials?
- Which ServiceNow capabilities are best suited for each requirement?

### 9.2 Trade Calculation Questions

- How does the user currently calculate the target selling price?
- Does the current calculation correctly account for all trading fees?
- How should multiple purchases of the same asset be handled?
- Should AssetOps use average cost, individual lots, or another cost-basis method?
- How should partial sales be handled?
- How should previous sales affect the remaining position?
- Should the user specify a desired percentage return, desired monetary return, or both?
- Should AssetOps calculate a break-even selling price?
- Should the application distinguish between realized and unrealized results?
- Which transaction information can be retrieved directly from Mercado Bitcoin?
- Can the API provide enough historical information to reconstruct the user's existing portfolio and trade history?

### 9.3 Order Execution and Notification Questions

- Can AssetOps determine directly from the Mercado Bitcoin API when an order has been executed?
- If execution information is available through the API, is the email notification still necessary for the application workflow?
- Should email remain only as an external confirmation mechanism?
- How quickly does an updated order execution status become available through the API?
- Can orders be partially executed?
- How should partial executions be represented?
- How should cancelled and replaced orders be related to one another?

### 9.4 Precision and Calculation Questions

- What quantity precision does Mercado Bitcoin support for each asset or trading pair?
- What price precision does Mercado Bitcoin support for each trading pair?
- Are there minimum quantity increments?
- Are there minimum price increments?
- What rounding rules are applied?
- At which stage are fees calculated?
- In which asset or currency is each fee charged?
- Does precision vary by trading pair?
- Can precision rules be retrieved through the API?
- Why do current spreadsheet calculations sometimes differ from Mercado Bitcoin calculations?
- How should AssetOps normalize calculated values before comparing them with exchange values?

### 9.5 Trade Cycle Questions

- What rules does the user currently use to determine a desired positive return?
- Is the target expressed as a percentage, monetary amount, or both?
- Should fees be included when determining the target sell price?
- Should taxes be considered separately from exchange fees?
- What should happen when several purchases of the same asset occur at different prices?
- What should happen when only part of a position is sold?
- How should a new buy target be calculated after a sale?
- Should a new buy target be based on the previous selling price?
- Should the user define a desired price decrease before re-entry?
- Should AssetOps provide multiple hypothetical buy scenarios rather than one recommended buying price?
- How should AssetOps represent a complete buy/sell trade cycle?
- How should cancelled and replacement orders affect the trade cycle?

### 9.6 Trading Fee Requirements to Validate

- AssetOps should retrieve the current maker fee for a trading pair whenever possible.
- AssetOps should retrieve the current taker fee for a trading pair whenever possible.
- Fee rates should not be hard-coded.
- Fee information should be associated with the corresponding trading pair.
- Planned transactions should use applicable fee information to estimate transaction costs.
- Completed transactions should store the actual fee returned by Mercado Bitcoin whenever available.
- Completed executions should store whether the execution was maker or taker whenever this information is available.
- Completed executions should store the actual fee rate returned by Mercado Bitcoin whenever available.
- Estimated and actual fees should be stored and displayed separately.
- AssetOps should be able to identify differences between estimated and actual transaction costs.

---

## 10. Initial Hypothesis

If Mercado Bitcoin account, transaction, execution, fee, and market information is consolidated into a structured ServiceNow application, the user will be able to reduce manual transaction tracking, improve the consistency of trade calculations, better understand the financial result of completed trades, and evaluate future trade scenarios more efficiently.

If AssetOps can automatically retrieve exchange data and apply validated calculation, fee, precision, and rounding rules, it may reduce the discrepancies currently experienced between spreadsheet calculations and Mercado Bitcoin values.

The product may also provide a simpler way to monitor digital assets, understand portfolio allocation, and analyze portfolio evolution over time.

These hypotheses will be validated and refined as product discovery and technical investigation progress.

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

## 12. Current Trading Goals and Behaviors

The user currently follows a small-value trading strategy while learning and validating the process.

These goals describe the user's current behavior and should not be interpreted as guaranteed or expected investment returns provided by AssetOps.

### 12.1 Current Transaction Size

Typical transactions currently range between approximately BRL 1 and BRL 2.

The user intends to experiment with larger transaction values in the future after gaining confidence in the process and calculations.

### 12.2 Minimum Monetary Result

The user currently aims for a minimum positive result of approximately BRL 0.01 per completed buy/sell cycle after trading fees.

This is a user-defined target rather than a guaranteed outcome.

### 12.3 Target Return

The user would like to evaluate trading scenarios that produce positive returns while accounting for trading fees.

An exploratory daily return objective between approximately 0.5% and 3% has been identified by the user.

This is a user-defined objective and not a guaranteed or validated investment outcome.

AssetOps may calculate whether hypothetical or completed transactions meet a user-defined objective, but it should not represent such objectives as guaranteed future returns.

### 12.4 Order Placement Behavior

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

### 12.5 Tax Considerations

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

## 13. Discovery Principles

The following principles will guide the next stages of the project:

### 13.1 Do Not Assume Exchange Rules

Fee, precision, rounding, order, and execution rules must be validated against Mercado Bitcoin documentation and actual API behavior.

### 13.2 Separate Estimated and Actual Values

AssetOps should clearly distinguish between:

- Planned transactions and real orders.
- Estimated fees and actual fees.
- Estimated results and realized results.
- Hypothetical prices and executed prices.

### 13.3 Support Decisions, Do Not Guarantee Outcomes

AssetOps may calculate scenarios and expected results based on user-defined assumptions.

It should not guarantee that a particular buy or sell price will result in future profit.

### 13.4 Prefer Source Data Over Manual Reconstruction

Whenever reliable information is available directly from Mercado Bitcoin, AssetOps should prefer that information over manually reconstructed values.

### 13.5 Validate Before Automating

Existing spreadsheet formulas should be treated as current-state business logic to investigate, not automatically as the correct future-state implementation.

Each financial calculation should be documented, validated, and tested before being implemented in ServiceNow.
