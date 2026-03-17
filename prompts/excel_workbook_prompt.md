# Excel Workbook Prompt — Claude Excel Plug-in

Use this prompt with the Claude Excel plug-in to generate the full March Madness analytics workbook.

---

## Master Workbook Generation Prompt

```
Create a comprehensive March Madness 2026 analytics Excel workbook with the following sheets:

SHEET 1: "Team Profiles"
Columns: Team | Seed | Region | Record | KenPom Overall | KenPom Offense | KenPom Defense |
         AEM (Adjusted Efficiency Margin) | Injury Flag | Injured Player | Ceiling | Floor |
         Pool Ownership % | Contrarian Value | Bracket Path Difficulty | Champion Filter Pass

Formatting:
- Header row: Dark blue background, white bold text
- Rows where Champion Filter Pass = "Yes": Light green background
- Rows where Injury Flag = "Yes": Light yellow background
- Rows where Pool Ownership > 25%: Light red background
- Freeze top row
- Auto-filter on all columns

Sort: By KenPom Overall rank ascending

SHEET 2: "Team Stats"
Columns: Team | Seed | PPG | OPP PPG | FG% | OPP FG% | 3P% | Rebounds/G |
         Assists/G | Turnovers/G | FT% | Pace | Experience Tier |
         Star Player | Star PPG | Star RPG | Star APG | KenPom OE | KenPom DE

Formatting:
- Header row: Dark green background, white bold text
- Conditional formatting on PPG: Color scale from white (low) to dark blue (high)
- Conditional formatting on OPP FG%: Color scale from dark red (high, bad) to white (low, good)
- Freeze top row and first two columns

SHEET 3: "Bracket Predictions"
Layout: Full bracket tree visualization
- Left side: East and West regions (Round of 64 through Elite 8)
- Right side: South and Midwest regions (Round of 64 through Elite 8)
- Center: Final Four + Championship

Formatting:
- Each game box: team name + seed + win probability %
- Champion pick box: Gold background, bold text
- Upset picks (our calls): Orange border
- Color-code by seed: 1-seeds blue, 2-seeds teal, 3-4 green, 5-8 yellow, 9+ orange

SHEET 4: "Roster Madness"
Columns: Seed Slot | Team | Seed | Region | KenPom | Record | Key Metric |
         Projected Round | Est. Points | Pool Ownership | Contrarian Tier | Reasoning

Formatting:
- Header row: Purple background, white bold text
- Seed slots 9/10/11: Orange background (high value tier)
- Seed slots 1-3: Blue background (chalk tier)
- Add a total estimated points cell at the bottom

SHEET 5: "Upset Tracker"
Columns: Round | Higher Seed Team | Seed | Lower Seed Team | Seed | Upset Tier |
         KenPom Gap | Confidence % | Primary Reason | Injury Factor | Predicted Winner

Formatting:
- Header row: Dark orange background, white bold text
- "Major" upset tier: Red background
- "Moderate" upset tier: Orange background
- "Minor" upset tier: Yellow background
- Confidence > 65%: Bold text

SHEET 6: "Historical Filters"
Columns: Filter | Pass Rate | Rule Type | Weight (1-10) | Years Verified |
         Teams That Pass 2026 | Teams That Fail 2026 | Notes

Formatting:
- Header row: Dark gray background, white bold text
- Hard Rules: Green left border (4px)
- Soft Rules: Yellow left border (4px)
- Low Weight: Gray left border (4px)
- Weight column: Data bar visualization

WORKBOOK SETTINGS:
- Workbook title: "2026 March Madness Analytics"
- Tab colors: Blue (Team Profiles), Green (Team Stats), Gold (Bracket), Purple (Roster), Orange (Upsets), Gray (Filters)
- Page setup on all sheets: Landscape orientation, fit to page width
- Add workbook cover sheet: Title page with project name, date, and brief methodology summary
```

---

## Individual Sheet Update Prompts

### Update Team Stats Sheet
```
In the "Team Stats" sheet, update the following teams' KenPom ranks to reflect
post-injury adjustments:
- Duke: Offense drops from #5 to #5 (same — injury is defensive), Defense drops from #9 to #14
- UNC: Offense drops from #12 to #22, Defense stays at #38
- Gonzaga: Defense drops from #28 to #52

Add a new column "Injury-Adjusted KenPom Overall" that recalculates the overall rank
based on these adjusted offensive and defensive ranks.

Add conditional formatting: if Injury-Adjusted rank is 3+ spots worse than Standard rank,
highlight the cell in yellow with a note icon.
```

### Add Championship Probability Column
```
In the "Team Profiles" sheet, add a new column "Champion Probability (%)" after the
"Contrarian Value" column.

Use this formula logic:
- Base probability from KenPom rank: =IF(KenPom<4, 15%, IF(KenPom<8, 10%, IF(KenPom<12, 6%, 3%)))
- Injury adjustment: multiply by 0.7 if injury flag = "Yes", 1.0 if No
- Ownership adjustment: multiply by (1 / (Ownership% / 14%)) to normalize to Arizona baseline
- Path adjustment: multiply by 1.1 if path = "Easy", 0.9 if "Hard"

Format the column as percentage with 1 decimal place.
Add a pie chart below the table showing champion probability distribution for top 8 teams.
```

---

## Pivot Table Prompts

### KenPom Analysis Pivot
```
Create a pivot table on a new sheet called "KenPom Analysis":
- Rows: Region
- Columns: Seed (1, 2, 3, 4, 5-8, 9-16)
- Values: Average KenPom Rank (to show how balanced/unbalanced each region is)

Add a second pivot:
- Rows: Experience Tier (Senior-led, Junior-led, Sophomore-heavy, Freshman-heavy)
- Values: Average Champion Filter Pass rate, Average KenPom, Count of teams

This shows which experience tier produces the best tournament teams historically.
```
