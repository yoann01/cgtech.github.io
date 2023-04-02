# OCIO

## OpenColorIO

OpenColorIO (OCIO) was initially developed (since 2003), open-sourced by Sony Pictures Imageworks and ❝ is an Academy Scientific and Technical Award winning color management solution for creating and displaying consistent images across multiple content creation applications during visual effects and animation production ❞ - It became the primary color management framework solution many software vendor started to support.


The Academy Software Foundation (ASWF) was founded in 2018 to help foster and shepherd the development of open source software projects in the visual effects industry [ASWF 2018]. OpenColorIO was the second project accepted into the foundation [Olin 2019] (source). OCIO is open-source, free and is licensed under the BSD-3-Clause license. The Technical Steering Committee (“TSC”) is responsible for all technical oversight of the open source project. Last but not least, there are significant contributions that have also been made by Industrial Light & Magic, DNEG, and many individuals (contributors list). Version 2.0 is the second major version of OCIO, led by full-time Autodesk software engineers. 

!!! note
    Open Color IO (OCIO) is a color management framework:
    “OCIO enables color transforms and image display to be handled in a consistent manner across multiple graphics applications.     Unlike other color management solutions, OCIO is geared towards motion-picture post production, with an emphasis on visual     effects and animation color pipelines. OpenColorIO has been used since 2003 to address the challenges of working with multiple     commercial image-processing applications that have different approaches to color management” - Sony Imageworks


## OCIO Configuration Files
The configuration file “controls” OCIO (its file package), is usually named config.ocio and is a YAML document that can be opened in most text or code (e.g VSC) editors.



## OCIO Configuration Files

### Loading OCIO Package

Environment Variable
The operating-system environment-variables (shortened as env-var) allows all software (supporting OCIO) to automatically load the same OCIO configuration file (shortened to config-file) by setting a file path.






https://www.elsksa.me/scientia/cgi-offline-rendering/ocio