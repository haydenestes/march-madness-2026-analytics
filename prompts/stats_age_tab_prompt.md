# Stats & Age Tab Prompt — Team Experience Analysis

Use this prompt to generate the team experience and roster age analysis tab.

---

## Experience Tier Analysis Prompt

```
Analyze the 2026 NCAA Tournament field for roster experience and age advantages.

INPUT:
[Paste team_stats.csv content here — specifically the experience_tier column]

TASK: For each team in the field, evaluate their "experience advantage" in March:

EXPERIENCE SCORING:
- Senior-led (majority of rotation = seniors/5th-year): +3 points
- Junior-led (majority = juniors): +2 points
- Sophomore-led: +1 point
- Freshman-heavy: 0 points (penalty in March)
- Transfer portal heavy (3+ key transfers): +1.5 points (tournament experience adds up)

AGE ADVANTAGE IN KEY MATCHUPS:
For each predicted upset matchup, calculate the experience differential:
- Texas A&M (9 seniors) vs Saint Mary's (senior-led): Roughly equal — look at other factors
- VCU (senior-led) vs UNC (junior-led + key injury): VCU +2 experience edge
- Iowa (junior-led) vs Clemson (senior-led): Clemson +1 — but KenPom gap overrides

HISTORICAL PATTERN:
- Final Four teams average experience tier score: 2.4/3
- Champions average: 2.7/3
- First-round upset winners average: 2.1/3 (experience alone doesn't explain upsets — KenPom matters more)

Output:
1. Experience tier table sorted by score
2. Top 5 "experience mismatches" in the bracket (where one team has significant edge)
3. Bottom 3 "experience red flags" (highly ranked teams with youth concerns)
4. Championship bracket note: does our champion pick (Arizona) have sufficient experience?
```

---

## Age/Roster Tab Excel Structure

```
Create an "Age & Experience" sheet in the Excel workbook with this structure:

SECTION 1: Experience Tier Rankings
Columns: Team | Seed | Experience Tier | Experience Score | Avg Player Age |
         Seniors on Roster | Transfers | Tournament Games (returning players) |
         Experience Advantage Rating

SECTION 2: Key Matchup Experience Comparison
For each of our 10 upset calls, show:
- Higher seed team + experience score
- Lower seed team + experience score
- Experience differential
- Does experience favor the upset or the chalk?

SECTION 3: Historical Champion Experience Profile
Show the experience tier of the last 10 national champions:
Year | Champion | Experience Tier | Experience Score | KenPom Rank

Add a trendline: is experience becoming more or less important in the transfer portal era?

SECTION 4: Team Age Distribution Chart
Bar chart showing the distribution of experience tiers across all 68 teams:
- Freshman-heavy: X teams
- Sophomore-led: X teams
- Junior-led: X teams
- Senior-led: X teams

Overlay the champion win rate for each tier.

FORMATTING:
- Header: Dark navy background, white text
- Senior-led rows: Deep green highlight
- Freshman-heavy rows: Light orange highlight (risk indicator)
- Experience Score > 2.5: Bold
```

---

## Age Factor in Upset Prediction Prompt

```
Given these 8/9, 7/10, and 6/11 matchups with experience tier data:

[Matchup] | [Higher Seed Experience Tier] | [Lower Seed Experience Tier]

For each matchup, apply this scoring:
1. If lower seed is more experienced: +15% upset probability adjustment
2. If lower seed has 3+ seniors and higher seed is sophomore/freshman heavy: +20%
3. If both teams are similar experience: 0% adjustment
4. If higher seed is more experienced: -10% upset probability adjustment

Then combine with KenPom gap adjustment:
- KenPom gap 1-5 spots: base upset probability 45%
- KenPom gap 6-10 spots: base upset probability 35%
- KenPom gap 11-15 spots: base upset probability 25%
- KenPom gap 16+ spots: base upset probability 15%

Output final adjusted upset probability for each 8/9, 7/10, 6/11 matchup.
Flag any matchup where the upset probability exceeds 50% (genuine coin flip or pick the upset).
```

---

## 2026 Experience Quick Reference

| Team | Seed | Experience Tier | Score | Key Seniors |
|------|------|-----------------|-------|-------------|
| Arizona | 1 | Senior-led | 3.0 | Caleb Love + 4 others |
| Texas A&M | 10 | Senior-led | 3.0 | 9 seniors total |
| Saint Mary's | 7 | Senior-led | 2.8 | Mitchell Saxen |
| Saint Louis | 8 | Senior-led | 2.7 | Full senior core |
| Iowa | 9 | Junior-led | 2.2 | Owen Freeman (Jr) |
| UNC | 5 | Junior-led | 2.0 | RJ Davis (Sr) + injury |
| VCU | 11 | Senior-led | 2.8 | Ace Baldwin Jr. (Sr) |
| Duke | 1 | Freshman-heavy | 1.2 | Cooper Flagg (Fr) |
| Michigan State | 3 | Senior-led | 2.7 | Tom Izzo system |
| Wisconsin | 5 | Senior-led | 2.5 | John Tonje (Sr) |

**Experience insight:** Duke's freshman-heavy roster is a significant March risk factor ON TOP of the Flagg injury. Even if Flagg is healthy, young teams historically underperform seeding in close games.
