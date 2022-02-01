---
layout: contents
language: en
title: Developer
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: developerja.html
lang_opp_word: To Japanese
prev_url: setup.html
prev_string: Setup
top_url: index.html
top_string: TOP
next_url: environments.html
next_string: Environments/Settings
---

# Development & Contribution

This page provides information about local development of each subsystem and contribution to it.

## K2HR3 Repositories structure

This chapter describes the `k2hr3` repository on GitHub.

The `k2hr3` repository consists of the following submodules.

- k2hr3_app
  - a repository for Web Application server
- k2hr3_api
  - a repository for REST API server
- k2hr3_osnl
  - a repository for K2HR3 OpenStack Notification Listener
- k2hr3_sidecar
  - kubernetes Pod Sidecar docker image repository for automatically registoration/deletion Pods(Containers) from kubernetes
- k2hr3_utils
  - a repository for utilities
- k2hr3_get_resource
  - a repository for a `Systemd` service for retrieving RESOURCE
- k2hr3_cli
  - a repository for Command Line Interface(CLI)

The latter part of this page will describe how to build packages in these repositories and test them.


## The k2hr3_api repository

This chapter instructs how to build a `k2hr3_api` package and test it in your local development environment.

k2hr3_api repository is a repository for K2HR3 API server.

1. Fork the [https://github.com/yahoojapan/k2hr3_api](https://github.com/yahoojapan/k2hr3_api) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_api.git
    ```

3. install dependent packages to your local development environment. To build a k2hr3_api package, *k2hdkc* shared library and the header files are required.
   
    For recent Debian-based Linux distributions users, follow the steps below::
    ```
    $ sudo apt-get update -y
    $ sudo apt-get install curl -y
    $ curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.deb.sh | sudo bash
    $ sudo apt-get install k2hdkc-dev
    ```

    For CentOS users, runt the following commands. To compile a Node.js for `k2hdkc`, you need install the [devtoolset](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-7/) package::
    ```
    $ sudo yum install centos-release-scl
    $ sudo yum install devtoolset-7
    $ scl enable devtoolset-7 bash
    ```

    For users who use supported Fedora other than latest version, follow the steps below::
    ```
    $ sudo dnf makecache
    $ sudo dnf install curl -y
    $ curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.rpm.sh | sudo bash
    $ sudo dnf install k2hdkc-devel
    ```

    For other recent RPM-based Linux distributions users, follow the steps below::
    ```
    $ sudo yum makecache
    $ sudo yum install curl -y
    $ curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.rpm.sh | sudo bash
    $ sudo yum install k2hdkc-devel
    ```

    For other Linux system users, build sources on the [https://github.com/yahoojapan/k2hdkc](https://github.com/yahoojapan/k2hdkc) repository and install *k2hdkc* shared library and the header files. See [https://k2hdkc.antpick.ax/build.html](https://k2hdkc.antpick.ax/build.html) for details.

    After installing the *k2hdkc* shared library and the header files, install the npm package. Run the following commands::
    ```
    $ cd k2hr3_api/
    $ npm install
    ```

4. Create a branch for local development::
    ```
    $ git checkout -b my-first-contribution
    ```

	Now you are ready for local code changes.

5. The following command run tests. When you change codes locally, make sure the tests finish correctly.
    ```
    $ npm run test
    ```

6. Commit your code changes and push your branch to GitHub when you change codes::
    ```
    $ git add .
    $ git commit -m "Short description of your changes."
    $ git push origin my-first-contribution
    ```
    
7. Submit a pull request through the GitHub website when you change codes.


## The k2hr3_app repository

This chapter instructs how to build a `k2hr3_app` package and test it in your local development environment.

k2hr3_api repository is a repository for K2HR3 Web server.

1. Fork the [https://github.com/yahoojapan/k2hr3_app](https://github.com/yahoojapan/k2hr3_app) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_app.git
    ```

3. install dependent packages to your local development environment.

    ```
    $ cd k2hr3_app/
    $ npm install
    ```

4. Create a branch for local development::

    ```
    $ git checkout -b my-first-contribution
    ```

5. The following command run syntax validations and tests. When you change codes locally, make sure the tests finish correctly.

    ```
    $ npm run build
    $ npm run test
    ```

6. Commit your code changes and push your branch to GitHub when you change codes::

    ```
    $ git add .
    $ git commit -m "Short description of your changes."
    $ git push origin my-first-contribution
    ```
    
7. Submit a pull request through the GitHub website when you change codes.



## The k2hr3_osnl repository

This chapter instructs how to build a `k2hr3_osnl` package and test it in your local development environment.

k2hr3_osnl repository is a repository for K2HR3 OpenStack Notification Listener.


1. Fork the [https://github.com/yahoojapan/k2hr3_osnl](https://github.com/yahoojapan/k2hr3_osnl) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_osnl.git
    ```

3. install dependent packages to your local development environment.

    ```
    $ cd k2hr3_osnl/
    $ pip3 install pipenv
    $ python3 -m pipenv install -dev --python /path/to/python3
    $ pipenv shell
    ```
    
4. Create a branch for local development

    ```
    (k2hr3_osnl) $ git checkout -b my-first-contribution
    ```

5. The following command run syntax validations and tests. When you change codes locally, make sure the tests finish correctly.

    ```
    (k2hr3_osnl) $ make lint test
    ```

6. Commit your code changes and push your branch to GitHub when you change codes

    ```
    (k2hr3_osnl) $ git add .
    (k2hr3_osnl) $ git commit -m "Short description of your changes."
    (k2hr3_osnl) $ git push origin my-first-contribution
    ```
    
7. Submit a pull request through the GitHub website when you change codes.





## The k2hr3_sidecar repository
This chapter instructs how to build a `k2hr3_sidecar` docker image and test it in your local development environment.

k2hr3_sidecar repository is a repository for managing Sidecar docker images required to automatically register and delete Pods(Conatainers) from kubernetes.

1. Fork the [https://github.com/yahoojapan/k2hr3_sidecar](https://github.com/yahoojapan/k2hr3_sidecar) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_sidecar.git
    ```

3. install dependent packages to your local development environment.

    ```
    $ cd k2hr3_osnl/
    $ pip3 install pipenv
    $ python3 -m pipenv install -dev --python /path/to/python3
    $ pipenv shell
    ```
    

3. Install docker in the local environment using the following method.
- [Get Docker Engine - Community for Debian](https://docs.docker.com/install/linux/docker-ce/debian/)
- [Install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)
- [Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)

4. Create a branch for local development::
    ```
    (k2hr3_sidecar) $ git checkout -b my-first-contribution
    ```

5. Create a sidecar docker image and check it::

    ```
    (k2hr3_sidecar) $ sudo docker build --tag antpickax/k2hr3.sidecar:0.1 .
    (k2hr3_sidecar) $ sudo docker run -i -t antpickax/k2hr3.sidecar:0.1 /bin/sh
    ```

6. Commit your code changes and push your branch to GitHub when you change codes

    ```
    (k2hr3_sidecar) $ git add .
    (k2hr3_sidecar) $ git commit -m "Short description of your changes."
    (k2hr3_sidecar) $ git push origin my-first-contribution
    ```
    
7. Submit a pull request through the GitHub website when you change codes.

## The k2hr3_utils repository

This chapter instructs how to test codes in your local development environment.

This repository contains many utilities and tools for K2HR3. 

The following example shows the *devcluster* tool.

1. Fork the [https://github.com/yahoojapan/k2hr3_utils](https://github.com/yahoojapan/k2hr3_utils) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_utils.git
    ```
    
3. Create a branch for local development::

    ```
    $ cd k2hr3_utils/devcluster
    $ git checkout -b my-first-contribution
    ```

4. The following command start installing `K2HR3` subsystems with debug mode. When you change codes locally, make sure the installation finishes correctly.

    ```
    $ sh cluster.sh -d
    ```

5. Commit your code changes and push your branch to GitHub when you change codes::

    ```
    (k2hr3_osnl) $ git add .
    (k2hr3_osnl) $ git commit -m "Short description of your changes."
    (k2hr3_osnl) $ git push origin my-first-contribution
    ```
    
6. Submit a pull request through the GitHub website when you change codes.

## The k2hr3_get_resource repository

This chapter instructs how to build a `k2hr3_get_resource` package and test it in your local development environment.

The k2hr3_get_resource repository is a **Systemd service** for periodically retrieving RESOURCE data from a HOST registered in a ROLE members.
k2hr3_ge_resource repository is a repository for K2HR3 Get Resource.

1. Fork the [https://github.com/yahoojapan/k2hr3_get_resource](https://github.com/yahoojapan/k2hr3_get_resource) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_get_resource.git
    ```
    
3. Create a branch for local development

    ```
    $ cd k2hr3_get_resource
    $ git checkout -b my-first-contribution
    ```

4. Install the required packages in your local environment

    ```
    [Ubuntu/Debian]
    $ sudo apt-get install git autoconf autotools-dev make dh-make dh-systemd fakeroot dpkg-dev devscripts pkg-config ruby-dev rubygems rubygems-integration procps
    
    [CentOS/Fedora]
    $ sudo yum install autoconf automake gcc-c++ make pkgconfig redhat-rpm-config rpm-build procps
    ```

5. Build and create the package

    ```
    $ ./autogen.sh
    $ ./configure
    $ make
    $ make check
    
    [Ubuntu/Debian]
    $ ./buildutil/debian_build.sh
    
    [CentOS/Fedora]
    $ ./buildutil/rpm_build.sh
    ```

6. Commit your code changes and push your branch to GitHub when you change codes::

    ```
    $ git add .
    $ git commit -m "Short description of your changes."
    $ git push origin my-first-contribution
    ```

7. Submit a pull request through the GitHub website when you change codes.

## The k2hr3_cli repository

This chapter instructs how to build a `k2hr3_cli` package and test it in your local development environment.

The k2hr3_cli repository is a Command Line Interface(CLI) program that uses the K2HR3 REST API.  
Users can use this K2HR3 Command Line Interface(CLI) to perform the same operations as the K2HR3 Web Application from the command line.  

1. Fork the [https://github.com/yahoojapan/k2hr3_cli](https://github.com/yahoojapan/k2hr3_cli) repository in GitHub.

2. Clone your forked repository locally.

    ```
    $ git clone https://github.com/YOUR-USERNAME/k2hr3_cli.git
    ```
    
3. Create a branch for local development

    ```
    $ cd k2hr3_cli
    $ git checkout -b my-first-contribution
    ```

4. Install the required packages in your local environment

    ```
    [Ubuntu/Debian]
    $ sudo apt-get install git autoconf autotools-dev make dh-make fakeroot dpkg-dev devscripts pkg-config ruby-dev rubygems rubygems-integration procps shellcheck
    
    [CentOS/Fedora]
    $ sudo yum install git autoconf automake gcc-c++ make pkgconfig redhat-rpm-config rpm-build ruby-devel rubygems procps
    ```

5. Build and create the package

    ```
    $ ./autogen.sh
    $ ./configure
    $ make build
    $ make check
    
    [Ubuntu/Debian]
    $ ./buildutil/debian_build.sh
    
    [CentOS/Fedora]
    $ ./buildutil/rpm_build.sh
    ```

6. Commit your code changes and push your branch to GitHub when you change codes::

    ```
    $ git add .
    $ git commit -m "Short description of your changes."
    $ git push origin my-first-contribution
    ```

7. Submit a pull request through the GitHub website when you change codes.
