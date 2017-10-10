# IRIS PROJECT

## SEMESTER AND CLASS TITLE

Fall 2017, DATA 550 Data Visualization by Dr. Bora Pajo

## PURPOSE

To analyze the Iris data from Kaggle. To write a description of each line of code and make modifications 

Using pandas, seaborn, matplotlib to create scatterplots, seaborn jointplot, boxplots, striplot, violin plot, kdeplot, pairplot, and andrews curves

## DATA SOURCE 

https://www.kaggle.com/benhamner/python-data-visualizations

The columns in the IRIS dataset include: Id, SepalLengthCm, SepalWidthCm, PetalLengthCm, PetalWidthCm, and Species

## KAGGLE LINK 

https://www.kaggle.com/oddinigwe/iris-flower-project/

## AUTHOR'S NAME AND CONTACT

Oddinigwe Onyemenem - oddinigwe@gmail.com

```
#to enable visualizations 
%matplotlib inline

# First, import pandas, a useful data analysis tool especially when working with labeled data
import pandas as pd

# import seaborn, visualization library in python 
import warnings # current version of seaborn generates a bunch of warnings that we'll ignore
warnings.filterwarnings("ignore")
import seaborn as sns
import matplotlib.pyplot as plt
sns.set(style="white", color_codes=True)

# Next, we'll load the Iris flower dataset, which is in the specified directory below
iris = pd.read_csv("Iris.csv") # this makes the iris dataset a Pandas Dataframe
```
```
to count the frequency of values for each species
iris["Species"].value_counts()

Output:
Iris-virginica     50
Iris-versicolor    50
Iris-setosa        50
Name: Species, dtype: int64
```
```
Use the .plot extension from Pandas dataframes to plot things
Use this to make a scatterplot of the Iris features-sepallengthcm on the x-axis and sepalwidthcm on the y-axis.
iris.plot(kind="scatter", x="SepalLengthCm", y="SepalWidthCm")
```
![GitHub Logo](output_2_1.png) 

```
Use the .plot extension from Pandas dataframes to plot things
Use this to make a scatterplot of the Iris features-petallengthcm on the x-axis and petalwidthcm on the y-axis.
iris.plot(kind="scatter", x="PetalLengthCm", y="PetalWidthCm")```
```
![GitHub Logo](output_3_1.png)

```
Use the seaborn library to make a similar plot
Seaborn jointplot shows two kinds of distribution in one visualization i.e. bivariate scatterplots and univariate histograms in the same figure
changed the size to 8 to make it bigger
sns.jointplot(x="SepalLengthCm", y="SepalWidthCm", data=iris, size=8)
```
![GitHub Logo](output_4_1.png)
```
using the petallegth and petalwidth features
Use the seaborn library to make a similar plot for the petallength and petalwidth
Seaborn jointplot shows two kinds of distribution in one visualization
i.e. bivariate scatterplots and univariate histograms in the same figure
changed the size to 8 to make it bigger
sns.jointplot(x="PetalLengthCm", y="PetalWidthCm", data=iris, size=8)
```
![GitHub Logo](output_5_1.png)
```
One piece of information missing in the plots above is what species each plant is
We'll use seaborn's FacetGrid to color the scatterplot by species
changed the size to 8
sns.FacetGrid(iris, hue="Species", size=8) \
   .map(plt.scatter, "SepalLengthCm", "SepalWidthCm") \
   .add_legend()
```
![GitHub Logo](output_6_1.png)
```
We can look at an individual feature in Seaborn through a boxplot
this shows the distribution of the petal length
sns.boxplot(x="Species", y="PetalLengthCm", data=iris)
```
![GitHub Logo](output_7_1.png)

```
A good way to complement the boxplot is by using the Seaborn's striplot
Use jitter=True so that all the points are not represented(clustered) on the same axis
this allows the data to be properly represented
Saving the resulting axes as ax each time causes the resulting plot to be shown
on top of the previous axes
added size to make the change the size of the dots i.e. bigger or smaller
changed edge color
ax = sns.boxplot(x="Species", y="PetalLengthCm", data=iris)
ax = sns.stripplot(x="Species", y="PetalLengthCm", data=iris, jitter=True, size = 6, edgecolor="black")
```
![GitHub Logo](output_8_1.png)

```
A violin plot combines the benefits of the previous two plots and simplifies them
Violin plot, unlike box plots, depict the density of the data
Denser regions of the data are fatter, and sparser thiner in a violin plot
further showing the distributions of the features i.e. petallength
sns.violinplot(x="Species", y="PetalLengthCm", data=iris, size=8)
```
![GitHub Logo](output_9_1.png)

```
A final seaborn plot useful for looking at univariate relations is the kdeplot,
which creates and visualizes a kernel density estimate of the underlying feature
sns.FacetGrid(iris, hue="Species", size=6) \
   .map(sns.kdeplot, "PetalLengthCm")\
   .add_legend()
 ```
![GitHub Logo](output_10_1.png)

```
Use Pairplot to depict mpairwise relationship between the features in the Iris dataset
From the pairplot, we'll see that the Iris-setosa species is separataed from the other
two across all feature combinations
sns.pairplot(iris.drop("Id", axis=1), hue="Species", size=3)
```
![GitHub Logo](output_11_1.png)

```
The diagonal elements in a pairplot show the histogram by default
Use kde to update the diagonal subplots instead of histogram
id is dropped 
sns.pairplot(iris.drop("Id", axis=1), hue="Species", size=3, diag_kind="kde")
```
![GitHub Logo](output_12_1.png)

```
This boxplot using pandas depicts the distribution by species and makes it more visually appealing
changes to the figsize, alters the height and width of the plots
iris.drop("Id", axis=1).boxplot(by="Species", figsize=(14, 7))
```
![GitHub Logo](output_13_1.png)

```
Import Andrews Curves 
Andrews curves uses curves to depict data which involve using and plotting attributes of samples as coefficients for Fourier series
from pandas.tools.plotting import andrews_curves
andrews_curves(iris.drop("Id", axis=1), "Species")
```
![GitHub Logo](output_14_1.png)
```
Parallel coordinates plots each feature on a separate column & then draws lines
connecting the features for each data sample
from pandas.tools.plotting import parallel_coordinates
parallel_coordinates(iris.drop("Id", axis=1), "Species")
```
![GitHub Logo](output_15_1.png)
```
Which puts each feature as a point on a 2D plane, and then simulates
having each sample attached to those points through a spring weighted
by the relative value for that feature
from pandas.tools.plotting import radviz
radviz(iris.drop("Id", axis=1), "Species")
```
![GitHub Logo](output_16_1.png)


