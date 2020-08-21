# The DHuS Addon for Envisat

## Introduction.

The DHuS addon is a Java package that contains the definitions and extraction rules and operations for the Envisat products. The central element of this package is the ontology definition file ([aeolus.owl](src/main/resources/META-INF/envisat.owl)) located in the META-INF folder inside the resources directory.

The addon works in conjunction with the DRBX cortex definition (separate package), currently designed to support the following product types from the Envisat satellite mission:

- AATSR sensor
  - ATS\_LST\_2P
- ASAR sensor  
  - ASA\_WSM\_1P
  - ASA\_IMM\_1P
  - ASA\_APM\_1P
- MERIS sensor  
  - MER\_RR\_\_2P
  - MER\_FRS\_2P
- RA2 sensor
  - RA2\_GDR\_2P
  - RA2\_MWS\_2P

## Metadata Attributes

All metadata that will be extracted and made available via DHuS is defined within the OWL file mentioned above. The following is a complete list of metadata attributes implemented with this addon. Sample outputs to demonstrate which values these attributes can take can be found in the [samples](src/main/resources/samples) folder inside the resources directory.

| OData Name                 | OpenSearch Name          | Description                                                                          | AATSR   | ASAR    | MERIS (SEN3) | MERIS (N1) | RA2     |
|----------------------------|--------------------------|--------------------------------------------------------------------------------------|---------|---------|--------------|------------|---------|
| Satellite                  | -                        | Name of the satellite                                                                | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Instrument                 | -                        | Name of the instrument                                                               | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Date                       | -                        | Same as sensing start date                                                           | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Sensing start              | beginposition            | Sensing start date                                                                   | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Sensing stop               | endposition              | Sensing stop date                                                                    | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Footprint                  | gmlfootprint             | GML footprint                                                                        | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| JTS footprint              | footprint                | JTS footprint                                                                        | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Platform name              | platformname             | Name of the platform                                                                 | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Platform short name        | platformshortname        | Short name of the platform                                                           | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Platform serial identifier | platformserialidentifier | Identification number of the platform among the mission                              | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Platform NSSDC identifier  | platformnssdcidentifier  | The National Space Science Data Center (NSSDC) identification number of the platform | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Instrument name            | instrumentname           | Name of the instrument                                                               | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Instrument short name      | instrumentshortname      | Short name of the instrument                                                         | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Polarisation               | polarisation             | Polarisation combination                                                             | &#9744; | &#9745; | &#9744;      | &#9744;    | &#9744; |
| Polarisation mode          | polarisationmode         | Name of the polarisation mode                                                        | &#9744; | &#9745; | &#9744;      | &#9744;    | &#9744; |
| Instrument swath           | swathidentifier          | Swath identifier                                                                     | &#9744; | &#9745; | &#9744;      | &#9744;    | &#9744; |
| Orbit number               | orbitnumber              | Absolute orbit number                                                                | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Relative orbit number      | relativeorbitnumber      | Relative orbit number                                                                | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Cycle                      | cycle                    | Number of cycles                                                                     | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Phase                      | phase                    | Mission phase                                                                        | &#9745; | &#9745; | &#9744;      | &#9745;    | &#9745; |
| Orbit direction            | orbitdirection           | Orbit direction (ascending or descending)                                            | &#9744; | &#9745; | &#9745;      | &#9744;    | &#9744; |
| Processing level           | processinglevel          | The value of the last processing                                                     | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Processing center          | processingcenter         | Processing center ID                                                                 | &#9745; | &#9744; | &#9744;      | &#9744;    | &#9744; |
| Generation time            | -                        | Product generation date                                                              | &#9745; | &#9744; | &#9745;      | &#9745;    | &#9745; |
| Product type               | producttype              | Product type designation                                                             | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Product description        | productdescription       | One line description of the file                                                     | &#9745; | &#9745; | &#9744;      | &#9744;    | &#9745; |
| Size                       | size                     | File size                                                                            | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Format                     | format                   | Product format description                                                           | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |
| Filename                   | filename                 | File name                                                                            | &#9745; | &#9745; | &#9745;      | &#9745;    | &#9745; |



More information on the source of the respective attributes can be found directly by looking at the OWL file itself.

## Footprint Extraction

The footprint coordinates are extracted from the mixed ASCII/binary data file (N1), the netCDF (nc) file or the xfdumanifest.xml file, depending on the product. For the N1 files, the cortex topic (separate package) uses an XML schema definition file to create a tree of nodes which is then navigable within the addon OWL. This functionality is already provided for netCDF files by using the DRB netCDF extension in the topic class definition.

### Latitudes and Longitudes

The generation of the footprints is based on the following sources:

- AATSR: Latitude (Lat) and Longitude (Lon) variables in netCDF (Section 2.3 in [(A)ATSR Land Surface Temperature (LST) Product (UOL_LST_L2) Level 2 User Guide](https://earth.esa.int/documents/10174/1415229/ATSR_UOL_LST_L2_User_Guide_v1-0))
- ASAR: Product Positioning Information (Table 8.4.1.7-1 in [VOLUME 8: ASAR PRODUCTS SPECIFICATIONS](https://earth.esa.int/c/document_library/get_file?folderId=231342&name=DLFE-2136.pdf))
- MERIS (SEN3): footprint attribute in xfdumanifest.xml file
- MERIS (N1): Product Positioning Information (Table 11.4.1.6-1 in [ENVISAT-1 PRODUCTS SPECIFICATIONS, VOLUME 11: MERIS PRODUCTS SPECIFICATIONS](https://earth.esa.int/documents/700255/707222/Vol11_Meris_6a.pdf/58f5780c-adfd-407f-b924-91603cb5b0d5?version=1.0))
- RA2: 1 Hz Latitude (lat_01) and Longitude (lon_01) (Table 14.13.1.5.2 in [ENVISAT-1 PRODUCTS SPECIFICATIONS, VOLUME 14: RA2 PRODUCTS SPECIFICATIONS LEVEL 2](https://earth.esa.int/documents/700255/3528455/Vol14_Ra2mwr_5I_Level2.pdf))

For the following products, the values are provided in the unit of microdegrees and need to be scaled accordingly:

- ASAR
- MERIS (N1)
- RA2

 Furthermore, longitudes need to be converted from the (0-360) range to the (-180 to 180) range for the RA2 products.

### Geometry

The AATSR footprint covers one full orbit. The width of the swath is based on the coordinates given by the netCDF variables.

The ASAR products represent individual images, the corresponding footprints are hence rectangles.

The MERIS products are simple polygons in case of the N1 format and more enhanced footprints with the SEN3 format (determined externally using Sentinel-3 tools). 

For the RA2 product, the coordinates provided are the orbit coordinates. A continuous polygon having a fictional width of 1 millidegree was chosen to represent the footprint (defined by the offset variable in the OWL):

The number of points per polygon needs to be small enough for the DHuS to be able to handle it. A total number of approximately 400 points was chosen.

