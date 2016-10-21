HCPyTools
---------

The aim of ``HCPyTools`` is to make it easy to do data science with healthcare
data. The package has two main goals:

-  Allow one to easily create models based on tabular data, and deploy a best
model that pushes predictions to SQL Server.

-  Provide tools related to data cleaning, manipulation, and imputation.

To get started, check out this `notebook`_.

.. _notebook: notebooks/HCPyToolsExample1.ipynb

Documentation
=============

To render docs, create a virtualenvironment for ``hcpytools`` and
install required python modules with ``pip install -r dev-requirements.txt``.

Then simply run ``inv docs`` and a new browser window should open to http://127.0.0.1:8001