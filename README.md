# Laminauts Website Code

This is the code base for [laminauts.com](https://laminauts.com). We hope it will serve as a resource for the layer fMRI community. Simultaneously, we will experiment with using this repository as a way for the community to contribute to the website through pull requests and github issues.

## Working with this codebase

This website code was created with [Sphinx](https://www.sphinx-doc.org/en/master/) and uses the [Furo](https://pradyunsg.me/furo/) theme. If you have not worked with Sphinx before, you will need to install it:

    pip install sphinx
    pip install furo

You can then clone this repository and build it:

    git clone https://github.com/andrewtmorgan/laminauts_website.git
    cd laminauts_website
    sphinx-build -b html source build

This will produce a local version of the website in a build folder. You can examine it using:

    open build/index.html

Feel free to add or edit anything on the website, we encourage contributions from the community. Sphinx uses a markup language called [reStructuredText](https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html). If you are not interested in diving into a new language, you can also open an issue in this repository to suggest changes or additions to the site.

Alternatively, if you prefer not to deal with github or edits, feel free to email us at [laminauts@gmail.com](mailto:laminauts@gmail.com) to suggest changes.


