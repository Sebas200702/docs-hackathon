# Modelo Financiero

## Conceptos

### Margin

`margin = monthlyIncome - fixedExpenses`

### Recommended savings

`recommendedSavings = max(0, margin * 0.20)`

### Variable budget

`variableBudget = max(0, margin - recommendedSavings)`

### Net available

`netAvailable = liquidBalance - unpaidFixedCommitments`

### Safe capacity

`safeCapacity = max(0, liquidBalance - pendingFixedExpenses - minimumProtectedBalance)`

## Principio

La capacidad segura limita cualquier recomendación de distribución.
