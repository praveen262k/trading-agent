you’re talking about a multi-leg options strategy around earnings (likely something like an iron condor, iron fly, or long/short straddle/strangle hybrid) that plays a predicted price range after earnings.

The tricky part is that the stock’s actual move can be the same, yet your P/L can vary wildly depending on implied volatility (IV) crush, skew, and timing.
That’s why sometimes it works and sometimes it doesn’t — even when the post-earnings move looks “similar.”

⸻

Why the results vary
	1.	Implied Volatility Crush
	•	Pre-earnings, IV is elevated. After the earnings report, IV usually collapses.
	•	If your strategy is net short options (like iron condors or short straddles), the IV crush helps you.
	•	If you’re net long options (like long straddles or long strangles), the IV crush hurts — you need a big move to offset the lost extrinsic value.
	2.	Market Maker Expected Move
	•	The “similar range” you see in price movement might not be the same as the expected move priced into the options.
	•	Example: Stock moves $5. Market expected move was $3 last quarter but $6 this quarter.
→ In the $3 case, short premium wins big.
→ In the $6 case, same $5 move actually loses if you sold options too close.
	3.	Strike Placement
	•	The width between your short strikes vs. the expected move is key.
	•	If your shorts are inside or near the expected move, even “average” moves can breach them.
	•	Selling far OTM reduces breach risk but also reduces reward.
	4.	Direction & Skew
	•	IV skew can make one side richer than the other (especially in single-stock names where downside puts are juiced).
	•	If the move is in the rich side, IV crush benefit is greater.

⸻

Best way to make the judgment

Here’s a repeatable process you can run before every earnings trade:

Step 1 – Get the Market’s Expected Move
	•	Check the At-The-Money Straddle price for the earnings expiry (or use platforms that show expected move).
	•	Example:
	•	Stock: $100
	•	ATM call + ATM put for earnings expiry = $6.50 → Expected move ≈ $6.50.

Step 2 – Compare to Historical Post-Earnings Moves
	•	Look at last 8 quarters → median % move and dollar move.
	•	If the expected move is bigger than most historical actual moves, short premium strategies have the edge.
	•	If the expected move is smaller, the market is underpricing risk → long premium can win.

Step 3 – Assess IV Crush Potential
	•	Check IV rank / IV percentile for that stock.
	•	High (>70%) → large crush likely → good for short premium.
	•	Low (<30%) → less crush → less edge for short premium.

Step 4 – Adjust Strike Placement
	•	For an iron condor:
	•	Place short strikes just outside the expected move to balance risk/reward.
	•	For an iron fly:
	•	Ensure premium collected ≥ 1.5× the expected move breakeven distance.

Step 5 – Position Size for Breach Probability
	•	Use delta as a breach probability estimate.
	•	If short strike delta > 20, you’re playing closer to the fire.

⸻

💡 Rule of Thumb:
	•	Short premium → When market’s expected move > historical actual move, and IV is high.
	•	Long premium → When market’s expected move < your forecasted move, and IV is low.
	•	If both are “meh” → skip the trade. Sitting out is often the most profitable “strategy.”



Logic Flow
	1.	Inputs (from APIs like yfinance, Tradier, or Polygon)
	•	Current stock price
	•	Implied Volatility for earnings expiry (ATM options)
	•	ATM call & put price for earnings expiry (to calculate expected move)
	•	Historical post-earnings price changes (last N quarters)
	2.	Calculations
	•	Expected Move = (ATM Call Price + ATM Put Price)
	•	Historical Median Move = median absolute % move over last N quarters × current stock price
	•	IV Rank = position of current IV in last 1-year range
	3.	Decision Rules
	•	If Expected Move > Historical Move and IV Rank > 50% → Short premium
	•	If Expected Move < Historical Move and IV Rank < 50% → Long premium
	•	Else → Skip trade
	4.	Strike Placement
	•	For Short Iron Condor:
	•	Short strikes at Stock Price ± Expected Move
	•	Long strikes 2–5% further OTM
	•	For Long Straddle/Strangle:
	•	Buy ATM strikes (or ± Expected Move for strangle)


    Automatically fetches past 8 earnings dates & post-earnings % moves
	•	Uses real IV history (via yfinance or Polygon.io)
	•	Spits out trade type + exact strikes in one run.
    •	clear design and type hints,
	•	robust error handling and logging,
	•	config via environment variables,
	•	a fallback path (yfinance) if Polygon isn’t available,
	•	decision logic (expected move vs historical median move + IV-rank),
	•	strike-placement suggestions for short premium (iron condor) and long premium (straddle/strangle).

    How to use
	1.	Get a Polygon API key (or Tradier/ORATS key). Set POLYGON_API_KEY in your environment.
	2.	pip install -r requirements.txt (requirements listed below).
	3.	Run the module’s example at the bottom or import the functions into your trading app.