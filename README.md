## UN Data Exploration Bonus Questions

This set of exercises is designed to give you a chance to try out some more advanced features of the pandas library.
These exercises will be using the gdp_le DataFrame that you created for the regular exercises, meaning that it will have columns for Country, Year, GDP_Per_Capita, Continent, and Life_Expectancy.

1. Let's compare the median life expectacy for each across all of the years of data that we have. Perform a groupby on both Year and Continent and then aggregate using the median and save the results to a new object.  
	a. What type of object results from this?  
	b. Look at the index of the resulting object. What do you notice about it?  
	c. Use .loc to select the median life expectancy for Asia in 2010.  
	d. Use .loc to select the median life expectancy for both Asia and Africa in 2010.  
	e. Use .loc to select the values for all continents for the year 2010.  
	f. Use .loc to select the median life expectancy for Asia across all years. Hint: One way to do this is to use the swaplevels method.  
2. Group gdp_le by both Year and Continent and find the min, median, and max values for both gdp per capita and life expectancy. Hint: You may want to use the [agg method](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.agg.html).  
	a. Look at the columns of the resulting object. What do you notice?  
	b. Select the median gdp per capita value for Asia in 2010.
3. In this question, we'll see how the median gdp per capita has changed over time. Start by creating a Series, gdp_median_per_year by grouping by the Year variable and calculating the median gdp per capita.  
	a. Convert gdp_median_per_year to a DataFrame by using the [reset_index method](https://pandas.pydata.org/docs/reference/api/pandas.Series.reset_index.html).  
	b. The [shift method](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.shift.html) will allow you to compare values across rows. Use this method to create a new column showing the change in gdp per capita since the prior year.  
	c. How many times was there a drop in median gdp per capita from one year to the next?  
4. Now, let's expand on the prior question to find the change in GDP from year to year for each country.  
	a. Add a new column to the gdp_le DataFrame showing the change in gdp per capita from the prior year for that country. Hint: You can combine groupby with the shift method.  
	b. Which country had the largest one year increase in gdp per capita? Which had the largest one year drop in gdp per capita?
5. When looking at time series data, there can often be a large amount of observation to observation variability, making it more difficult to see general trends. This variability can be smoothed out by calculating rolling averages. We'll see how in this question.  
	a. First, filter gdp_le down to just the rows for the United States and save the result to a DataFrame named gdp_le_us.  
	b. Use [rolling](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rolling.html) to calculate the 3-year moving average of gdp per capita for the US.  
	c. Plot both the original gdp per capita values and the rolling average on the same plot.
6. When working with large datasets, it can sometimes pay off to be mindful of what data types you are using for each variable.  
	a. Create a new column, Continent_Category by converting the Continent column to a [category](https://pandas.pydata.org/docs/user_guide/categorical.html).  
	b. Use the memory_usage method to compare the memory used by the original Continent column compared to the category version.  
	c. You can also sometimes get speedups for groupby operations by using category datatypes. In Jupyter, if you want to estimate how long it takes to run a block of code, you can add the %%timeit magic to the top of a cell. Compare doing a groupby + aggregation on the original Continent column compared to the Continent_Category column.  
	d. You can also sometimes save memory usage by adjusting the size that is stored for integer values. By default, the int64 type is used which can store values between –9223372036854775808 and 9223372036854775807. However, for the Year variable, we really don't need that large of a range. We could get by with a 16 bit integer, whose range is -32768 to 32768. Convert the Year column to int16 type and then compare the memory usage.  
	e. Finally, you don't have to make these datatype changes after the data has been read in. Add some parameters to the read_csv call that imports the GDP data. Read in only the needed columns (not the Value Footnotes column). Also, read in the Country or Area column as a category type and the Year column as an int16 type.