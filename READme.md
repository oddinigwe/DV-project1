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
iris = pd.read_csv("../input/Iris.csv") # this makes the iris dataset a Pandas Dataframe

# Next, display the first few rows and columns of the iris dataframe, good way to see the colum headings for the dataset 
iris.head()
Out[1]:
Id	SepalLengthCm	SepalWidthCm	PetalLengthCm	PetalWidthCm	Species
0	1	5.1	3.5	1.4	0.2	Iris-setosa
1	2	4.9	3.0	1.4	0.2	Iris-setosa
2	3	4.7	3.2	1.3	0.2	Iris-setosa
3	4	4.6	3.1	1.5	0.2	Iris-setosa
4	5	5.0	3.6	1.4	0.2	Iris-setosa
In [2]:
# to count the frequency of values for each species
iris["Species"].value_counts()
Out[2]:
Iris-versicolor    50
Iris-setosa        50
Iris-virginica     50
Name: Species, dtype: int64
In [3]:
# Use the .plot extension from Pandas dataframes to plot things
# Use this to make a scatterplot of the Iris features-sepallengthcm on the x-axis and sepalwidthcm on the y-axis.
iris.plot(kind="scatter", x="SepalLengthCm", y="SepalWidthCm")
Out[3]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f274351b550>

In [4]:
# Use the .plot extension from Pandas dataframes to plot things
# Use this to make a scatterplot of the Iris features-petallengthcm on the x-axis and petalwidthcm on the y-axis.
iris.plot(kind="scatter", x="PetalLengthCm", y="PetalWidthCm")
Out[4]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f273fca0a20>

In [5]:
# Use the seaborn library to make a similar plot
# Seaborn jointplot shows two kinds of distribution in one visualization i.e. bivariate scatterplots and univariate histograms in the same figure
# changed the size to 8 to make it bigger
sns.jointplot(x="SepalLengthCm", y="SepalWidthCm", data=iris, size=8)
Out[5]:
<seaborn.axisgrid.JointGrid at 0x7f273fbf1978>

In [6]:
#using the petallegth and petalwidth features
# Use the seaborn library to make a similar plot for the petallength and petalwidth
# Seaborn jointplot shows two kinds of distribution in one visualization
# i.e. bivariate scatterplots and univariate histograms in the same figure
# changed the size to 8 to make it bigger
sns.jointplot(x="PetalLengthCm", y="PetalWidthCm", data=iris, size=8)
Out[6]:
<seaborn.axisgrid.JointGrid at 0x7f273fcd2b00>

In [7]:
# One piece of information missing in the plots above is what species each plant is
# We'll use seaborn's FacetGrid to color the scatterplot by species
# changed the size to 8
sns.FacetGrid(iris, hue="Species", size=8) \
   .map(plt.scatter, "SepalLengthCm", "SepalWidthCm") \
   .add_legend()
Out[7]:
<seaborn.axisgrid.FacetGrid at 0x7f273f5c96a0>

In [8]:
# We can look at an individual feature in Seaborn through a boxplot
# this shows the distribution of the petal length
sns.boxplot(x="Species", y="PetalLengthCm", data=iris)
Out[8]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f273f4f6cf8>

In [9]:
# A good way to complement the boxplot is by using the Seaborn's striplot
# 
# Use jitter=True so that all the points are not represented(clustered) on the same axis,
#this allows the data to be properly represented
# 
# Saving the resulting axes as ax each time causes the resulting plot to be shown
# on top of the previous axes
# added size to make the change the size of the dots i.e. bigger or smaller
# changed edge color
ax = sns.boxplot(x="Species", y="PetalLengthCm", data=iris)
ax = sns.stripplot(x="Species", y="PetalLengthCm", data=iris, jitter=True, size = 6, edgecolor="black")

In [10]:
# A violin plot combines the benefits of the previous two plots and simplifies them
# Violin plot, unlike box plots, depict the density of the data
# Denser regions of the data are fatter, and sparser thiner in a violin plot
# further showing the distributions of the features i.e. petallength
sns.violinplot(x="Species", y="PetalLengthCm", data=iris, size=8)
Out[10]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f273fbf9588>

In [11]:
# A final seaborn plot useful for looking at univariate relations is the kdeplot,
# which creates and visualizes a kernel density estimate of the underlying feature
#
sns.FacetGrid(iris, hue="Species", size=6) \
   .map(sns.kdeplot, "PetalLengthCm")\
   .add_legend()
Out[11]:
<seaborn.axisgrid.FacetGrid at 0x7f273ef44e80>

In [12]:
# Use Pairplot to depictmpairwise relationship between the features in the Iris dataset
# 
# From the pairplot, we'll see that the Iris-setosa species is separataed from the other
# two across all feature combinations
sns.pairplot(iris.drop("Id", axis=1), hue="Species", size=3)
Out[12]:
<seaborn.axisgrid.PairGrid at 0x7f273ef4edd8>

In [13]:
# The diagonal elements in a pairplot show the histogram by default
# Use kde to update the diagonal subplots instead of histogram
# id is dropped 
sns.pairplot(iris.drop("Id", axis=1), hue="Species", size=3, diag_kind="kde")
Out[13]:
<seaborn.axisgrid.PairGrid at 0x7f273dad20f0>

In [14]:
# This boxplot using pandas depicts the distribution by species and makes it more visually appealing
# changes to the figsize, alters the height and width of the plots
iris.drop("Id", axis=1).boxplot(by="Species", figsize=(14, 7))
Out[14]:
array([[<matplotlib.axes._subplots.AxesSubplot object at 0x7f2736f18f98>,
        <matplotlib.axes._subplots.AxesSubplot object at 0x7f2736bd1828>],
       [<matplotlib.axes._subplots.AxesSubplot object at 0x7f2736be1630>,
        <matplotlib.axes._subplots.AxesSubplot object at 0x7f2736b17f28>]], dtype=object)

In [15]:
# Import Andrews Curves 
# Andrews curves uses curves to depict data which involve using and plotting attributes of samples as coefficients for Fourier series
from pandas.tools.plotting import andrews_curves
andrews_curves(iris.drop("Id", axis=1), "Species")
Out[15]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f2736922518>

In [16]:
# Parallel coordinates plots each feature on a separate column & then draws lines
# connecting the features for each data sample
from pandas.tools.plotting import parallel_coordinates
parallel_coordinates(iris.drop("Id", axis=1), "Species")
Out[16]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f2736f05828>

In [17]:
# Which puts each feature as a point on a 2D plane, and then simulates
# having each sample attached to those points through a spring weighted
# by the relative value for that feature
from pandas.tools.plotting import radviz
radviz(iris.drop("Id", axis=1), "Species")
Out[17]:
<matplotlib.axes._subplots.AxesSubplot at 0x7f27361f01d0>
