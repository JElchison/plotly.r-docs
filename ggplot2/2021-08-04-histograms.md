---
description: How to make Histogram plots in MATLAB<sup>&reg;</sup> with Plotly.
name: Histograms
display_as: statistical
order: 3
permalink: matlab/histograms/
thumbnail: thumbnail/histogram.jpg
layout: base
language: matlab
page_type: u-guide
---

## Histogram of Vector

Generate 10,000 random numbers and create a histogram. The `histogram` function automatically chooses an appropriate number of bins to cover the range of values in `x` and show the shape of the underlying distribution.

<pre class="mcode">
x = randn(10000,1);
h = histogram(x)

fig2plotly()
</pre>

plot_0_0_histogram_of_vector


<pre class="codeoutput">h = 
  Histogram with properties:

             Data: [10000x1 double]
           Values: [1x37 double]
          NumBins: 37
         BinEdges: [1x38 double]
         BinWidth: 0.2000
        BinLimits: [-3.8000 3.6000]
    Normalization: 'count'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]

  Show all properties

</pre>


When you specify an output argument to the `histogram` function, it returns a histogram object. You can use this object to inspect the properties of the histogram, such as the number of bins or the width of the bins.

Find the number of histogram bins. 

<pre class="mcode">
nbins = h.NumBins

fig2plotly()
</pre>


<pre class="codeoutput">nbins = 37
</pre>




<!--------------------- EXAMPLE BREAK ------------------------->

## Specify Number of Histogram Bins

Plot a histogram of 1,000 random numbers sorted into 25 equally spaced bins.

<pre class="mcode">
x = randn(1000,1);
nbins = 25;
h = histogram(x,nbins)

fig2plotly()
</pre>

plot_1_0_specify_number_of_histogram_bins


<pre class="codeoutput">h = 
  Histogram with properties:

             Data: [1000x1 double]
           Values: [1x25 double]
          NumBins: 25
         BinEdges: [1x26 double]
         BinWidth: 0.2800
        BinLimits: [-3.4000 3.6000]
    Normalization: 'count'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]

  Show all properties

</pre>


Find the bin counts.

<pre class="mcode">
counts = h.Values

fig2plotly()
</pre>


<pre class="codeoutput">counts = <span class="emphasis"><em>1×25</em></span>

     1     3     0     6    14    19    31    54    74    80    92   122   104   115    88    80    38    32    21     9     5     5     5     0     2

</pre>




<!--------------------- EXAMPLE BREAK ------------------------->

## Change Number of Histogram Bins

Generate 1,000 random numbers and create a histogram. 

<pre class="mcode">
X = randn(1000,1);
h = histogram(X)

fig2plotly()
</pre>

plot_2_0_change_number_of_histogram_bins


<pre class="codeoutput">h = 
  Histogram with properties:

             Data: [1000x1 double]
           Values: [1x23 double]
          NumBins: 23
         BinEdges: [1x24 double]
         BinWidth: 0.3000
        BinLimits: [-3.3000 3.6000]
    Normalization: 'count'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]

  Show all properties

</pre>


Use the `morebins` function to coarsely adjust the number of bins.

<pre class="mcode">
Nbins = morebins(h);
Nbins = morebins(h)

fig2plotly()
</pre>

plot_2_1_change_number_of_histogram_bins


<pre class="codeoutput">Nbins = 29
</pre>


Adjust the bins at a fine grain level by explicitly setting the number of bins.

<pre class="mcode">
h.NumBins = 31;

fig2plotly()
</pre>

plot_2_2_change_number_of_histogram_bins



<!--------------------- EXAMPLE BREAK ------------------------->

## Specify Bin Edges of Histogram

Generate 1,000 random numbers and create a histogram. Specify the bin edges as a vector with wide bins on the edges of the histogram to capture the outliers that do not satisfy |x|<2. The first vector element is the left edge of the first bin, and the last vector element is the right edge of the last bin.

<pre class="mcode">
x = randn(1000,1);
edges = [-10 -2:0.25:2 10];
h = histogram(x,edges);

fig2plotly()
</pre>

plot_3_0_specify_bin_edges_of_histogram

Specify the `Normalization` property as `'countdensity'` to flatten out the bins containing the outliers. Now, the area of each bin (rather than the height) represents the frequency of observations in that interval.

<pre class="mcode">
h.Normalization = 'countdensity';

fig2plotly()
</pre>

plot_3_1_specify_bin_edges_of_histogram



<!--------------------- EXAMPLE BREAK ------------------------->

## Plot Categorical Histogram

Create a categorical vector that represents votes. The categories in the vector are `'yes'`, `'no'`, or `'undecided'`.

<pre class="mcode">
A = [0 0 1 1 1 0 0 0 0 NaN NaN 1 0 0 0 1 0 1 0 1 0 0 0 1 1 1 1];
C = categorical(A,[1 0 NaN],{'yes','no','undecided'})
</pre>


<pre class="codeoutput">C = <span class="emphasis"><em>1x27 categorical</em></span>
  Columns 1 through 9

     no      no      yes      yes      yes      no      no      no      no 

  Columns 10 through 16

     undecided      undecided      yes      no      no      no      yes 

  Columns 17 through 25

     no      yes      no      yes      no      no      no      yes      yes 

  Columns 26 through 27

     yes      yes 

</pre>


Plot a categorical histogram of the votes, using a relative bar width of `0.5`.

<pre class="mcode">
h = histogram(C,'BarWidth',0.5)

fig2plotly()
</pre>

plot_4_0_plot_categorical_histogram


<pre class="codeoutput">h = 
  Histogram with properties:

              Data: [1x27 categorical]
            Values: [11 14 2]
    NumDisplayBins: 3
        Categories: {'yes'  'no'  'undecided'}
      DisplayOrder: 'data'
     Normalization: 'count'
      DisplayStyle: 'bar'
         FaceColor: 'auto'
         EdgeColor: [0 0 0]

  Show all properties

