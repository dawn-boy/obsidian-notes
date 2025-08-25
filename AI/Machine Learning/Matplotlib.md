## Anatomy of Matplotlib Plot
![[Matplotlib-1755140766819.png]]
 - Figure -> The big, outer container
 - Axes -> The actual plotting area inside the figure
 - Axis labels, titles, legends, ticks, grid lines -> Decorations
## The Object Hierarchy
`Figure` -> has one or more `Axes` -> Each `Axes` has its own `X/Y Axis`

## 2. Object Oriented Workflow
```python
import matplotlib.pyplot as plt

# step 1 - Prepare data
x = [1, 2, 3, 4, 5]
y = [1, 4, 7, 9]

# step 2 - create figure & axes
fig, ax = plt.subplots(figsize=(10, 10))

# step 3 - plot data
ax.plot(x, y)

# step 4 - customize
ax.set_title("Simple plot")
ax.set_xlabel("X axis")
ax.set_ylabel("Y axis")

# step 5 - save
fig.savefig("Sample.png")
```
## Different types of plots
```python
data = { col1: ["values"], col2: ["values"]}
x = np.random.randn(1000)

ax.plot(data.keys, data.values) # line graph
ax.bar(data.keys, data.values) # bar graph
ax.barh(list(data.keys), list(data.values)) # horizontal bar graph
ax.scatter(data.keys, data.values) # scatter graph
ax.hist(x)
```
## subplots
```python
# option 1
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(nrows=2, ncols=2, figsize=(5,5))

ax1.plot(data.keys, data.values) 
ax2.bar(data.keys, data.values) 
ax3.barh(list(data.keys), list(data.values)) 
ax4.scatter(data.keys, data.values) 

# option 2
fig, ax = plt.subplots(nrows=2, ncols=2, figsize=(5,5))

ax[0,0].plot(data.keys, data.values) 
ax[0,1].bar(data.keys, data.values) 
ax[1,0].barh(list(data.keys), list(data.values)) 
ax[1,1].scatter(data.keys, data.values) 
```
***
# Example: Generating a Random Walk
- A sequence where each value depends on previous value plus a random change.
- This is often used to model stock prices, temperature changes or other processes that evolve over time with random fluctuations.
$$X_t = X_{t-1} + \epsilon_t$$
where, $\epsilon_t$ is random noise, (e.g. from a normal distribution)

## Code
```python
dates = pd.date_range('05/11/2005', periods=1000) # a thousand dates

changes = np.random.randn(1000) # the normal distribution randomness

random_walk_data = pd.Series(changes, index=dates)
random_walk = random_walk_data.cumsum()
random_walk.plot()
```
## Output
![[Matplotlib-1755168370331.png]]
***
# Advanced plotting

## Scatter Plot
```python
plt.style.available # shows the availabe frame styles
plt.style.use('seaborn-v0_8')
fig, (ax0, ax1) = plt.subplots(figsize=(13,10), nrows = 2, sharex=True)

ax0_scatter = ax0.scatter(
    x=df['age'],
    y=df['chol'],
    c=df['target'],
    cmap='GnBu'
)
ax0.set_xlim([30,80])
ax0.set(
    title="Cholestrol vs. Age",
    ylabel='Cholestrol')
ax0.legend(*ax0_scatter.legend_elements(), title='Legend')
ax0.axhline(df['chol'].mean(), linestyle="--", c='darkblue')

ax1_scatter = ax1.scatter(
    x=df['age'],
    y=df['thalach'],
    c=df['target'],
    cmap='GnBu'

)
ax1.set(
    title="Max Heart Rate vs. Age",
    xlabel='Age',
    ylabel='Max Heart Rate'
)
ax1.legend(*ax1_scatter.legend_elements(), title='Legend')
ax1.axhline(df['thalach'].mean(), linestyle="--", c='darkblue');

fig.suptitle("Heart Diseases Analysis", fontsize=16, fontweight='bold')
```
## Output
![[Matplotlib-1755177798606.png]]