# utl-using-functions-in-formats-to-right-justify-character-variables
Using functions in formats to right justify character variables
    %let pgm=utl-using-functions-in-formats-to-right-justify-character-variables;

    Using functions in formats to right justify character variables

    Aligning the results od proc transpose

    github
    https://tinyurl.com/4f2ha6u2
    https://github.com/rogerjdeangelis/utl-using-functions-in-formats-to-right-justify-character-variables

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /*************************************************************************************************************************/
    /*                                      |                                           |                                    */
    /*              INPUT                   |               PROCESS                     |              OUTPUT                */
    /*                                      |                                                                                */
    /* WHEN I PRINT RESULTS OF TRANSPOSE    | options cmplib=(work.functions);          |_NAME_   JOHN     JOYCE    JUDY     */
    /*                                      | * functions in formats Rick Langston;     |                                    */
    /* proc transpose data=sashelp.class    |                                           |     NAME     John    Joyce    Judy */
    /*   (firstobs=10 obs=12) out=xpo;      | proc fcmp outlib=work.functions.charRight;|      SEX        M        F       F */
    /* format _character_ $8. _numeric_ 4.; |  function charRight(txt $) $255;          |      AGE       12       11      14 */
    /* id name;                             |     ryght=right(txt);                     |   HEIGHT       59       51      64 */
    /* var _all_;                           |   return(ryght);                          |   WEIGHT      100       51      90 */
    /* run;quit;                            | endsub;                                   |                                    */
    /*                                      | run;quit;                                 |                                    */
    /* proc print data=xpo;                 |                                           |                                    */
    /* run;quit;                            | * put the function in a format;           |                                    */
    /*                                      | proc format;                              |                                    */
    /*                                      |   value $charRight other=[charRight()];   |                                    */
    /* I GET                                | run;quit;                                 |                                    */
    /*                                      |                                           |                                    */
    /* XPO total obs=5                      | proc print data=xpo                       |                                    */
    /*                                      |    format _character_ $charRight8.;       |                                    */
    /* _NAME_    JOHN     JOYCE      JUDY   | run;quit;                                 |                                    */
    /*                                      |                                           |                                    */
    /* NAME    John      Joyce     Judy     |                                           |                                    */
    /* SEX     M         F         F        |                                           |                                    */
    /* AGE           12        11        14 |                                           |                                    */
    /* HEIGHT        59        51        64 |                                           |                                    */
    /* WEIGHT       100        51        90 |                                           |                                    */
    /*                                      |                                           |                                    */
    /*************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    proc transpose data=sashelp.class
      (firstobs=10 obs=12) out=xpo;
    format _character_ $8. _numeric_ 4.;
    id name;
    var _all_;
    run;quit;

    proc print data=xpo;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  XPO total obs=5                                                                                                       */
    /*                                                                                                                        */
    /*  Obs    _NAME_      JOHN        JOYCE       JUDY                                                                       */
    /*                                                                                                                        */
    /*   1     NAME        John        Joyce       Judy                                                                       */
    /*   2     SEX         M           F           F                                                                          */
    /*   3     AGE               12          11          14                                                                   */
    /*   4     HEIGHT            59          51          64                                                                   */
    /*   5     WEIGHT           100          51          90                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    options cmplib=(work.functions);
    * functions in formats Rick Langston;

    proc fcmp outlib=work.functions.charRight;
     function charRight(txt $) $255;
        ryght=right(txt);
      return(ryght);
    endsub;
    run;quit;

    * put the function in a format;
    proc format;
      value $charRight other=[charRight()];
    run;quit;

    proc print data=xpo;
       format _character_ $charRight8.;
    run;quit;


    /*************************************************************************************************************************/
    /*                                                                                                                       */
    /*_NAME_   JOHN     JOYCE    JUDY                                                                                        */
    /*                                                                                                                       */
    /*     NAME     John    Joyce    Judy                                                                                    */
    /*      SEX        M        F       F                                                                                    */
    /*      AGE       12       11      14                                                                                    */
    /*   HEIGHT       59       51      64                                                                                    */
    /*   WEIGHT      100       51      90                                                                                    */
    /*                                                                                                                       */
    /*************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
