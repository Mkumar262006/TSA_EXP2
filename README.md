# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# GEG NO:212223240082
# Date: 11-05-2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load IPL dataset
d = pd.read_csv('matches.csv')

# Convert date column
d['date'] = pd.to_datetime(d['date'], format='mixed', dayfirst=True)

# Extract year
d['Year'] = d['date'].dt.year

# Count matches per year
r = d.groupby('Year')['id'].count().reset_index()
r.rename(columns={'id': 'Matches'}, inplace=True)

# Linear Trend Calculation
X = r['Year'] - r['Year'].mean()

b, a = np.polyfit(X, r['Matches'], 1)

print(f"Linear Equation: y = {a:.2f} + {b:.2f}(Year - {r['Year'].mean():.0f})")

# Predicted trend values
r['Linear Trend'] = a + b * X

# Plot
r.set_index('Year')[['Matches', 'Linear Trend']].plot(marker='o')

plt.title('Linear Trend of IPL Matches')
plt.ylabel('Number of Matches')
plt.grid()
plt.show()
```

B- POLYNOMIAL TREND ESTIMATION
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load IPL dataset
d = pd.read_csv('matches.csv')

# Convert date column
d['date'] = pd.to_datetime(d['date'], format='mixed', dayfirst=True)

# Extract year
d['Year'] = d['date'].dt.year

# Count matches per year
r = d.groupby('Year')['id'].count().reset_index()
r.rename(columns={'id': 'Matches'}, inplace=True)

# Polynomial Trend Calculation
X = r['Year'] - r['Year'].mean()

c, b, a = np.polyfit(X, r['Matches'], 2)

print(f"Polynomial Equation: y = {a:.2f} + {b:.2f}(Year - {r['Year'].mean():.0f}) + {c:.4f}(Year - {r['Year'].mean():.0f})²")

# Predicted polynomial trend
r['Polynomial Trend'] = a + b * X + c * X**2

# Plot
r.set_index('Year')[['Matches', 'Polynomial Trend']].plot(marker='o')

plt.title('Polynomial Trend of IPL Matches')
plt.ylabel('Number of Matches')
plt.grid()
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="852" height="592" alt="image" src="https://github.com/user-attachments/assets/ff4a46b0-fc32-40e0-98be-237bb43a3a59" />


B- POLYNOMIAL TREND ESTIMATION
<img width="870" height="591" alt="image" src="https://github.com/user-attachments/assets/017b364c-d55c-49d8-ace8-1288d7bd6e36" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
