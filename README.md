# utl_how_normalization_can_lead_to_faster_more_normal_and_a_smaller_database_footprint
How normalization can lead to faster more normal and a smaller database footprint.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    How normalization can lead to faster more normal and a smaller database footprint

    see github
    https://tinyurl.com/yc4xw7mu
    https://github.com/rogerjdeangelis/utl_how_normalization_can_lead_to_faster_more_normal_and_a_smaller_database_footprint

    Thoughts on normalization(skinny), skewness, faster and more concise tables.
    This is helpful when setting up tables for a relational database.

    You can even save the skew statistics which is critical for data partitioning and
    parallel processing


    https://communities.sas.com/t5/SAS-Communities-Library/Normalize-a-SAS-Dataset/ta-p/489357

    Tom Vicent profile
    https://communities.sas.com/t5/user/viewprofilepage/user-id/144199


    Chris Hemedinger profile
    https://communities.sas.com/t5/user/viewprofilepage/user-id/4


    INPUT
    =====

     WORK.CLASS total obs=19

        Up to 40 obs WORK.CLASS total obs=19

        Obs    NAME       SEX                   FAT1                                   FAT2

          1    Alfred      M     M--O--O--O--O--O--O--O--O--O--O--O-    0--X--X--X--X--X--X--X--X--X--X--X-
          2    Alice       F     F--O--O--O--O--O--O--O--O--O--O--O-    2--X--X--X--X--X--X--X--X--X--X--X-
          3    Barbara     F     F--O--O--O--O--O--O--O--O--O--O--O-    0--X--X--X--X--X--X--X--X--X--X--X-
          4    Carol       F     F--O--O--O--O--O--O--O--O--O--O--O-    0--X--X--X--X--X--X--X--X--X--X--X-
          5    Henry       M     M--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-
          6    James       M     M--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-
          7    Jane        F     F--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-
          8    Janet       F     F--O--O--O--O--O--O--O--O--O--O--O-    3--X--X--X--X--X--X--X--X--X--X--X-
          9    Jeffrey     M     M--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-
         10    John        M     M--O--O--O--O--O--O--O--O--O--O--O-    0--X--X--X--X--X--X--X--X--X--X--X-
         11    Joyce       F     F--O--O--O--O--O--O--O--O--O--O--O-    2--X--X--X--X--X--X--X--X--X--X--X-
         12    Judy        F     F--O--O--O--O--O--O--O--O--O--O--O-    2--X--X--X--X--X--X--X--X--X--X--X-
         13    Louise      F     F--O--O--O--O--O--O--O--O--O--O--O-    3--X--X--X--X--X--X--X--X--X--X--X-
         14    Mary        F     F--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-
         15    Philip      M     M--O--O--O--O--O--O--O--O--O--O--O-    2--X--X--X--X--X--X--X--X--X--X--X-
         16    Robert      M     M--O--O--O--O--O--O--O--O--O--O--O-    2--X--X--X--X--X--X--X--X--X--X--X-
         17    Ronald      M     M--O--O--O--O--O--O--O--O--O--O--O-    2--X--X--X--X--X--X--X--X--X--X--X-
         18    Thomas      M     M--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-
         19    William     M     M--O--O--O--O--O--O--O--O--O--O--O-    1--X--X--X--X--X--X--X--X--X--X--X-


    WANT
    ====

     Two dimension tables and one central table make up this little 'star?' schema

     DIMENSION TABLES
     ----------------

     WORK.SK_FAT1 total obs=2

                      FAT1                    SK_FAT1

       F--O--O--O--O--O--O--O--O--O--O--O-       1
       M--O--O--O--O--O--O--O--O--O--O--O-       2

       SKEWNESS
       ----------------------------
          19         2       9.5      19/2=9.5 (higher is better)
                                      9.5 to two distinct cores


     WORK.SK_FAT2 total obs=2
                      FAT2                    SK_FAT2

       0--X--X--X--X--X--X--X--X--X--X--X-       1
       1--X--X--X--X--X--X--X--X--X--X--X-       2
       2--X--X--X--X--X--X--X--X--X--X--X-       3
       3--X--X--X--X--X--X--X--X--X--X--X-       4

       SKEWNESS
       ----------------------------
             19         4      4.75   19/4 levels = 4.75 (observations per level)


     CENTRAL TABLE
     -------------

     WORK.CLASS2 total obs=19

        NAME       SEX    SK_FAT1    SK_FAT2

        Alfred      M        2          1
        Alice       F        1          3
        Barbara     F        1          1
        Carol       F        1          1
        Henry       M        2          2
        James       M        2          2
        Jane        F        1          2
        Janet       F        1          4
        Jeffrey     M        2          2
        John        M        2          1
        Joyce       F        1          3
        Judy        F        1          3
        Louise      F        1          4
        Mary        F        1          2
        Philip      M        2          3
        Robert      M        2          3
        Ronald      M        2          3
        Thomas      M        2          2
        William     M        2          2


    PROCESS
    =======

    %normalize(WORK,CLASS);

    Using this macro

    %macro normalize(lib,dsn);

        PROC SQL;
            SELECT name into :name1 -
                FROM dictionary.columns
            WHERE compress(libname||'.'||memname) = "&lib..&dsn" AND length > 8;
        quit;

        %if &SQLOBS = 0 %then %return;

        %let reccnt = &sqlobs;

        PROC SQL;
            CREATE TABLE &lib..&dsn.2 AS SELECT * FROM &lib..&dsn;
            QUIT;

        %do i = 1 %to &reccnt;

            %put &&name&i;

            proc sql;
                select count(*),COUNT(DISTINCT(&&name&i)),count(*)/COUNT(DISTINCT(&&name&i))
                into :count,:countdist,:pct
                from &lib..&dsn;
            quit;

            %put &=count &=countdist &=pct;

            %if &pct > 10 %then %do;

                proc sql;
                    CREATE TABLE work.distinct AS
                    SELECT DISTINCT &&name&i
                    FROM &lib..&dsn;
                quit;

                data &lib..sk_&&name&i; set work.distinct; sk_&&name&i =_n_; run;

                PROC SQL;
                    CREATE TABLE &lib..&dsn.3 AS
                        SELECT t2.*, t1.sk_&&name&i

                        FROM &lib..sk_&&name&i t1
                            INNER JOIN &lib..&dsn.2 t2 ON (t1.&&name&i = t2.&&name&i);
                QUIT;

                data &lib..&dsn.2; set &lib..&dsn.3; drop &&name&i; run;

            %end;

         %end;

     %mend normalize;

    OUTPUT
    ======

      Four tables (class3 can be deleted)
      see above

      WORK.SK_FAT1
      WORK.SK_FAT1
      WORK.CLASS2

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

     data class;
      set sashelp.class(keep=name sex);
      fat1=sex!!'-'!!repeat('-O-',10);
      fat2=put(3*uniform(31234),1.)!!'-'!!repeat('-X-',10);
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;
    %normalize(WORK,CLASS);

