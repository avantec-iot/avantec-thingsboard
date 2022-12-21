# Using Avantec HVAC device with ThingsBoard

* [Read document](https://avantec-thingsboard.readthedocs.org)
* [Install tools](#install-tools)
* [Build document](#generate-web-pages)


This technical document is in the format of [reStructuredText](https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html) and Markdown/[CommonMark](https://commonmark.org/). It's generated using [Sphinx](https://www.sphinx-doc.org/).

## Install tools

### Prerequisites

* Install Python 3.5+ (for Sphinx).

<!-- * Install Java 8 or later (for sphinxcontrib-plantuml). -->

<!-- ### Step 1. Install Graphviz on Windows (for plantuml)

1. Download **Graphviz 2.38 Stable Release** from this [link](https://graphviz.org/_pages/Download/Download_windows.html).

2. Execute this windows installation package. The default installation path is: ***C:\Program Files (x86)\GraphvizX.XX\bin*** (Example: Graphviz**X.XX** → Graphviz**2.38**).

3. Set the PATH system variable and add `C:\Program Files (x86)\GraphvizX.XX\bin` to the existing path, eg: `C:\Program Files (x86)\Graphviz2.38\bin`.

4. Check with `dot -version` at the command prompt whether your changes are reflected:

    ```log
    C:\Users\Avantec>dot -version
    dot - graphviz version 2.38.0 (20140413.2041)
    libdir = "C:\Program Files (x86)\Graphviz2.38\bin"
    Activated plugin library: gvplugin_dot_layout.dll
    Using layout: dot:dot_layout
    Activated plugin library: gvplugin_core.dll
    ...
    ``` -->

### Step 1. Install Sphinx

Sphinx is a tool that makes it easy to create documentation.

Sphinx_intl is a useful tool for internationalization and localization.

1. On Windows, you should open Command Prompt (⊞Win-r and type **cmd**) and run the same command.
    
    It is a good moment to create a Python virtual environment and install the required tools. For that, open a command line terminal, `cd` into the directory you just created, and run the following commands <https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment>:

    * Windows:

    ```cmd
    > cd /path/to/project
    > python -m venv .venv                               # Creating a virtual environment
    > .\.venv\Scripts\activate                           # Activating a virtual environment
    (.venv) > where python                               # ...\.venv\Scripts\python.exe
    (.venv) > python -m pip install sphinx sphinx_intl   # Installing packages
    (.venv) > ...
    (.venv) > deactivate                                 # Leaving the virtual environment
    ```
    * Linux:

    ```sh
    $ cd /path/to/project
    $ python -m venv .venv                               # Creating a virtual environment
    $ source .venv/bin/activate                          # Activating a virtual environment
    (.venv) $ which python                               # .../env/bin/python
    (.venv) $ python -m pip install sphinx sphinx_intl   # Installing packages
    (.venv) $ ...
    (.venv) $ deactivate                                 # Leaving the virtual environment
    ```

    ***Note: venv will create a virtual Python installation in the `.venv` folder. You should exclude your virtual environment directory from your version control system using `.gitignore` or similar.***

2. After installation, type `sphinx-build --version` on the command prompt. If everything worked fine, you will see the version number for the Sphinx package you just installed.

3. Sphinx comes with a script called **sphinx-quickstart** that sets up a source directory and creates a default **conf.py** with the most useful configuration values from a few questions it asks you. To use this, run:

    ```sh
    cd /path/to/project
    (.venv) $ sphinx-quickstart docs
    cd docs
    ```

    We will be presented with a series of questions, the answer to which can depend from project to project.

    Now we can see that some foldes and files have been autogenerated for us:

    * `conf.py` : This is the file where all Sphinx configuration settings (including the settings we specified during the sphinx-quickstart setup) are specified.
    * `index.rst` : This is the file which tells Sphinx how to render our index.html page.
    * `_static` : image, script, etc.
    * `_build` : This is the directory where the output of any builder is stored when a `make <builder>` is called.

### Step 2. Install recommonmark

You can use **Markdown** and reStructuredText in the same Sphinx project.

1. Run the following command (using Command Prompt):

    ```sh
    (.venv) $ pip install recommonmark
    ```

2. Then in your `conf.py`:

    ```python
    extensions = ['recommonmark']
    extensions = ['sphinx.ext.autodoc']
    ```

    **Note**: You should skip this step(2). The above code is already in you `conf.py`.

**warning**: Markdown doesn’t support a lot of the features of Sphinx, like inline markup and directives. However, it works for basic prose content. reStructuredText is the preferred format for technical documentation

### Step 3. Install sphinx_rtd_theme

Sphinx_rtd_theme is a html theme.

1. Run the following command (using Command Prompt):

    ```sh
    (.venv) $ pip install sphinx_rtd_theme
    ```

2. Add this theme extension module in ```conf.py```

    ```python
    html_theme = 'alabaster'
    ```

    to

    ```python
    # html_theme = 'alabaster'
    import sphinx_rtd_theme
    html_theme = "sphinx_rtd_theme"
    html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
    ```

    **Note**: You should skip this step(2). The above code is already in you `conf.py`.

### Step 5. Install PlantUML

Plantuml is a library for generating UML diagrams from a simple text markup language.

1. On Windows, run the following command (using Command Prompt):

    ```sh
    (.venv) $ pip install plantweb
    ```
<!--
2. Add this *UML* extension modules in ```conf.py```:

    ```python
    extensions = ['plantweb.directive']
    ```

    **Note**: You may skip this step(2). The above code is already in you `conf.py`.
-->

<!-- ### Step 5. Install sphinxcontrib-plantuml

Plantuml is a library for generating UML diagrams from a simple text markup language.

1. On Windows, run the following command (using Command Prompt):

    ```sh
    pip install sphinxcontrib-plantuml
    # pip install plantweb
    ```

    **note**: When you install **sphinxcontrib-plantuml**, you may get a error: *attributeerror '_namespacepath' object has no attribute 'sort'*. Please execute command `python -m pip install --upgrade pip setuptools wheel` to fixed it.

2. Download plantuml.xxx.jar from this [link](https://plantuml.com/en/download), then save it to `docs\tool\`.

    **Note**: You may skip this step(2), because we already save `plantuml.xxx.jar` in `docs/tool/`.

3. Check with `java -jar docs\tool\plantuml.xxx.jar -version` at the command prompt whether your changes are reflected:

    ```log
    PlantUML version 1.2020.15 (Sun Jun 28 19:39:45 CST 2020)
    (GPL source distribution)
    Java Runtime: OpenJDK Runtime Environment
    JVM: OpenJDK 64-Bit Server VM
    Default Encoding: MS950_HKSCS
    Language: zh
    Country: HK

    PLANTUML_LIMIT_SIZE: 4096

    Dot version: dot - graphviz version 2.38.0 (20140413.2041)
    Installation seems OK. File generation OK
    ```

4. Add this *UML* extension modules in ```conf.py```:

    ```python
    extensions = ['sphinxcontrib.plantuml']

    import os
    plantuml_relative_path_ = r'tool\plantuml.1.2020.15.jar'
    plantuml = 'java -jar ' + os.path.join(os.path.abspath(os.getcwd()), plantuml_relative_path_)
    ```

    **Note**: You may skip this step(4). The above code is already in you `conf.py`. -->

## Generate web pages

You can following this command to build HTML document at `docs\`:

```shell
make html
```

Your `index.rst` has been built into `index.html` in your documentation output directory (typically `_build/html/index.html`). Open this file in your web browser to see your docs.

## Licenses

This project is released under [Apache 2.0 License](./LICENSE).

<!-- [plantuml.jar](https://plantuml.com/) is released under [Apache 2.0 License](./docs/tool/COPYING). -->

<!-- [ThingsBoard document](https://github.com/thingsboard/thingsboard.github.io) is released under [Apache 2.0 License](https://github.com/thingsboard/thingsboard.github.io/blob/master/LICENSE). -->
