
Основной инструмент для реализации OHIFGateway.

Применяем как lib в OHIFGateway-service, которая затем применяется в  OHIFGateway

dcm4che v.X.Y.Z  ->  mvn install  ->  dcm4che-X.Y.Z-bin.zip -> copy to OHIFGateway-service\lib -> libOHIF-X.Y.Z.bin -> copy to OHIFGateway\lib

!!!!!!!!!!!!!!!!!!!

notes to release

!!!!!!!!!!!!!!!!!!!

во время mvn install ругалки

[INFO] Scanning for projects...

[WARNING] Some problems were encountered while building the effective model for org.dcm4che:dcm4che-core:bundle:5.10.6
[WARNING] 'build.plugins.plugin.version' for org.codehaus.mojo:build-helper-maven-plugin is missing.
@ org.dcm4che:dcm4che-core:[unknown-version], D:\dop\java\OHIFGateway-base\dcm4che-core\pom.xml, line 179, column 15

[WARNING] 'build.plugins.plugin.version' for org.codehaus.mojo:xml-maven-plugin is missing.
@ org.dcm4che:dcm4che-core:[unknown-version], D:\dop\java\OHIFGateway-base\dcm4che-core\pom.xml, line 99, column 15

[WARNING] Some problems were encountered while building the effective model for org.dcm4che:dcm4che-dict-arc:bundle:5.10.6
[WARNING] 'build.plugins.plugin.version' for org.codehaus.mojo:build-helper-maven-plugin is missing.
@ org.dcm4che:dcm4che-dict-arc:[unknown-version], D:\dop\java\OHIFGateway-base\dcm4che-dict-arc\pom.xml, line 136, column 15

[WARNING] 'build.plugins.plugin.version' for org.codehaus.mojo:xml-maven-plugin is missing.
@ org.dcm4che:dcm4che-dict-arc:[unknown-version], D:\dop\java\OHIFGateway-base\dcm4che-dict-arc\pom.xml, line 82, column 15

[WARNING] Some problems were encountered while building the effective model for org.dcm4che:dcm4che-imageio:bundle:5.10.6
[WARNING] 'build.plugins.plugin.version' for org.apache.maven.plugins:maven-surefire-plugin is missing.
@ org.dcm4che:dcm4che-imageio:[unknown-version], D:\dop\java\OHIFGateway-base\dcm4che-imageio\pom.xml, line 46, column 14

[WARNING] Some problems were encountered while building the effective model for org.dcm4che:dcm4che-assembly:pom:5.10.6
[WARNING] 'build.plugins.plugin.version' for org.codehaus.mojo:xml-maven-plugin is missing.
@ org.dcm4che:dcm4che-assembly:[unknown-version], D:\dop\java\OHIFGateway-base\dcm4che-assembly\pom.xml, line 74, column 15

