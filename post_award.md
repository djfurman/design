# Post Award

The post award application supports the review and execution phases of the procurement life cycle after the contract has been awarded. This application discontinues support at the point where a contract has been closed out and reconciled.

## Life-cycle Events

- Agreement was issued
- Agreement was received
- Funding was received
- Shipment was scheduled
- Items were shipped
- Bill was received
- Shipment was received
- Items were accepted
- Funds availability were verified
- Bill was scheduled for payment
- Bill was paid
- Accounting period ended
- Payment was released
- All items were shipped
- Agreement was terminated
- Agreement was closed

## Program Increment 1

Agreement receipt, basic validation and user review of online data

### Epics

- Fill in object model with realistic but fake data, normalize data in db, retrieve data from db
- Show agreement on screen for review, allowing user to see all details
- Show agreement validation on screen for review with meaningful validation failures

### Agreement validation

Do as listeners

- No shipments before effective date
- Approved Vendor
- Sum(`[cost = item.quantity * item.unit_price for item in items_list]`) <= agreement.total_value
- Valid delivery locations
- Both a buyer and seller party are required
- Sum(`[amount_funded = account.fund_amount for account in fund_list]`) <= agreement.total_value

### Assumptions

- No need to validate buyers, they wouldn't be here if they weren't valid
- Implements Agreement was received life-cycle event
- Okay to mock lookups for validations
