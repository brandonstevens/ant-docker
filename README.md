ant
============

# What is Ant?

[Apache Ant](http://ant.apache.org/) is a Java library and command-line tool whose mission is to drive processes described in build files as targets and extension points dependent upon each other. The main known usage of Ant is the build of Java applications. Ant supplies a number of built-in tasks allowing to compile, assemble, test and run Java applications. Ant can also be used effectively to build non Java applications, for instance C or C++ applications. More generally, Ant can be used to pilot any type of process which can be described in terms of targets and tasks.


# How to use this image


## Run a single Ant command

For many simple projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a Ant project by using the Ant Docker image directly, passing a Ant command to `docker run`:

    docker run -it --rm -v "$(pwd)":/src brandonstevens/ant

### Set ANT Environment Variables

Ant includes two environment variables that can be set when you run the container.

* ANT_OPTS - command-line arguments that should be passed to the JVM. For example, you can define system properties or set the maximum Java heap size here.
* ANT_ARGS - Ant command-line arguments. For example, set ANT_ARGS to point to a different logger, include a listener, and to include the -find flag.

(Taken from https://ant.apache.org/manual/running.html)

    docker run -it --rm -v "$(pwd)":/src -e "ANT_OPTS=-Xmx256m" -e "ANT_ARGS=-buildfile build-all.xml" brandonstevens/ant

## Create a Dockerfile for your Ant project

Create a Dockerfile at the root of your project:

    FROM brandonstevens/ant

    ADD . /src

    WORKDIR /src

    RUN ant

    WORKDIR /src/build

    CMD ["java", "-jar", "project.jar"]
