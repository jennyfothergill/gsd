Installation
============

**GSD** binaries are available in the `glotzerlab-software <https://glotzerlab-software.readthedocs.io>`_
`Docker <https://hub.docker.com/>`_/`Singularity <https://www.sylabs.io/>`_ images and in packages on
`conda-forge <https://conda-forge.org/>`_ and `PyPI <https://pypi.org/>`_. You can also compile **GSD** from source,
embed ``gsd.c`` in your code, or read gsd files with a single file pure python reader ``pygsd.py``.

Binaries
--------

Anaconda package
^^^^^^^^^^^^^^^^

**GSD** is available on `conda-forge <https://conda-forge.org/>`_. To install, first download and install
`miniconda <http://conda.pydata.org/miniconda.html>`_.
Then add the ``conda-forge`` channel and install **GSD**:

.. code-block:: bash

   ▶ conda install -c conda-forge gsd

Singularity / Docker images
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

See the `glotzerlab-software documentation <https://glotzerlab-software.readthedocs.io/>`_ for container usage
information and cluster specific instructions.

PyPI
^^^^

Use **pip** to install **GSD**:

.. code-block:: bash

   ▶ pip install gsd


Compile from source
-------------------

Obtain the source
^^^^^^^^^^^^^^^^^

Download source releases directly from the web: https://glotzerlab.engin.umich.edu/downloads/gsd

.. code-block:: bash

   ▶ curl -O https://glotzerlab.engin.umich.edu/downloads/gsd/gsd-v1.8.0.tar.gz

Or, clone using git:

.. code-block:: bash

   ▶ git clone https://github.com/glotzerlab/gsd

Configure a virtual environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When using a shared Python installation, create a `virtual environment
<https://docs.python.org/3/library/venv.html>`_ where you can install
**gsd**::

    ▶ python3 -m venv /path/to/environment --system-site-packages

Activate the environment before configuring and before executing
**gsd** scripts::

   ▶ source /path/to/environment/bin/activate

.. note::

   Other types of virtual environments (such as *conda*) may work, but are not thoroughly tested.

Install Prerequisites
^^^^^^^^^^^^^^^^^^^^^

**gsd** requires:

* A standards compliant C compiler
* Python >= 3.5
* numpy

Additional packages may be needed:

* nose (unit tests)
* sphinx (documentation)
* ipython (documentation)
* an internet connection (documentation)
* Cython >= 0.22 (to build non-tagged releases)
* cmake (for development builds)

Install these tools with your system or virtual environment package manager. GSD developers have had success with
``pacman`` (`arch linux <https://www.archlinux.org/>`_), ``apt-get`` (`ubuntu <https://ubuntu.com/>`_), `Homebrew
<https://brew.sh/>`_ (macOS), and `MacPorts <https://www.macports.org/>`_ (macOS)::

    ▶ your-package-manager install ipython python python-nose python-numpy cmake cython python-sphinx python-sphinx_rtd_theme

Typical HPC cluster environments provide python, numpy, and cmake via a module system::

    ▶ module load gcc python cmake

.. note::

    Packages may be named differently, check your system's package list. Install any ``-dev`` packages as needed.

.. tip::

    You can install numpy and other python packages into your virtual environment::

        python3 -m pip install numpy


Install with setuptools
^^^^^^^^^^^^^^^^^^^^^^^

Use ``python setup.py`` to install the python module into your virtual environment::

.. code-block:: bash

    ▶ python3 setup.py install

Build with cmake for development
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can assemble a functional python module in the build directory. Configure with **cmake** and compile with **make**.

.. code-block:: bash

   ▶ mkdir build
   ▶ cd build
   ▶ cmake ../
   ▶ make

Add the build directory path to your ``PYTHONPATH`` to test **GSD**:

.. code-block:: bash

   ▶ export PYTHONPATH=$PYTHONPATH:/path/to/build

Run tests
^^^^^^^^^

Run ``nosetests`` in the source directory to execute all unit tests. This requires that the
python module is on the python path.

.. code-block:: bash

   ▶ cd /path/to/gsd
   ▶ nosetests

Build user documentation
^^^^^^^^^^^^^^^^^^^^^^^^

Build the user documentation with **sphinx**. ``ipython`` is also required to build the documentation, as is an active
internet connection. To build the documentation:

.. code-block:: bash

   ▶ cd /path/to/gsd
   ▶ cd doc
   ▶ make html
   ▶ open _build/html/index.html

Using the C library
^^^^^^^^^^^^^^^^^^^^^^^^

GSD is implemented in less than 1k lines of C code. It doesn't build a shared library, just
copy ``gsd/gsd.h`` and ``gsd/gsd.c`` into your project and compile it directly in.

Using the pure python reader
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you only need to read files, you can skip installing and just extract the module modules ``gsd/pygsd.py`` and
``gsd/hoomd.py``. Together, these implement a pure-python reader for GSD and hoomd files - no C compiler required.
