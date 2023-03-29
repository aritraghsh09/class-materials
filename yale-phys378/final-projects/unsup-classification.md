# An Unsupervised Approach to Classify Astronomical Objects

## Objective
Develop an unsupervised algorithm that separates astronomical objects based on their type (star, galaxy, quasar) 

## Background
Different types of astronomical objects emit different amounts of light at different wavelengths. By observing the same object at different wavelengths (through different filters) or by observing the spectrum of an object, astronomers are able to tell what type an object is. The goal of this project is to develop an unsupervised algorithm that can take as an input the brightness of the object at different wavelengths; and then cluster them according to their type. 


## Data
The data consists of a `csv` file containing astronomical objects imaged using the [Sloan Digital Sky Survey](https://www.sdss.org/) (Data Release 12). The goal of this project is to use the brightness of the astronomical objects at different filters (u,g,r,i,z) to predict their object type -- star, galaxy or quasar. For this, you need to use an unsupervized ML framework. 


The file `sdss_dr12_objects.csv` contains 30,000 object and the  relevant columns are :-

* `u` --> Brightness of the object in the u-filter
* `g` --> Brightness of the object in the g-filter
* `r` --> Brightness of the object in the r-filter
* `i` --> Brightness of the object in the i-filter
* `z` --> Brightness of the object in the z-filter
* `redshift` --> How far the object is from us
* `class` --> Classification of the object (`STAR`,`GALAXY`,`QSO`) 

Our of the 30,000 objects; use the first 22,000 rows as the training + validation set (split according to your will). Use the last 8,000 rows as the test set. You cannot use the test set in any way while designing your unsupervized framework. 

### Data Notes
* The brightness of the objects are in magnitudes. Magnitudes are a unit commonly used in astronomy and roughly scales as the logarithm of the flux of the objects. Note that the magnitude scale is inverted. So a magnitude 15 object is brighter than an object with magnitude 17.

* Redshift determines how far the object is from earth. For the purposes of this project, treat is as a number with the only significance that an object a redshift 0.01 is closer to us than an object at 0.02

### Prediction Variable
The primary variable you should use to verify the performance of your unsupervized framework is the `class` column.


### How to Get the Data 

Using Linux/MacOS Command Line, first navigate to the location where you want to download the data. Then type in the following commands
```bash
ftp ftp.astro.yale.edu
cd pub/aghosh/phys_378_projects/unsup_class/
get *.csv
```

If you are using Windows, or if the above method fails, use your browser to navigate to 
```
ftp://ftp.astro.yale.edu/pub/aghosh/phys_378_projects/unsup_class/
```
Connect as guest if a prompt appears. Now download the `csv` file.



## Notes for Reproducability 
SQL query to recreate the table (this is not needed for the project in any way) 

```sql
SELECT TOP 30000
   p.objid,p.ra,p.dec,p.u,p.g,p.r,p.i,p.z,
   s.specobjid, s.class, s.z as redshift
FROM PhotoObj AS p
   JOIN SpecObj AS s ON s.bestobjid = p.objid
WHERE 
   p.u BETWEEN 0 AND 19.5
   AND s.z BETWEEN 0 AND 0.15
```


 
