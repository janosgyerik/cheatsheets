* Skip tests during the install step

        mvn install -Dmaven.test.skip=true

* Run unit test of specific class only:

        # can omit package name
        mvn test -Dtest=TheSimpleName

* Force re-downloading artifacts from Nexus

        mvn compile -U

* Deploy a JAR file to Nexus

        mvn --settings=settings.xml deploy:deploy-file \
          -Durl=http://nexushost/nexus/content/repositories/REP_ID \
          -DrepositoryId=REP_ID \
          -Dversion=VERSION \
          -Dfile=/path/to/artifact.jar \
          -DartifactId=ARTIFACT_ID \
          -Dpackaging=jar \
          -DgroupId=GROUP_ID \
          -Dclassifier=BRANCH

* Print list of dependencies:

        mvn dependency:list

* Print tree of dependencies:

        mvn dependency:tree
