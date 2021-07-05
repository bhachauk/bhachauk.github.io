---
github: patch_antenna
---

<kbd class="imgtitle">Contents</kbd>

- [Overview](#overview)
- [Step 1: Finalize your python package](#step-1--finalize-your-python-package)
- [Step 2: Add test scripts](#step-2--add-test-scripts)
- [Step 3: Release the distribution to PyPI](#step-3--release-the-distribution-to-pypi)
- [Step 4: Use GitHub and CI Tools](#step-4--use-github-and-ci-tools)
- [Reference](#references)
{: .contentBorder .txt-pad}


#### Overview

In this post, I will try to share my observations and best practices to publish a python package. The four simple steps
mentioned below will help you to implement a systematic approach and make your publishing work easy.  

![4 steps to publish python package](/images/post_img/PythonPackage.png)

---

#### Step 1 : Finalize your python package

Yes. This also a step and the first one to be done. In this step you need to check some plenty of points and also some
post development points such as,
 
- Check whether all the facilities in our checklist covered.
- Find and remove dead codes if available in current version.
- Update the readme and other notes if present.
- Add **TODOs** or future plant comments as mentioned in your readme.
- Please review your once again from end to end, sure you will find some enhancement.

---

#### Step 2 : Add test scripts

Adding test scripts will make the package more proper and will help you to find one or more cases to be covered. Also, python
package : **pytest** offers test facility to check your package with the test cases. Whenever you add new facility or made changes,
try to add the respective test case.

**PyTest**

- [PyTest : Basic patterns and examples](https://docs.pytest.org/en/6.2.x/example/simple.html)
- [Examples and customization tricks](https://docs.pytest.org/en/6.2.x/example/index.html)

---


#### Step 3 : Release the distribution to PyPI

I suggest to read the post from reference : [How to Publish an Open-Source Python Package to PyPI](https://realpython.com/pypi-publish-python-package/).
However here the summarized points as steps are added,

- Use the link : [https://pypi.org/account/register/](https://pypi.org/account/register/) to register in PyPI if not yet done.
- Configuring the package using <mark>setup.py</mark> which consists all info about your package.
- Build and test your project using python package <mark>twine</mark>. The commands are,

```
python setup.py sdist bdist_wheel
twine check dist/*
```

- To publish your package to PyPI, use the command,

```
twine upload dist/*
```

- As there are other packages also mentioned on that post. If wish, have a look at [Poetry](https://python-poetry.org/), 
[Flit](https://flit.readthedocs.io/en/latest/), [Cookiecutter](https://cookiecutter.readthedocs.io/).

---


#### Step 4 : Use GitHub and CI Tools

In this step, The usages of **GitHub** and **Travis CI** in publishing python packages are explained.

- The **Travis CI** is used to verify the **build passing status** and **test results** of the latest commit.
- GitHub workflows facility is used to publish the package to PyPI.

I have added these both facilities in my github repo [patch_antenna](https://github.com/Bhanuchander210/patch_antenna). 
Let us take this repo as an example for the further discussion.

###### Travis CI

Integrating [Travis CI](https://travis-ci.org/) to your github repo is done by adding a <mark>.travis.yml</mark> file in the same repo.
I have added the steps what are all need to be done to test my package in that yaml file like shown below. 

**.travis.yml**

```yaml
sudo: false
language: python
python:
  - "3.7"
before_install:
  - pip3 install scipy
  - python3 setup.py install
script: pytest
notifications:
  email: false
```

Once this added to your github repo, you need to enable travis ci in github authorized [Applications](https://github.com/settings/applications) and
also configure which repo need to be used by travis ci in [https://travis-ci.com/](https://travis-ci.com/).

###### GitHub workflows

GitHub offers workflows facility to do various of our requirements. I am using this facility to publish my python package
to PyPI on release based mode like we did it with travis ci. 

To avail the facility, a yaml file <mark>.github/workflows/python-publish.yml</mark> created in the same repo.

**python-publish.yml**

```yaml
name: Upload Python Package              
on:
  release:
    types: [created]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install setuptools wheel twine
    - name: Build and publish
      env:
{% raw %}
        TWINE_USERNAME: ${{ secrets.PYPI_USERNAME }}
        TWINE_PASSWORD: ${{ secrets.PYPI_PASSWORD }}
{% endraw %}
      run: |
        python setup.py sdist bdist_wheel
        twine upload dist/*
```

The user name and password which asked by twine can be added as **secrets** in the same repository **settings > secrets** like shown below image.

**Screenshot**
![git secrets](/images/post_img/github_secrets.png)

Once you done all the above points, follow these steps as best practices to publish you package.

- Do your regular commits with test cases and also verify the build status using travis ci.
- Keep update readme and todo notes in your repo to track your goals.
- Once you feel done with the facilities and also build passes, Make a release on github with respected version and release notes. (Also don't forget to add the latest version in setup.py)
- This will release new package version as you mentioned in setup.py file using github workflows and also you can check with workflow results in **actions** page.

#### References

- [https://realpython.com/pypi-publish-python-package/](https://realpython.com/pypi-publish-python-package/)
- [https://docs.pytest.org/en/stable/goodpractices.html](https://docs.pytest.org/en/stable/goodpractices.html)
- [Publishing package distribution releases using GitHub Actions CI/CD workflows](https://packaging.python.org/guides/publishing-package-distribution-releases-using-github-actions-ci-cd-workflows/)
- [Building and testing Python](https://docs.github.com/en/actions/guides/building-and-testing-python)
- [Travis CI Tutorial](https://docs.travis-ci.com/user/tutorial/)