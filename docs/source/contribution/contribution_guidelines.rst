.. _contribution-guidelines:

Contribution Guidelines
=======================

Contributing to Flightmare
--------------------------

The Flightmare team is glad to accept contributions from anybody willing to collaborate. 
There are different ways to contribute to the project, depending on the capabilities of the contributor. 
The team will work as much as possible so that contributions are successfully integrated into Flightmare.  

.. _report-bugs:

Report Bugs
-----------

Issues can be reported in the `client issues section <https://github.com/uzh-rpg/flightmare/issues>`_ or `server issues section <https://github.com/uzh-rpg/flightmare_unity/issues>`_ on GitHub. Before reporting a new bug, make sure to do some checkups.  

1. **Check if the bug has been reported.** 
Look it up in that same issue section on GitHub.

2. **Read the docs.** 
Make sure that the issue is a bug, not a misunderstanding of how Flighmare is supposed to work.

Code Contributions
------------------

In order to start working, fork the `client Flightmare repository <https://github.com/uzh-rpg/flightmare>`_ and/or the `server Flightmare repository <https://github.com/uzh-rpg/flightmare_unity>`_, and clone said fork in your computer. 
Remember to keep your fork in sync with the original repository.

Learn about Unity3D
^^^^^^^^^^^^^^^^^^^

Especially, if you work on the server-side of Flightmare then get familiar with the basics of Unity3D.
Lots of tutorials can be found at `Unity3D learning hub <https://learn.unity.com/tutorials>`_.

Coding Standard
^^^^^^^^^^^^^^^

Follow the current :ref:`coding standard <coding-standard>` when submitting new code.

.. _submission:

Submission
^^^^^^^^^^

Contributions and new features are not merged directly to the ``master`` branch, but to an intermediate branch named `dev`. 
This `Gitflow <https://nvie.com/posts/a-successful-git-branching-model/>`_ branching model makes it easier to maintain a stable master branch. 
This model requires a specific workflow for contributions.  

*   Always keep your ``dev`` branch updated with the latest changes. 

*   Develop the contribution in child branch from ``dev`` named as ``username/name_of_the_contribution``. 

*   Once the contribution is ready, submit a pull-request from your branch to ``dev``. 
    Try to be as descriptive as possible when filling the description. 
    Note that there are some checks that the new code is required to pass before merging. 
    The checks are automatically run by the continuous integration system. 
    A green tick mark will appear if the checks are successful. 
    If a red mark, please correct the code accordingly.  

Once the contribution is merged in ``dev``, it can be tested with the rest of the new features. 
By the time of the next release, the ``dev`` branch will be merged to ``master``, and the contribution will be available and announced.  

Checklist
^^^^^^^^^

*   [ ] Your branch is up-to-date with the ``dev`` branch and tested with latest changes.  

*   [ ] Extended the README/documentation, if necessary.  

*   [ ] Code compiles correctly.  

*   [ ] Pull requests is passing all tests.  

Art Contributions
-----------------

Art contributions include quadrotors, environments or any other type of assets to be used in Flighmare. 
Due to space limitations of the Github repository, please first get in touch with the Flightmare team to add your assets to the ``flightmare-unity`` repository.

Documentation Contributions
---------------------------

If some documentation is missing, vague or imprecise, it can be reported as with any other bug (read the previous section on :ref:`how to report bugs <report-bugs>`). 
However, users can contribute by writing documentation.  

The documentation is written with Sphinx as ReStructuredText.
If you are not familiar with Sphinx then read `this first to get started <https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html>`_.

Follow the steps below to start writing documentation.

.. important::
    To submit docs contributions, follow the same workflow explained right above in :ref:`code contributions <submission>`. 
    To sum up, contributions are made in a child branch from ``dev`` and merged to said branch.  

1. Clone the latest version of ``master``.

2. Install Sphinx.

  .. code-block:: bash

    pip install sphinx
    pip install sphinx-rtd-theme

3. Make the docs.

  .. code-block:: bash

    cd /FLIGHTMARE_PATH/docs
    make html
    # then open the created html in your favorite browser


4. Create a git branch. 

  Make sure to be in the ``dev`` branch (updated to latest changes) when creating a new one.
  .. code-block:: bash

    git checkout -b <contributor_name>/<branch_name>

5. Write the docs. 

  Edit the files following the guidelines in the :ref:`documentation standard <documentation-standard>` page.

6. Submit the changes. 

  Create a pull request in the GitHub repository, and add one of the suggested reviewers. 
  Try to be as descriptive as possible when filling the pull-request description.  

7. Wait for review. 

  The team will check if everything is ready to be merged or any changes are needed.  

.. warning:: The local repository must be updated with the latest updates in the `dev` branch.  
