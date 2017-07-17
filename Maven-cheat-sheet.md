## Downloading sources

Download all sources of all dependencies:

    mvn dependency:sources

Download sources only of artifacts with id `abc`:

    mvn dependency:sources -DincludeArtifactIds=abc

Download sources only of artifacts with group id `abc`:

    mvn dependency:sources -DincludeGroupIds=abc
    
Note: in addition to saving the sources in the local repository,
the `dependency` plugin keeps its own cache in `target` of the project,
in directories named `dependency-maven-plugin-markers`.
An easy way to clear these markers is `mvn clean`.

To download the javadoc:

    mvn dependency:resolve -Dclassifier=javadoc

For more details see the [docs](https://maven.apache.org/plugins/maven-dependency-plugin/sources-mojo.html).

## Misc

Skip tests during the install step:

    mvn install -Dmaven.test.skip=true

Run unit test of specific class only:

    # can omit package name
    mvn test -Dtest=TheSimpleName

Force re-downloading artifacts:

    mvn compile -U

Deploy a JAR file to Nexus:

    mvn --settings=settings.xml deploy:deploy-file \
      -Durl=http://nexushost/nexus/content/repositories/REP_ID \
      -DrepositoryId=REP_ID \
      -Dversion=VERSION \
      -Dfile=/path/to/artifact.jar \
      -DartifactId=ARTIFACT_ID \
      -Dpackaging=jar \
      -DgroupId=GROUP_ID \
      -Dclassifier=BRANCH

Print list of dependencies:

    mvn dependency:list

Print tree of dependencies:

    mvn dependency:tree

Override local repository location (use a clean new local repo):

    mvn package -Dmaven.repo.local=/tmp/repo
