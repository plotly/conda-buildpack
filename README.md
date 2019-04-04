## Conda Buildpack

This is a Buildpack for [Conda](http://conda.pydata.org/), the Python distribution for scientific computing by Continuum Analytics.

This buildpack enables the installation of binary packages through the open source [conda](http://conda.pydata.org/) application.  Conda is recognized as being core to Continuum's Anaconda Scientific Python distro but it's also at the heart of the lighter weight [Miniconda](http://conda.pydata.org/miniconda.html) distro which we use here to install _only_ the binary packages we need for our apps deployed on [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) platforms like [Heroku](https://www.heroku.com/) and [Dash Deployment Server](https://plot.ly/dash/pricing/).

### Usage and files needed

#### conda runtime

A `conda-runtime.txt` file is needed, it should contain the version of `conda` to install, in the form of `Miniconda<2-or-3>-<conda-version>`, e.g. `Miniconda3-4.5.12`

The supported runtimes are the ones in [this list](https://repo.continuum.io/miniconda/) and `>= 3.18.3`

If this buildpack is used for a deployment to [Plotly's Dash Deployment Server](https://plot.ly/dash/pricing/) in `airgapped` (offline) mode, the only conda runtimes currently supported are `Miniconda3-4.5.12` and `Miniconda2-4.5.12`

#### conda requirements

To control what binary packages are installed by conda, supply a `conda-requirements.txt` file (which can be created by capturing the output of `conda list -e` for your working conda environment).

#### pip requirements

Like when using the standard `buildpack` for python from Heroku, you can also still supply a `requirements.txt` file for [pip](https://github.com/pypa/pip) to process. This allows you to install binary packages via `conda` when possible and still use pip for packages that are not available via `conda`.

