---
layout: post
title:  "Heat Maps for Dummies (or Smart People who Don't Know About Heat Maps)"
author: Nate Lewis
description: Short yet informative description
image: /assets/images/blog-image.jpg
---

# Why Do Heat Maps Matter?

A heat map is a representation of data where individual values are represented as colors,
where each cell's color represents a specific value, allowing patterns or trends to be identified intuitively and easily.
There are many use cases and industries where heat maps can be useful. Industries where heat maps are regularly used include:
+ Finance
+ Travel
+  Sports
+  Healthcare
+  Marketing
+  Technology
+  and many more

Usecases for heat maps include correlation matrixes, website heat maps, and geographic heat maps. In this tutorial we will go over the process of creating a basic 12x12 grid heat map in python using Matplotlib.

## Basic Setup

For demonstration purposes we will be looking at a dataset that contains records of the annual monthly average temperatures
in Aomori City, Aomori, Japan. To be clear heat maps do not have to use data involving temperatures, that is just the example I am using.
The data set being used can be found
[here on Kaggle.com](https://www.kaggle.com/datasets/akioonodera/monthly-temperature-of-aomori-city/data).
The heat map we create will allow us to see the trends in temperature for every month across a twelve year period.

      # First, I import the libraries that will be used for this tutorial
      import pandas as pd
      import matplotlib.pyplot as plt
      import numpy as np
      
      # Next I read in the data I will be using and make some basic changes to get it into the right format
      df = pd.read_csv("temp_aomori.csv")
      filtered_df = df[(df['year'] >= 2009) & (df['year'] <= 2020)]
      temp_data = filtered_df.pivot('year', 'month', 'temperature')
      
      # Fianlly we create our heat map using plt.imshow()
      plt.imshow(temp_data)
      plt.show()

Creating a heat map is as simple as that, but of course the heat map as created above is extremely barebones. 
In the following section we'll cover how to customize our heat map to make it both more aesthetically pleasing and to add more context to make it easier to understand.
  
## Customizing the Heat Map

Here's a look at some of the customization options available to you when making a heat map. 

#### Shape and Color

    # Read in and setup the data identically to in the Basic Setup section
    import pandas as pd
    import matplotlib.pyplot as plt
    import numpy as np
    df = pd.read_csv("C:\\Users\\natel\\Documents\\Fall2023\\temp_aomori.csv")
    filtered_df = df[(df['year'] >= 2009) & (df['year'] <= 2020)
    temp_data = filtered_df.pivot('year', 'month', 'temperature')

    # Create a new figure with a size of 10x8 inches
    plt.figure(figsize=(10, 8))
    
    # Create a heat map as before, but this time with the added aparameter "cmap"
    # cmap will change colors used in the heat map to make them more fitting for our data and more aesthetically pleasing
    plt.imshow(temp_data, cmap='coolwarm')
Other options for cmap values besides coolward include jet, summer, spring, inferno, and cool. You can also create your own custom color gradients. I encourage you when making your own heat maps to experiment with coloring to maximize the ability to intuitively understand your heat map.


#### Colorbar

    # Add a colorbar. The color bar informs the reader of what the colors in the heat map actually represent
    # and by labeling the colorbar we add the additional context of the units being used
    plt.colorbar(label='Temperature (°C)')

#### Labels

    # Add a title, and label the x and y axis
    plt.title('Temperature heat map (2009-2020)')
    plt.xlabel('Month')
    plt.ylabel('Year')

    # Customize the x and y ticks to represent the months and years
    # Without this step the ticks for both axis read as 0-11 instead of 2009-2020 and January-December
    # We also use "rotation=45" on the xticks to make our plot more readable
    plt.xticks(np.arange(len(temp_data.columns)), temp_data.columns, rotation=45)
    plt.yticks(np.arange(len(temp_data.index)), temp_data.index)

    plt.show()

## Conclusion

Following this tutorial, you should now be able to make your own basic heatmaps in Python. I encourage you, the reader, to 
attempt to make your own heat map, as they are used in some form in almost all fields of interest for statisticians.
