# Experiment-2-Fitting-Poisson-Distribution
Aim: 
To fit Poisson distribution for the arrival of objects per minute from the feeder. 
# Software required: 

Python and Visual Component Tool
# Theory: 

1. The Poisson distribution gives the probability of a number of events occurring in a fixed interval of time or space when events occur independently and at a constant average rate (λ).
2. The probability mass function (PMF) is:  
<img width="1171" height="73" alt="image" src="https://github.com/user-attachments/assets/e28da9e9-3b3f-4969-baa9-2ff06c3358ba" />
3. Here, λ = mean number of occurrences, and e = 2.718 (base of natural logarithm).
4. The mean and variance of a Poisson distribution are both equal to λ.
5. Applicable when events occur independently, singly, and at a constant rate.
# Algorithm
<img width="1144" height="412" alt="image" src="https://github.com/user-attachments/assets/6bf357bd-7ba2-4908-8c93-ef74e4747a4f" />

# Program
```
Name: Monika V
Reg.no: 25017555
Slot.no:3P1-1


import numpy as np
import math
import scipy.stats

# Input
L = [int(i) for i in input("Enter data: ").split()]
N = len(L)
M = max(L)

X = []
f = []

# Frequency calculation
for i in range(M + 1):
    c = 0
    for j in range(N):
        if L[j] == i:
            c += 1
    f.append(c)
    X.append(i)

sf = np.sum(f)

# Probability P(x)
p = []
for i in range(M + 1):
    p.append(f[i] / sf)

# Mean of Poisson distribution
mean = np.inner(X, p)

# Reset lists
p = []
E = []
xi = []

print("X   P(X=x)   Obs.Fr   Exp.Fr   xi")
print("-----------------------------------")

# Poisson probability, expected frequency & Chi-square term
for x in range(M + 1):
    px = math.exp(-mean) * (mean ** x) / math.factorial(x)
    p.append(px)

    exp_f = px * sf
    E.append(exp_f)

    xi_val = ((f[x] - exp_f) ** 2) / exp_f if exp_f != 0 else 0
    xi.append(xi_val)

    print("%2d   %.3f   %4d   %.2f   %.3f" %
          (x, px, f[x], exp_f, xi_val))

print("-----------------------------------")

# Chi-square
cal_chi2 = np.sum(xi)
print("Calculated value of Chi-square = %.4f" % cal_chi2)

# Table value (1% LOS)
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print("Table value at 1%% LOS = %.4f" % table_chi2)

# Conclusion
if cal_chi2 < table_chi2:
    print("The given data CAN be fitted to Poisson Distribution at 1% LOS")
else:
    print("The given data CANNOT be fitted to Poisson Distribution at 1% LOS")

colab link:https://colab.research.google.com/drive/1dqcq9kmSWHh8LMwbJ7XWXjdYkfLm-DdV?usp=sharing 



# Output
```
Enter data: 5 6 7 8 9 3 15 7 9 4
X   P(X=x)   Obs.Fr   Exp.Fr   xi
-----------------------------------
 0   0.001      0   0.01   0.007
 1   0.005      0   0.05   0.049
 2   0.018      0   0.18   0.180
 3   0.044      1   0.44   0.721
 4   0.080      1   0.80   0.050
 5   0.117      1   1.17   0.024
 6   0.142      1   1.42   0.124
 7   0.148      2   1.48   0.182
 8   0.135      1   1.35   0.091
 9   0.110      2   1.10   0.746
10   0.080      0   0.80   0.800
11   0.053      0   0.53   0.531
12   0.032      0   0.32   0.323
13   0.018      0   0.18   0.181
14   0.009      0   0.09   0.095
15   0.005      1   0.05   19.773
-----------------------------------
Calculated value of Chi-square = 23.8780
Table value at 1% LOS = 30.5779
The given data CAN be fitted to Poisson Distribution at 1% LOS

```



# Result
The Poisson Distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 

