# IBM-PC-BIOS

This is a reconstruction of the IBM PC, PC XT, PC AT and PC XT 286 BIOS source code using scanning and transcription of the BIOS listings found in the IBM Technical Reference manuals. This historically relevant source code is presented here for software preservation.

The following BIOS source code has been reconstructed:
IBM PC version 1     04/21/81
IBM PC version 2     10/19/81
IBM PC version 3     10/27/82

Notes:

• All 3 versions of the IBM PC BIOS and the first version of the IBM PC XT BIOS were built using Intel ASM86 on an Intel development system. In each case the BIOS source code is a single large file and the BIOS code is 8KB which resides at F000:E000

• The IBM PC AT version 1 BIOS was built using IBM MASM 1.0 on DOS. This is the first IBM BIOS which uses multiple source files. Since IBM MASM 1.0 did not support the 80286 there is a macro file (IAPX286.MAC) which is used to generate the necessary opcodes. This is also the first BIOS to be split into two parts: the main BIOS code resides at F000:0000 and the compatibility section (ORGS.ASM) resides at F000:E000. An additional file FILL.ASM has been added to define the area between the end of the main BIOS code and the compatibility section to allow the BIOS to be linked properly. It is currently unknown how this was originally handled.

• The IBM PC AT version 2 and 3 BIOS and the IBM PC XT 286 BIOS were built using IBM MASM 2.0 on DOS. These are similar to the PC AT version 1 BIOS but there are fewer source files as some files were combined and a bit of cleanup was done. IAPX286.INC is used to generate the protected-mode 80286 opcodes which IBM MASM 2.0 did not support. FILL.ASM serves the same purpose as it does for the PC AT version 1 BIOS though in each case the file is specific to the particular BIOS being built.

• The IBM PC XT version 2 and 3 BIOS were built using IBM MASM 2.0 on DOS. The later PC XT BIOS code was restructured to be similar to the PC AT BIOS code so there are multiple source files. Like the PC AT BIOS the code is split into two parts though the compatibility section is in the file POST.ASM. Again the additional file FILL.ASM is used to define the area between the end of the main BIOS code and the compatibility section.

• The following code is present in all versions of the PC AT BIOS and the PC XT 286 BIOS but does not appear in the published listings. It is inferred from the public symbols in ORGS.ASM and code disassembly. It is unknown what purpose this code serves.

.XLIST
;;-     ORG     0FF5AH
        ORG     01F5AH

HRD     PROC    FAR
        CALL    DISK_SETUP
        RET
HRD     ENDP

FLOPPY  PROC    FAR
        CALL    DSKETTE_SETUP
        RET
FLOPPY  ENDP

SEEKS_1 PROC    FAR
        CALL    SEEK
        RET
SEEKS_1 ENDP

TUTOR:
        JMP     K16
.LIST
• In all cases the 32KB ROM BASIC code which resides at F6000 is not available as its source code was never published.

• Versions of MASM later than 4.0 cannot be used to build the IBM BIOS source code since older constructs and macros are used.

More information about functionality changes in the IBM PC BIOS code is listed here: IBM PC BIOS version history




