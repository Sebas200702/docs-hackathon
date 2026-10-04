# Modelo de Dominio

## Entidades

- User
- FinancialProfile
- Income
- Expense
- Transaction
- Budget
- Goal
- Recommendation
- Wallet
- Payment
- Challenge
- Achievement
- SavingsGroup
- SavingsGroupMember
- GroupContribution
- DecisionLog
- PaymentSimulation

## Relaciones principales

User → FinancialProfile

User → Goals

User → Transactions

User → Wallet

User → Recommendations

SavingsGroup → Members → User

SavingsGroup → Contributions

Recommendation → DecisionLog

Payment → Goal/Distribution → Audit
