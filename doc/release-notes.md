GiveHope Core version 1.0.0 is now available from:

  <https://github.com/givehopecoin/GiveHopeCore.git>

This is the initial release of GiveHope Coin.  Credit must be given to the teams
before (BitCoin, Dash, Pivx, Worx) for the initial work that has been contributed
to the base code.  The GiveHope Dev Team have improved and added additional features
that users will love compared to other existing qt wallets out currently.

Please report bugs using the issue tracker at github:

  <https://github.com/givehopecoin/GiveHopeCore/issues>

Compatibility
==============

GiveHope Core is extensively tested on multiple operating systems using
the Linux kernel, macOS 10.8+, and Windows Vista and later.

Microsoft ended support for Windows XP on [April 8th, 2014](https://www.microsoft.com/en-us/WindowsForBusiness/end-of-xp-support),
No attempt is made to prevent installing or running the software on Windows XP, you
can still do so at your own risk but be aware that there are known instabilities and issues.
Please do not report issues about Windows XP to the issue tracker.

GiveHope Core should also work on most other Unix-like systems but is not
frequently tested on them.

Notable Changes
===============

| Ability to change from 'Default' to 'Dark' color scheme on the qt wallet
| Ability to define how many transactions are listed on the main Overview page
| Many compiler warnings have been re-factored to the up-to-date c++ routines
 


RPC changes
--------------

#### Update of RPC commands to comply with the forthcoming RPC Standards PIP ####

| Old Command | New Command | Notes |
| --- | --- | --- |
| `masternode count` | `getmasternodecount` | |
| `masternode list` | `listmasternodes` | |
| `masternodelist` | `listmasternodes` | renamed |
| `masternode connect` | `masternodeconnect` | |
| `masternode current` | `getcurrentmasternode` | |
| `masternode debug` | `masternodedebug` | |
| `masternode enforce` |  | removed |
| `masternode outputs` | `getmasternodeoutputs` | |
| `masternode status` | `getmasternodestatus` | |
| `masternode list-conf` | `listmasternodeconf` | added optional filter |
| `masternode genkey` | `createmasternodekey` | |
| `masternode winners` | `listmasternodewinners` | |
| `masternode start` | `startmasternode` | see notes below |
| `masternode start-alias` | `startmasternode` | see notes below |
| `masternode start-<mode>` | `startmasternode` | see notes below |
| `masternode create` | | removed - not implemented |
| `masternode calcscore` | `listmasternodescores` | |
| --- | --- | --- |
| `mnbudget prepare` | `preparebudget` | see notes below |
| `mnbudget submit` | `submitbudget` | see notes below |
| `mnbudget vote-many` | `mnbudgetvote` | see notes below |
| `mnbudget vote-alias` | `mnbudgetvote` | see notes below |
| `mnbudget vote` | `mnbudgetvote` | see notes below |
| `mnbudget getvotes` | `getbudgetvotes` | |
| `mnbudget getinfo` | `getbudgetinfo` | see notes below |
| `mnbudget show` | `getbudgetinfo` | see notes below |
| `mnbudget projection` | `getbudgetprojection` | |
| `mnbudget check` | `checkbudgets` | |
| `mnbudget nextblock` | `getnextsuperblock` | |

##### `startmasternode` Command #####
This command now handles all cases for starting a masternode instead of having multiple commands based on the context. Command arguments have changed slightly to allow the user to decide wither or not to re-lock the wallet after the command is run. Below is the help documentation:

```
startmasternode "local|all|many|missing|disabled|alias" lockwallet ( "alias" )

 Attempts to start one or more masternode(s)

Arguments:
1. set         (string, required) Specify which set of masternode(s) to start.
2. lockWallet  (boolean, required) Lock wallet after completion.
3. alias       (string) Masternode alias. Required if using 'alias' as the set.

Result: (for 'local' set):
"status"     (string) Masternode status message

Result: (for other sets):
{
  "overall": "xxxx",     (string) Overall status message
  "detail": [
    {
      "node": "xxxx",    (string) Node name or alias
      "result": "xxxx",  (string) 'success' or 'failed'
      "error": "xxxx"    (string) Error message, if failed
    }
    ,...
  ]
}

Examples:
> digiwage-cli masternodestart "alias" "my_mn"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "masternodestart", "params": ["alias" "my_mn"] }' -H 'content-type: text/plain;' http://127.0.0.1:46002/
```

##### `preparebudget` & `submitbudget` Commands #####
Due to the requirement of maintaining backwards compatibility with the legacy command, these two new commands are created to handle the preparation/submission of budget proposals. Future intention is to roll these two commands back into a single command to reduce code-duplication. Paramater arguments currently remain unchanged from the legacy command equivilent.

##### `mnbudgetvote` Command #####
This command now handles all cases for submitting MN votes on a budget proposal. Backwards compatibility with the legacy command(s) has been retained, with the exception of the `vote-alias` case due to a conflict in paramater type casting. A user running `mnbudget vote-alias` will be instructed to instead use the new `mnvote` command. Below is the full help documentation for this new command:

```
mnvote "local|many|alias" "votehash" "yes|no" ( "alias" )

Vote on a budget proposal

Arguments:
1. "mode"      (string, required) The voting mode. 'local' for voting directly from a masternode, 'many' for voting with a MN controller and casting the same vote for each MN, 'alias' for voting with a MN controller and casting a vote for a single MN
2. "votehash"  (string, required) The vote hash for the proposal
3. "votecast"  (string, required) Your vote. 'yes' to vote for the proposal, 'no' to vote against
4. "alias"     (string, required for 'alias' mode) The MN alias to cast a vote for.

Result:
{
  "overall": "xxxx",      (string) The overall status message for the vote cast
  "detail": [
    {
      "node": "xxxx",      (string) 'local' or the MN alias
      "result": "xxxx",    (string) Either 'Success' or 'Failed'
      "error": "xxxx",     (string) Error message, if vote failed
    }
    ,...
  ]
}

Examples:
> givehope-cli mnvote "local" "ed2f83cedee59a91406f5f47ec4d60bf5a7f9ee6293913c82976bd2d3a658041" "yes"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "mnvote", "params": ["local" "ed2f83cedee59a91406f5f47ec4d60bf5a7f9ee6293913c82976bd2d3a658041" "yes"] }' -H 'content-type: text/plain;' http://127.0.0.1:46002/
```

##### `getbudgetinfo` Command #####
This command now combines the old `mnbudget show` and `mnbudget getinfo` commands to reduce code duplication while still maintaining backwards compatibility with the legacy commands. Given no parameters, it returns the full list of budget proposals (`mnbudget show`). A single optional parameter allows to return information on just that proposal (`mnbudget getinfo`). Below is the full help documentation:

```
getbudgetinfo ( "proposal" )

Show current masternode budgets

Arguments:
1. "proposal"    (string, optional) Proposal name

Result:
[
  {
    "Name": "xxxx",               (string) Proposal Name
    "URL": "xxxx",                (string) Proposal URL
    "Hash": "xxxx",               (string) Proposal vote hash
    "FeeHash": "xxxx",            (string) Proposal fee hash
    "BlockStart": n,              (numeric) Proposal starting block
    "BlockEnd": n,                (numeric) Proposal ending block
    "TotalPaymentCount": n,       (numeric) Number of payments
    "RemainingPaymentCount": n,   (numeric) Number of remaining payments
    "PaymentAddress": "xxxx",     (string) GiveHope address of payment
    "Ratio": x.xxx,               (numeric) Ratio of yeas vs nays
    "Yeas": n,                    (numeric) Number of yea votes
    "Nays": n,                    (numeric) Number of nay votes
    "Abstains": n,                (numeric) Number of abstains
    "TotalPayment": xxx.xxx,      (numeric) Total payment amount
    "MonthlyPayment": xxx.xxx,    (numeric) Monthly payment amount
    "IsEstablished": true|false,  (boolean) Established (true) or (false)
    "IsValid": true|false,        (boolean) Valid (true) or Invalid (false)
    "IsValidReason": "xxxx",      (string) Error message, if any
    "fValid": true|false,         (boolean) Valid (true) or Invalid (false)
  }
  ,...
]

Examples:
> givehope-cli getbudgetprojection
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbudgetprojection", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:46002/
```

#### Masternode network protocol layer reporting ####
The results from the `listmasternodes` and `getmasternodecount` commands now includes details about which network protocol layer is being used (IPv4, IPV6, or Tor).



Credits
=======

Thanks to everyone who directly contributed to this release:
- pavhash
- ebailey
- greg

And all the alpha/beta testers..


