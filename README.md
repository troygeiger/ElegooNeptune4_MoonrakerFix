# Elegoo Neptune 4 Pro - Moonraker Metadata FIx

Up to and including the latest firmware version (1.1.2.53), thumbnails and other
metadata would not be displayed when using other slicers such as Orca Slicer or
PrusaSlicer. 

I was able to track the issue down to the metadata.py file and parse_gimage and
parse_simage being implemented for the Cura class but not the BaseSlicer class
and then those methods being added to the SUPPORTED_DATA variable. This causes
the def extract_metadata method to error when using any other slicer.
By moving those two methods to the BaseSlicer class resolves the errors and the
metadata is parsed correctly.

I also added 'OrcaSlicer': r"OrcaSlicer\s(.*)\son" to the PrusaSlicer class
aliases variable so that Orca Slicer gcode is parsed correctly. With these
changes, all metadata and the thumbnail shows on the touchscreen and
the web ui.

My hope is that this repo will only need to be temporary and that Elegoo will
implement these changes.
