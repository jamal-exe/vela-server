# Stellar reconciliation contract

Payment status is reconciled from the locally submitted transaction hash by
polling Horizon. A confirmed provider record returns the hash and ledger; a
known failed record returns a typed transaction failure; a missing record is
polled again within the configured bounded attempt count; and a provider
outage returns the typed network error without exposing upstream details.

Provider records are treated as untrusted input. Missing or incorrectly typed
fields never count as confirmation and are mapped to a safe transaction
failure. Clients should use the typed public error code and retry status
lookups within the documented bounded policy rather than replaying a signed
payment submission.
