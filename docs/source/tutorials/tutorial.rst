Tutorial
========

Installation
------------

In order to install the Countoscope Python tool, clone the repository using:

..  code:: bash

  git clone https://github.com/Countoscope/countoscope.git

Install all the required Python packages using:

..  code:: bash

    pip install -r requirements.txt

Then, type:

..  code:: bash

    pip install .

Use
---

In a Python script or a Jupyter Notebook, define the path to the data trajectory
file. For instance, using the `3D-closed` dataset provided in the `datasets`
repository:

..  code:: python

  path_to_data = "/mpath/datasets/datasets/3D-closed/trajectory.xyz"

Import the Countoscope as well as NumPy by typing:

..  code:: python

  from countoscope import Countoscope
  import numpy as np

The trajectory file `trajectory.xyz` corresponds to a system of 190 particles in
a :math:`(30 Å)^3` box. Let us define the system size as a NumPy array:

..  code:: python

    system_size = np.array([30, 30, 30])

Finally, let us choose a grid size for the Countoscope measurement:

..  code:: python

    box_size=np.array([10, 10, 10])

Then, launch the Countoscope calculation using *trajectory_file*, *system_size*,
and *box_size* as input parameters:

..  code:: python

    results = Countoscope(trajectory_file = path_to_data,
                        system_size=system_size,
                        box_size=box_size)
    results.run()

After the calculation is done, all the computed data can be obtained from the
`results` object. For instance, for :math:`\langle N \rangle`, type:

..  code:: python

    print(np.round(results.mean_of_N,2))

which will return:

..  code:: bash

    0.84

To plot :math:`\langle \Delta N^2 \rangle`, let us import Pyplot first:

..  code:: python

    import matplotlib.pyplot as plt
    plt.loglog(results.delta_n2)