</pre>




<!--------------------- EXAMPLE BREAK ------------------------->

## Histogram with Specified Normalization

Generate 1,000 random numbers and create a histogram using the `'probability'` normalization.

<pre class="mcode">
x = randn(1000,1);
h = histogram(x,'Normalization','probability')

fig2plotly()
</pre>

plot_5_0_histogram_with_specified_normalization


<pre class="codeoutput">h = 
  Histogram with properties:

             Data: [1000x1 double]
           Values: [1x23 double]
          NumBins: 23
         BinEdges: [1x24 double]
         BinWidth: 0.3000
        BinLimits: [-3.3000 3.6000]
    Normalization: 'probability'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]

  Show all properties

</pre>


Compute the sum of the bar heights. With this normalization, the height of each bar is equal to the probability of selecting an observation within that bin interval, and the height of all of the bars sums to 1.

<pre class="mcode">
S = sum(h.Values)

fig2plotly()
</pre>


<pre class="codeoutput">S = 1
</pre>




<!--------------------- EXAMPLE BREAK ------------------------->

## Plot Multiple Histograms

Generate two vectors of random numbers and plot a histogram for each vector in the same figure. 

<pre class="mcode">
x = randn(2000,1);
y = 1 + randn(5000,1);
h1 = histogram(x);
hold on
h2 = histogram(y);

fig2plotly()
</pre>

plot_6_0_plot_multiple_histograms

Since the sample size and bin width of the histograms are different, it is difficult to compare them. Normalize the histograms so that all of the bar heights add to 1, and use a uniform bin width.

<pre class="mcode">
h1.Normalization = 'probability';
h1.BinWidth = 0.25;
h2.Normalization = 'probability';
h2.BinWidth = 0.25;

fig2plotly()
</pre>

plot_6_1_plot_multiple_histograms



<!--------------------- EXAMPLE BREAK ------------------------->

## Adjust Histogram Properties

Generate 1,000 random numbers and create a histogram. Return the histogram object to adjust the properties of the histogram without recreating the entire plot.

<pre class="mcode">
x = randn(1000,1);
h = histogram(x)

fig2plotly()
</pre>

plot_7_0_adjust_histogram_properties


<pre class="codeoutput">h = 
  Histogram with properties:

             Data: [1000x1 double]
           Values: [1x23 double]
          NumBins: 23
         BinEdges: [1x24 double]
         BinWidth: 0.3000
        BinLimits: [-3.3000 3.6000]
    Normalization: 'count'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]

  Show all properties

</pre>


Specify exactly how many bins to use.

<pre class="mcode">
h.NumBins = 15;

fig2plotly()
</pre>

plot_7_1_adjust_histogram_properties

Specify the edges of the bins with a vector. The first value in the vector is the left edge of the first bin. The last value is the right edge of the last bin.

<pre class="mcode">
h.BinEdges = [-3:3];

fig2plotly()
</pre>

plot_7_2_adjust_histogram_properties

Change the color of the histogram bars.

<pre class="mcode">
h.FaceColor = [0 0.5 0.5];
h.EdgeColor = 'r';

fig2plotly()
</pre>

plot_7_3_adjust_histogram_properties



<!--------------------- EXAMPLE BREAK ------------------------->

## Determine Underlying Probability Distribution

Generate 5,000 normally distributed random numbers with a mean of 5 and a standard deviation of 2. Plot a histogram with `Normalization` set to `'pdf'` to produce an estimation of the probability density function.

<pre class="mcode">
x = 2*randn(5000,1) + 5;
histogram(x,'Normalization','pdf')

fig2plotly()
</pre>

plot_8_0_determine_underlying_probability_distribution

In this example, the underlying distribution for the normally distributed data is known. You can, however, use the `'pdf'` histogram plot to determine the underlying probability distribution of the data by comparing it against a known probability density function.

The probability density function for a normal distribution with mean μ, standard deviation σ, and variance σ<sup>2</sup> is



<pre class="mcode">

</pre>



Overlay a plot of the probability density function for a normal distribution with a mean of 5 and a standard deviation of 2.

<pre class="mcode">
hold on
y = -5:0.1:15;
mu = 5;
sigma = 2;
f = exp(-(y-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi));
plot(y,f,'LineWidth',1.5)

fig2plotly()
</pre>

plot_8_1_determine_underlying_probability_distribution



<!--------------------- EXAMPLE BREAK ------------------------->

## Saving and Loading Histogram Objects

Use the `savefig` function to save a `histogram` figure.

<pre class="mcode">
histogram(randn(10));
savefig('histogram.fig');
close gcf

fig2plotly()
</pre>

Use `openfig` to load the histogram figure back into MATLAB. `openfig` also returns a handle to the figure, `h`. 

<pre class="mcode">
h = openfig('histogram.fig');

fig2plotly()
</pre>

plot_9_0_saving_and_loading_histogram_objects

Use the `findobj` function to locate the correct object handle from the figure handle. This allows you to continue manipulating the original histogram object used to generate the figure.

<pre class="mcode">
y = findobj(h,'type','histogram')

fig2plotly()
</pre>


<pre class="codeoutput">y = 
  Histogram with properties:

             Data: [10x10 double]
           Values: [2 17 28 32 16 3 2]
          NumBins: 7
         BinEdges: [-3 -2 -1 0 1 2 3 4]
         BinWidth: 1
        BinLimits: [-3 4]
    Normalization: 'count'
        FaceColor: 'auto'
        EdgeColor: [0 0 0]

  Show all properties

</pre>




<!--------------------- EXAMPLE BREAK ------------------------->

