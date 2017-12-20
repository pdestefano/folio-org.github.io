---
layout: guidelines
title: Coding Style
heading: Coding Style
permalink: /guidelines/codingconventions/
---

# Coding Conventions

## Style Guidelines and Configuration

Follow the coding style that is being used by each repository for each
file type. Some projects do provide a `.editorconfig` file.

For Java code, we basically try to adhere to Sun Java coding
[conventions](http://www.oracle.com/technetwork/java/codeconvtoc-136057.html)
(that document is old and unmaintained, but seems to be good enough as it is).

There are a few exceptions:

- We indent with two spaces only, because vert.x uses deeply nested callbacks.
- We _don't_ use tab characters for indents, only spaces.

For XML and JSON and RAML files, the same: two-space indent and no tabs.

Remember to set your IDE and editors to remove trailing spaces on saving files,
since those produce unnecessary diffs in Git.
Refer to coding style [configuration](/guidelines/codingconventions/) assistance.

For JSON key names we use camelCase.

For JavaScript code we are implementing an automated lint facility.

Some modules have linter and code-style tools implemented as part of their build process.
Some modules provide configuration files to assist code management tools.

## Use EditorConfig for Whitespace

Many FOLIO repositories have a `.editorconfig` configuration file at their top level. This enables consistent whitespace handling.

Refer to [EditorConfig.org](http://editorconfig.org) which explains that some text editors have native support, whereas others need a plugin.

Consult its documentation for each plugin. Note that some do not handle all EditorConfig properties.
In such cases refer to the documentation for the particular text editor, as it might have its own facilities.
For example, the Java text editor in Eclipse has its own configuration for `trim_trailing_whitespace`
(see [notes](http://stackoverflow.com/questions/14178839/is-there-a-way-to-automatically-remove-trailing-spaces-in-eclipse)).

### Use .gitignore

The `.gitignore` file in each repository can be minimal if each developer handles their own.
One way is to [configure](https://git-scm.com/docs/gitignore) a user-specific global file (i.e. add `core.excludesFile` to `~/.gitconfig`).

Then either use something like [gitignore.io](https://github.com/joeblau/gitignore.io),
or just use a simple set such as the following.
Add other specific ones for your particular operating system, text editors, and IDEs.

    ## general
    *.log

    ## macos
    *.DS_Store

    ## maven
    target/

    ## gradle
    .gradle/
    build/

    ## node
    node_modules/
    npm-debug.log

    ## vim
    *~
    .*.sw?

    ## folio
    **/src/main/java/org/folio/rest/jaxrs/
    .vertx/
	
### Update git submodules

Some FOLIO repositories utilize "git submodules" for sections of common code.

For example, each `mod-*` module and `raml-module-builder` include the "raml" repository as a git submodule as its `raml-util` directory.

Note that when originally cloning a repository, use 'git clone --recursive ...'
Some git clients do not. If you then have an empty "raml-util" directory, then do 'git submodule update --init'.

Thereafter updating that submodule is deliberately not automated, so that we can ensure a stable build when we git checkout in the future.

So when an update is needed to be committed, do this:

    cd mod-configuration (for example)
    git submodule foreach 'git checkout master && git pull origin master'
    git commit ...

Now when people update their local checkout, then some git clients do not automatically update the submodules. If that is the case, then follow with 'git submodule update'.

This part can be automated with client-side git hooks. Create the following two shell scripts:

    mod-configuration/.git/hooks/post-checkout
    mod-configuration/.git/hooks/post-merge

using this content:

    #!/bin/sh
    git submodule update

and make them executable: 'chmod +x post-checkout post-merge'

Now subsequent updates will also update the submodules to their declared revision.

## License

Licensed under the Apache License, Version 2.0

## Testing

We aim to write a lot of tests -- each module should have at least some kind of
test associated with it. These can be traditional unit tests, black-box tests
that talk through the WS API, and/or proper integration tests.

When hunting down problems, it is considered good form to write a test that
demonstrates the problem first, then a fix that makes the test pass.

We have a Jenkins test system that gets invoked when you push something
to master, and/or make a pull request. It should flag any errors, but be
nice and run a ```mvn install``` on your own machine before every
```git commit```

## Best Practices for Docker Files

Since FOLIO modules can consist of range of application and programming environments,
running modules as Linux containers provides a nice way to avoid issues related to
the complexities of installing and managing a system with mixed environments.  Docker
is a popular container framework and has been adopted as a primary distribution
model for FOLIO modules.  Dockerfiles describe how to build and run an application in
a Docker container.

The following outlines some general best practices for adding Dockerfiles to
a FOLIO module project.   This is by no means a comprehensive list, and, as with
all best practices, there will always be exceptions as well as a bit of controversy
(indeed, it may be less controversial to re-title this document "FOLIO Dockerfile
tips").  This [best practice guide](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
from Docker also provides a good overview.

* All FOLIO modules should include one or more Dockerfiles called 'Dockerfile' that
will build and run a Docker container suitable for a runtime environment.  As a general
rule, images should be as lean and concise as possible and should not contain things
like SDKs, build dependencies, and development tools.  It is often desirable to include
a separate Dockerfile that will bootstrap a module from source to get something up and
running quickly for prototyping and development. This type of Dockerfile should be named
'Dockerfile.build' to differentiate it from the runtime Dockerfile.

* Most FOLIO Docker images will be derived from a pre-existing base image.  If possible,
use an existing base image from an "official repository" located on Docker Hub.
Examples include the following:

  - [OpenJDK for Java-based modules](https://hub.docker.com/_/openjdk)
  - [Node.js-based modules](https://hub.docker.com/_/node)
  - [Python-based modules](https://hub.docker.com/_/python)

  If it is necessary to start with an OS base image, the following are good choices:

  - [Debian OS base image](https://hub.docker.com/_/debian)
  - [Alpine OS base image](https://hub.docker.com/_/alpine)

  Alpine is ideal because of its small footprint. However, it may not be compatible
with all projects.  Test your Docker image to ensure your module functions correctly.

* Utilize the "one process per container" rule whenever possible and run the
process as PID 1 to ensure that the process responds properly to a SIGTERM sent by
'docker stop'.  Using the exec form of the CMD or ENTRYPOINT instruction will
typically accomplish this.

  ```
  CMD ["executable", "param1", "param2"]
  ENTRYPOINT ["executable", "param1", "param2"]

  ```

  This can become more complex depending on whether the process started in the container
is actually coded to exit gracefully when receiving a SIGTERM. If a different signal
should be used to gracefully stop a container process, i.e. SIGQUIT or something else,
it should be noted somewhere in the module documentation.

* If it is necessary to run more than one process in your container,  use 'supervisord'
to manage your processes. Supervisor should be run as PID 1 in this case.
See [Using Supervisor](https://docs.docker.com/engine/admin/using_supervisord/) for
additional information.

* It is often necessary to pass optional arguments to a module running inside a
container.  For example,  the FOLIO  mod-circulation module can take an optional
argument to run an embedded MongoDB data store (generally NOT a good idea for a production
module!).

  ```
  docker run -d mod-circulation embed_mongo=true

  ```

  One way to accomplish this is to exec the module using ENTRYPOINT
and include CMD with an empty array. For example:

  ```
  ENTRYPOINT ["java", "-jar", "circulation-fat.jar"]
  CMD []

  ```

* With Java-based modules, it is often necessary to pass options to Java
  (as opposed to the application) at runtime.   The exec forms of ENTRYPOINT
  and CMD in the previous example, however, do not support variable substitution.
  A method to accomplish this is to use the shell form of ENTRYPOINT instead.

  ```
  ENTRYPOINT exec java $JAVA_OPTS circulation-fat.jar

  ```

  Now run the container by passing in JAVA_OPTS as an environment
  variable:

  ```
  docker run -d -e JAVA_OPTS='-Xmx1g -Xms1g' mod-circulation

  ```

  Unfortunately, mixing the shell form of ENTRYPOINT with the exec form of CMD
  is not possible, so combining support for application options as outlined
  in the previous example with support for Java options becomes much more
  difficult.  At this point, it's probably time to start thinking about a proper
  ENTRYPOINT script.

* Limit the number of RUN steps in your Dockerfile by chaining together commands with
  '&&' when possible.

* Run the container process as a non-root user by utilizing 'USER' in your Dockerfile.
Note, it is necessary to ensure that the user exists or is created in the container image
in order for USER to work.

  ```
  # Create user/group 'folio'
  RUN groupadd folio && \
      useradd -r -d $VERTICLE_HOME -g folio -M folio && \
      chown -R folio.folio $VERTICLE_HOME

  # Run as this user
  USER folio

  ```

* The module running inside the container should log to STDOUT by default - not to a log
file inside the container.  By logging to STDOUT,  the developer can easily look at
module logs when debugging and the Docker administrator can choose to redirect the logs
elsewhere according to their own site preferences.

## RAML

Remember to update these if you ever change anything in the API.
And update the documentation too, of course.

For Okapi, we keep the API specs in RAML files under `okapi-core/src/main/raml/`.

For [server-side modules](/source/components/),
the [raml](https://github.com/folio-org/raml)
repository is the master location for the traits and resource
types, while each module is the master for its own schemas, examples,
and actual RAML files.

