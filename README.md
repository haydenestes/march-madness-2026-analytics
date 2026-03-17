# 2026 March Madness Analytics

A systematic, data-driven approach to 2026 NCAA Tournament bracket construction
and Roster Madness picks using KenPom metrics, historical champion filters,
injury-adjusted team evaluation, and pool ownership game theory.

---

## Final Picks

### Bracket
| Round | Pick |
|-------|------|
| **Champion** | **Arizona** (West, #1 seed, KenPom #3) |
| **Runner-Up** | **Michigan** (Midwest, #2 seed, KenPom #9) |
| Final Four — East | UConn (KenPom #7) |
| Final Four — West | Arizona (KenPom #3) |
| Final Four — South | Houston (KenPom #5) |
| Final Four — Midwest | Michigan (KenPom #9) |

**Champion rationale:** Arizona is the healthiest #1 seed, KenPom top-3, top-10
offense and defense, Tommy Lloyd's best team, and sitting at only 14% public
ownership — highest pool equity of any legitimate champion candidate.

**Fade Duke:** Cooper Flagg back injury + 38% pool ownership = worst equity in
the field. Best team on paper, worst bracket value.

### Key Upset Calls
| Round | Matchup | Confidence | Edge |
|-------|---------|-----------|------|
| Round of 64 | Iowa (9) over Clemson (8) | 75% | 11 KenPom spots gap |
| Round of 32 | BYU (6) over Gonzaga (3) | 65% | Huff knee injury, defense drops to ~55 KenPom |
| Round of 32 | Texas A&M (10) over Saint Mary's (7) | 60% | 9 seniors, 87.7 PPG pace mismatch |
| Round of 32 | VCU (11) over UNC (6) | 60% | Wilson out — UNC offense collapses |
| Sweet 16 | Kansas (4) over Duke (1) | 55% | Flagg injury + Bill Self system creates chaos |
| Elite 8 | Houston (2) over Florida (1) | 50% | KenPom #3 defense vs overowned #1 seed |

### Roster Madness Picks
| Slot | Team | Reasoning | Contrarian Tier |
|------|------|-----------|-----------------|
| 1 | Arizona | Healthiest 1-seed, champion pick, KenPom #3 | Medium |
| 2 | Purdue | #2 KenPom offense nationally, clean West path | Medium |
| 3 | Michigan State | Izzo, #1 rebounding rate, top-10 KenPom defense | High |
| 4 | Nebraska | KenPom #6 defense, 26-6, vastly underrated | High |
| 5 | Wisconsin | Underseeded — beat Michigan/Purdue/Illinois | High |
| 6 | Louisville | Best KenPom profile among all 6-seeds (#19 overall) | Medium |
| 7 | Saint Mary's | Tournament system, pedigree, Randy Bennett | Low |
| 8 | Georgia | 8 KenPom spots above likely opponent | Medium |
| 9 | Iowa | 11 KenPom spots above Clemson (8-seed) | High |
| 10 | Texas A&M | 9 seniors + 87.7 PPG (most in field) | High |
| 11 | VCU | #47 KenPom + UNC missing Jalen Wilson | High |
| 12 | High Point | 30-4 record, best 12-seed profile in field | Medium |
| 13 | Hawaii | Most legitimate 13-seed, 27-6 record | High |
| 14 | North Dakota State | 27-7, best cover chance among 14-seeds | Low |
| 15 | Queens NC | Floor pick — no 15 has ever made Final Four | Low |
| 16 | Siena | Best cover chance among 16-seeds (MAAC champ) | Low |

---

## Methodology

### Core Principles
1. **Separate "best team" from "best bracket pick."** The goal is expected pool
   equity, not accuracy.
2. **Hard champion filters first.** A team must pass KenPom top-20 offense,
   top-40 defense, and 1–3 seeding before consideration.
3. **Ownership is part of the model.** A 38%-owned team with a 16% win
   probability is a bad pick. A 14%-owned team with 14% win probability is great.
4. **Injuries change the calculus.** Four teams are flagged — Duke, Gonzaga, UNC,
   Texas Tech — and each is either faded or downgraded.
5. **Experience matters in March.** Senior-led teams are systematically
   underestimated by public pickers who chase narrative.

### KenPom Filter System
| Filter | Rule Type | Weight | Years Verified |
|--------|-----------|--------|---------------|
| No 9-16 seed wins national championship | Hard | 10/10 | 40 years |
| KenPom top-20 offense for champion | Hard | 9/10 | 15 years |
| KenPom top-40 defense for champion | Hard | 9/10 | 15 years |
| KenPom top-3 overall OR defending champion | Hard | 8/10 | 10 years |
| Champion seeded 1-3 | Hard | 8/10 | 30 years |
| Champion from power conference | Hard | 9/10 | 40 years |
| Week 6 AP Poll top-12 | Soft | 6/10 | 20 years |
| Coach with 3+ tournament wins | Soft | 7/10 | 20 years |
| Final Four has at least one double-digit seed | Soft | 5/10 | 30 years |

### Injury Adjustments Applied
| Team | Player | Status | Adjustment |
|------|--------|--------|-----------|
| Duke | Cooper Flagg (back) | Game-time decision | Defense rank +5, overall +2 |
| Gonzaga | Ryan Huff (knee) | Out | Defense rank +24, overall +8 |
| UNC | Jalen Wilson (knee) | Out 4-6 weeks | Offense rank +10, overall +10 |
| Texas Tech | Pop Toppin (ankle) | Questionable | Offense rank +5, overall +4 |

---

## Notebook Visualizations

The Jupyter notebook (`notebooks/march_madness_analysis.ipynb`) generates four
core charts plus supplemental analysis:

| Chart | File | Description |
|-------|------|-------------|
| 1 — KenPom Scatter | `chart1_kenpom_scatter.png` | Offense vs defense scatter with hard filter cutoff lines and pool ownership bar |
| 2 — Experience Tier | `chart2_experience_tier.png` | Stacked bar by seed tier + Senior-led teams KenPom ranking |
| 3 — Upset Tracker | `chart3_upset_tracker.png` | Confidence bars + KenPom gap vs confidence bubble chart |
| 4 — Roster Projection | `chart4_roster_points_projection.png` | Stacked points bar (standard + bonus) + ownership value map |
| Supp — Champion Equity | `supp_champion_equity.png` | Pool equity score per champion candidate |

### How to Run the Notebook

```bash
cd march-madness-2026-analytics
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook notebooks/march_madness_analysis.ipynb
```

Run all cells top-to-bottom. Charts are saved automatically to `/results/`.

---

## Project Structure

```
march-madness-2026-analytics/
├── README.md
├── data/
│   ├── team_profiles.csv        # Seeds, KenPom ranks, injuries, ownership
│   ├── team_stats.csv           # PPG, FG%, tempo, experience tier, star player
│   ├── roster_picks.csv         # 16 Roster Madness picks with point projections
│   ├── upset_tracker.csv        # 6 upset calls with confidence and reasoning
│   └── historical_filters.csv  # 9 champion filters with pass/fail verdicts
├── analysis/
│   ├── bracket_predictions.md  # Full round-by-round bracket
│   ├── executive_summary.md    # Top-line findings
│   ├── historical_filter_audit.md
│   ├── injury_report.md        # Team-by-team injury impact analysis
│   ├── pool_strategy.md        # Ownership modeling and game theory
│   └── roster_madness_picks.md # Detailed Roster Madness reasoning
├── prompts/
│   ├── bracket_analysis_prompt.md
│   ├── excel_workbook_prompt.md
│   └── stats_age_tab_prompt.md
├── results/
│   └── results_tracker.md      # Live tournament results log
└── notebooks/
    └── march_madness_analysis.ipynb
```

### Data Dictionary

**team_profiles.csv**

| Column | Description |
|--------|-------------|
| `team` | Team name |
| `seed` | Tournament seed (1–16) |
| `region` | East / West / South / Midwest |
| `record` | Season record |
| `kenpom_rank` | Overall KenPom rank |
| `kenpom_offense_rank` | Adjusted offensive efficiency rank |
| `kenpom_defense_rank` | Adjusted defensive efficiency rank |
| `adjusted_efficiency_margin` | KenPom AEM |
| `injury_flag` | Yes / No |
| `injured_player` | Player name if injured |
| `injury_status` | Out / Questionable / Game-time decision |
| `ceiling` | Best projected round (Champion → Round of 64) |
| `floor` | Conservative projected round |
| `ownership_estimate_pct` | Estimated pool pick % |
| `contrarian_value` | High / Medium / Low |
| `bracket_path_difficulty` | Easy / Medium / Hard |
| `champion_filter_pass` | Yes / No — passes all hard rules |
| `notes` | Analysis notes |

**team_stats.csv**

| Column | Description |
|--------|-------------|
| `ppg` | Points per game |
| `opp_ppg` | Opponent points per game |
| `fg_pct` | Field goal percentage |
| `three_pt_pct` | 3-point percentage |
| `experience_tier` | Senior-led / Junior-led / Sophomore-led / Freshman-heavy |
| `star_player` | Team's primary star player |
| `star_player_ppg` | Star player scoring average |
| `kenpom_oe` | KenPom adjusted offensive efficiency |
| `kenpom_de` | KenPom adjusted defensive efficiency |
| `tempo` | Possessions per 40 minutes |

---

## Data Sources

- **KenPom.com** — efficiency ratings and tempo metrics
- **ESPN** — bracket pick distributions and injury updates
- **CBS Sports** — team rankings and previews
- **NCAA.com** — official statistics
- **RotoWire** — injury reports

## Tools

- **Claude (Anthropic)** — analysis framework, filter system, prompt engineering
- **Python / Jupyter** — data processing and visualization
- **pandas / matplotlib / seaborn** — chart generation
- **GitHub** — version control

---

## Results Tracking

Update `/results/results_tracker.md` after each round. The tracker includes:
- Live bracket score by round
- Upset call scoreboard (6 calls to track)
- Final Four and Championship results
- Roster Madness results by seed slot
- Post-tournament analysis template

**Tournament dates:**
- Round of 64: March 20–21, 2026
- Round of 32: March 22–23, 2026
- Sweet 16: March 27–28, 2026
- Elite 8: March 29–30, 2026
- Final Four: April 4, 2026
- National Championship: April 6, 2026

---

*This project is for analytical and educational purposes only.*
