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

Based on the user's current workflow, the following pain points have been identified.

### 5.1 Manual Transaction Tracking

Every buy or sell transaction needs to be manually recorded or updated in a spreadsheet.

This creates repetitive work and introduces the possibility of data-entry errors, missing transactions, and outdated information.

### 5.2 Manual Trade Calculations

The spreadsheet contains calculated fields that help the user understand the financial result of individual trades.

These calculations depend on manually maintained transaction data and manually configured formulas.

### 5.3 Target Selling Price Calculation

After purchasing an asset, the user needs to determine an appropriate selling price for a future limit order.

The target price may depend on factors such as:

- Purchase price.
- Purchased quantity.
- Trading fees.
- Desired monetary return.
- Desired percentage return.
- Numeric precision and exchange restrictions.
- Previous transactions involving the same asset.

The user currently relies on spreadsheet calculations to support this decision.

### 5.4 Buy Target Decision

After a sell transaction is completed, the user wants to eventually create another buy order.

However, the user does not currently have a clearly defined rule for determining the next target buying price.

This is different from calculating a selling target after a known purchase because the future market price is unknown.

A future AssetOps capability could support scenario analysis, allowing the user to evaluate hypothetical buy and sell combinations and their estimated results.

The application should not assume that a specific buying price will guarantee a future profit.

### 5.5 Fragmented Workflow

Trade execution happens in Mercado Bitcoin, execution confirmation is received by email, and trade analysis happens in a separate spreadsheet.

The user therefore needs to move between multiple tools throughout the trade cycle.

### 5.6 Data Synchronization

Because transaction information is manually transferred from Mercado Bitcoin into the spreadsheet, the spreadsheet may not always represent the latest account state.

### 5.7 Portfolio Visibility

Individual transactions are tracked, but understanding their relationship with the overall portfolio requires additional calculations and organization.

Initial hypotheses include:

- Difficulty consolidating portfolio information.
- Limited visibility into portfolio evolution over time.
- Need to manually combine information from different sources.
- Difficulty understanding portfolio allocation.
- Difficulty connecting trading activity with overall portfolio performance.

### 5.8 Numeric Precision and Rounding

The user has identified differences between spreadsheet calculations and the values accepted or calculated by Mercado Bitcoin.

One possible source of these differences is the number of decimal places and increments supported for asset quantities, prices, or monetary values.

The spreadsheet may use a different numeric precision from the exchange.

The exact Mercado Bitcoin rules for the following have not yet been fully validated:

- Asset quantity precision.
- Price precision.
- Minimum quantity increments.
- Minimum price increments.
- Rounding behavior.
- Order quantity restrictions.
- Trading fee precision.

This creates uncertainty when transferring calculated transaction values from the spreadsheet into Mercado Bitcoin.

AssetOps must not assume precision or rounding rules. These rules must be identified from official API or exchange specifications and tested before financial calculations are implemented.

### 5.9 Trading Fee Calculation

Trading fees directly affect the actual cost and return of each transaction.

The user's current spreadsheet calculations account for trading fees, which may differ depending on whether an execution is classified as maker or taker.

Incorrect or outdated fee assumptions can cause differences between spreadsheet calculations and the actual financial result of a trade.

AssetOps should minimize manual fee configuration whenever reliable fee information is available through the Mercado Bitcoin API.

The application should distinguish between estimated fees for planned transactions and actual fees associated with completed executions.

---

## 6. Existing Solutions

The primary existing solution is the Mercado Bitcoin platform itself.

The user also maintains a custom spreadsheet to complement the exchange by tracking transactions, calculating fees, planning future orders, and calculating trade results.

AssetOps is not intended to replace Mercado Bitcoin as an exchange.

Instead, it explores how ServiceNow can be used as an application platform to integrate exchange data with personalized portfolio management, trade tracking, calculations, and decision-support capabilities.

---

## 7. Opportunity

There is an opportunity to replace part of the user's spreadsheet-based workflow with an integrated application.

By retrieving account, order, execution, fee, and market data directly from Mercado Bitcoin, AssetOps could reduce manual data entry and provide calculated information that helps the user understand individual trades and the overall portfolio.

Potential capabilities include:

- Automatically retrieving transaction and execution information.
- Maintaining a structured transaction history.
- Tracking planned, open, executed, and cancelled orders.
- Calculating acquisition costs.
- Calculating average purchase prices.
- Tracking current asset positions.
- Retrieving applicable maker and taker fees.
- Recording actual execution fees.
- Estimating the result of a potential sale.
- Calculating target selling prices based on user-defined return objectives.
- Supporting hypothetical buy and sell scenarios.
- Comparing target prices with current market prices.
- Monitoring portfolio allocation and performance.
- Identifying differences between estimated and actual transaction results.

The initial goal is not to automate investment decisions.

AssetOps should provide information, calculations, and scenario analysis that support the user's own decision-making process.

### 7.1 Automated Trading Fee Handling

AssetOps should retrieve the user's current maker and taker trading fees from Mercado Bitcoin whenever possible.

For planned transactions, these rates can be used to estimate transaction costs and potential results.

For completed transactions, AssetOps should prioritize actual execution data returned by Mercado Bitcoin whenever available.

This allows AssetOps to distinguish between:

- Estimated fees before execution.
- Actual fees after execution.
- Maker executions.
- Taker executions.
- Estimated transaction results.
- Actual transaction results.

---

## 8. Assumptions

The initial assumptions are:

- The user has an active Mercado Bitcoin account.
- The Mercado Bitcoin API provides enough data to support the initial use cases.
- The application can securely authenticate with the Mercado Bitcoin API.
- ServiceNow can consume and process the required API data.
- Order execution information can be retrieved from Mercado Bitcoin without relying exclusively on email notifications.
- Trading fee information can be retrieved or reliably derived from Mercado Bitcoin data.
- Instrument-specific precision and order restrictions can be identified.
- The first version will focus on read-only portfolio and trade management.
- Real trading functionality will not be part of the initial MVP.
- Planned transactions and scenario analysis can initially exist only inside AssetOps without creating real exchange orders.
- Tax calculations will not be implemented until the applicable rules have been separately researched and validated.

These assumptions must be validated during discovery and technical investigation.

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
