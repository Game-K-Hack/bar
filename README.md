# LOADING BAR

Ce bout de code créer une barre de chargement pour vos programmes

```py
class progress_bar():
    def __init__(self, total):
        self.total = total
        self.current = 0
        self.length = 50
        self.pattern = '[=.]%'

    def format(self, format=None, side=None, full=None, empty=None, percent=True):
        if format is not None and side is None and full is None and empty is None:
            self.pattern = format
        elif format is None and side is not None and full is not None and empty is not None:
            if len(side) != 2:
                raise ValueError("Error: side is not equal to 2, but is equal to " + str(len(side)))
            self.pattern = f"{side[0]}{full}{empty}{side[0]}{'%' if percent else ''}"
        else:
            raise ValueError("Invalid arguments")

    def update(self):
        self.current += 1
        # Val to percent
        valp = round(100*self.current/self.total, 1)
        # Val to format bar
        valb = round(self.length*self.current/self.total)
        # Patern
        try: b = f"{self.pattern[0]}{self.pattern[1]*int(valb)}{self.pattern[2]*int(self.length-valb)}{self.pattern[3]}"
        except: pass
        p = f"{' '*(5-len(str(valp)))}{valp}%"
        # Return
        if len(self.pattern) == 5: return f'{b} {p}'
        elif len(self.pattern) == 4 and '%' not in self.pattern: return b
        elif '%' == self.pattern: return p
        else: raise ValueError("Invalid pattern")
```

### Test 1
```py
p = progress_bar(500)
for i in range(500):
    print('\r'+p.update(),end='')
```
```
[==================================================] 100.0%
```

### Test 2
```py
p = progress_bar(10)
p.format('(# )%')
for i in range(10):
    print('\r'+p.update(),end='')
```
```
(##################################################) 100.0%
```

### Test 3
```py
p = progress_bar(100)
p.format('%')
for i in range(100):
    print('\r'+p.update(),end='')
```
```
100.0%
```
