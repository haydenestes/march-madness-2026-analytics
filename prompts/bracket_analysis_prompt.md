# Bracket Analysis Prompt

Use this prompt with Claude to generate or refine bracket analysis for the 2026 NCAA Tournament.

---

## Master Bracket Analysis Prompt

```
You are a March Madness bracket analyst using a data-driven, game-theory approach.

CONTEXT:
- Current date: March 2026, Selection Sunday just passed
- Framework: KenPom efficiency ratings + historical champion filters + ownership/pool modeling
- Goal: Maximize expected pool equity, not raw accuracy

INPUT DATA TO ANALYZE:
[Paste team_profiles.csv content here]
[Paste team_stats.csv content here]

TASK:
1. Apply the following hard rules to eliminate champion candidates:
   - No 9-16 seed can win the championship (40-year rule, zero exceptions)
   - Champion must have KenPom top-20 offense (1 exception in 25 years: 2019 Virginia)
   - Champion must have KenPom top-40 defense (zero exceptions in 25 years)
   - Champion must be seeded 1-3 (one exception: 2014 UConn as 7-seed)

2. After elimination, rank remaining champion candidates by:
   a. KenPom adjusted efficiency margin
   b. Injury-adjusted probability (reduce injured teams by appropriate amount)
   c. Pool ownership percentage (heavily penalize teams above 25% ownership)
   d. Path difficulty to Final Four (reward teams in soft brackets)

3. For each region, identify:
   - Most likely Final Four representative (chalk)
   - Best upset candidate in Round of 32 (6/3 or 7/10 games)
   - Best upset candidate in Sweet 16 (4/1 or 5/2 games if injury-driven)
   - KenPom gaps in 8/9 games (flag if one team is 8+ spots above other)

4. Build the Final Four and champion pick using:
   - Value investing framework: best risk-adjusted pick, not "best team"
   - Ownership-weighted: if two teams are close statistically, pick the lower-owned one
   - Geography: note home region advantages for 1-seeds

5. Output format:
   - Champion: [Team] with reasoning in 3 sentences
   - Final Four: [4 teams] with one-line reasoning each
   - Top 3 upset calls: Round, teams, confidence %, key reason
   - One sentence on what makes this bracket different from the field

CONSTRAINTS:
- Do not pick Duke if Cooper Flagg is listed as injured/questionable
- Do not pick any team with KenPom offense rank 21+ as champion (unless extraordinary defense)
- Always identify the highest ownership team and explain why you're picking or fading them
```

---

## Quick Upset Finder Prompt

```
Given this list of first-round matchups with KenPom rankings:
[Paste matchups with KenPom ranks]

Find all games where:
1. The lower seed (higher number) has a KenPom rank within 15 spots of the higher seed
2. The higher seed has a confirmed injury to a key player
3. The game involves a 7/10, 6/11, or 5/12 matchup

For each qualifying upset, rate it:
- HIGH: KenPom gap < 8 spots, injury present, or strong historical pattern
- MEDIUM: KenPom gap 8-15 spots, slight edge to lower seed
- LOW: KenPom gap > 15 spots, chalky game

Output as a prioritized list with one-line reasoning per upset.
```

---

## Ownership-Adjusted Champion Selector Prompt

```
Given these champion candidates and their estimated pool ownership percentages:
[Team]: [KenPom rank] / [Ownership %] / [Injury status]
[Repeat for all top candidates]

Calculate the expected equity score for each candidate:
- Base equity = (probability of winning title) × (1 / ownership%)
- Injury adjustment: reduce win probability by 15% for "questionable", 30% for confirmed injury
- Path adjustment: add 5% to win probability for "easy" regional draw, subtract 5% for "hard"

Rank all candidates by expected equity score and recommend the top 2.
Explain in plain language why the top pick maximizes pool value over raw probability.
```

---

## Prompt Usage Notes

1. **Replace bracketed placeholders** with actual data from the `/data` CSV files
2. **Run the master prompt first** for full bracket construction
3. **Run the upset finder second** to validate upset calls
4. **Run the ownership selector last** to confirm the champion pick
5. Save all outputs as comments or additions to `/analysis/bracket_predictions.md`
