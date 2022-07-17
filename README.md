# Find Symbols

This class find posative symbol base on Currency pares in this case "BUSD".



```
import pandas as pd

import sys

sys.path.append("..")

from api_callling.api_calling import APICall


class FindSymbols:

    def get_all_symbols(self):
        ticker_info = pd.DataFrame(APICall.client.get_ticker())
        busd_info = ticker_info[ticker_info.symbol.str.contains('BUSD')]
        non_leverage = busd_info[~(busd_info.symbol.str.contains('UP')) | (busd_info.symbol.str.contains('DOWN'))]
        non_leverage.priceChangePercent = non_leverage['priceChangePercent'].astype(float)
        non_leverage = non_leverage.sort_values(by='priceChangePercent', ascending=False)
        print(non_leverage)
        non_leverage = non_leverage.iloc[:, :4]
        # TODO : Terminal Error
        symbols = non_leverage.loc[non_leverage['priceChangePercent'].astype(float) > 0]
        print(f"{len(symbols)} symbol we are processing.")
        return symbols


# fs = FindSymbols()
# fs.get_all_symbols()
```
