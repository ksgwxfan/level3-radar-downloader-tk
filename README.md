# Level 3 Radar Downloader Tk, v1.0

The purpose of this Python Tkinter Zipapp is to expedite the retrieval and archival of the most-recent Level-III Radar data.

## Contents

- [Feature Highlights](#feature-highlights)
- [Requirements / Installation / Operation](#requirements--installation--operation)
- [Defaults Management](#defaults-management)
- [Filename Convention](#filename-convention)
- [Note on Low Beam Angle Availability](#note-on-low-beam-angle-availability)
- [Data Origin](#data-origin)
- [Viewing the Files](#viewing-the-files)
- [Roadmap](#roadmap)
- [Credits / Copyright](#credits--copyright)

## Feauture Highlights

- Rapidly retrieve the most-recent Level-3 Radar Data
- Access to radar data for over 200 weather radars (159 WSR-88D; 45 TDWR), primarily found in the contiguous United States.
- Over 120 products are made accessible to download, with 112 being available for all WSR-88D Sites.
  - Many of these products are very similar, and just differ by scan angle
- Maintain a "Favorites" radar site-list. This will streamline retrieval for your most-frequently accessed sites.
- Change the default (think *'start-up'* or *'Home'*) radar site.
- Keeps track of the downloaded files, and indicates previous download of a file through changing the background color (but it does not prevent one from downloading again)
  - This download history can be deleted via the `File`, `Options` Menu.
  - As typical products hold no more that 1 or 2 days worth of products, this should be done regularly

[&#8679; back to Contents](#contents)

## Requirements / Installation / Operation

#### Requirements

- Python (`v3.5` or newer)
- Tkinter must be installed with Python

#### Installation

- Simply download `level3_radar_downloader_tk.pyz`
- Place it into its own folder
- Run it. That's it!

#### Operation

\* For Convenience, these same instructions can be found within the `Instructions / Overview` option in the `Help` menu.

1) Select the radar site of interest, either from your favorites or the full list.
2) Select the category.
3) Select the product desired.

\*\* **The radar site, category and product lists respond to arrow keys for movement; no need to press Enter/Return afterward.**

4) Click `Refresh URL List`. (*Shortcut Key:* `R`)
    - Previously downloaded files will be highlighted in green. But the program does not prevent the user from downloading it again. It's there as a visual assist.
	- A label above the clock will appear.
	  - This label refers to the data in the URL box only. It ***does not*** reflect the currently-selected radar site or product.
	  - So even if you browse through the sites and products, it won't affect the URL List until you reload URLs via this button
5) Select the items you want to download.
6) Click `Get Selected URL(s)`. (*Shortcut Key:* `U`)
  - Items will be downloaded into corresponding folders based on their AWIPS Code (i.e. `N0Q`, `N0U`, etc).

[&#8679; back to Contents](#contents)

## Defaults Management

- It is recommended to save your most-frequently used radar sites and use a default radar site. These features make accessing those sites much faster.
- Modifying the defaults can happen in two places within the app:
  - via Context Menu
  - via options Menu
- Your default settings will load upon every use of the app!
- Context Menu
  - Right-click on any site of interest and a context menu will appear, giving a description of the site (so you don't accidentally operate on the wrong one)
  - From the Favorites context menu, only a removal option will be given.
  - If changing the default site, a confirmation dialog will appear first.
- Options Menu
  - Click `File` &gt; `Options`.
  - A menu will appear with essentially the same options as the context-menus, with an additional command to clear your favorites.

[&#8679; back to Contents](#contents)

## Filename Convention

Upon retrieving a list of contained URL's, you'll notice a common, but confusing, file-name structure.
- They'll be listed as an iteration of `sn.NNNN` where `NNNN` is typically a number between 0 and 300.
  - i.e. `sn.0030`, `sn.0201`, `sn.last`
- These are the actual files which will be downloaded.
- To assist you, associated dates/times with those files will be listed.
- Natively, though they follow an iterative pattern, files higher in the sequence does not mean it is a newer file. There isn't any guaranteed order by filename.
- So the app does this for you. The results are re-sorted to display in time-descending order (newest to oldest).
- Upon downloading (but prior to saving), the data within the file is inspected to retrieve the proper WMO Header and Volume Time-Stamp.
- The file is then saved with a readable filename:
  - `SSSS_WMOHDR_AAACCC_YYYYMMDDHHMM`
    - `SSSS` is the radar's parent's Weather Forecast Office (WFO) callsign (i.e. `KRNK`)
	- `WMOHDR` is the WMO Header (i.e. `SDUS51`)
	- `AAA` is the AWIPS product code
	  - Examples
	    - `N0Q` is 0.5deg Base Reflectivity
	    - `N0U` is 0.5deg Base Velocity
	    - `EET` is Enhanced Echo Tops
	- `CCC` is the radar callsign (i.e. `FCX`)
	- `YYYYMMDDHHMM` is the date-string, comprising of the Year, Month, Day, Hour, and Minute.
  - Example saved file name: `KRNK_SDUS51_N0QFCX_202110090426`
  - This file name structure is the formal standard, as far as I know. It's probably associated with the NEXRAD Information Dissemination Service (NIDS). I can't find any documentation to back that up though.

[&#8679; back to Contents](#contents)

## Note on Low Beam Angle Availability

Most categories feature products of low beam angles.
  - `NX_` products have a -0.2&deg; angle
  - `NY_` products have a 0&deg; angle;
  - `NZ_` products have a 0.3&deg; angle

For a significant majority of WSR-88D sites, these products are not currently available.

As such, the standard 0.5&deg; angle product (`N0_`) will be auto-selected for categories supporting these low-beam products.

[&#8679; back to Contents](#contents)

## Data Origin

- The data comes from the Radar Product Central Collection Dissemination Service ([RPCCDS](https://www.weather.gov/tg/rpccds)) on the [NWS Telecommunication Gateway](https://tgftp.nws.noaa.gov).
  - In particular, the radar data is contained within the folder of https://tgftp.nws.noaa.gov/SL.us008001/DF.of/DC.radar/
- This page is a great resource in explaining the folder structure of the data and interpretation of the products that are stored there:
  - https://www.weather.gov/tg/radfiles
    - *Of note, this page is slightly outdated, as a lot of the legacy radar products (lower-quality, in general) are no longer maintained.*
- This `PDF` was referenced to assist in compiling the needed codes and descriptions:
  - https://www.weather.gov/media/tg/rpccds_radar_products.pdf
- In general, you can expect the 300-or-so most-recent radar outputs available for each product.

[&#8679; back to Contents](#contents)

## Viewing the Files

You'll need some other software for viewing or working with the files. Below are just a few options

- [NOAA's Weather Climate Toolkit (WCT)](https://www.ncdc.noaa.gov/wct)
- [Unidata Integrated Data Viewer (IDV)](https://www.unidata.ucar.edu/software/idv)
- [McIDAS-V](https://www.ssec.wisc.edu/mcidas/software)

[&#8679; back to Contents](#contents)

## Roadmap

- [ ] Better management of download history by removing from the history files that aren't part of the most-recent data any longer
- [ ] Comment the Python code (even though the general accessibility is that of an app, not `.py` files)
- [ ] Investigate if a small image of radar imagery can appear to give reference to the file being inquired about


[&#8679; back to Contents](#contents)

## Credits / Copyright

- `Level 3 Radar Downloader Tk`, &copy; 2021, Kyle S. Gentry
- https://ksgwxfan.github.io
- for the clock update method, I did look it up, but do not remember where exactly I got the idea for the code

[&#8679; back to Contents](#contents)
























