# Territorial Timezones
## World timezones including territorial waters

[efele.net/tz](http://efele.net/maps/tz/world/) have done a wonderful job curating world timezones. However the maps used only include land. Harbours, coastal waters, and large lakes are considered international waters.

![Sydney Harbour](https://cloud.githubusercontent.com/assets/1595448/16751619/10ffdce4-47a9-11e6-8c79-c6cc7214d739.png)

I've expanded on the tz_world_mp to include territorial waters of 22.224km. When timezones overlap, the closest landmass is used.

![Western water border between Canada and US](https://cloud.githubusercontent.com/assets/1595448/16751388/06c279fa-47a7-11e6-94c5-2f790d0d7f7c.png)

The closest landmass was calculated using [QGIS](http://www.qgis.org/) by simplifying the original multipolygons, converting to points, and then calculating a Voronoi diagram. Simplification was required because of processing limitations. The original multipolygons were buffered using [PostGIS](http://postgis.net/) to 22.224km and simplified as accuracy in the ocean was not a concern of mine. PostGIS was significantly faster than QGIS for the buffering process. I intersected and dissolved the results to create a map with the original land borders and simplified coast including territorial waters. The process has significantly simplified the coastal shapes reducing the shape files from 35.8MB to 14.5MB without affecting land borders.

## Known issues

### Simplified Voronoi Diagram

Simplifying the original multipolygon prior to converting to points and processing a Voronoi diagram lead to some unfortunate artifacts around complex areas. 

#### Result
![image](https://cloud.githubusercontent.com/assets/1595448/16751956/56dcd0e4-47ab-11e6-891e-48f4f150d65b.png)

#### Actual
[![image](https://cloud.githubusercontent.com/assets/1595448/16752055/3ca6b626-47ac-11e6-969b-af84495e5d66.png)](https://www.openstreetmap.org/#map=12/49.0146/-123.1104)
