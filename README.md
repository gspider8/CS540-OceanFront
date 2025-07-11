# CS540-OceanFront
**Author:** Matthew Lehr<br>
**Class:** CS 540, Spring 2021<br>
**Professor:** Steven Lehr<br>
**Institution:** Embry-Riddle Aeronautical University<br>
**Description:** Volusia county oceanfront property identification<br>

---
![](cs_540_ocean_front_1.PNG)

## How to Use this data
The datset is located in `ocean_front.zip`, this data can be joined to an existing table using Altkey.
Additionally update your hydrology shape file which is in the zipped folder hydrology-updated.zip

Code to add ocean_front field

alter table volusia.parcel add column ocean_front integer;
update volusia.parcel set ocean_front = 0;

alter table volusia.sales_analysis add column ocean_front integer;
update volusia.sales_analysis set ocean_front = 0;

--download and unzip ocean_front.zip to C:\temp\cs540

drop table if exists volusia.ocean_front_parcels;

create table volusia.ocean_front_parcels (
parid integer,
ocean_front integer
);

copy volusia.ocean_front_parcels from to 'C:\temp\cs540\ocean_front.txt' WITH (FORMAT 'csv', DELIMITER E'\t', NULL '', HEADER);

create index idx_ocean on volusia.ocean_front_parcels (parid);

update volusia.parcel p set ocean_front=o.ocean_front from volusia.ocean_front_parcels o where p.parid=o.parid;

update volusia.sales_analysis s set ocean_front=o.ocean_front from volusia.ocean_front_parcels o where s.parid=o.parid;

To update hydrology layer, in command prompt
cd c:\temp\cs540\gis
del hydrology.*

download and unzip hydrology-updated.zip into c:\temp\cs540\gis
and run the following commands to load shapefile into postgres
"c:\Program Files\PostgreSQL\13\bin\shp2pgsql.exe" -d -I -s 2236 -W "latin1" -g geom hydrology.shp volusia.gis_hydrology > create_hydrology.sql

"c:\Program Files\PostgreSQL\13\bin\psql.exe" -U postgres -d spatial -f create_hydrology.sql


## Steps I took to edit hydrology shapefile to have a better ocean front
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

 ## Limitations
 Parcels within a parcel on the coastline such as a condo building or individual units are not designated as ocean front. The analysis needed to correct this is beyond the scope of the course
