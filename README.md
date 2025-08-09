A backtest done on the performance of moving averages in daily timeframe.
Done usnig public library yfinance.
(Intraday is not currently possible as max lookback is 60d - unreliable)
<i><center>Calculation of formulas below</center></i>

## RESULTS OF DEATH CROSS 50/200
SHARPE: 0.43185
SORTINO: 0.54418
KELLY: 3.3693%
CAGR: 6.5265%
Win rate: 53.13%
Avg win: 0.768%
Avg loss: -0.816%
<img width="552" height="435" alt="image" src="https://github.com/user-attachments/assets/8c2c1d71-a44a-4c9d-961d-8c0f0d2c71e4" />
<img width="543" height="435" alt="image" src="https://github.com/user-attachments/assets/7046c211-92c5-43e3-9894-73449781ec94" />


## RESULTS OF ONLY LONGS
<img width="552" height="435" alt="image" src="https://github.com/user-attachments/assets/c2c41fcd-9948-403b-985c-44ff9131ed71" />
<img width="543" height="435" alt="image" src="https://github.com/user-attachments/assets/c40db729-74d6-4916-8994-9fd78e9f4466" />
SHARPE: 0.72650
SORTINO: 0.78452
KELLY: -21.752%
CAGR: 9.4155%
Win rate: 40.94%
Avg win: 0.660%
Avg loss: -0.707%

## RESULTS OF ONLY SHORTS
SHARPE: -0.14555
SORTINO: -0.09993
KELLY: -73.846%
CAGR: -2.64044%
Win rate: 12.19%
Avg win: 0.111%
Avg loss: -0.109%
<img width="552" height="435" alt="image" src="https://github.com/user-attachments/assets/9f615a00-1e8f-4537-b09b-89b26515e52a" />
<img width="543" height="435" alt="image" src="https://github.com/user-attachments/assets/28290066-07c0-48b7-b11f-cd7b78d122f4" />

## 

<b><p>Formula for Sharpe Ratio</p></b>
<i><p>This tells us the unit of excess return for each unit of total risk taken.</p></i>
<img src='https://a.c-dn.net/c/content/dam/publicsites/igcom/uk/images/ContentImage/Sharpe%20ratio.png' height='200' width='400'><br>

<b><p>Formula for Sortino Ratio</p></b>
<i><p>This tells us the unit of excess return for each unit of downside risk taken.</p></i>
<img src='https://lh7-us.googleusercontent.com/uZOqsSTlmYtna8V494JZ1PjL4LSfsVRuXn661UQ9_Etb4Dp5XnWt4gWZFKFTmKZiEJtCZf97KJp3i6FOd_KjAvq9SMnoly7RaVDoi-BtGmL7TY4B2AyeMPOJ7lhn6JvSTth_2pw0_oj1qEjgj297TZU' height='200' width='400'>

<b><p>Formula for Kelly Criterion</p></b>
<i><p>Determines how much to invest to maximise returns.</p></i>
<img src='https://static.hdfcsky.com/wp-content/uploads/2024/09/article-image-263.jpeg' height='200' width='400'>
