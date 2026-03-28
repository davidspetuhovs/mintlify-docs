# Change analysis time period

## Overview

| Property | Value |
|----------|-------|
| **Flow** | Change analysis time period |
| **Starting Page** | `/platform/{chatbotId}` |
| **Persona** | Analyst comparing metrics across different time periods |

## Description

Change the dashboard date range to filter analytics data

## Preconditions

- User is logged in
- User is on the chatbot dashboard

## Steps

### Step 1

Click 'This month' date range button to open date picker

### Step 2

Date picker opens with presets: Today, Yesterday, This week, Last week, This month, Last month, This year, Last year, All time, Custom. Dual calendar grid.

### Step 3

Select 'Last week' and click Apply — dashboard data updates (frustrations: 3 vs 5, users: 1 vs 3, languages: en 100%)

## Expected Outcome

All dashboard KPIs, charts, and tables update to reflect the selected date range

## Related Flows

- [Investigate a dissatisfied user](investigate-a-dissatisfied-user.md)
