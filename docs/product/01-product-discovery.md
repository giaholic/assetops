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

The initial user of AssetOps is the product creator herself, who actively uses Mercado Bitcoin to buy and sell digital assets.

The user currently relies on a spreadsheet to manually track transactions and perform calculations related to purchases, sales, trading fees, portfolio positions, target selling prices, and trade results.

### 3.2 User Context

The user:

- Has an active Mercado Bitcoin account.
- Buys and sells digital assets.
- Primarily uses limit orders when planning trades.
- Records transactions manually in a spreadsheet.
- Uses calculated spreadsheet fields to analyze trades.
- Evaluates potential selling prices after purchasing an asset.
- Wants to understand whether a potential sale would achieve a desired positive return after fees.
- Uses email notifications as the primary trigger for identifying completed orders.
- Manually transfers information between Mercado Bitcoin and the spreadsheet.
- Wants to reduce the amount of manual data entry and calculation involved in this process.
- Wants to better understand how to determine potential re-entry prices after completing a sale.

---

## 4. Current Workflow (As-Is)

The user's current trading workflow is highly manual and is split between Mercado Bitcoin, email notifications, and a spreadsheet.

### 4.1 Buy Order Execution

1. The user manually creates a buy order in Mercado Bitcoin.
2. Mercado Bitcoin executes the order when the required market conditions are met.
3. The user receives an email notification informing her that the order has been executed.
4. The email notification is currently the primary trigger used by the user to identify that an order has been completed.
5. The user opens her spreadsheet.
6. She manually marks the corresponding buy order as executed.
7. She records or updates the transaction information.
8. She creates a new row representing a planned future sell transaction.
9. Spreadsheet formulas are used to calculate a target selling price intended to produce a desired positive return after trading fees.
10. The user opens Mercado Bitcoin again.
11. She manually creates a limit sell order using the calculated transaction values.
12. She compares Mercado Bitcoin's calculated values with the spreadsheet results before submitting the order.
13. If the values differ, she may need to manually adjust the transaction values.

### 4.2 Sell Order Execution

1. Mercado Bitcoin executes the sell order.
2. The user receives an email notification confirming the execution.
3. The user opens the spreadsheet.
4. She marks the corresponding sell transaction as executed.
5. She records or updates the transaction information.
6. The spreadsheet calculates the monetary result and percentage return of the completed buy/sell cycle.
7. The user then considers creating another buy order to start a new trade cycle.
8. Unlike the selling-price calculation, the user does not currently have a well-defined rule for determining an appropriate new buying price.

### 4.3 Open Order Reassessment

If an order remains open for too long, the user may:

1. Cancel the existing order.
2. Re-evaluate the current market price.
3. Recalculate a target price.
4. Verify whether the new scenario still produces an acceptable estimated result after fees.
5. Submit a replacement order.

### 4.4 Current Trade Cycle

The current process can therefore be represented as:

Buy Order  
→ Execution  
→ Email Notification  
→ Spreadsheet Update  
→ Sell Target Calculation  
→ Manual Limit Sell Order  
→ Execution  
→ Email Notification  
→ Spreadsheet Update  
→ Result Calculation  
→ New Buy Target Decision  
→ Manual Buy Order  
→ Repeat

### 4.5 Systems Currently Used

The workflow currently depends on three separate tools:

- **Mercado Bitcoin:** order creation, execution, cancellation, and market information.
- **Email:** execution notification.
- **Spreadsheet:** transaction tracking, calculations, trade planning, and result analysis.

The user manually transfers and reconciles information between these systems.

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
