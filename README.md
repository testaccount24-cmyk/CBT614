# CBT614
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 614 is from Sam Golob and contains load module libraries  *   FILE 614
//*           for various versions of the SHOWMVS and SHOWZOS       *   FILE 614
//*           programs from File 492.  Roland Schiradin requested   *   FILE 614
//*           that I not include load module libraries in File      *   FILE 614
//*           492 itself, because of the various versions of z/OS   *   FILE 614
//*           products such as ISPF and LE and TCP/IP which may     *   FILE 614
//*           be included in the final load module and which may    *   FILE 614
//*           cause some problem in some systems, if they are the   *   FILE 614
//*           wrong version for that system.  So it is best for     *   FILE 614
//*           each installation to assemble and linkedit SHOWMVS    *   FILE 614
//*           or SHOWZOS for itself.                                *   FILE 614
//*                                                                 *   FILE 614
//*           However, it is difficult for some shops to assemble   *   FILE 614
//*           SHOWMVS and SHOWZOS, because they don't have the      *   FILE 614
//*           proper version of the High Level Assembler (ASMA90)   *   FILE 614
//*           or they are missing some of the other requirements    *   FILE 614
//*           for properly creating a SHOWMVS or SHOWZOS load       *   FILE 614
//*           module.  Therefore, I have created this file so       *   FILE 614
//*           that such shops can have a quick install of SHOWMVS   *   FILE 614
//*           or SHOWZOS, to suit (at least) most of their needs.   *   FILE 614
//*                                                                 *   FILE 614
//*       email:  sbgolob@cbttape.org                               *   FILE 614
//*                                                                 *   FILE 614
//*       To create a load library from one of these members,       *   FILE 614
//*       use the RECEIVE command under TSO:                        *   FILE 614
//*                                                                 *   FILE 614
//*       RECEIVE INDS(hlq.FILE614.pds(memname))                    *   FILE 614
//*                                                                 *   FILE 614
//*       and answer the prompts for DSN( ), VOL( ), UNIT( ) etc.   *   FILE 614
//*       or just press ENTER.                                      *   FILE 614
//*                                                                 *   FILE 614
//*  Note:  SHOWzOS 7.17 and 7.18 assemble differently on z/OS 1.8  *   FILE 614
//*         systems and on z/OS 1.9 systems.  The z/OS 1.9 assembly *   FILE 614
//*         load module will work on 1.8, but the z/OS 1.8 load     *   FILE 614
//*         module will get an abend when run on z/OS 1.9 or 1.10.  *   FILE 614
//*         Similar results occur for SHOWzOS 7.19, and I suppose,  *   FILE 614
//*         for 7.20.                                               *   FILE 614
//*                                                                 *   FILE 614
//*         Therefore if you have multiple systems, it is           *   FILE 614
//*         recommended that you assemble SHOWzOS on z/OS 1.9 or    *   FILE 614
//*         higher.  Members marked SHO9xxxx were assembled at      *   FILE 614
//*         the z/OS 1.9 level.  Members marked SHOAxxxx were       *   FILE 614
//*         assembled on a z/OS 1.10 system.  Members marked        *   FILE 614
//*         SHOBxxxx were assembled on a z/OS 1.11 system.          *   FILE 614
//*         Similarly, SHOCxxxx on 1.12, and SHODxxxx on 1.13,      *   FILE 614
//*         and SHOExxxx on 2.1, and SHOGxxxx on 2.2.               *   FILE 614
//*                                                                 *   FILE 614
//*         Reassembled 2013/12/12 for z/OS 1.13, PUT LEVEL 1311.   *   FILE 614
//*         Members:  ASMLD721, SHOD721M.                           *   FILE 614
//*                                                                 *   FILE 614
//*         Reassembled 2014/05/15 for z/OS 2.1, PUT LEVEL 1403.    *   FILE 614
//*         Members:  ASMLE722, SHOE722L.                           *   FILE 614
//*                                                                 *   FILE 614
//*         Reassembled 2015/01/20 for z/OS 2.1, PUT LEVEL 1412.    *   FILE 614
//*         PTF Levels:  UA90741, UA90742, UA90740 and z/OS 2.2.    *   FILE 614
//*         Members:  ASMLF722, SHOF722L.  Old versions of          *   FILE 614
//*         SHOWzOS will not work if ULUT is Type 3 (now 64-bit)    *   FILE 614
//*         after PUT 1412 maintenance is applied.                  *   FILE 614
//*                                                                 *   FILE 614
//*         Reassembled 2015/06/09 for z/OS 2.1 PUT LEVEL 1503.     *   FILE 614
//*         This is SHOWzOS 7.23.  ASMLF723, SHOF723L.              *   FILE 614
//*                                                                 *   FILE 614
//*         There is a newer SHOWzOS 7.23 version, as below.        *   FILE 614
//*                                                                 *   FILE 614
//*         Reassembled the newer SHOWzOS 7.23 version using        *   FILE 614
//*         z/OS 2.1 at PUT Level 1505.  Dated 2015/08/02.          *   FILE 614
//*         This is SHOWzOS 7.23.  ASMLF723, SHOF723M.              *   FILE 614
//*                                                                 *   FILE 614
//*         The "final" version of SHOWzOS 7.23 was assembled       *   FILE 614
//*         on z/OS 2.2 at PUT Level 1611.  Members SHOG723M        *   FILE 614
//*         and ASMLH723.  Solved LOGGER problem.                   *   FILE 614
//*                                                                 *   FILE 614
//*         The initial version of SHOWzOS 7.25 was assembled       *   FILE 614
//*         on z/OS 2.4 at PUT Level 2004.  Members SHOH725L        *   FILE 614
//*         and ASMLH725.                                           *   FILE 614
//*                                                                 *   FILE 614
//*         SHOWzOS 8.01 was assembled on z/OS 2.4 at PUT level     *   FILE 614
//*         2008.  Members SHOH801L and ASMLH801.                   *   FILE 614
//*                                                                 *   FILE 614
//*         SHOWzOS 8.01 was assembled on z/OS 2.5 at PUT level     *   FILE 614
//*         2112.  Members SHOI801L and ASMLI801.                   *   FILE 614
//*                                                                 *   FILE 614
//*         SHOWzOS 8.02 is much improved from 8.01.                *   FILE 614
//*                                                                 *   FILE 614
//*         SHOWzOS 8.02 was assembled on z/OS 2.5 at PUT level     *   FILE 614
//*         2303.  Members SHOI802L and ASMLI802.                   *   FILE 614
//*                                                                 *   FILE 614
//*         SHOWzOS 8.03 was assembled on z/OS 2.5 at PUT level     *   FILE 614
//*         2303.  Members SHOI803L and ASMLI803.                   *   FILE 614
//*                                                                 *   FILE 614
//*         SHOWzOS 8.03 was assembled on z/OS 3.1 at PUT level     *   FILE 614
//*         2403.  Members SHOJ803L and ASMLJ803.                   *   FILE 614
//*                                                                 *   FILE 614
//*         (Some machines cannot run SHOWzOS 8.02.  It is          *   FILE 614
//*         suggested to run SHOWzOS 7.25 in these cases.  It       *   FILE 614
//*         should run fine.)                                       *   FILE 614
//*                                                                 *   FILE 614
```
