# Build

mvn -Dsettings.security=./settings-security.xml -s settings.xml -B clean deploy


# Release
mvn  -B \
    -Dtag=v1.0.0 \
    -DreleaseVersion=1.0.0 \
    -DdevelopmentVersion=1.0.1 \
    release:prepare \
    release:perform 