[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.

[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.


добавили версии

        <groupId>org.codehaus.mojo</groupId>
        <artifactId>build-helper-maven-plugin</artifactId>
        <version>3.0.0</version>

        <groupId>org.codehaus.mojo</groupId>
        <artifactId>xml-maven-plugin</artifactId>
        <version>1.0.1</version>

        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.20.1</version>



добвавить конструктор

org.dcm4che3.net.Device

    //[injections of mikivan][0001]
    private transient ExecutorService executorService;
    //[end][0001]

    //[injections of mikivan][0002]
    public final ExecutorService getExecutor2() {
        return  executorService;
    }

    public final void setExecutor2(ExecutorService executorService) {

        this.executorService = executorService;
        this.executor = executorService;
    }
    //[end][0002]





dcm4che-3.x DICOM Toolkit
=========================
Sources: https://github.com/dcm4che/dcm4che  
Binaries: https://sourceforge.net/projects/dcm4che/files/dcm4che3  
Issue Tracker: http://www.dcm4che.org/jira/browse/LIB  
Build Status: [![Build Status](https://travis-ci.org/dcm4che/dcm4che.svg?branch=master)](https://travis-ci.org/dcm4che/dcm4che)

This is a complete rewrite of [dcm4che-2.x](http://www.dcm4che.org/confluence/display/d2/).

One main focus was to minimize the memory footprint of the DICOM data sets.
It already provides modules to store/fetch configuration data to/from LDAP,
compliant to the DICOM Application Configuration Management Profile,
specified in [DICOM 2011, Part 15][1], Annex H.

[1]: ftp://medical.nema.org/medical/dicom/2011/11_15pu.pdf

Build
-----
After installation of [Maven 3](http://maven.apache.org):

    > mvn install

Modules
-------
- dcm4che-audit
- dcm4che-conf
  - dcm4che-conf-api
  - dcm4che-conf-api-hl7
  - dcm4che-conf-ldap
  - dcm4che-conf-ldap-audit
  - dcm4che-conf-ldap-hl7
  - dcm4che-conf-ldap-imageio
  - dcm4che-conf-prefs
  - dcm4che-conf-prefs-audit
  - dcm4che-conf-prefs-hl7
  - dcm4che-conf-prefs-imageio
- dcm4che-core
- dcm4che-emf
- dcm4che-hl7
- dcm4che-image
- dcm4che-imageio
- dcm4che-imageio-rle
- dcm4che-net
- dcm4che-net-audit
- dcm4che-net-hl7
- dcm4che-net-imageio
- dcm4che-soundex
- dcm4che-jboss-modules
- dcm4che-servlet

Utilities
---------
- [dcm2dcm][]: Transcode DICOM file according the specified Transfer Syntax
- [dcm2jpg][]: Convert DICOM image to JPEG or other image formats
- [dcm2xml][]: Convert DICOM file in XML presentation
- [dcmdir][]: Dump, create or update DICOMDIR file
- [dcmdump][]: Dump DICOM file in textual form
- [dcmqrscp][]: Simple DICOM archive
- [dcmvalidate][]: Validate DICOM object according a specified Information Object Definition
- [emf2sf][]: Convert DICOM Enhanced Multi-frame image to legacy DICOM Single-frame images
- [findscu][]: Invoke DICOM C-FIND Query Request
- [getscu][]: Invoke DICOM C-GET Retrieve Request
- [hl72xml][]: Convert HL7 v2.x message in XML presentation
- [hl7pix][]: Query HL7 v2.x PIX Manager
- [hl7rcv][]: HL7 v2.x Receiver
- [hl7snd][]: Send HL7 v2.x message
- [ianscp][]: DICOM Instance Availability Notification receiver 
- [ianscu][]: Send DICOM Instance Availability Notification
- [mkkos][]: Make DICOM Key Object Selection Document
- [modality][]: Simulates DICOM Modality
- [movescu][]: Invoke DICOM C-MOVE Retrieve request
- [mppsscp][]: DICOM Modality Performed Procedure Step Receiver
- [mppsscu][]: Send DICOM Modality Performed Procedure Step
- [stgcmtscu][]: Invoke DICOM Storage Commitment Request
- [storescp][]: DICOM Composite Object Receiver
- [storescu][]: Send DICOM Composite Objects
- [xml2dcm][]: Create/Update DICOM file from/with XML presentation
- [xml2hl7][]: Create HL7 v2.x message from XML presentation
- [xml2prefs][]: Import Java Preferences

[dcm2dcm]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcm2dcm/README.md
[dcm2jpg]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcm2jpg/README.md
[dcm2xml]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcm2xml/README.md
[dcmdir]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcmdir/README.md
[dcmdump]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcmdump/README.md
[dcmqrscp]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcmqrscp/README.md
[dcmvalidate]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-dcmvalidate/README.md
[emf2sf]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-emf2sf/README.md
[findscu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-findscu/README.md
[getscu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-getscu/README.md
[hl72xml]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-hl72xml/README.md
[hl7pix]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-hl7pix/README.md
[hl7rcv]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-hl7rcv/README.md
[hl7snd]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-hl7snd/README.md
[ianscp]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-ianscp/README.md
[ianscu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-ianscu/README.md
[mkkos]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-mkkos/README.md
[modality]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-ihe/dcm4che-tool-ihe-modality/README.md
[movescu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-movescu/README.md
[mppsscp]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-mppsscp/README.md
[mppsscu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-mppsscu/README.md
[stgcmtscu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-stgcmtscu/README.md
[storescp]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-storescp/README.md
[storescu]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-storescu/README.md
[xml2dcm]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-xml2dcm/README.md
[xml2hl7]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-xml2hl7/README.md
[xml2prefs]: https://github.com/dcm4che/dcm4che/blob/master/dcm4che-tool/dcm4che-tool-xml2prefs/README.md

License
-------
* [Mozilla Public License Version 1.1](http://www.mozilla.org/MPL/1.1/)

