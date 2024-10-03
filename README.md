# geoimagine04-conda_py_env

Explanation on how to setup virtual python environment for GeoImagine04 using Anaconda. A more in-depth discussion is available for [GeoImagine03](https://karttur.github.io/setup-ide/setup-ide/conda-environ/). The conda page on [Managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) is a more extensive explanation on how to manage virtual environments.

## Prerequisit

Anaconda must be installed.

## Create virtual environment

To setup a new virtual environment from using <span class='terminalapp'>conda</span> you can either
- define default packages in a file called .condarc,
- directly specify packages as part of the creation,
- use an exported configuration (yml) file, or
- set up a default environment and add individual packages afterwards

The last alternative, to install individual packages as a post-process, is not recommended. As the packages are not installed simultaneously, <span class='terminalapp'>conda</span> can not assure the coherence between the installed packages.

## Alt 1 Defining packages in .condarc

To create a virtual environment with many packages from scratch, the simplest way is to list the core packages you need in the <span class='file'>.condarc</span> configuration file in you personal folder.

The <span class='file'>.condarc</span> was not included by default when you installed conda. To find out if you have a <span class='file'>.condarc</span> file open a <span class='app'>terminal</span> window and type:
 <span class='terminal'>$ conda info</span>

Look for the line <span class='terminal'>user config file:</span> in the results.

If you do not have a <span class='file'>.condarc</span> file, you can create it by using a text editor or directly from the command line (e.g. <span class='terminal'>~$ pico .condarc</span>) or by running the command:

<span class='terminal'>$ conda config</span>

You can set a lot of parameters and functions in <span class='file'>.condarc</span> (as described [here](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html)), but for now you will only use it for defining a set of default packages that will always be included when creating a new environment.

### Default packages

The manual for setting default packages to install with every new environment is described [here](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#config-add-default-pkgs). Lists of available default packages for different conda distributions are found [here](https://docs.anaconda.com/anaconda/packages/pkg-docs/). The advantage with installing the core components in a single command is that conda will solve conflicts among dependencies. In other words, it is best to install all packages at once, so that all of the dependencies are installed at the same time. The above list will also install several other packages that are required by the Framework.

#### Default packages only

For creating virtual conda python environments only using [conda default packages](https://docs.anaconda.com/anaconda/packages/pkg-docs/) for Karttur's GeoImagine Framework, add the following lines to your <span class='file'>.condarc</span> file:

```
create_default_packages:
  - cartopy
  - fiona
  - gdal
  - geopandas
  - h5py
  - matplotlib
  - netcdf4
  - numba
  - numpy
  - pandas
  - pip
  - psycopg2
  - rasterio
  - scipy
  - statsmodels
  - xmltodict
channels:
  - defaults
```

#### Default and conda-forge packages

[conda-forge](https://conda-forge.org) is a community-led collection of recipes, build infrastructure and distributions for the conda package manager. Some of the conda packages required to run the complete Framework are not available as default packages, but with conda-forge. You can extent the <span class='file'>.condarc</span> configuration to also include packages available at [conda-forge](https://conda-forge.org). You can also install the [conda-forge](https://conda-forge.org) packages after you have set up the default packages - the commands for the latter are given further down in this post. If you want to try out using extending the configuration, update your <span class='file'>.condarc</span> file:

```
create_default_packages:
  - cartopy
  - fiona
  - gdal
  - geopandas
  - h5py
  - matplotlib
  - netcdf4
  - numba
  - numpy
  - pandas
  - pip
  - psycopg2
  - rasterio
  - scipy
  - statsmodels
  - xmltodict
  - plotnine
  - pypng
  - sentinelsat
  - svgwrite
  - tqdm
channels:
  - conda-forge
  - defaults
```

#### Create new environment from .condarc

Create a new environment:

<span class='terminal'>$ conda create ----name geoimagineXYZ</span>

To force a specific python version (recommended)

<span class='terminal'>$ conda create ----name geoimagineXYZ python=3.9</span>

The terminal reports the progress and you might need to respond to conflicts. Sticking to default answers to any questions usually solves any conflicts.

## Alt 2 Direct specification

An alternative to setting default packages using <span class='file'>.condarc</span>, is to directly specify the additional packages to bring along while creating the virtual environment:

<span class='terminal'>conda create \-n ossl_py39a python=3.9 cartopy fiona ... tqdm</span>

The reporting in the terminal will be similar as when installing using default packages defined in <span class='file'>.condarc</span>.

## Alt 3 From an exported configuration (yml) file

The [GitHub repo geoimagine04-conda_py_env](https://github.com/karttur/geoimagine04-conda_py_env) contains two exported conda virtual environment (yml) files. To set up a new virtual environment using an exported environment make sure the yml file is in the active path of the <span class='app'>Terminal</span> and then type (for all Operating Systems):

<span class='terminal'>conda env create \-f geoimagine_py37_from-history.yml</span>

If you run this on MacOS you can instead use the yml file for MacOS:

<span class='terminal'>conda env create \-f geoimagine_py37_for-macos.yml</span>

The reporting in the terminal will be similar as when installing using default packages defined in <span class='file'>.condarc</span>.
