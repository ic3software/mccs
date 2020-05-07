# Functionality - Alpha Release

[User Functionality](#user-functionality)  
[Admin Functionality](#admin-functionality)

## User Functionality

There are four main functions that the MCCS web application provides to end users:

1. **Manage accounts** - create and modify user records and their related entity details
2. **Find entities** - view and search for entities based on the good and services they provide and need
3. **Transfer mutual credits** - create and complete/cancel mutual credit (MC) transfers between entities
4. **Review transfer activity** - view one's pending and completed MC transfers and current MC balance

### Manage Accounts

Individual users can create an account in MCCS by providing an email address, creating a password and adding some other details about themselves and their related entities: an incorporated business, a not-for-profit organization, etc. An entity need not be a formal business or organization; it can  be a sole proprietorship with a list of services or goods that the individual is willing to offer to other participants in the network. Account management includes standard features like:

- Create account
- Login/logout
- View and modify one's user & entity details
- Reset a lost password
- Change password

Review the [MCCS data model](alpha-data-model.md) to see how users and entities are related.

### Find Entities

MCCS enables each entity to list its "offers" (goods and services it can provide to the network) and "wants" (goods and services it would like to procure from the network), and to see the offers and wants of the other participants. There is a matching algorithm that looks for corresponding wants that match am entity's offers and offers that match an entity's wants.

From the users' perspective, once they have listed their entities' offers and wants, MCCS will propose potential trades to them with other users' entities. These potential trades are searchable through the `GET /entities` API endpoint, and entities can opt into a daily email notification that displays all of the matches to their offers and wants that occured in the previous 24 hours.

MCCS' matching logic searches for exact matches, wildcard matches and fuzzy matches, so a search for "vegetables" will not only turn up "vegetables" (exact match) but also "organic-vegetables" (wildcard match) and "vegetalbes" (fuzzy match, which can pick up typos or spelling variations).

Aside from the tagging feature on offers and wants, MCCS also offers a standard directory (like the Yellow Pages). An admin running MCCS can assign one or more categories to each entity and the users can browse these categories alphabetically, just like in a telephone directory.

Entities are able to send introductory emails to each other to start a dialog about a trade. The entity receiving the first email does not have to expose its email address to the party contacting them. Only if the contacted entity replies will its email be exposed as the conversation continues between them through regular email.

Finally, entities can flag other entities as "favorites" so they can be easily found.

### Transfer Mutual Credits

Each entity in MCCS has a MC transfer account that it can pay from or accept payment to in order to facilitate transfers between entities. The sum of those increases and decreases will yield the current balance of that entities' transfer account. IOW, it is the same functionality you would expect from a [basic bank accounting system](https://medium.com/@RobertKhou/double-entry-accounting-in-a-relational-database-2b7838a5d7f8).

The following rules will be enforced by MCCS:

- Every increase in one account must be offset by an equal decrease in another account (or set of accounts in the case of collecting fees). So if Account A is decreased by 50, Account B will be increased by 50 (or Account B could be increased by 49 and Account C by 1).
- Given the above, the sum total of all transfers, and the overall balance in the system must always equal zero. These are the two foundational principles of double-entry bookkeeping and they must be enforced at all times.
- In order to start the transfer process, some accounts will need to be able to have a negative balance (see Account A above), but not all accounts may need be allowed to have a negative balance. MCCS admins will need to make a decision about which entities may have an account whose balance can be negative.
- There needs to be a limit to the positive and negative balances for accounts (maxPositiveBalance and maxNegativeBalance). A transfer can only be processed if the resulting balances of all accounts involved in the transfer do not exceed these limits. Continuing the example above, if the maxNegativeBalance for Account A is set to -40, the transaction above would not be processed because the balance of Account A would be exceeding this limit by going to -50. And if the maxNegativeBalance for an account is set to 0, then that account is not allowed to have a negative balance at all.

#### Initiating Debits or Credits

Users will be able to create transfers that result in either a **debit from** or a **credit to** their account. This is unusual given that most online payment systems only allow the former. A practical application of this ability to initiate a credit to one's account is that a supplier could setup the payment from their customer within MCCS. The customer would login, see the invoice link in the payment description and if in agreement, confirm the debit of funds from their entity's account.

#### Two-Step Transfers

One of the objectives behind a mutual credit system is to enable participants to vet transfers before the mutual credits (MCs) are added to or, in the case of payee-initiated transfers, removed from their accounts. This requires that a transfer must first be authorized by by both the sender and receiver of the MCs before the transfer is completed and the accounts are debited and credited accordingly.

To enable this two step transfer process, state has been introduced into transfers, so a transfer can be in one of only three possible states at any given moment:

1. **Initiated** - a transfer has been initiated by either the payer or payee of the MCs.
2. **Completed** - a transfer is completed because the payee/payer has authorized the credit to/debit from their account that was proposed in the initiated transfer.
3. **Cancelled** - a transfer can be cancelled because (a) the initiator cancels it before the receiver has a chance to accept it, (b) the receiver can decide to reject the transfer, or (c) the transfer is not allowed by the system due to balance limits or other reasons even if the receiver accepts it.

Only transfers in the completed state will affect the balances of the payer's and payee's accounts. Cancelled transfers will trigger an email to both the payer and payee to inform them of the cancelled transfer.

### Review Transfer Activity

A user can review the initiated, cancelled and completed transfers in their entity's MC transfer account. For each transfer in the _initiated_ state, if the user created the transfer, that user has the option to cancel it before the receiver of the transfer approves or rejects the transfer. If the user has received a transfer, that user can decide whether to approve or reject it. Transfers approved by the receiver are set to _completed_ state, while transfers rejected (by the receiver) and cancelled (by the initiator) are set to _cancelled_ state.

A user can also request the current MC balance of their entity's account.

## Admin Functionality

🚧 **This is a work in progress** 🚧

There are five main functions that the MCCS web application provides to admin users:

1. **Manage users** - view, modify and delete user records
2. **Manage entities** - view, modify and delete entity records
3. **Manage categories and tags** - view, modify and delete categories and tags
4. **Manage transfers** - view user transfers and initiate transfers on behalf of users
5. **Audit logs** - view all admin and user activity that modifies DB data (change of details, transfers, etc.)

### Manage Users

- Can only change user email to a unique email (can't already be used by another user)
- Future-proofed entity mapping by storing an array of linked entities
- `email` needs to be renamed to `userEmail` (TODO)

### Manage Entities

- `email` needs to be renamed to `userEmail` (TODO)
- `accountNumber` is the unique key that links an in MongoDB to its transfer and balance data in PostgreSQL
- `status` should be renamed to `entityStatus` (TODO)
- `entityStatus` drives functionality available to an entity and can have 6 possible values (TODO - _how to split these so trading status is not dependent on directory status?_):
    - `pending`
    - `rejected`
    - `accepted`
    - `tradingPending`
    - `tradingAccepted`
    - `tradingRejected`
- Future-proofed user mapping by storing an array of linked users
- Explain purpose of `dailyNotification` boolean field
- `turnover` should be renamed `expectedTurnover` since it is only an estimate provided by the user that needs to be verified (historic accounts and/or volumes in MCCS over time)

### Manage Categories and Tags

- Explain purpose of `offerAddedAt` and `wantAddedAt` datetime fields

### Manage Transfers

- `account_number` is the unique key that links transfer and balance data in PostgreSQL to an entity in MongoDB
- Explain `cancellation_reason` field
- `status` should be renamed to `transferStatus`, and can have 3 possible values:
    - `initiated`
    - `cancelled`
    - `completed`
- Explain `initiated_by` field
- Explain `from_*` and `to_*` fields
- Explain the `type` field (future-proofing different transaction types in addition to user-initiated)

TODO - Link `postgresql_accounts` and `postgresql_balance_limits` by `account_number` instead of `id`

### Audit Logs

Logs show all actions by users and admins that change the data in MCCS' DBs. IOW, all POST, PATCH and DELETE actions performed are logged stating the prior and subsequent state of all affected DB fields (for changes) or what information has been created (POSTs) or removed (DELETEs).
