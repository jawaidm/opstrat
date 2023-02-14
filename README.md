# Installation
https://medium.datadriveninvestor.com/visualizing-option-trading-strategies-in-python-35bfa61151d9

````
mkdir /var/www/opstrat
cd /var/www/opstrat

virtualenv venv
source venv/bin/activate

pip install opstrat
pip install ipython
pip install scipy
````


# Start ipython shell
(venv) jawaidm@xps:/var/www/opstrat$ ipython
Python 3.8.10 (default, Nov 14 2022, 12:59:47) 
Type 'copyright', 'credits' or 'license' for more information
IPython 8.10.0 -- An enhanced Interactive Python. Type '?' for help.

````
import opstrat as op

op.single_plotter()

````

# Customisation

## Plotting Simple Pay-off Diagrams - Single Options

### Put Option - SELL
Sell
Put
Price = 460
Strike = 460
Option_Price = 12.5

````
In [3]: op.single_plotter(spot=460, strike=460, op_type='p', tr_type='s', op_pr=12.5)
````

### Call Option
Buy
Call
Price = 235
Strike = 235
Option_Price = 10.63

````
op_list=[{'tr_type':'b', 'op_type':'c', 'strike':235, 'op_pr': 10.63}]

op.multi_plotter(spot=235, op_list=op_list)
````

## Plotting for Multiple Options strategy

### Example 1: Short Strangle
A short strangle is an options trading strategy that involve:
a. selling of a slightly out-of-the-money put and
b. a slightly out-of-the-money call of the same underlying stock and expiration date

````
op_1 = {'op_type':'c','strike':110,'tr_type':'s','op_pr':2}
op_2 = {'op_type':'p','strike':95,'tr_type':'s','op_pr':6}

op.multi_plotter(spot=100, op_list=[op_1,op_2])
````

### Example 2 : Iron Condor (Option strategy with 4 options)
An iron condor is an options strategy consisting of two puts (one long and one short) and two calls (one long and one short), and four strike prices, all with the same expiration date.

The stock currently trading at $212.26 (Spot Price)
Option 1: Sell a call with a $215 strike, which gives $7.63 in premium
Option 2: Buy a call with a strike of $220, which costs $5.35.
Option 3: Sell a put with a strike of $210 with premium received $7.20
Option 4: Buy a put with a strike of $205 costing $5.52.


````
op1={'op_type': 'c', 'strike': 215, 'tr_type': 's', 'op_pr': 7.63}
op2={'op_type': 'c', 'strike': 220, 'tr_type': 'b', 'op_pr': 5.35}
op3={'op_type': 'p', 'strike': 210, 'tr_type': 's', 'op_pr': 7.20}
op4={'op_type': 'p', 'strike': 205, 'tr_type': 'b', 'op_pr': 5.52}

op_list=[op1, op2, op3, op4]

op.multi_plotter(spot=212.26,spot_range=10, op_list=op_list)
````
The optional argument, spot range limits the range of spot values covered in the plot. The default spot range in +/-20%. If the underlying asset is less volatile and the strike price of options are within a small range, smaller spot range like 5% can be considered. For highly volatile underlying asset, higher spot range can be used.


### Example 3: Straddle (Option strategy with 2 options)
Strangle is a strategy which involves simultaneous purchase of call option and put option near the spot price allowing the purchaser to make a profit whether the price of the stock goes up or down.

Option 1: Buy Call at Strike Price 3070
Option 2: Buy Put option at Strike price 3070
Option expiry date can be specified as parameter ‘exp’ in the format ‘YYYY-MM-DD’.


```
op_1={'op_type': 'c', 'strike':3070, 'tr_type': 'b', 'op_pr': 108.63}
op_2={'op_type': 'p', 'strike':3070, 'tr_type': 'b', 'op_pr': 107.63}

op.multi_plotter(spot=3070, op_list=[op_1,op_2])
```

