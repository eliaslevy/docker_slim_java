FROM frolvlad/alpine-glibc:alpine-3.6

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=144 \
    JAVA_BUILD=01 \
    JAVA_PATH=090f390dda5b47b9b721c7dfaa008135 \
    JAVA_HOME=/usr/lib/jvm/default-jvm

RUN apk add --no-cache --virtual=build-dependencies \
      ca-certificates \
      unzip           \
      wget            \
      zip &&          \
    #
    # Install the JRE
    wget -nv -P /tmp --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
      "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/${JAVA_PATH}/jre-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    mkdir -p "/usr/lib/jvm/java-${JAVA_VERSION}-oracle" && \
    tar -C "/usr/lib/jvm/java-${JAVA_VERSION}-oracle" --strip-components=1 -xzf "/tmp/jre-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    ln -s "java-${JAVA_VERSION}-oracle" "$JAVA_HOME" && \
    ln -s "$JAVA_HOME/bin/"* /usr/bin/ && \
    #
    # Download Unlimited Strength Java Cryptography Extension policy
    wget -nv -P /tmp --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jce/${JAVA_VERSION}/jce_policy-${JAVA_VERSION}.zip" && \
    unzip -jo -d "${JAVA_HOME}/lib/security" "/tmp/jce_policy-${JAVA_VERSION}.zip" && \
    #
    # Slimdown the JRE
    cd "$JAVA_HOME" && \
    rm -rf \
      # Text files
      COPYRIGHT                                   \
      LICENSE                                     \
      README                                      \
      THIRDPARTYLICENSEREADME*                    \
      Welcome.html                                \
      lib/jvm.hprof.txt                           \
      lib/management/jmxremote.password.template  \
      lib/management/snmp.acl.template            \
      lib/security/README.txt                     \
      man                                         \
      # Uneeded commands
      bin/keytool                                 \
      bin/policytool                              \
      # Remote Method Invocation deamon, object registry, and tooling
      bin/rmid                                    \
      bin/rmiregistry                             \
      bin/servertool                              \
      # Control panel tool
      bin/ControlPanel                            \
      bin/jcontrol                                \
      # CORBA
      bin/orbd                                    \
      bin/tnameserv                               \
      # Web Start /  Java Network Launch Protocol
      bin/javaws                                  \
      bin/pack200                                 \
      bin/unpack200                               \
      lib/deploy*                                 \
      lib/javaws.jar                              \
      lib/amd64/libdeploy.so                      \
      lib/security/javaws.policy                  \
      # Javascript engine (Nashorn)
      bin/jjs                                     \
      lib/ext/nashorn.jar                         \
      # Component to enable direct execution of jars by Linux
      lib/jexec                                   \
      # Fonts
      lib/amd64/libfontmanager.so                 \
      lib/fonts                                   \
      lib/fontconfig*                             \
      lib/oblique-fonts                           \
      # PostScript printer properties
      lib/psfont*                                 \
      # Locale support
      lib/calendars.properties                    \
      lib/charsets.jar                            \
      lib/ext/localedata.jar                      \
      lib/hijrah-config-umalqura.properties       \
      lib/locale                                  \
      # Desktop related files
      lib/amd64/libjsound.so                      \
      lib/amd64/libjsoundalsa.so                  \
      lib/amd64/libsplashscreen.so                \
      lib/desktop                                 \
      lib/flavormap.properties                    \
      lib/images                                  \
      lib/sound.properties                        \
      # Brower Plugin
      plugin                                      \
      lib/applet                                  \
      lib/plugin.jar                              \
      lib/amd64/libnpjp2.so                       \
      # Accessibility support
      lib/ext/jaccess.jar                         \
      # Color Profiles
      lib/cmm                                     \
      # AWT GUI API
      lib/amd64/libawt.so                         \
      lib/amd64/libawt_headless.so                \
      lib/amd64/libawt_xawt.so                    \
      lib/amd64/libjawt.so                        \
      # JavaFX GUI API
      lib/amd64/libavplugin-*                     \
      lib/amd64/libdecora_sse.so                  \
      lib/amd64/libfxplugins.so                   \
      lib/amd64/libglass.so                       \
      lib/amd64/libgstreamer-lite.so              \
      lib/amd64/libjavafx*.so                     \
      lib/amd64/libjfx*.so                        \
      lib/amd64/libprism_*.so                     \
      lib/ext/jfxrt.jar                           \
      lib/javafx.properties                       \
      lib/jfxswt.jar                              \
      # Java Naming and Directory Interface (JNDI) implementation for Domain Name Service look-up
      lib/ext/dnsns.jar &&                        \
    #
    cp /dev/null lib/management/management.properties && \
    #
    zip -q -d lib/rt.jar \
      # Abstract Window Toolkit (AWT)
      com/sun/awt/\*                              \
      java/awt/\*                                 \
      sun/awt/\*                                  \
      # Swing
      com/sun/java/swing/\*                       \
      com/sun/swing/\*                            \
      javax/swing/\*                              \
      sun/swing/\*                                \
      # Applets
      com/sun/java/browser/\*                     \
      java/applet/\*                              \
      org/w3c/dom/\*                              \
      sun/applet/\*                               \
      # Java 2D
      sun/java2d/\*                               \
      # Sound
      com/sun/media/sound/\*                      \
      javax/sound/\*                              \
      sun/audio/\*                                \
      # Corba
      com/sun/corba/\*                            \
      com/sun/org/omg/\*                          \
      # needed for JMX
      #javax/rmi/CORBA/\*                          \
      #org/omg/\*                                  \
      sun/corba/\*                                \
      # Accessibility
      javax/accessibility/\*                      \
      com/sun/accessibility/\*                    \
      # Java Print Service
      javax/print/\*                              \
      sun/print/\* &&                             \
    #
    zip -q -d lib/resources.jar \
      # Corba
      com/sun/corba/\*                            \
      # Swing
      com/sun/java/swing/\*                       \
      javax/swing/\*                              \
      # Localization
      \*_de.properties                            \
      \*_es.properties                            \
      \*_fr.properties                            \
      \*_it.properties                            \
      \*_ja.properties                            \
      \*_ko.properties                            \
      \*_pt_\*.properties                         \
      \*_sv.properties                            \
      \*_zh_\*.properties                         \
      # Print
      META-INF/services/javax.print.\*            \
      sun/print/\*                                \
      # Sound
      META-INF/services/javax.sound.\*            \
      # Java 2d
      META-INF/services/sun.java2d.\* &&          \
    #
    # Clean up.
    apk del build-dependencies && \
    rm /tmp/*
