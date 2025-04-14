# CBT245
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 245 IS FROM PHILIP PECKSEN OF NFU MUTUAL INSURANCE IN     *   FILE 245
//*           STRATFORD UPON AVON, ENGLAND.  THIS FILE COMES FROM   *   FILE 245
//*           A TAPE AVAILABLE TO MEMBERS OF UK G.U.I.D.E.  THIS    *   FILE 245
//*           FILE IS ADMINISTERED BY RICHARD HAYDOCK OF NORWICH    *   FILE 245
//*           UNION INSURANCE IN ENGLAND.  ITS CONTENTS IS          *   FILE 245
//*           DESCRIBED BELOW.                                      *   FILE 245
//*                                                                 *   FILE 245
//*    GENERAL NOTES ON THIS LIBRARY                                *   FILE 245
//*    =============================                                *   FILE 245
//*                                                                 *   FILE 245
//*    PREPARED - 29/04/93                                          *   FILE 245
//*                                                                 *   FILE 245
//*    BY       - RICHARD HAYDOCK                                   *   FILE 245
//*               SYSTEMS PROGRAMMER                                *   FILE 245
//*               NORWICH UNION INSURANCE                           *   FILE 245
//*                                                                 *   FILE 245
//*               EMAIL - GBNUHCCF ON IBM MAIL EXCHANGE             *   FILE 245
//*               PHONE - +44-1-603-687709                          *   FILE 245
//*                                                                 *   FILE 245
//*    FOLLOWING A PRESENTATION ON 'TSO AND PERSONAL USERIDS AT     *   FILE 245
//*    NORWICH UNION' GIVEN AT THE UK LARGE SYSTEMS GUIDE ON        *   FILE 245
//*    24/03/93 (BRITISH GAS, SOUTHAMPTON) I PUT THIS COLLECTION    *   FILE 245
//*    OF BITS AND PIECES TOGETHER FOR THE GUIDE GOODIES TAPE       *   FILE 245
//*                                                                 *   FILE 245
//*    AT NORWICH UNION, A 'PROJECT' IS EFFECTIVELY THE SAME AS     *   FILE 245
//*    A RACF GROUP MANY OF OUR TSO USERS BELONG TO MORE THAN       *   FILE 245
//*    ONE 'PROJECT' SO IN THE PAST THEY HAD A NUMBER OF TSO        *   FILE 245
//*    USERIDS, BUT NOW THEY HAVE ONE USERID WHICH IS CONNECTED     *   FILE 245
//*    TO A NUMBER OF RACF GROUPS FOR TSO PURPOSES                  *   FILE 245
//*                                                                 *   FILE 245
//*    RACF GROUPS USED FOR TSO AT NU HAVE NAMES WHICH BEGIN        *   FILE 245
//*    'NU' AND ARE 5 CHARACTERS IN LENGTH                          *   FILE 245
//*                                                                 *   FILE 245
//*    THE BITS AND PIECES ARE AS FOLLOWS:                          *   FILE 245
//*                                                                 *   FILE 245
//*    JCL USED TO CREATE SYSTEM LIBRARIES                          *   FILE 245
//*    -----------------------------------                          *   FILE 245
//*                                                                 *   FILE 245
//*    TSOLOAD1- IS USED TO CREATE A SET OF LARGE SYSTEM            *   FILE 245
//*              LIBRARIES FOR USE BY ALL TSO USERS ON OUR          *   FILE 245
//*              PRODUCTION SYSTEMS (IBM1 AND IBM2)                 *   FILE 245
//*                                                                 *   FILE 245
//*    TSOLOAD3- SIMILAR TO TSOLOAD1, BUILDS LIBRARIES FOR IBM3     *   FILE 245
//*              (OUR MAIN TESTING SYSTEM)                          *   FILE 245
//*                                                                 *   FILE 245
//*    TSOLOAD6- SIMILAR TO TSOLOAD1, BUILDS LIBRARIES FOR IBM6     *   FILE 245
//*              (OUR SYSTEMS PROGRAMMER TEST SYSTEM)               *   FILE 245
//*                                                                 *   FILE 245
//*    FOR EACH ENVIRONMENT, WE MAINTAIN TWO SETS OF LIBRARIES -    *   FILE 245
//*    AN 'A' SET AND A 'B' SET. AT A GIVEN TIME, ONLY ONE SET IS   *   FILE 245
//*    ALLOCATED TO A LARGE NUMBER OF USERS, SO THE OTHER SET CAN   *   FILE 245
//*    BE REBUILT WITHOUT CAUSING CONTENTION. ONCE A NEW SET OF     *   FILE 245
//*    LIBRARIES HAS BEEN BUILT AND TESTED, IT CAN BE 'ROLLED IN'   *   FILE 245
//*    BY CHANGING THE SYSTEM LEVEL TSO PARAMETERS.                 *   FILE 245
//*                                                                 *   FILE 245
//*    A FEW DAYS AFTER A SUCCESSFUL 'ROLL-IN' THE INACTIVE SET     *   FILE 245
//*    OF LIBRARIES IS RE-BUILT TO MIRROR THE SET JUST ROLLED IN.   *   FILE 245
//*    THIS MEANS WE HAVE TWO IDENTICAL SETS WHICH BACK EACH        *   FILE 245
//*    OTHER UP UNTIL WE NEXT NEED TO MAKE CHANGES.                 *   FILE 245
//*                                                                 *   FILE 245
//*    THIS SYSTEM USES SEVERAL HUNDRED CYLINDERS OF EXTRA DASD,    *   FILE 245
//*    BUT GIVES A FLEXIBLE AND RESILIENT ENVIRONMENT AND           *   FILE 245
//*    ELIMINATES THE NEED FOR LONG CONCATENATIONS OF DATASETS.     *   FILE 245
//*                                                                 *   FILE 245
//*    TO MINIMISE THE EXTRA DASD USAGE, WE ONLY COPY THE MOST      *   FILE 245
//*    COMMONLY USED ISPF DIALOG ELEMENTS INTO THE LARGE SYSTEM     *   FILE 245
//*    LIBRARIES. GROUPS USING LESS COMMONLY USED FACILITIES        *   FILE 245
//*    (SUCH AS RACF DIALOGS) CAN EITHER USE FRONT-END DRIVERS TO   *   FILE 245
//*    MAKE NECESSARY ALLOCATIONS AND INVOKE THE FACILITY, OR       *   FILE 245
//*    ARRANGE FOR EXTRA ALLOCATIONS TO BE MADE WHEN THEY LOG ON    *   FILE 245
//*                                                                 *   FILE 245
//*    LOGON PROCEDURES, 'STARTUP' REXX AND TSO PARAMETERS          *   FILE 245
//*    ---------------------------------------------------          *   FILE 245
//*                                                                 *   FILE 245
//*    TSODFLT - IS A SIMPLE LOGON PROCEDURE ALLOWING BASIC ISPF    *   FILE 245
//*              ACCESS                                             *   FILE 245
//*                                                                 *   FILE 245
//*    TSOTS   - IS A LOGON PROCEDURE USED BY 'TERMINAL             *   FILE 245
//*              SUPERVISORS' - A LARGE GROUP OF TSO USERS WHO DO   *   FILE 245
//*              NOT NEED THE FULL RANGE OF POSSIBILITIES OFFERED   *   FILE 245
//*              BY 'TSOPROC'                                       *   FILE 245
//*                                                                 *   FILE 245
//*    TSOPARM - MEMBER OF SYS1.PROCLIB REFERENCED BY 'TSOTS' TO    *   FILE 245
//*              DETERMINE WHETHER 'A' OR 'B' SYSTEM LIBRARIES      *   FILE 245
//*              SHOULD BE ALLOCATED                                *   FILE 245
//*                                                                 *   FILE 245
//*    TSOPROC - IS THE NU 'STANDARD' LOGON PROCEDURE.  IT          *   FILE 245
//*              ALLOCATES ONLY SYS1.ISRCLIB IN WHICH WE KEEP:      *   FILE 245
//*                                                                 *   FILE 245
//*    TSOTESTA- IS SIMILAR TO TSOPROC BUT USED FOR LOGGING ON      *   FILE 245
//*              WITH A NEW SET OF 'A' SYSTEM LIBRARIES WHEN THE    *   FILE 245
//*              'B' LIBRARIES ARE IN PRODUCTION.  BY USING         *   FILE 245
//*              TSOTESTA, WE CAN GET EARLY WARNING OF DIALOG       *   FILE 245
//*              ERRORS WITHOUT EXPOSING ALL OUR USERS TO THEM      *   FILE 245
//*                                                                 *   FILE 245
//*              WE ALSO HAVE A PROCEDURE CALLED TSOTESTB FOR       *   FILE 245
//*              TESTING NEW 'B' LIBRARIES                          *   FILE 245
//*                                                                 *   FILE 245
//*    STARTUP - A REXX EXEC WHICH ALLOCATES THE USER'S ISPF        *   FILE 245
//*              PROFILES AND PROCESSES 'TSO PARAMETER' DATASETS    *   FILE 245
//*              IN ORDER TO DETERMINE WHICH DATASETS SHOULD BE     *   FILE 245
//*              ALLOCATED TO THE USER'S TSO/ISPF SESSION, AND      *   FILE 245
//*              THEN ALLOCATES THEM. OTHER PROCESSING MAY ALSO     *   FILE 245
//*              BE DONE DEPENDING ON THE PARAMETERS ENCOUNTERED.   *   FILE 245
//*                                                                 *   FILE 245
//*    PARMSEX - A LIST OF EXAMPLE PARAMETERS SHOWING THE SYNTAX    *   FILE 245
//*              RECOGNISED BY 'STARTUP'                            *   FILE 245
//*                                                                 *   FILE 245
//*    PARMSUSR- MY OWN 'PERSONAL' TSO PARAMETERS FOR USE ON OUR    *   FILE 245
//*              TEST SYSTEM (CALLED IBM3). THEY ARE STORED IN      *   FILE 245
//*              THE ISPF PROFILE I USE ON IBM3                     *   FILE 245
//*                                                                 *   FILE 245
//*    PARMSGRP- TSO PARAMETERS FOR USE BY ALL MEMBERS OF THE       *   FILE 245
//*              GROUP (NUSSS) TO WHICH I AM CONNECTED FOR TSO      *   FILE 245
//*              PURPOSES                                           *   FILE 245
//*                                                                 *   FILE 245
//*    PARMSSYS- TSO PARAMETERS FOR USE BY ALL USERS OF TSO ON      *   FILE 245
//*              IBM3                                               *   FILE 245
//*                                                                 *   FILE 245
//*    ROG*    - ALL MEMBERS PREFIXED 'ROG' ARE USED TO SET UP      *   FILE 245
//*              ISPF READ ONLY VARIABLES FOR ACCOUNT CODE,         *   FILE 245
//*              SYSTEM ID AND RACF CURRENT CONNECT GROUP. THE      *   FILE 245
//*              STARTUP REXX INVOKES 'ROGS'                        *   FILE 245
//*                                                                 *   FILE 245
//*    ISPF DIALOG FOR ADMINISTRATION OF TSO PARAMETERS             *   FILE 245
//*    ------------------------------------------------             *   FILE 245
//*                                                                 *   FILE 245
//*    ONLY SYSTEMS PROGRAMMERS CAN MODIFY SYSTEM LEVEL             *   FILE 245
//*    PARAMETERS.                                                  *   FILE 245
//*                                                                 *   FILE 245
//*    TRUSTED INDIVIDUALS WITHIN GROUPS CAN MODIFY THOSE           *   FILE 245
//*    PARAMETERS WHICH BELONG TO THEIR GROUP(S) SO THEY HAVE       *   FILE 245
//*    SOME CONTROL OVER WHAT WILL BE ALLOCATED TO THEIR GROUP      *   FILE 245
//*    MEMBERS AFTER LOGGING ON.                                    *   FILE 245
//*                                                                 *   FILE 245
//*    INDIVIDUAL USERS CAN (IF THEY WISH) SET UP PERSONAL          *   FILE 245
//*    PARAMETERS IN ORDER TO HAVE PERSONALISED ISPF                *   FILE 245
//*    ENVIRONMENTS.                                                *   FILE 245
//*                                                                 *   FILE 245
//*    USERS CAN DISPLAY/MODIFY PARAMETERS AT USER, GROUP OR        *   FILE 245
//*    SYSTEM LEVEL IN ISOLATION, OR OBTAIN A 'MERGED' LIST WHICH   *   FILE 245
//*    LOOKS A LITTLE LIKE THE RESULT OF ISSUING A 'TSO LISTALC'    *   FILE 245
//*    COMMAND AFTER LOGGING ON.                                    *   FILE 245
//*                                                                 *   FILE 245
//*    NORWICH UNION HAS ITS OWN STANDARD VERSION OF THE            *   FILE 245
//*    'ISR@PRIM' PANEL WHICH WE INSIST ON USERS USING. IT HAS 3    *   FILE 245
//*    SPECIAL OPTIONS:                                             *   FILE 245
//*                                                                 *   FILE 245
//*    'S' - SYSTEM PROVIDED, NU-SPECIFIC FACILITIES                *   FILE 245
//*                                                                 *   FILE 245
//*    'P' - PROJECT FUNCTIONS. THESE FUNCTIONS ARE ENTIRELY        *   FILE 245
//*          UNDER THE CONTROL OF THE PROJECT (GROUP OF USERS) SO   *   FILE 245
//*          THERE ARE DIFFERENT SETS OF PROJECT FUNCTIONS FOR      *   FILE 245
//*          DIFFERENT RACF GROUPS.                                 *   FILE 245
//*                                                                 *   FILE 245
//*    'U' - USER FUNCTIONS. THESE ARE AVAILABLE FOR INDIVIDUALS    *   FILE 245
//*          FAMILIAR WITH ISPF WHO WISH TO SET UP DIALOGS OF       *   FILE 245
//*          THEIR OWN.                                             *   FILE 245
//*                                                                 *   FILE 245
//*    THE ELEMENTS OF THE TSO PARAMETER ADMIN DIALOG ARE:          *   FILE 245
//*                                                                 *   FILE 245
//*    TSOA000 - REXX TO DRIVE THE DIALOG (THIS IS PACKAGED AS      *   FILE 245
//*              MEMBER TSOA000X HERE, AS ITS NAME IS THE SAME AS   *   FILE 245
//*              ONE OF THE PANELS)                                 *   FILE 245
//*                                                                 *   FILE 245
//*    TSOA000-TSOA006 - PANELS USED BY THIS DIALOG                 *   FILE 245
//*                                                                 *   FILE 245
//*    TSOA01  - MESSAGES (1)                                       *   FILE 245
//*    TSOA02  - MESSAGES (2)                                       *   FILE 245
//*                                                                 *   FILE 245
//*    TTSOA000-TTSOA003 - HELP PANELS FOR TSOA000-TSOA003          *   FILE 245
//*                                                                 *   FILE 245
//*    ISPF DIALOG USED BY USERS CONVERTING TO USE PERSONAL         *   FILE 245
//*    USERIDS FOR TSO                                              *   FILE 245
//*    ----------------------------------------------------         *   FILE 245
//*                                                                 *   FILE 245
//*    THIS DIALOG BEGINS WITH PANEL SPU (HELP PANEL TSPU).         *   FILE 245
//*    MESSAGES ARE IN MEMBER SPUM01                                *   FILE 245
//*    THERE ARE 4 OPTIONS:                                         *   FILE 245
//*                                                                 *   FILE 245
//*    1 - DISPLAY RACF GROUPS YOU ARE CONNECTED TO, SELECT NEW     *   FILE 245
//*        DEFAULT IF DESIRED                                       *   FILE 245
//*                                                                 *   FILE 245
//*    2 - DATASET RENAMING UTILITY (USEFUL FOR USERS WITH LARGE    *   FILE 245
//*        NUMBERS OF PERSONAL DATASETS). FOR VSAM DATASETS, DO     *   FILE 245
//*        NOT TRY TO CHANGE THE HIGH LEVEL QUALIFIER. THIS         *   FILE 245
//*        UTILITY USES IDCAMS 'ALTER NEWNAME' COMMANDS TO RENAME   *   FILE 245
//*        VSAM CLUSTER COMPONENTS.                                 *   FILE 245
//*                                                                 *   FILE 245
//*    3 - DISPLAY/CHANGE ISPF ACCOUNT CODE VARIABLE (THE           *   FILE 245
//*        NU-DEFINED ISPF VARIABLE CALLED 'Z#ACCT' IS USED BY      *   FILE 245
//*        THIS UTILITY. THE IBM-DEFINED 'ZACCTNUM' VARIABLE IS     *   FILE 245
//*        UNCHANGEABLE)                                            *   FILE 245
//*                                                                 *   FILE 245
//*    4 - ISPF PROFILE CONVERTER. USEFUL FOR USERS WHOSE OLD IDS   *   FILE 245
//*        HAD A HIGH LEVEL OF ISPF CUSTOMISATION.                  *   FILE 245
//*                                                                 *   FILE 245
//*    THE CALL SEQUENCES ARE AS FOLLOWS:                           *   FILE 245
//*                                                                 *   FILE 245
//*    1 - REXX XNUCHGRP, PANEL NUCHGRP (HELP PANEL - TNUCHGRP)     *   FILE 245
//*                                                                 *   FILE 245
//*    2 - REXX XNUDSREN, PANEL NUDSREN (HELP PANEL - TNUDSREN)     *   FILE 245
//*        SKEL NUDSREN   INVOKES REXX XNUDSRN1 IN BATCH MODE       *   FILE 245
//*                                                                 *   FILE 245
//*        (NOTE - SKEL NUDSREN IS PACKAGED AS SNUDSREN DUE TO      *   FILE 245
//*                NAME CLASH)                                      *   FILE 245
//*                                                                 *   FILE 245
//*    3 - REXX XNUCHACC, PANEL RESETACC (HELP PANEL - TNUCHACC)    *   FILE 245
//*                                                                 *   FILE 245
//*    4 - REXX XNUCVPRF, PANEL NUCVPRF (HELP PANEL - TNUCVPRF)     *   FILE 245
//*        SKEL NUCVPRF   INVOKES REXX XNUCVPR1 IN BATCH MODE       *   FILE 245
//*                                                                 *   FILE 245
//*        (NOTE - SKEL NUCVPRF IS PACKAGED AS SNUCVPRF DUE TO      *   FILE 245
//*                NAME CLASH)                                      *   FILE 245
//*                                                                 *   FILE 245
//*        AFTER USING OPTION 4, USERS ARE INVITED TO RUN THE       *   FILE 245
//*        REXX XNURNPRF FROM OUTSIDE ISPF. THIS BACKS UP THE       *   FILE 245
//*        ISPF PROFILE THEY WERE USING AND ACTIVATES TO THE ONE    *   FILE 245
//*        JUST CREATED FOR THEM                                    *   FILE 245
//*                                                                 *   FILE 245
//*    OTHER REXX UTILITIES                                         *   FILE 245
//*    --------------------                                         *   FILE 245
//*                                                                 *   FILE 245
//*    CHECKGRP - USED TO CHECK WHETHER OR NOT A USER IS            *   FILE 245
//*               CONNECTED TO A SPECIFIED RACF GROUP. THIS IS      *   FILE 245
//*               OFTEN USED AS A CONTROL MECHANISM TO DECIDE       *   FILE 245
//*               WHETHER OR NOT IT IS APPROPRIATE FOR A GIVEN      *   FILE 245
//*               USER TO USE A CERTAIN APPLICATION.                *   FILE 245
//*                                                                 *   FILE 245
//*    XNUCA1A  - USED TO INVOKE THE CA-ONE ISPF DIALOG. CA-ONE     *   FILE 245
//*               IS A TAPE MANAGEMENT SYSTEM USED BY A FEW OF      *   FILE 245
//*               OUR GROUPS, SO THOSE THAT NEED IT CAN INVOKE IT   *   FILE 245
//*               USING 'XNUCA1A' WITHOUT NEEDING TO ALLOCATE ANY   *   FILE 245
//*               OTHER LIBRARIES.                                  *   FILE 245
//*                                                                 *   FILE 245
//*    XNUCA1B  - CALLED BY XNUCA1A TO COMPLETE THE INVOCATION OF   *   FILE 245
//*               CA-ONE                                            *   FILE 245
//*                                                                 *   FILE 245
//*    XNUTSM53 - USED TO INVOKE TSO/MON 5.3 THIS INVOCATION IS     *   FILE 245
//*               SIMPLER THAN THAT OF CA-ONE SINCE NO ISPF         *   FILE 245
//*               'NEWAPPL' IS INVOLVED                             *   FILE 245
//*                                                                 *   FILE 245
//*    ASSEMBLER CODE                                               *   FILE 245
//*    --------------                                               *   FILE 245
//*                                                                 *   FILE 245
//*    ISP*     - USED TO MAKE ISPF USER EXIT 16 WORK. APART FROM   *   FILE 245
//*               CODING UP ISPF EXIT 16 ITSELF, THE INSTALLATION   *   FILE 245
//*               ALSO HAS TO CODE A MODIFIED 'ISPDFLTS' MODULE     *   FILE 245
//*               TO INDICATE TO ISPF THAT USER EXITS ARE BEING     *   FILE 245
//*               TAKEN, AND 'ISPXDT' (EXIT DEFINITION TABLE) TO    *   FILE 245
//*               IDENTIFY WHICH EXITS ARE IN USE, WHAT THE CSECT   *   FILE 245
//*               NAMES ARE ETC. SEE ISPF 'INSTALLATION &           *   FILE 245
//*               CUSTOMISATION' FOR MORE DETAILS.                  *   FILE 245
//*                                                                 *   FILE 245
//*    IEFUTL   - NU VERSION OF THE SMF USER TIME LIMIT EXIT.       *   FILE 245
//*               SHOWS HOW RACF IS USED TO CONTROL WHICH USERS     *   FILE 245
//*               ARE EXEMPT FROM TIMEOUT CONTROL AND CPU TIME      *   FILE 245
//*               LIMIT CONTROL. THIS VERSION OF IEFUTL NO LONGER   *   FILE 245
//*               REQUIRES ANY MODIFICATION BY US.                  *   FILE 245
//*                                                                 *   FILE 245
//*    NUIGACCT - TSO COMMAND USED TO SET UP ISPF VARIABLES FOR     *   FILE 245
//*               ACCOUNT CODE SYSTEM NAME AND CURRENT RACF         *   FILE 245
//*               CONNECT GROUP                                     *   FILE 245
//*                                                                 *   FILE 245
//*               DSMMACS AND NUTETE ARE NEEDED TO ASSEMBLE         *   FILE 245
//*               NUIGACCT - IT HAS TO RUN IN AN ISPF ENVIRONMENT   *   FILE 245
//*                                                                 *   FILE 245
//*    FINDGRP  - TSO COMMAND USED TO SET UP TSO VARIABLE 'GRPID'   *   FILE 245
//*               AND OTHERS (SEE SOURCE). USEFUL IN CLISTS OR      *   FILE 245
//*               REXXS TO FIND A USER'S CURRENT CONNECT GROUP      *   FILE 245
//*               WHEN PERSONAL USERIDS ARE IN USE.                 *   FILE 245
//*                                                                 *   FILE 245
//*    FINDSYS  - TSO COMMAND USED TO SET UP TSO VARIABLE 'SYSID'   *   FILE 245
//*                                                                 *   FILE 245
//*        THE FINDGRP AND FINDSYS COMMANDS ARE BOTH USED BY THE    *   FILE 245
//*        'STARTUP' REXX                                           *   FILE 245
//*                                                                 *   FILE 245
```
