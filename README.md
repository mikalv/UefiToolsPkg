UefiToolsPkg
============

Various useful utilities for UEFI.

* AcpiDump   - Dump system ACPI tables to storage.
* AcpiLoader - Load system ACPI tables from storage.

Building
--------

Assuming you have EDK2 (http://www.tianocore.org/edk2/)
all configured and capable of producing builds for your
target architecture:

    $ git clone https://github.com/andreiw/UefiToolsPkg.git
    $ build -p UefiToolsPkg/UefiToolsPkg.dsc

To override architecture and/or toolchain:

    $ build -p UefiToolsPkg/UefiToolsPkg.dsc -a PPC64
    $ build -p UefiToolsPkg/UefiToolsPkg.dsc -a X64 -t GCC49

There's no architecture-specific code.

AcpiDump
--------

AcpiDump will dump all of the ACPI tables to the same volume
the tool is located on. This is sometimes useful, but keep
in mind that some UEFI implementations can patch ACPI tables
on the way out during ExitBootServices, meaning you might
not get the same (correct) data if you dumped tables from
the OS proper.

An optional parameter specifies the path, relative to the
volume root, where to place the tables. E.g.:

    fs16:> AcpiDump.efi
    fs16:> AcpiDump.efi MyFunkySystem

The files produced can be loaded by AcpiLoader.

AcpiLoader
----------

AcpiLoader will remove all of the existing ACPI tables
and install tables loaded from the same volume the
tool is on. Every file with an AML (aml) extension
is loaded.

An optional parameter specifies the path, relative to
the volume root, where the tables are loaded from. E.g.:

    fs16:> AcpiLoader.efi
    fs16:> AcpiLoader.efi MyFunkySystem

Features (or limitations, depending on how you look):
* XSDT only.
* No ACPI 1.0.
* No special ordering (i.e. FADT can be in any XSDT slot).
* No 32-bit restrictions on placement.
* 32-bit DSDT and FACS pointers are not supported.

Contact Info
------------

Andrei Warkentin (andrey.warkentin@gmail.com).
