# Build

mvn -Dsettings.security=./settings-security.xml -s settings.xml -B clean deploy


# Release
mvn -Dsettings.security=./settings-security.xml -s settings.xml -B \
    -Dtag=v1.0.0 \
    -DreleaseVersion=1.0.0 \
    -DdevelopmentVersion=1.0.1 \
    -Darguments="-Dsettings.security=./settings-security.xml -s settings.xml"
    release:prepare \
    release:perform 


