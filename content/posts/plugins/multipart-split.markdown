---

date: 2014-03-25 08:41:42+00:00
title: Multipart Split
menu:
  sidebar:
    name: Multipart Split
    identifier: multipart-split
    parent: plugins
    weight: 20

---

This QGIS plugin Multipart Split allows the user to, during edition, split the active layer’s selected multipart features into single part features. Unlike the “Multipart to single part” from the Vector > Geometry Tools menu, the plugin only splits the selected elements, and does not need to create new files.


### Installation

The plugin is available in the QGIS official repository, therefore the installation is done in the Manage and Install Plugins (Plugins > Manage and Install plugins…).

### Usage

With the selected vector layer in edition mode (Layer > Toogle edition), select all elements that you want to split e click the plugin’s icon available in the Advanced digitizing toolbar (View > Toolbars > Advanced digitizing) or in View > Split Feature(s) Part(s). In the end, a message with the results will be showed in the top of the map canvas. (Note that the icons on gets active if you select a layer in edition that has, at least, one selected feature)

Page: http://plugins.qgis.org/plugins/splitmultipart/

Repository: https://github.com/SrNetoChan/MultipartSplit