# political_event_study_uk
How UK shares and gilts react to elections, budgets and referendums; event study in Python
How much do UK housebuilders, banks, mid-sized companies and government bonds move in response to elections, referendums and budgets, and which kinds of political event matter most?


Using Data from daily closing prices from Yahoo Finance, downloaded with the yfinance Python library and adjusted for dividends and share splits.

Period: January 2013 to September 2026.

Benchmark: FTSE All-Share index (^FTAS).

Assets studied: FTSE 250 (^FTMC), Persimmon (PSN.L), Taylor Wimpey (TW.L), Lloyds Banking Group (LLOY.L), NatWest Group (NWG.L) and the iShares UK Gilts ETF (IGLT.L), used as a proxy for UK government bond prices.

Events (9): the 2014 Scottish independence referendum, the 2015, 2017, 2019 and 2024 general elections, the 2016 EU referendum, the September 2022 mini-budget, Liz Truss's resignation in October 2022 and the October 2024 Autumn Budget. Dates are the first trading day after each result or announcement; the full list is in events.csv.
Method

This is an event study. For each event and asset, I first estimate how the asset normally moves with the overall market, using a market model fitted over a calm window of 220 trading days that ends 30 days before the event. The slope of that line is the asset's beta.

I then apply the model to the event window (1 day before to 5 days after) to predict what the asset should have done given the market's moves. The gap between the actual and predicted return is the abnormal return: the part of the move attributable to the event. Summing these gives the cumulative abnormal return (CAR), and a t-statistic compares the CAR with the asset's normal day to day noise, with values beyond ±2 treated as significant.

Limitations
Other news: other announcements on the same days, such as company results or global market moves, may account for part of the abnormal returns.
Small sample: nine events are too few to draw firm general conclusions about each event type.
Bond proxy: the gilts ETF only approximates moves in gilt yields; it holds bonds of many maturities and charges fees.
Simple significance test: the t-statistic assumes each day's abnormal return is independent of the others, which may overstate significance when markets keep reacting over several days.
Choice of windows: results can change with different estimation or event windows.

How to run it
Install the libraries: pip install pandas numpy matplotlib yfinance
Open event_study.ipynb in Jupyter and run all cells (Kernel → Restart Kernel and Run All Cells).
To add events, add rows to events.csv using the same format.
