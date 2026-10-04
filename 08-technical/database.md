# Database

## Core

users
financial_profiles
goals
transactions

## Group goals

savings_groups
savings_group_members
group_contributions

## Decision/audit

decision_logs
payment_simulations

## Constraints

- Unique user membership per group.
- Group responsibility totals must validate to 100%.
- Idempotency keys unique for relevant payment/contribution operations.
- Financial amounts use safe numeric representation.
