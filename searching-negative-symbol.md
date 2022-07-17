# Searching Negative Symbol

```
"""
This class used to find negative coins . 
When you call this method you need to pass all positive symbol as  argument. 
"""

from dataframe.dataframe import GetDataframe

from main.all_variable import Variable


class SearchingNegetiveSymbol:

    def negative_coin(self, all_symbol):
        disable_coins = ['RAMPBUSD']
        coins = []
        index = []
        all_symbols = [symbol for symbol in all_symbol['symbol']]
        for disable_coin in disable_coins:
            if disable_coin in all_symbols:
                all_symbols.remove(disable_coin)
        for symbol in all_symbols:
            dataframe = GetDataframe()
            index.append(len(all_symbols))
            print("We are searching in " + str(len(index)) + " no symbol named " + symbol)
            try:
                day_data = dataframe.get_day_data(symbol, 1, Variable.DAYS_TO_FIND_DATA)
            except ValueError:
            #TODO: Make a mail where get exception
                disable_coins.append(symbol)
                self.negative_coin()
            day_data_change_list = day_data['Change'].tolist()
            negative_coin_last_days = [value for value in day_data_change_list if
                                       value < 0 and day_data_change_list[-1] > 0]
            # print(negative_coin_last_days)
            if len(negative_coin_last_days) == (len(day_data_change_list) - 1):
                print(
                    f"\nWe find coin number {str(len(index))}  "
                    f"was negative {int(Variable.DAYS_TO_FIND_DATA) - 1} days,"
                    f"coin name: {symbol}\n")

                coins.append(day_data['symbol'][0])
        print(coins)
        return coins


# from get_symbol.find_symbols import FindSymbols
# fs = FindSymbols()
# all_symbol= fs.get_all_symbols()
# fk = SearchingNegetiveSymbol()
# fk.negative_coin(all_symbol)
```
