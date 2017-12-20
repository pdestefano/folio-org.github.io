---
layout: getstarted
title: Basics
permalink: /getstarted/gsinfo/
---

# Basics

Get started with FOLIO development here.  Gain initial background and understanding.

- [Which forum](/guidelines/communityguidelines/) to use for communication:
  Issue tracker, Slack chat, Discuss discussion, GitHub pull requests.
  Some guidelines about when to use each, some usage tips, and links to each.
- [Guidelines for Contributing Code](/guidelines/contrib-code/) --
  GitHub Flow, feature branches, pull requests, version numbers, coding style,
  tests, etc.
- A [FOLIO glossary](/reference/refinfo/) of some terms and technologies used in FOLIO.
- [Guidelines for FOLIO issue tracker](/guidelines/communityguidelines/#issue-tracker).

## Setup and Configuration

- Some tips to assist developers to configure their
  [local workstation setup](/devtools/setupdevenv/).
- [Built artifacts](/download/download-built-artifacts/) -- released and snapshot FOLIO artifacts in various formats.
Configurations for accessing.
- [Source code](/source/components/) -- explanation of each repository.

## Reference Documentation

- [Overiew](/reference/refinfo/) of all technical reference documentation.
- <span id="api-reference"/> The set of automatically generated [API documentation](/reference/refinfo/).

## Development Tips

- Conduct [troubleshooting](/devtools/setupdevenv/#troubleshooting).

## Lessons

- The [FOLIO Developer's Curriculum](/tutorials/foliodeveloperscurr/) is a series
of lessons that can be followed on your own or can form the basis of an
instructor-led workshop.

## Development Management

- [Release procedures](/devguides/release-procedures).
- [Create a new FOLIO module and do initial setup](/source/components/).
- The [FOLIO project roadmap](https://wiki.folio.org/display/PC/FOLIO+Roadmap).

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
