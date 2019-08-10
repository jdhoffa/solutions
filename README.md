# Project Drawdown Model Engine

This is the [Project Drawdown](https://www.drawdown.org/) model engine. This is intended to be a replacement for the series of interconnected Excel spreadsheets currently used by the project to do climate solution modeling. The intention is to create an implementation which will allow us to broaden the use of the climate solution models to policymakers, business leaders, and other decisionmakers and interested parties.

## Getting started

You will need [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Python 3](https://docs.python.org/3/using/index.html) installed.

Get a copy of this source code:

```sh
git clone git@gitlab.com:codeearth/drawdown.git
cd drawdown
```

Create and activate a python virtual environment. We recommend [Anaconda](https://www.anaconda.com/distribution/#download-section).

```sh
$ conda create --name drawdown
$ conda activate drawdown
(drawdown) $ conda install -c conda-forge jupyterlab altair bqplot
(drawdown) $ conda install -c conda-forge ipywidgets nodejs xlrd pytest
(drawdown) $ conda install -c conda-forge ipyvolume pillow qgrid
(drawdown) $ jupyter labextension install @jupyter-widgets/jupyterlab-manager
(drawdown) $ jupyter labextension install bqplot ipyvolume jupyter-threejs qgrid
```

Then start the Jupyter Notebook:
```sh
(drawdown) $ jupyter lab ./Drawdown.ipynb
```

---

## Road Map

### Core model complete

At this point in development the core model for computing adoption, costs, and benefits is substantially complete and fully handles 68 of the 79 total solutions models developed by the project. The remaining solutions are believed to be feasible, but are being pursued at a lower priority. Work from this point is focussing on several areas described below.

### User Interface
The ultimate goal of this project is to produce a compelling, browser-delivered GUI. There are at least three mostly distinct audiences:
+ Researchers who want to work with the models, add data sources, etc.
+ Policy makers and deciders, who need tools to help guide effective use of resources.
+ Interested parties and the general public, to evangelize that there *are* solutions to global warming.

UI work has focussed on the first point about the audience of researchers. This need is expected to be met using [Jupyter Notebook](https://jupyter.org), eventually hosted via an instance of [JupyterHub](https://jupyter.org/hub).

### Automated testing
One other goal for the project is to build a model implementation with good coverage by automated tests. There is a [YouTube video which demonstrates the different layers of tests](https://youtu.be/ipZrQWuMU3w) and another which [focuses on the Excel-based system test specifically](https://youtu.be/HLL7HrFcmjc).

Tests exist at several layers:
1. unit tests of each function
1. integration tests which compose modules to test an entire solution
1. a system test which starts Excel to compare the original, unmodified spreadsheet to the results from the new implementation

[Python test code coverage](https://codeearth.gitlab.io/drawdown/coverage/) reports are maintained as part of the CI/CD process.

---

## Drawdown Solution Models

[Documentation of the Excel models](https://gitlab.com/codeearth/drawdown/blob/master/Documentation/RRS_Model_Framework_and_Guidelines_v1.1.pdf) has been written, as well as a [design doc](https://docs.google.com/document/d/18nUKV-qltsaSD8kZd5gHswQu82Ot9rg19KIU8_eOisY/view) of how we expect the new implementation to be completed. We refer to this development effort as a Remodel, of course.

A climate solution model is the computation of outputs from a large number of inputs. Each of the outputs is a table with years as rows and regions as columns, where the value of a cell in this table is scalar.

The three outputs are:
* CO2 equivalents per year per region
* Cost of solution per year per region
* Functional Units per year per region.

The Functional Unit is a type which varies and might be different for every model. A functional unit is always a good that society needs. For example, it could be Terawatt-hours of electricity or person-kilometers of travel.

Every solution provides a certain number of functional units per year per region, depending on how the much the solution is adopted. For example, rooftop solar provides Terawatt-hours of electricity, in proportion to the capacity which is installed. Increased adoption provides increased functional units. It may also bring with it increased or decreased CO2 emissions, in a proportion depending on its nature. Rooftop solar produces fewer emissions that burning fossil fuel, for example. Each solution also has costs (potentially negative, or benefits) in proportion to its adoption.

The input to a given model is various data such as costs per installed watt of rooftop solar and the expected adoption of the solution. Additionally, Solutions are typically organized into "low adoption", "medium adoption", and "high adoption" scenarios.

Each model and functional unit has a notion of a Total Available Market. There is no benefit to install more rooftop solar than the total market for electricity, for example. The prevents unrealistic optimism on a single solution, for example.

Reaching the drawdown point, where humanity ceases to add greenhouses gases to the atmosphere, will require many solutions to be adopted and to harmonize synergistically.

---

## License
This program (excluding the Excel code) is part of the &lt;code&gt;/earth project. The python code for the model engine is licensed under the GNU Affero General Public license and subject to the license terms in the LICENSE file found in the top-level directory of this distribution and at https://gitlab.com/codeearth/drawdown. No part of this Project, including this file, may be copied, modified, propagated, or distributed except according to the terms contained in the LICENSE file.

Data supplied from Project Drawdown (mostly in the form of CSV files) is licensed under the [CC-BY-NC-2.0](https://creativecommons.org/licenses/by-nc/2.0/) license for non-commercial use. The code for the model can be used (under the terms of the AGPL) to process whatever data the user wishes under whatever license the data carries. The data supplied for the Project Drawdown solutions is CC-BY-NC-2.0.

---

## Contribution

Contributors to the project should submit to the project using the Developer Certificate of Origin. For more information, contact Denton Gentry (dgentry@carboncaptu.re).

---

## Acknowledgements

Many thanks to the contributors of the &lt;code&gt;earth hackathon held at the Internet Archive on Sept. 5, 6, and 7 of 2018 which began this project. They are: Owen Barton, Denton Gentry, Greg Elin, Marc Jones, Henry Poole, Robert L. Read, Stephanie Liu and Richard Stallman, in addition to Project Drawdown scientists and volunteers, Ryan Allard, Catherine Foster, Chad Frischmann, and Nick Peters.

Huge thanks to Beni Bienz of The Climate Foundation for his work in implementing a substantial portion of the system.

---

## Contact

Denton Gentry (dgentry@carboncaptu.re) is currently the technical point of contact for this project.
