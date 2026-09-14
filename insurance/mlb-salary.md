---
permalink: /mlb-salary/
title: "MLB Salary Arbitration: Does Position Matter?"
author_profile: true
---

Every young MLB player follows a similar pattern. He spends a few years earning close to the league minimum salary. Then he becomes eligible for arbitration, and his salary can increase very quickly.

![Top 5 CAGR](/images/Figure_1.png)

These five players started around 700,000 dollars in 2022. Two years later, they were all earning more than 10 million dollars. This growth pattern is well known in baseball economics.

## But look closer: position changes everything

What is less known is that this growth is not the same for every position. I calculated the average annual salary growth (measured with CAGR, the Compound Annual Growth Rate) for every position, using several hundred players tracked individually across three consecutive seasons (2022 to 2024).

![CAGR by position](/images/CAGR_per_position.png)

Second basemen show almost twice the salary growth of shortstops during these arbitration years (65.74% compared to 32.56%). Both positions play under the same league rules. Yet the position a player holds seems to influence how fast his salary grows.

## Method

I used SQL self joins to compare individual player salaries across three consecutive MLB seasons from the same data provider (USA Today). This method links each player's own salary history year by year, instead of comparing different groups of players. I also used it to check a common assumption about the 2025 to 2026 salary data. The average salary appeared to drop by 31%, but this drop came from a change in data provider methodology, not from a real decrease. When comparing the same 712 players present in both years, their average salary actually stayed almost the same.

Before drawing conclusions, I also checked the data for duplicate player names. I found 17 cases where two different real players shared the same name, and I verified each one using their unique player ID.
