# utl-altair-personal-slc-odbc-connections-to-and-from-mysql-with-and-without-passthru
altair personal slc odbc connections to and from mysql with and without passthru
    %let pgm=utl-altair-personal-slc-odbc-connections-to-and-from-mysql-with-and-without-passthru;

    %stop_submission;

    altair personal slc odbc connections to and from mysql with and without passthru

    Too Long to post here, see git hub

       TWO SOLUTION

           1 without passthru (explicit-execute using sas language)
           2 with passthru (implicit - execute using sql server sql dialect inside the sql server database)

    github
    https://github.com/rogerjdeangelis/utl-altair-personal-slc-odbc-connections-to-and-from-ms-sql-server-with-and-without-passthru

    PREP (Local Win11 workstation)

    1  Download MySql
    2  Install MySQl
    3  Use legacy authetification
    4  After the install choce install from mysql in start menu
    5  Start install and use the add option
       Add the latest version of MySQl Workbence
    6  Download the sakila database
    7  Run the schema and data sql scripts
    8  Download and install mySQL ODBC Driver MySQL ODBC 9,4 ANSI Driver
    9  Create a dsn i use mysql8

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    ods listing;
    data class;
      input
        name$
        sex$ age;
    cards4;
    Alfred  M 14
    Alice   F 13
    Barbara F 13
    Carol   F 14
    Henry   M 14
    James   M 12
    ;;;;
    run;quit;

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    375      data class;
    6376        input
    6377          name$
    6378          sex$ age;
    6379      cards4;

    NOTE: Data set "WORK.class" has 6 observation(s) and 3 variable(s)
    NOTE: The data step took :
          real time : 0.005
          cpu time  : 0.000


    6380      Alfred  M 14
    6381      Alice   F 13
    6382      Barbara F 13
    6383      Carol   F 14
    6384      Henry   M 14
    6385      James   M 12
    6386      ;;;;
    6387      run;quit;


    /*           _ _   _                 _                        _   _
    / |__      _(_) |_| |__   ___  _   _| |_  _ __   __ _ ___ ___| |_| |__  _ __ _   _
    | |\ \ /\ / / | __| `_ \ / _ \| | | | __|| `_ \ / _` / __/ __| __| `_ \| `__| | | |
    | | \ V  V /| | |_| | | | (_) | |_| | |_ | |_) | (_| \__ \__ \ |_| | | | |  | |_| |
    |_|  \_/\_/ |_|\__|_| |_|\___/ \__,_|\__|| .__/ \__,_|___/___/\__|_| |_|_|   \__,_|
                                             |_|
                         _         _        _     _        _               _    _ _
      ___ _ __ ___  __ _| |_ ___  | |_ __ _| |__ | | ___  (_)_ __   ___  __ _| | _(_) | __ _
     / __| `__/ _ \/ _` | __/ _ \ | __/ _` | `_ \| |/ _ \ | | `_ \ / __|/ _` | |/ / | |/ _` |
    | (__| | |  __/ (_| | ||  __/ | || (_| | |_) | |  __/ | | | | |\__ \ (_| |   <| | | (_| |
     \___|_|  \___|\__,_|\__\___|  \__\__,_|_.__/|_|\___| |_|_| |_||___/\__,_|_|\_\_|_|\__,_|

    */

    libname db
       mysql
       user=root
       password="Sas2@rlxxlr@2saS"
       database='sakila'
       ;

    /*-- print sakila table film ---*/
    proc print data=db.film;
    run;quit;

    proc sql;
      drop table db.class_from_slc
    ;quit;

    /*--- subset slc class and store in salila table class_from_slc ---*/
    data db.class_from_slc;
      set class;
      if sex="M";
    run;quit;

    proc print data=db.class_from_slc;
    run;quit;

    OUTPUT
    ======

    Obs    name        sex         age

     1     Alfred      M            14
     2     Henry       M            14
     3     James       M            12

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    178
    179       libname db
    180          mysql
    181          user=root
    182          password=XXXXXXXXXXXXXXXXXX
    NOTE: Library db assigned as follows:
          Engine:        MYSQL
          Physical Name:  (MySQL version 8.0.43)

    183          database='sakila'
    184          ;
    WARNING: truncating character column description to 1024 characters long, based on dbmax_text
             setting.
    185
    186       /*-- print sakila table film ---*/
    187       proc print data=db.film;
    188       run;quit;
    NOTE: 1000 observations were read from "DB.film"
    NOTE: Procedure print step took :
          real time : 0.106
          cpu time  : 0.093


    189
    190       proc sql;
    191         drop table db.class_from_slc
    192       ;quit;
    NOTE: Table DB.class_from_slc has been dropped.
    NOTE: Procedure sql step took :
          real time : 0.032
          cpu time  : 0.000


    193
    194       /*--- subset slc class and store in salila table class_from_slc ---*/
    195       data db.class_from_slc;
    196         set class;
    197         if sex="M";
    198       run;

    NOTE: 6 observations were read from "WORK.class"
    NOTE: Data set "DB.class_from_slc" has an unknown number of observation(s) and 3 variable(s)
    NOTE: The data step took :
          real time : 0.266
          cpu time  : 0.156


    198     !     quit;
    199
    200       proc print data=db.class_from_slc;
    201       run;quit;
    NOTE: 3 observations were read from "DB.class_from_slc"
    NOTE: Procedure print step took :
          real time : 0.011
          cpu time  : 0.000

    /*                   _             _        _        _     _        __                           _ _
      ___ _ __ ___  __ _| |_ ___   ___| | ___  | |_ __ _| |__ | | ___  / _|_ __ ___  _ __ ___     __| | |__
     / __| `__/ _ \/ _` | __/ _ \ / __| |/ __| | __/ _` | `_ \| |/ _ \| |_| `__/ _ \| `_ ` _ \   / _` | `_ \
    | (__| | |  __/ (_| | ||  __/ \__ \ | (__  | || (_| | |_) | |  __/|  _| | | (_) | | | | | | | (_| | |_) |
     \___|_|  \___|\__,_|\__\___| |___/_|\___|  \__\__,_|_.__/|_|\___||_| |_|  \___/|_| |_| |_|  \__,_|_.__/

    */

    data males;
      set db.class_from_slc;
      if sex="M";
    run;quit;

    208       data males;
    209         set db.class_from_slc;
    210         if sex="M";
    211       run;

    NOTE: 3 observations were read from "DB.class_from_slc"
    NOTE: Data set "WORK.males" has 3 observation(s) and 3 variable(s)
    NOTE: The data step took :
          real time : 0.005
          cpu time  : 0.000

    OUTPUT
    ======

    Obs    name        sex         age

     1     Alfred      M            14
     2     Henry       M            14
     3     James       M            12


    /*___             _ _   _                          _   _                           _
    |___ \  __      _(_) |_| |__   _ __   __ _ ___ ___| |_| |__  _ __ ___  _   _  __ _| |__
      __) | \ \ /\ / / | __| `_ \ | `_ \ / _` / __/ __| __| `_ \| `__/ _ \| | | |/ _` | `_ \
     / __/   \ V  V /| | |_| | | || |_) | (_| \__ \__ \ |_| | | | | | (_) | |_| | (_| | | | |
    |_____|   \_/\_/ |_|\__|_| |_|| .__/ \__,_|___/___/\__|_| |_|_|  \___/ \__,_|\__, |_| |_|
                                  |_|                                            |___/
                         _         _        _     _        _             _ _
      ___ _ __ ___  __ _| |_ ___  | |_ __ _| |__ | | ___  (_)_ __     __| | |__
     / __| `__/ _ \/ _` | __/ _ \ | __/ _` | `_ \| |/ _ \ | | `_ \   / _` | `_ \
    | (__| | |  __/ (_| | ||  __/ | || (_| | |_) | |  __/ | | | | | | (_| | |_) |
     \___|_|  \___|\__,_|\__\___|  \__\__,_|_.__/|_|\___| |_|_| |_|  \__,_|_.__/

    */

    /*--- filter table inside sql server with sql server sql dialect ---*/
    /*--- output to a SLC wpd table                                  ---*/
    proc sql;
      connect to mysql (
        user=root
        password="Sas2@rlxxlr@2saS"
        database='sakila'
       );
      create table tst as (
      select * from connection to mysql
        (select * from film where rating="G")
      );
      disconnect from mysql;
    quit;

    proc print data=tst(obs=4);
    var film_id rating;
    run;quit;


    OUTPUT
    ======

    Obs    film_id    rating

      1           2    G
      2           4    G
      3           5    G
      4          11    G

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */


    56       proc sql;
    357         connect to mysql (
    358           user=root
    359           password=XXXXXXXXXXXXXXXXXX
    360           database='sakila'
    361          );
    NOTE: Successfully connected to database MYSQL as alias MYSQL.
    362         create table tst as (
    363         select * from connection to mysql
    364           (select * from film where rating="G")
    365         );
    WARNING: truncating character column description to 1024 characters long, based on dbmax_text
             setting.
    NOTE: Data set "WORK.tst" has 178 observation(s) and 13 variable(s)
    366         disconnect from mysql;
    NOTE: Successfully disconnected from database MYSQL.
    367       quit;
    NOTE: Procedure sql step took :
          real time : 0.029
          cpu time  : 0.031


    368
    369
    370       proc print data=tst(obs=4);
    371       var film_id rating;
    372       run;quit;
    NOTE: 4 observations were read from "WORK.tst"
    NOTE: Procedure print step took :
          real time : 0.015
          cpu time  : 0.000

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
