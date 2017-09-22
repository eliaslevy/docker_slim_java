Oracle Java Base Docker Image
=============================

This is a slim Oracle Java base image.  It is meant for executing containerized services.
It is based on Alpine Linux with Glibc support, uses the the JRE, and a number of components 
and code removed to make a minimal image.

Removed:
- Accessibility
- Applets
- Brower Plugin
- Control Panel
- CORBA
- Desktop related code
- Fonts
- GUI Toolkits
  - AWT
  - JavaFX
  - Swing
- Java 2D
- Javascript engine (Nashorn)
- JNDI extension for DNS look-up
- Locale
- Printing
- Remote Method Invocation deamon, object registry, and tooling
- Sound
- Web Start /  Java Network Launch Protocol
- Uneeded command line tools


