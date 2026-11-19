# Is December really the worst month to fly?

The analysis behind the video [What's the Worst Month to Fly?](https://youtu.be/FbTJMWxUSPo)

Everyone knows winter is the worst time to fly. This notebook checks that with **every flight at
UK airports from January 2006 to September 2026**: 33,260,357 take-offs and landings, including
every flight between the UK and the rest of Europe. The data is the UK Civil Aviation Authority's
punctuality statistics, published monthly by airport, route and airline.

## The yardstick

- **Late** = more than 15 minutes after the timetable at the gate (the industry standard)
- **3 hours+** = more than 180 minutes, where EU/UK261 compensation can start
- **Cancelled** = called off less than 24 hours before departure (only counted from 2018 on)
- **A flight** = one take-off or one landing at a UK airport; a domestic flight between two
  reporting airports counts at both ends, the same as in the CAA's own tables
- Comparisons between years only use the **8 airports in every month** (Birmingham, Edinburgh,
  Gatwick, Heathrow, Luton, Manchester, Newcastle, Stansted), because the CAA went from 10 to 25
  airports in 2014

## What it found

| | |
|---|---|
| December 2010 | **50%** of flights late, 1 in 27 more than 3 hours late |
| December the worst month of its year | 2006, and every year from 2009 to 2014 |
| Since 2023 (same 8 airports) | July is the worst month (43%), December comes **5th** (33%) |
| Decembers 2022 → 2025 | 47% → 39% → 34% → 27% late |
| 3 hours+, July vs December (2023 on) | 0.9% in both |
| Cancelled, December vs July | 1.7% vs 1.2% |
| Worst European airports in December | Helsinki 46%, Munich 42%, Lisbon 40% |
| Best | Malaga 27%, Alicante 25%, Faro 24% |

More findings in the notebook:

- **Fewer delays, not fewer bad ones.** December has fewer flights late than July, but just as many
  3-hour delays, more cancellations, and four of the five worst months for long delays in twenty years.
- **The flip.** In July the worst airports are the beaches (Antalya 65%, Nice, Athens). In December
  they're the cold, busy hubs.
- **One weekend can do it.** Heavy snow closed Munich airport at the start of December 2023: 16%
  of that month's UK–Munich flights were cancelled, against 3% the December after.
- **The Christmas trips.** Lapland is the latest trip of all (48% late), but only 1 flight in 254 is
  cancelled. The family hubs (Dublin, Amsterdam, Paris, Frankfurt, Munich) cancel 1 in 34. The
  Canaries are 29% late, and Spain and Portugal's sun airports 25%.
- **The routes.** Of the ten UK routes with the most December cancellations, seven go to Amsterdam.
  From Glasgow, about 3 in 10 December flights to Barra and Tiree are cancelled (small numbers).
- **Cancel or fly late.** In December Lufthansa cancels 1 flight in 22 and KLM 1 in 17, while
  Ryanair cancels 1 in 245 and Jet2 1 in 281. The budget airlines are more often 3 hours late
  instead (about 1 in 100 to 110).
- **Last December**, at UK airports: 835 take-offs and landings were more than 3 hours late and
  1,766 were cancelled.

## Running it

```
pip install -r requirements.txt
```

Open `december_flights.ipynb` and run all cells. It has three parts:

1. **Download** the monthly "Full Analysis Arr Dep" CSVs from the CAA (about 250 MB, ~250 files).
   The CAA has no fixed file names, so the notebook reads each year's page and picks the monthly
   links. Months already downloaded are skipped, so re-run the cell if one fails.
2. **Prepare** one table with the yardstick applied to every month (a minute or two).
3. **Analyse**: every number and chart above.

Data quirks handled in the prepare step:

- **2018 method change:** delay is now gate time vs planned gate time (before: runway time with a
  standard taxi time), and there are more delay bands and a cancellation count. The bands are
  merged back to the old ones for long series.
- Some older files are Windows-1252, not UTF-8.
- Airlines are grouped into brands (easyJet UK / Europe / Switzerland = easyJet), and "Teesside
  International" and "Durham Tees Valley" are one airport.
- Aer Lingus is left out of the cancellation comparison: its regional flights show more
  cancellations than flights at Belfast City in the CAA files.

## Limits

UK airports only: a flight from Munich to Vienna isn't in here, but a flight from Munich to London
is. The data is monthly, so there's no Christmas week or Christmas Eve, only December as a whole.
It shows how late a flight was, not why: weather, strikes and technical problems look the same,
and that decides whether 3 hours late means compensation. Before 2018 cancelled flights aren't in
the files, so older months only show the flights that flew. Small routes (Lapland, Chambéry, the
Scottish islands) are a few hundred flights a year, so read those numbers as rough.

## Data and credits

- Flights: [UK Civil Aviation Authority punctuality statistics](https://www.caa.co.uk/data-and-analysis/uk-aviation-market/flight-punctuality/).
  Source: UK Civil Aviation Authority. The CAA's statistics may not be sold on, so **the raw files
  aren't in this repository**: the notebook downloads them from the CAA
- Passenger rights: [CAA, delays and cancellations](https://www.caa.co.uk/passengers-and-public/resolving-travel-problems/delays-and-cancellations/delays/)
