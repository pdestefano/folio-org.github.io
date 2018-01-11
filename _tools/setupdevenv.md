---
layout: tools
title: Setting Up the Developer Environment
heading: Developer Tools
permalink: /tools/setupdevenv/
---


# Setting Up the Dev Environment

A collection of tips to assist developers to configure their local workstation setup environment for FOLIO development.

<!-- ../../okapi/doc/md2toc -l 2 -h 3 setup.md -->

Assume already doing other development, so know how to keep the operating system up-to-date, know its quirks, know how to use the various package managers. So this document will not go into detail about that.

FOLIO modules can be developed in any suitable programming language.

The [FOLIO-Sample-Modules](https://github.com/folio-org/folio-sample-modules) explains about module development.
The various [Stripes](/devguides/introduction/) documentation explains user-interface development.
Those also have more notes about setting up and managing the local development environment.

## Local Instances and Tooling

<!-- ../../okapi/doc/md2toc -l 2 -h 3 setup.md -->

Developers will probably want to explore the whole FOLIO system, so would need a local instance of Okapi and
[server-side](/source/components/) modules,
and the [client-side](/source/components/) Stripes toolkit.

Note that some parts of the development environment could be handled using
[folio-ansible](https://github.com/folio-org/folio-ansible) (virtual machines using Vagrant and Ansible).

Otherwise the development environment would need the following fundamental tools:

* Apache Maven (3.3+) and Java (8+) -- For building and deploying Okapi and some server-side modules.
* Node.js (6+) -- For Stripes and for some modules.
* Docker -- Recommended method for deployment.

As each FOLIO component can utilise whatever suite of appropriate tools, refer to its requirements and notes to assist with setup.

## Minimum Versions

Occasionally it becomes necessary to specify minimum versions of some tools:

* Java: [1.8.0-101](/devtools/setupdevenv/#missing-certificate---lets-encrypt)

## Other Tools

* PostgreSQL -- For running an external database to support storage modules.
This will enable faster startup and operations during development.
Note that this is not required to be installed for running modules using the "embed_postgres" option.

## Configuration

FOLIO utilizes the Nexus OSS Repository Manager to host Maven artifacts and NPM packages for FOLIO projects.
Docker images are the primary distribution model for FOLIO modules.

See [Built artifacts](/download/download-built-artifacts/) for configuration details for accessing the released and snapshot FOLIO artifacts.

For developers needing to publish artifacts, an overview and usage configuration details are provided, see
[Build, test, and deployment infrastructure](/devguides/system/).

# Troubleshooting

A collection of general tips to assist developers to conduct troubleshooting.
Some FOLIO repositories also have specific notes.

## Keep system tools up-to-date

As [explained](/devtools/setupdevenv/) in the FOLIO setup documentation,
keeping the operating system and tools up-to-date will generally help to
avoid issues.

## Update git submodules

Some FOLIO repositories utilize “git submodules” for sections of common code.
Some git clients do not handle this properly.
See [notes](/devtools/setupdevenv/).

## Run as a regular user

As usual, do all development and running as a regular user, not as root.
Otherwise there will be strange behaviour, and various facilities and
tools might not be available.
For example, Postgres (including the embedded one) refuses to run as root.

## Launching Vagrant on Windows

If launching Vagrant from a Windows Command Prompt, be sure to use _Run As Administrator..._
when opening the Command Prompt itself (cmd.exe).
If you are seeing the error _"EPROTO: protocol error, symlink"_, the likely cause is that
Vagrant was not launched with administrator privileges.
See issue [STRIPES-344](https://issues.folio.org/browse/STRIPES-344) for details.

## Missing certificate - Let's Encrypt

If you are using a version of the Oracle JDK prior to `1.8.0_101`
then the [Let's Encrypt](https://letsencrypt.org/)
certificate authority is not in the Java trust store
([see notes](https://stackoverflow.com/questions/34110426/does-java-support-lets-encrypt-certificate)).
So it will not be possible to download components from the FOLIO Maven
repository. You will see error messages like:

> Could not resolve dependencies for project org.folio:mod-users:jar:0.1-SNAPSHOT: Failed to collect dependencies at org.folio:domain-models-api-interfaces:jar:0.0.1-SNAPSHOT: Failed to read artifact descriptor for org.folio:domain-models-api-interfaces:jar:0.0.1-SNAPSHOT: Could not transfer artifact org.folio:domain-models-api-interfaces:pom:0.0.1-SNAPSHOT from/to folio-nexus (https://repository.folio.org/repository/maven-folio): sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target -> [Help 1]

The fix is just to replace your JDK with a sufficiently recent replacement.
(Or you can use OpenJDK, which has supported Let's Encrypt for longer.)

## Other troubleshooting documents

* [Stripes troubleshooting](https://github.com/folio-org/stripes-core/blob/master/doc/troubleshooting.md)
* [Vagrant boxes troubleshooting](https://github.com/folio-org/folio-ansible/blob/master/doc/index.md#troubleshootingknown-issues)
* Investigate SonarQube [analysis](https://sonarcloud.io/organizations/folio-org/projects)
