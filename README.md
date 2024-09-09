# Bank_nifty_5yr
 ```markdown
```sql
SELECT *
	FROM public.banknifty5yr;

(data-1725879417336.csv)

select date ,
high_amt - low_amt as velocity
from banknifty5yr;

select * ,
extract (year from date) as year,
extract (month from date)	as month
from banknifty5yr;

select extract (year from date) as year,
avg(share_traded) as sharetraded_avg,
avg(turnover_cr) as turnoverCr_avg,
avg(open_amt) as openamt_avg,
avg(low_amt) as lowamt_avg,
avg(close_amt) as closeamt_avg,
avg(high_amt) as highamt_avg
from banknifty5yr
group by year
order by year asc;

select extract (month from date) as month ,
avg(share_traded) as sharetraded_avg,
avg(turnover_cr) as turnoverCr_avg,
avg(open_amt) as openamt_avg,
avg(low_amt) as lowamt_avg,
avg(close_amt) as closeamt_avg,
avg(high_amt) as highamt_avg
from banknifty5yr
group by month
order by month asc;

select corr (share_traded, turnover_cr) as traded_vs_turnover, 
corr (low_amt, share_traded) as low_amt_vs_traded,
corr (high_amt, share_traded) as high_amt_vs_traded,
corr (low_amt, turnover_cr) as low_amt_vs_turnover,
corr (high_amt, turnover_cr) as high_amt_vs_turnover,
corr (open_amt, close_amt) as openamt_vs_closeamt,
corr (open_amt, high_amt) as openamt_vs_highamt
from banknifty5yr;

select date, close_amt, high_amt, low_amt,
greatest (high_amt-low_amt,
high_amt - lag(close_amt) over (order by date),
low_amt -lag(open_amt)over (order by date)) as true_range
from banknifty5yr
order by true_range desc;

select date, close_amt,
avg (close_amt) over (order by date rows between 9 preceding and current row) as moving_average_close,
open_amt,
avg (open_amt) over (order by date rows between 9 preceding and current row) as moving_average_open,
low_amt,
avg (low_amt) over (order by date rows between 9 preceding and current row) as moving_average_low,
high_amt,
avg (high_amt) over (order by date rows between 9 preceding and current row) as moving_average_high
from banknifty5yr
order by date;
