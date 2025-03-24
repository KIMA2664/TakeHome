# Computational Research Assistant TakeHome Assignment #

**Data provided:** land_parcels
It contained 100 different regions, with the volume of carbon it could store, and the cost of storing the carbon.

**Purpose of project**
After some research, it seemed the question aimed at optimizing the volume of carbon dioxide it could store underground in a given region, with some constraints - namely a budget, a location, and an area constraints
1. Budget constraint - The project should be less than 50% of the cost of storing the carbon under the 100 parcels of land
2. Location constraint - No two land parcels adjacent to each other can be chosen
3. Area constraint - We should aim to cover at least 25% of the total land area

**Steps of the project**
1. _Loading the appropriate libraries_
The libraries used were: geopandas, matplotlib, pandas, numpy, shapely, pulp
(Please have those libraries installed to replicate the file)

2. Explore the data to better understand the purpose
Some conclusions were that all pieces of land were quadriliterals, the current coordinate system was made in angular units, and a visualization of the 100 polygons of land parcels.
  
![image](https://github.com/user-attachments/assets/26074a4b-b616-442b-a9b2-dbab8c16afb1)

3. Computing areas of each polygon
To obtain an accurate reading of the areas, it was important to reproject the polygon in an alternate coordinate system, from 4326 to 3347.
This changed the coordinate system from angular units to metric units, which led to a better calculation of the area of polygons.

4. Finding ranges, averages and potentially exclude outliers in data
The range of the amount of carbon stored and the cost of storing that carbon were found as well as its minimum and maximum values.
I also looked for the minimum, maximum, and average of the areas of the polygons and found out if some of them were outliers.
I used the outlier method of a boxplot, which mentions that an outlier is 1.5 * IQR below the lower quartile. I did not find any outliers.
  
![image](https://github.com/user-attachments/assets/c046dce4-f59e-4499-a4f1-c1065932f352)

5. To know if 2 polygons were adjacent to each other
To achieve it, I created a function that outputs all the different edges of the polygon.
Since we knew that the polygon was a quadrilateral, it was easier to create a dictionary to contain all of them.
Then, I iteratively compared them to one another to find which polygons were next to each other - and shared an edge.
We found that all the polygons were adjacent to at least 2 other polygons, which made sense given our diagram at the beginning.
Here is an extract of the result:  

![image](https://github.com/user-attachments/assets/b4c040c6-8505-40c5-b098-9d5e9bffa176)

6. Building the model
I used PuLP to build the optimization model. I loaded each constraint as stated above and obtained the optimized distribution of land parcels to store the carbon.
Here is a picture of the result: (The red represents the chosen land parcels)
  
![image](https://github.com/user-attachments/assets/80e05fc6-d13d-41e1-affc-8228de0993c8)

**Conclusion:**  
From the result of the model, we found that this distribution fits all the constraints:
- Budget: 139,712
- Total carbon storage: 2841
- And no two polygons are adjacent (visible from the graph)

To me, the solution makes sense. Given that we are limited to the constraint of 50% of the cost (total: 281,926), we obtained about 50.6% of the total carbon storage (total: 5606).  
Side note: I noticed that the 3rd constraint is superfluous, we obtain the same result of the optimization model with or without it.

 
