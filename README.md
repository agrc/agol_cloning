# agol_cloning
Cloning content between AGOL orgs

You can use the `CloneItemsAcrossOrgs` jupyter notebook to clone a user's items from one organization to another.

The notebook contains some helper methods and the `CloningTank` class. These create a framework for cloning the user's items folder by folder, creating the folder in the destination if it doesn't exist. It tries to work from most complex items to least complex: apps, web maps, feature services, any other types. The notebook includes some example code for setting up a `CloningTank` object and cloning items.

For each item, the `clone_items()` method in the ArcGIS API for Python will attempt to clone any dependencies for that item if they don't already exist in the target gis. Cloning an app will clone any web maps in the app, and the web map cloning operations will clone any feature services or other layer sources in turn. 

If the `CloningTank` framework encounters an error with a particular item, it will skip that item and any of its parents. For example, an app relies on a map which has a layer, and the layer throws an error while cloning its soruce. Neither the layer, web map, nor the app will clone (this behavior comes from `clone_items()`. However, the framework will then attempt the next item in the list for that particular folder instead of bombing out for the whole folder.

As of the current ArcGIS API for Python release (1.8.1), the newer version of several items can't be cloned. These include newer dashboards, Experience Builder apps, and the new JS 4.x Story Maps. 

For more info on cloning items, see [https://developers.arcgis.com/python/guide/cloning-content/](https://developers.arcgis.com/python/guide/cloning-content/).
