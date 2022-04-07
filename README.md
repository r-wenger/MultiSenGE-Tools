# MultiSenGE-Tools
This repository contains few tools to sort and extract stats on MultiSenGE dataset. If you want to download the dataset, please follow this [link](https://zenodo.org/record/6375466)

If you use this script and/or MultiSenGE dataset, please cite the paper as follow.

> Romain Wenger, Anne Puissant, Jonathan Weber, Lhassane Idoumghar, & Germain Forestier. (2022). A new remote sensing benchmark dataset for machine learning applications : MultiSenGE (1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.6375466
> Romain Wenger, Anne Puissant, Jonathan Weber, Lhassane Idoumghar & Germain Forestier (2022 - In Press) MultiSenGE : A Multimodal And Multitemporal Benchmark Dataset For Land Use/land Cover Remote Sensing Applications, ISPRS Annals of the Photogrammetry, Remote Sensing and Spatial Information Sciences, DOI: 

```
@article{MultiSenGE,
      title={MultiSenGE : A Multimodal And Multitemporal Benchmark Dataset For Land Use/land Cover Remote Sensing Applications}, 
      author={Romain Wenger, Anne Puissant, Jonathan Weber, Lhassane Idoumghar, Germain Forestier},
      journal={ISPRS Annals of the Photogrammetry, Remote Sensing and Spatial Information Sciences},
      volume={X},
      number={X},
      pages={X-Y},
      year={2022},
      doi={DOI}
}
```

Prerequisites
-----

Normally, json is a built-in library available in Python. In case it is not installed, I invite you to set it up with conda :

```
conda install -c jmcmurray json
```

List of methods in Patch class
-----

#### Methods :

* reconstruct_filename (Public) : Reconstruct the filename(s) of ground reference (gr) patch, Sentinel-2 (s2) patche(s) or Sentinel-1 (s1) patches.

* matching_periods (Public) : Check if the patch have nb_data_per_period for each period in periods (list of a list)

* has_nb_dates (Public) : Check if the patch has a certain number (nb_data patchs) of dates.

* has_matching_monthes (Public) : Check if the patch has a certain number (nb_data_per_month patchs) for each months (dates) for S1 or S2.

* get_centroid (Public) : Calculating the centroid of the patch.

* create_points_shapefile (Public Static) : Compute shapefile map from a list of points/centroids (default EPSG : 4326).

* change_coordinates (Public Static) : Changing coordinates from an epsg to an other.

* has_days_gap_s2 (Public) : Check if there is at least days_gap between each S2 image in each month.

* to_date (Public Static) : Convert a list of string dates in a format (date_format). Possibility to extract a date from a filename (S1 or S2 patches filename)

* generate_list_patches (Public Static) : Create a list of patches objects from json files available in MultiSenGE (labels folder).


#### Examples :

* This function read every json file in the folder. It returns a list containing x Patch objects according to the number of patches present in the dataset.
```
list_patches = Patch.generate_list_patches('./labels')
```

* There are two ways to use the constructor of the class. 
The first one is to give it a json filename from the labels folder.

```
constructor_wt_filename = Patch(json=os.path.join('./labels', '31UGP_2313_4883.json'))
```

The second one uses kwargs and you have to instantiate it with every parameters.

```
constructor_wt_params = Patch(x=x, y=y, tile=tile, s2_dates=s2_dates, s1_dates=s1_dates, projection=projection, labels=labels)
```

* With this function, you want to know if the current patch (mypatch) has at least 2 S2 patches for each period in periods.
```
periods = [['20200101', '20200731'], ['20200801', '20200930'], ['20201001', '20201231']]
mypatch.matching_periods(periods, 2)
```
#### Dataset visualization :

You can follow this [link](http://romainwenger.fr/Sentinel-GE/index.html) to visualize some informations extracted from MultiSenGE.

Contact
-----

This script was made by [Romain Wenger](http://romainwenger.fr/). For any questions or suggestions, do not hesitate to contact us : [Mail me](mailto:romain.wenger@live-cnrs.unistra.fr?subject=[GitHub]%20SEntinel-GE%20Tools)
