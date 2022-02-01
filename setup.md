---
layout: contents
language: en
title: Setup
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setupja.html
lang_opp_word: To Japanese
prev_url: usage.html
prev_string: Usage
top_url: index.html
top_string: TOP
next_url: developer.html
next_string: Developer
---

# Quick Start

This page provides information about quickly bringing up a complete K2HR3 system in a Linux host.  

## K2HR3 system

The following configuration example is a K2HR3 system that works with [OpenStack](https://www.openstack.org/).
The trial environment with the minimum configuration and the construction to the [kubernetes](https://kubernetes.io/) environment have almost the same configuration.

![K2HR3 Setup overview](images/setup_overview.png)

## Setup procedure

The K2HR3 system can be built on the IaaS(bare metal, [OpenStack](https://www.openstack.org/), [kubernetes](https://kubernetes.io/)).
The setup procedure according to the trial environment and IaaS environment is shown below.

- [Build a Trial Environment](setup_trial.html) (on the OpenStack)  
You can easily build and try a minimal K2HR3 system on [OpenStack](https://www.openstack.org/)(including OpenStack built with [devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack)).
- [Installation step by step](setup_manualja.html)  
The K2HR3 system consists of some subsystems.  
You can setup each subsystem step by step.  
- [Integrated installation](setup_integrate.html)  
You can setup a K2HR3 system that contains all the K2HR3 subsystems at once.
