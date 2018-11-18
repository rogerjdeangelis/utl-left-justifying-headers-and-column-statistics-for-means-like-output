# utl-left-justifying-headers-and-column-statistics-for-means-like-output
Left justifying headers and column statistics for means like output.

    Left justifying headers and column statistics for means like output

    Not exactly a response but perhaps more flexible and easier than templates?

    Just repalce proc means with proc replace;

    for pdf output
    https://tinyurl.com/ybf7vrjd

    github
    https://tinyurl.com/yan2nhhv
    https://github.com/rogerjdeangelis/utl-left-justifying-headers-and-column-statistics-for-means-like-output

    https://tinyurl.com/ydahp6kw
    https://communities.sas.com/t5/ODS-and-Base-Reporting/proc-freq-and-proc-means-imbedded-in-ods/m-p/514238

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories


    INPUT
    =====

    sashelp.class

    Proc Means standard output - this is the problem

      N     Median   Min   Max   Q1   Q3   Range
     19         13    11    16   12   15       5


    EXAMPLE OUTPUT (left justified headers and column statistics)
    --------------------------------------------------------------

     N     Median    Min   Max   Q1   Q3   Range
     19    13        11    16    12   15   5


    PROCESS
    =======

    %array(stats,values=N Median Min Max Q1 Q3 Range);

    ods pdf file=
     "d:/pdf/utl-left-justifying-headers-and-column-statistics-for-means-like-output.pdf";

    proc report data=sashelp.class list
         style(header)={just=left}  style(column)={just=left};

    cols %do_over(stats,phrase=%str(age=?));

    %do_over(stats,phrase=%str(define ? / ? "?";));

    run;quit;

    ods pdf close;


    /* generated code (cut and paste if uncomfortable with do_over in production)
    see log

    COLUMN  ( AGE=N AGE=Median AGE=Min AGE=Max AGE=Q1 AGE=Q3 AGE=Range );

    DEFINE  N / N  "N" ;
    DEFINE  Median / MEDIAN  "Median" ;
    DEFINE  Min / MIN "Min" ;
    DEFINE  Max / MAX "Max" ;
    DEFINE  Q1 / Q1  "Q1" ;
    DEFINE  Q3 / Q3  "Q3" ;
    DEFINE  Range / RANGE  "Range" ;
    */

    *                _          _                   _
     _ __ ___   __ _| | _____  (_)_ __  _ __  _   _| |_
    | '_ ` _ \ / _` | |/ / _ \ | | '_ \| '_ \| | | | __|
    | | | | | | (_| |   <  __/ | | | | | |_) | |_| | |_
    |_| |_| |_|\__,_|_|\_\___| |_|_| |_| .__/ \__,_|\__|
                                       |_|
    ;

    * output with the issue.
    * replace means with proc report;
    proc means data=sashelp.class;
    var age;
    run;quit;

