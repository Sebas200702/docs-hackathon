# API

## Auth

POST /auth/login

## Onboarding

POST /onboarding

## Dashboard

GET /dashboard

## Goals

POST /goals
GET /goals

## Group Goals

POST /group-goals
POST /group-goals/:id/members
POST /group-goals/:id/activate
GET /group-goals/:id
POST /group-goals/:id/recommend-contribution
POST /group-goals/:id/simulate-contribution

## Decisions

POST /decisions/recommend

## Financial

POST /affordability/check
POST /subscriptions/audit
POST /windfall/allocate
POST /micro-savings

## Payments

POST /payments/simulate
POST /payments/confirm

## Review

GET /weekly-review

## Demo

POST /demo/reset

## Health

GET /health
