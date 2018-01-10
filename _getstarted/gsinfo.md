---
layout: getstarted
title: Basics
permalink: /getstarted/gsinfo/
---

# Basics

Get started with FOLIO development here.  Gain initial background and understanding.

- [Which forum](/community/which-forum) to use for communication:
  Issue tracker, Slack chat, Discuss discussion, GitHub pull requests.
  Some guidelines about when to use each, and some usage tips.
  The [concise list](/community/#collaboration-tools) of forums.
- [Guidelines for Contributing Code](/community/contrib-code) --
  GitHub Flow, feature branches, pull requests, version numbers, coding style,
  tests, etc.
- [FOLIO Project Contributor License Agreement](/community/cla-process).
- A [FOLIO glossary](glossary) of some terms and technologies used in FOLIO.
- [Guidelines for FOLIO issue tracker](/community/guide-issues).
- [Search dev.folio.org](/search) and [other search and report facilities](/search-other).

## Setup and Configuration

- Some tips to assist developers to configure their
  [local workstation setup](setup).
- [Built artifacts](artifacts) -- released and snapshot FOLIO artifacts in various formats.
Configurations for accessing.
- [Source code](/source-code/) -- explanation of each repository.

## Reference Documentation

- [Overiew](reference) of all technical reference documentation.
- <span id="api-reference"/> The set of automatically generated [API documentation](api).

## Development Tips

- Conduct [troubleshooting](troubleshooting).
- [Code analysis and linting facilities](code-analysis) explains ESLint, SonarQube, other lint tools, and preparing for pull requests.
- For Contextual Query Language (CQL) examples, see the [Glossary](glossary#cql), the FOLIO [CQL to PostgreSQL JSON converter](https://github.com/folio-org/cql2pgjson-java), the [API docs](api), and the debug output for tests in each backend module.

## Tutorials

- The [FOLIO Developer's Curriculum](/curriculum/) is a series
of lessons that can be followed on your own or can form the basis of an
instructor-led workshop.

## Development Management

- [Release procedures](release-procedures).
- [Search and report facilities](/search-other) (e.g. open pull requests needing review).
- [Create a new FOLIO module and do initial setup](create-new-repo).
- The [FOLIO Project Roadmap](https://wiki.folio.org/display/PC/FOLIO+Roadmap) including the development and milestone plan for Version 1 and the feature backlog,
and the [FOLIO Development Process Overview](https://wiki.folio.org/display/COMMUNITY/FOLIO+Development+Process+Overview), and other important documents and resources are listed at the [Wiki](https://wiki.folio.org).

# Primer Develop Front End

- [Community](https://www.folio.org/community/)
- [Which forum](/guidelines/communityguidelines/) to use for communication.
- [Special Interest Groups](https://wiki.folio.org/display/PC/Special+Interest+Groups) (SIGs).
- [Guidelines for Contributing Code](/guidelines/contrib-code/).

Start with introduction to [user interface](/devguides/introduction/)
and the [client-side](/source/components/) source code repositories.

That leads to the Stripes [Documentation Roadmap](https://github.com/folio-org/stripes-core/blob/master/README.md#documentation-roadmap) and overview of the main docs, and necessary background understanding.

Eventually go via the foundation described in
[The Stripes Module Developer's Guide](https://github.com/folio-org/stripes-core/blob/master/doc/dev-guide.md)
to
[Skeleton module](https://github.com/folio-org/stripes-core/blob/master/doc/dev-guide.md#skeleton-module).

The [Regression tests for FOLIO UI](https://github.com/folio-org/ui-testing) will assist.

# Primer Develop Back End

Start with introduction to [core code](/devguides/introduction/)
and the [server-side](/source/components/) source code repositories.

The [Okapi Guide and Reference](https://github.com/folio-org/okapi/blob/master/doc/guide.md) provides the necessary background understanding.

The [FOLIO-Sample-Modules guide](https://github.com/folio-org/folio-sample-modules/blob/master/README.md) further explains what is a server-side module and how to develop one. Importantly, these examples show that any programming-language is possible.

The [RAML Module Builder](https://github.com/folio-org/raml-module-builder) (RMB) framework, is a special module that abstracts much functionality and enables the developer to focus on implementing business functions. Define the APIs and objects in RAML files and schema files, then the RMB generates code and provides tools to help implement the module.
(Note that at this stage of the FOLIO project, only this Java-based framework is available.)

# Community

- [Community](/community/)
- [Which forum](/community/which-forum) to use for communication.
- [Special Interest Groups](https://wiki.folio.org/display/PC/Special+Interest+Groups) (SIGs).
- [Guidelines for Contributing Code](/community/contrib-code).

# Other topics

- [Best practices for Dockerfiles](best-practices-dockerfiles).
- The FOLIO [build, test, and deployment infrastructure](automation).
- A proposal for [error response formats](https://github.com/folio-org/okapi/blob/master/doc/error-formats-in-folio.md).
- [FOLIO UX](http://ux.folio.org/) -- user experience (UX) driven design and prototypes.
- [FOLIOForums](https://www.openlibraryenvironment.org/archives/category/olfforum) -- upcoming events and recordings of past ones.