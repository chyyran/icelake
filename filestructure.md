#Icelake - File Structure

Icelake requires an organized file structure wherein ROMs must be located in order to recognize and quickly access ROM files. 

* **ROMS for different platforms must not be in the same directory**. Each platform must have it's own separate folder(s) for ROMs or ISOs. 
* Icelake does not impose a certain naming standard when naming your ROM files however it is highly recommended.
* A file named `dirinfo.yml` will specify what platform's ROMs or ISOs the directory contains.


The recommended directory structure is that only one directory per platform is provided, however, Icelake supports multiple directories for a platform. 
However, Icelake does specify this recommended directory structure that must be present. Other directories where ROMs are located can be added.

* Icelake Games
  - Platform
      - dirinfo.yml
  - Platform
      - dirinfo.yml
  - Platform
      - dirinfo.yml
And so forth, where platform would the `full_name` of a certain specified `PlatformInfo`. 

A list of directories for a platform will be located in `directories.yml`. 


##ROM Metadata
A ROM can have multiple metadata files attached to it. Icelake defines the following metadata filetypes:

* Box Art (`.img.boxart`) (PNG|JPG|BMP)
* Screenshots (.img.screen`) (PNG|JPG|BMP)
