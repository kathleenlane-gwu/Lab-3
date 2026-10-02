## AI Usage

## Copilot Model
I used the free version of Claude, Sonnet 5.5.

## First AI Prompt
I first asked Copilot to help me find Python code that would recreate the same visualization I made in RStudio. I am more confident about creating a visualization in R, and didn't know the Python code that would create the same output in my .ipynb file. I entered the following prompt:
```
ggplot(pbc,
       aes(x = age,
           y = platelet)) +
  geom_point(alpha = 0.5) +
  geom_smooth(se = FALSE) +
  facet_wrap(~sex) +
  labs(title = "Platelet Count Decreases with Age in Both Women and Men", x="Age",y="Platelet Count")

What code would mimic this output in Python
```
Response: If you prefer a more grammar-of-graphics style equivalent to ggplot2, use plotnine:
```
from plotnine import (
    ggplot, aes, geom_point, geom_smooth,
    facet_wrap, theme_bw, labs
)

(ggplot(pbc, aes(x='age', y='platelet'))
 + geom_point(alpha=0.5)
 + geom_smooth(method='loess', se=False, color='blue')
 + facet_wrap('~sex')
 + theme_bw()
 + labs(title = "Platelet Count Decreases with Age in Both Women and Men", x="Age",y="Platelet Count")
)
```

## Error
I then ran into this error while trying to run the code Copilot provided me.
```
ModuleNotFoundError                       Traceback (most recent call last)
Cell In[7], line 1
----> 1 from plotnine import (
      2     ggplot, aes, geom_point, geom_smooth,
      3     facet_wrap, theme_bw, labs
      4 )
      6 (ggplot(pbc, aes(x='age', y='platelet'))
      7  + geom_point(alpha=0.5)
      8  + geom_smooth(se=False)
      9  + facet_wrap('~sex')
     10  + theme_bw()
     11  + labs(title = "Platelet Count Decreases with Age in Both Women and Men", x="Age",y="Platelet Count")
     12 )

ModuleNotFoundError: No module named 'plotnine'
```
## AI Response
I first asked Copilot what this error meant, then I asked how to fix it. Copilot told me that Python was unable to find the `plotnine` package in the environment that was running in my notebook. I had used the terminal to import `plotnine`, entering `python3 -m pip install plotnine`. However, Copilot helped me identify that my terminal environment was different than my notebook environment. To resolve this issue, Copilot suggested I run the following code in my notebook:
