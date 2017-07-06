---
layout: page
title: Running a local FOLIO system
---

This document introduces the various ways to enable developers to run a complete FOLIO system to assist their local daily development.

## Introduction

There are various ways to run a complete FOLIO system. Each technique might be relevant at different times.

A complete system includes the Okapi gateway, the main back-end modules (especially the auth and user-related modules),
sample data for tenants and users and items, and the Stripes UI development server configured for various client-side modules.

## Deploy via local Okapi and Stripes

Follow the Guide to [start](https://github.com/folio-org/okapi/blob/master/doc/guide.md#running-okapi-itself)
Okapi in its clean state.

Develop a suite of 'curl' commands to create a test tenant and then deploy the main initial backend modules and your own additional modules.
Generate and load user sample data.
For guidance see Okapi's [doc/okapi-examples.sh](https://github.com/folio-org/okapi/blob/master/doc/okapi-examples.sh) script and Guide,
and [folio-ansible](https://github.com/folio-org/folio-ansible/doc/ansible-roles.md) roles and tasks,
and [folio-test-env](https://github.com/folio-org/folio-test-env) (a little out-of-date but still useful).

Follow the [Stripes: quick start](https://github.com/folio-org/stripes-core/blob/master/doc/quick-start.md) for the Stripes UI development server.
As explained there, the default will use released modules. It can be configured to use your local development versions.

## Ansible

Follow [folio-ansible](https://github.com/folio-org/folio-ansible) as a model for your own setup, and expand it to also deploy your modules and data.

## Prebuilt Vagrant boxes

See the [explanations](https://github.com/folio-org/folio-ansible/blob/master/doc/index.md) for each of the available boxes.

After starting a box, then issue the following command to show what versions of modules are available:
```curl -w '\n' http://localhost:9130/_/discovery/modules```

Consider some scenarios ...

A front-end developer with no need to tweak back-end modules:<br/>
Use the "folio/testing-backend" box and follow the [Stripes: quick start](https://github.com/folio-org/stripes-core/blob/master/doc/quick-start.md).

A front-end developer needing to also test their not-yet-released modifications to a back-end module:<br/>
[# FIXME]

A back-end developer needing to ensure that their not-yet-released modifications to a back-end module do solve a front-end issue:<br/>
[# FIXME]

A back-end developer needing to ensure that their not-yet-released modifications to a back-end module still operate with other released back-end modules:<br/>
[# FIXME]
