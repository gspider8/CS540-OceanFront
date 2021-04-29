# CS540-OceanFront
**Author:** Matthew Lehr<br>
**Email:** `lehrm@my.erau.edu`<br>
**Class:** CS 540, Spring 2021<br>
**Professor:** Steven Lehr<br>
**Description:** Volusia county oceanfront property identification<br>

---

## How to Use this data
The datset is located in `*.zip`, this data can be joined to an existing table using Altkey.
  

## Steps I took to edit hydrology shapefile to have a better oceanfront
Setting up environment<br>
1. Right click settings to ensure snapping and digitizing toolbars are available
2. Right click hydrology layer and toggle editing to on (a pencil should appear over the symbology icon)
3. Select the vertex tool and hover over the ocean hydrology polygon to see points
4. Toggle the magnet icon (snapping) to on
5. Going across the snapping toolbar, select the next icon and ensure snapping is set to all layers
6. On the third icon, select vertex and middle of segments 
7. On the fourth icon allow topographical editing<br>
**Editing coastline**
8. Move each point to endpoints of parcel layer by clicking hydrology point and hovering over end to find pink square and click to place the point
9. If a new point needs to be added, hover on area between two verticies until red, double click, and then add click to place point
10. Repeat up coastline
11. On breaks in parcel edge for beach access roads, draw straight line from corner of Northeast corner of more southern parcel up to southeast corner of more northern parcel
To Finish
12. Turn off snapping 
13. Toggle editing of hydrology layer to off

Notes:<br>
Save regularly since QGIS will crash<br>
Delete points one by one since at least on my computer, QGIS struggles to delete multiple points at once<br>
  -For future projects, a python script that runs the delete key every few seconds would be helpful to automate removal of uneeded points from old polygon<br><br>
If you are a visual learner refer to PolygonEditingSampleVideo.mp4 to see a step-by-step recording

  
