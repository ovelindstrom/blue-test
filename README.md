# Build

mvn -Dsettings.security=./settings-security.xml -s settings.xml -B clean deploy


# Release
mvn -Dsettings.security=./settings-security.xml -s settings.xml -B \
    -Dtag=v1.0.0 \
    -DreleaseVersion=1.0.0 \
    -DdevelopmentVersion=1.0.1 \
    -DmavenHome=/c/tools/apache/maven-3.5.0 \
    release:prepare \
    release:perform 


