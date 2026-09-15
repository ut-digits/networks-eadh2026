
# Network Visualization with Gephi

This document contains the stuff to be introduced at the workshop _Network Analysis for Digital Humanities_, taught at the EADH 2026 conference on Sept. 15, 2026, and organized by the project DigiTS (https://digits.ut.ee/). The current file discusses some functionalities of the program Gephi, which is a standalone open-source software to manipulate and visualize networks. See here for more details: [https://gephi.org/](https://gephi.org/). To download a version matching your operating system, go here: [https://gephi.org/desktop/](https://gephi.org/desktop/). A light in-the-browser version also exists, but its functionalities might be at times compromised.  


## Data and files

- a network of characters (interactions between characters) in _Hamlet_ by Shakespeare:
    - [../data/hamlet_network.gexf](../data/hamlet_network.gexf) (a native Gephi file)
    - [../../data/hamlet_network.csv](../../data/hamlet_network.csv) (a generic CSV file, more adventurous)
    - [https://dracor.org/shake/hamlet#downloads](https://dracor.org/shake/hamlet#downloads) (original dataset)
- a network of correspondence by John Locke:
    - [../../data/John_Locke_correspondence.gexf](../../data/John_Locke_correspondence.gexf) (a native Gephi file)
    - [https://github.com/claudewillan/JohnLocke](https://github.com/claudewillan/JohnLocke) (original dataset)
- a network of textual similarities in a corpus of 100 English novels:
    - [../../data/English_novels_network.csv](../../data/English_novels_network.csv) (a CSV file to import to Gephi)
    - [https://github.com/computationalstylistics/100_english_novels](https://github.com/computationalstylistics/100_english_novels) (100 English novels in a plain text format)
    - [https://computationalstylistics.github.io/projects/bootstrap-networks/](https://computationalstylistics.github.io/projects/bootstrap-networks/) (a blog post on how to get from raw texts to networks)



## Basic operations


### Before we even start

- Gephi develops fast: expect changes
- No undo button!
- Refresh button here and there

### General setup

- Overview
    - here you manipulate the nodes
    - add colors, shapes, sizes, labels, ...
    - compute statistics
- Data Laboratory
    - here you see the numeric data
        - edges
        - nodes
    - here you import spreadsheets
    - here you manipulate metadata
    - here you use regular expressions
- Preview
    - here you beautify your network
    - add curved lines
    - play with opacity, size, ...
    - here you export to PNG, PDF, SVG


### Layouts

#### Overview

- Manual layout 
    - (cf. Medici, Hamlet)
- Force-directed layout
    - play with [this toy example](https://vega.github.io/vega/examples/force-directed-layout/)
- Geoloyout
    - many examples, e.g. [this one](https://digilab.rara.ee/en/blog/national-library-of-estonia-datasets-on-map/)
    - geolayout in Gephi as [a plugin](https://gephi.org/desktop/plugins/geolayout-plugin/)
- Stressing divisions
    - e.g. the [OpenOrd layout](https://gephi.org/desktop/plugins/openord-layout/)
- Circular layout
    - e.g. [this one](https://gephi.org/desktop/plugins/concentric-layout/)
- ... and many other layouts
- but also: expansion, contraction, rotation (these are listed as layouts, too)

#### ForceAtlas2

- run it as is, stop it when you feel it's not improving anymore
- then play with expansion, contraction, rotation etc.
- Alternatively, set some parameters in ForceAtlas2:
    - scale
    - prevent overlap
    - dissuade hubs
    - stronger gravity
    - ...


### Manual edits

- Layout adjustments
- Coloring neighbors
- Label adjustments
- Manual tweaks:
    - particular nodes
    - node size
    - labels on/off




## Advanced stuff


### Automatic edits

- Label noverlap
- Coloring the nodes: partition
- Coloring the nodes: ranking
- Sizing the nodes
- Sizing edge weight


### Statistics

- Centrality, or "Who is the Main Character?"
- Modularity, or "Who is in which Clique?"
- The power of filtering
    - Range Filters: e.g., "Only show me nodes with a Degree >2"
    - Topology Filters: removing nodes with no edges (isolates)
- Now, use the newly computed data to color the nodes!


### Importing a spreadsheet

- Loading a file
    - go to Data Laboratory
    - import spreadsheet
    - check whether "nodes" and "edges" are there
- Extracting metadata from node IDs
    - create a new column using a regex
    - regex is a programming language for strings
    - to learn regex, see e.g. here: [https://regex101.com/](https://regex101.com/)
    - use the newly created column to color the nodes
- Extracting numeric data using regex
    - create a new column with a numeric regex, e.g. `[0-9]{4}` for years
    - copy it to a yet newer column as `string`
    - get rid of `[` and `]` characters
    - copy, again, to a new column as `integer` or `double`







## Appendix

Below, you will find some copy-pasted instructions on how to import a spreadsheet to Gephi, and how to extract metadata from filenames. The original source is [this slideshow](https://computationalstylistics.github.io/stylo_nutshell/) on how to use a stylometric package `stylo` in combination with Gephi. Certainly, applicability of the below instructions to the topics being discussed at the current workshop, is somehow limited, nonetheless please feel free to get inspired as much as you like.


#### Running Gephi: Import

* select **GEPHI > New Project**
* **Data laboratory > Import Spreadsheet**
* Import settings:
    * Separation: Comma
    * As table: Edges table
    * Charset: don’t bother if your filenames contain no fancy characters, e.g. `Brontë_Wuthering.txt`; otherwise choose wisely
    * Next
    * Select ALL available options
    * Finish!


#### Running Gephi: Labels

* We need to get authors’ names...
* Select **Create column with list of regex matching groups > ID**. 
    * Title: of your choice, e.g. Author, 
    * Regular Expression: limit what content to extract from the ID, 
        * e.g. to extract just the author from `Brontë_Wuthering.txt`: `^[A-Za-z]+`
* OK!
* **Copy data to other column > Author** to **Label**


#### Running Gephi: Overview

* Go to **Overview** panel
* In **Appearance >  Nodes > Partition**
* Select **Author**
* Apply
* Show labels (T icon on the bottom panel)


#### Running Gephi: Overview Layout

* Select **ForceAtlas 2**
* If you have a lot of data:
    * Dissuade Hubs
    * Prevent Overlap
* Edge Weight Influence 0.5
* Scaling: 500
* Run!


#### Running Gephi: Overview Layout (cont.)

* To make labels align:
    * select **Label Adjust**
* If your nodes stick together:
    * select **Expansion**
* Run! (for Expansion - a couple of times)


#### Running Gephi: Preview

* Go to **Preview** panel
* Node labels
    * Show labels
* Edges
    * Show edges
* Thickness: play with 0.1, 0.01, etc.
* Refresh!
* Reset zoom

#### Running Gephi: saving a network

* File > Save
    * with `.gephi` extension
* Picture
    * File > Export > SVG/PDF*/PNG
* For PDFs **Options > Landscape** & increase margins!
* OK!


