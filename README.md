    %let pgm=utl-running-your-matlab-script-in-the-altair-slc-motion-damped-spring;

    %stop_submission;

    Running your matlab script in the altair slc motion damped spring

    Too long to post in listserv, see github

    github
    https://github.com/rogerjdeangelis/utl-running-your-matlab-script-in-the-altair-slc-motion-damped-spring

    Graphical soluton from matlab for motion of a dampled sprint a damped spring.
    https://github.com/rogerjdeangelis/utl-running-your-matlab-script-in-the-altair-slc-motion-damped-spring/blob/main/matllab.png

    Python sympy can also solve this problem.

    Sandwich macros on end, in this report and in
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories
    You neeed to save the sandwich macros in your autocall library, seeend of this post.

    Without seeing your matlab script here is way to run a matlab script using the Altair slc.
    Note Octave is a free 'clone' of matlab

    community.altair.com
    https://community.altair.com/discussion/64536/is-it-possible-to-couple-altair-flux-with-a-matlab-script?tab=all#latest

    CONTENTS
      1 run matlab script
      2 macros to autocall
      3 related repose

    More detail
    https://github.com/rogerjdeangelis/utl-octave-sympy-solving-second-order-differential-equation-ode-of-motion-for-the-damped-spring

    /******************************************************************************************************************************/
    /* INPUT                          | PROCESS                                        | OUTPUT                                   */
    /* =====                          | =======                                        | ======                                   */
    /*         2                      |                                                |                                          */
    /*       d         d              | 1 MATLAB                                       | Plot hires https://tinyurl.com/5kjyaz6v  /
    /*  y=m*---x(t)+c*--x(t)+k*x(t)   | =========                                      |                                          */
    /*        2       dt              |                                                |                  TIME                    */
    /*      dt                        | %utl_slc_mbegin;                               |       1  2  3  4  5  6  7  8  9 10       */
    /*                                | parmcards4;                                    |    --+--+--+--+--+--+--+--+--+--+--      */
    /*  Boundary conditions           | function dydt = damped_spring_rhs(t, y)        | Y |        2                       |     */
    /*                                |  m = 1;                                        |   |      d         d               |     */
    /*  m=1   Solution                |  c = 0.5;                                      |   | y=m*---x(t)+c*--x(t)+k*x(t)    |     */
    /*  c=.5  y=0.126*sin(2*t) +      |  k = 2;                                        |   |       2       dt               |     */
    /*  k=2    cos(2*t)*exp(-0.25*t); |  dydt = zeros(2,1);                            |   |     dt                         |     */
    /*                                |  dydt(1) = y(2);                               |   |                                |     */
    /*                                |  dydt(2) = -(c/m)*y(2) - (k/m)*y(1);           |   | Boundary conditions            |     */
    /*                                | end                                            |   |                                |     */
    /*                                |                                                |   | m=1    Solution                |     */
    /*                                | % Initial conditions                           |   | c=.5   y=0.126*sin(2*t) +      |     */
    /*                                | y0 = [1; 0];   % x(0) = 1, x'(0) = 0           |   | k=2     cos(2*t)*exp(-0.25*t); |     */
    /*                                |                                                |   |                                |     */
    /*                                | % Time span                                    | Y |--------------------------------| Y   */
    /*                                | tspan = [0 10];                                |   |                                |     */
    /*                                |                                                | .6+                                + .6  */
    /*                                | % Solve ODE                                    |   |                                |     */
    /*                                | [t, y] = ode45(@damped_spring_rhs, tspan, y0); |   |                                |     */
    /*                                |                                                |   |       **                       |     */
    /*                                | % Plot results                                 | .4+       ***                      + .4  */
    /*                                | plot(t, y(:,1), 'b-', 'LineWidth', 2);         |   |       * *                      |     */
    /*                                | xlabel('Time');                                |   |      *  *                      |     */
    /*                                | ylabel('Displacement x(t)');                   |   |      *  *       **             |     */
    /*                                | title('Damped Spring-Mass System');            | .2+      *  **      ***            + .2  */
    /*                                | grid on;                                       |   |      *   *     *  *       ***  |     */
    /*                                | print('d:/png/matllab.png', '-dpng');          |   |      *   *     *  **     ** *  |     */
    /*                                | ;;;;                                           |   |      *   *    **   *     *   * |     */
    /*                                | %utl_slc_mend;                                 | .0+     *    *    *    *    *    * + .0  */
    /*                                |                                                |   |          **   *     *   *     *|     */
    /*                                |                                                |   |     *     *   *     *  *      *|     */
    /*                                |                                                |   |     *     *  *      ****       |     */
    /*                                |                                                |-.2+ *   *     *  *       **        +-.2  */
    /*                                |                                                |   |     *      ***                 |     */
    /*                                |                                                |   | *   *      **                  |     */
    /*                                |                                                |   | *  *                           |     */
    /*                                |                                                |-.4+ *  *  SOLUTION                 +-.4  */
    /*                                |                                                |   |  * *   y=0.126*sin(2*t) +      |     */
    /*                                |                                                |   |  * *    cos(2*t)*exp(-0.25*t)  |     */
    /*                                |                                                |   |  * *                           |     */
    /*                                |                                                |-.6+  * *                           +-.6  */
    /*                                |                                                |   |  **                            |     */
    /*                                |                                                |   |   *                            |     */
    /*                                |                                                |   |                                |     */
    /*                                |                                                |-.8+                                +-.8  */
    /*                                |                                                |   |                                |     */
    /*                                |                                                |   --+--+--+--+--+--+--+--+--+--+----     */
    /*                                |                                                |     1  2  3  4  5  6  7  8  9 10         */
    /*                                |                                                |                 TIME                     */
    /*                                |                                                |                                          */
    /*                                |                                                |------------------------------------------*/
    /******************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    /******************************************************************************************************************************/
    /* INPUT                                                                                                                      */
    /* =====                                                                                                                      */
    /*         2                                                                                                                  */
    /*       d         d                                                                                                          */
    /*  y=m*---x(t)+c*--x(t)+k*x(t)                                                                                               */
    /*        2       dt                                                                                                          */
    /*      dt                                                                                                                    */
    /*                                                                                                                            */
    /*  Boundary conditions                                                                                                       */
    /*                                                                                                                            */
    /*  m=1                                                                                                                       */
    /*  c=.5                                                                                                                      */
    /*  k=2                                                                                                                       */
    /******************************************************************************************************************************/
    /*                                      _   _       _                    _       _
    / |  _ __ _   _ _ __    _ __ ___   __ _| |_| | __ _| |__   ___  ___ _ __(_)_ __ | |_
    | | | `__| | | | `_ \  | `_ ` _ \ / _` | __| |/ _` | `_ \ / __|/ __| `__| | `_ \| __|
    | | | |  | |_| | | | | | | | | | | (_| | |_| | (_| | |_) |\__ \ (__| |  | | |_) | |_
    |_| |_|   \__,_|_| |_| |_| |_| |_|\__,_|\__|_|\__,_|_.__/ |___/\___|_|  |_| .__/ \__|
                                                                              |_|
    */

    %utlfkil(d:/png/matllab.png);

    %utl_slc_mbegin;
    cards4;
    function dydt = damped_spring_rhs(t, y)
     m = 1;
     c = 0.5;
     k = 2;
     dydt = zeros(2,1);
     dydt(1) = y(2);
     dydt(2) = -(c/m)*y(2) - (k/m)*y(1);
    end

    % Initial conditions
    y0 = [1; 0];   % x(0) = 1, x'(0) = 0

    % Time span
    tspan = [0 10];

    % Solve ODE
    [t, y] = ode45(@damped_spring_rhs, tspan, y0);

    % Plot results
    plot(t, y(:,1), 'b-', 'LineWidth', 2);
    xlabel('Time');
    ylabel('Displacement x(t)');
    title('Damped Spring-Mass System');
    grid on;
    print('d:/png/matllab.png', '-dpng');
    ;;;;
    %utl_slc_mend;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    Graphical soluton from matlab for motion of a dampled sprint a damped spring.
    https://github.com/rogerjdeangelis/utl-running-your-matlab-script-in-the-altair-slc-motion-damped-spring/blob/main/matllab.png

    /*___
    |___ \   _ __ ___   __ _  ___ _ __ ___  ___
      __) | | `_ ` _ \ / _` |/ __| `__/ _ \/ __|
     / __/  | | | | | | (_| | (__| | | (_) \__ \
    |_____| |_| |_| |_|\__,_|\___|_|  \___/|___/

    copy to autocall library
    */

    /*---- autocall library c:/wpsoto ----*/

    data _null_;
      file "c:/wpsoto/utl_slc_mbegin.sas";
      input;
      put _infile_;
    cards4;
    %macro utl_slc_mbegin;
    %utlfkil(c:/temp/m_pgm.m);
    %utlfkil(c:/temp/m_pgm.log);
    data _null_;
     infile cards4 ;
     file "c:/temp/m_pgm.m";
     input;
     put _infile_;
    %mend utl_slc_mbegin;
    ;;;;
    run;quit;

    data _null_;
      file "c:/wpsoto/utl_slc_mend.sas";
      input;
      put _infile_;
    cards4;
    %macro utl_slc_mend(returnvar=N);
    options noxwait noxsync;
    filename rut pipe  "octave-cli c:/temp/m_pgm.m > c:/temp/m_pgm.log";
    run;quit;
      data _null_;
        file print;
        infile rut recfm=v lrecl=32756;
        input;
        put _infile_;
        putlog _infile_;
      run;
      filename ft15f001 clear;
      * use the clipboard to create macro variable;
      %if &returnVar. ne N %then %do;
        filename clp clipbrd ;
        data _null_;
         length txt $200;
         infile clp;
         input;
         putlog "macro variable &returnVar = " _infile_;
         call symputx("&returnVar.",_infile_,"G");
        run;quit;
      %end;
    data _null_;
      file print;
      infile "c:/temp/m_pgm.log" ;
      input;
      put _infile_;
      putlog _infile_;
    run;quit;
    filename ft15f001 clear;
    %mend utl_slc_mend;
    ;;;;
    run;quit;

    /*____            _       _           _
    |___ /   _ __ ___| | __ _| |_ ___  __| |  _ __ ___ _ __   ___  ___
      |_ \  | `__/ _ \ |/ _` | __/ _ \/ _` | | `__/ _ \ `_ \ / _ \/ __|
     ___) | | | |  __/ | (_| | ||  __/ (_| | | | |  __/ |_) | (_) \__ \
    |____/  |_|  \___|_|\__,_|\__\___|\__,_| |_|  \___| .__/ \___/|___/
                                                      |_|
    */

    MATLAB

    --------------------------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-convert-a-sqlite-numeric-table-to-a-matrix-for-octave-matlab-processing
    https://github.com/rogerjdeangelis/utl-cumulative-sum-by-group-in-the-order-of-rank-variable-sas-and-sql-r-python-octave-excel
    https://github.com/rogerjdeangelis/utl-how-to-store-octave-matlab-objects-in-external-files-for-later-use-with-octave-r-and-python
    https://github.com/rogerjdeangelis/utl-matlab-select-all-possible-pairs-and-and-use-octave-sqlwrite-to-return-values-to-sas
    https://github.com/rogerjdeangelis/utl-octave-matlab-check-if-all-of-the-rows-of-a-dbtable-are-the-same
    https://github.com/rogerjdeangelis/utl-octave-matlab-deleting-rows-where-age-is-zero
    https://github.com/rogerjdeangelis/utl-octave-sympy-solving-second-order-differential-equation-ode-of-motion-for-the-damped-spring
    https://github.com/rogerjdeangelis/utl-runing-a-regression-using-matlab-syntax-using-the-open-source-r-octave-package
    https://github.com/rogerjdeangelis/utl-add-sqlite-windows-functions-to-octave-sqlite-temporary-solition-until-put-in-octave-forge

    SYMPY
    -------------------------------------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-area-between-curves-with-an-intersection-point-adding-negative-and-positive-areas-plot-sympy
    https://github.com/rogerjdeangelis/utl-calculating-the-cube-root-of-minus-one-with-drop-down-to-python-symbolic-math-sympy
    https://github.com/rogerjdeangelis/utl-closed-form-solution-for-sample-size-in-a-clinical-equlivalence-trial-using-r-and-sas-and-sympy
    https://github.com/rogerjdeangelis/utl-distance-between-a-point-and-curve-in-sql-and-wps-pythony-r-sympy
    https://github.com/rogerjdeangelis/utl-fun-with-sympy-infinite-series-and-integrals-to-define-common-functions-and-constants
    https://github.com/rogerjdeangelis/utl-maximum-likelihood-estimate-of--therate-parameter-lamda-of-a-Poisson-distribution-sympy
    https://github.com/rogerjdeangelis/utl-maximum-liklihood-regresssion-wps-python-sympy
    https://github.com/rogerjdeangelis/utl-mle-symbolic-solution-for-mu-and-sigma-of-normal-pdf-using-sympy
    https://github.com/rogerjdeangelis/utl-python-sympy-projection-of-the-intersection-of-two-parabolic-surfaces-onto-the-xy-plane-AI
    https://github.com/rogerjdeangelis/utl-r-python-compute-the-area-between-two-curves-AI-sympy-trapezoid
    https://github.com/rogerjdeangelis/utl-roots-of-a-non-linear-function-using-python-sympy
    https://github.com/rogerjdeangelis/utl-solve-a-system-of-simutaneous-equations-r-python-sympy
    https://github.com/rogerjdeangelis/utl-symbolic-algebraic-simplification-of-a-polynomial-expressions-sympy
    https://github.com/rogerjdeangelis/utl-symbolic-solution-for-the-gradient-of-the-cumulative-bivariate-normal-using-erf-and-sympy
    https://github.com/rogerjdeangelis/utl-symbolically-solve-for-the-mean-and-variance-of-normal-density-using-expected-values-in-SymPy
    https://github.com/rogerjdeangelis/utl-sympy-exact-pdf-and-cdf-for-the-correlation-coefficient-given-bivariate-normals
    https://github.com/rogerjdeangelis/utl-sympy-technique-for-symbolic-integration-of-bivariate-density-function
    https://github.com/rogerjdeangelis/utl-using-python-sympy-for-mathematical-characterization-of-the-human-face
    https://github.com/rogerjdeangelis/utl-vertical-distance-covered-by-a-bouncing-ball-for-infinite-number-of-bounces-using-sympy

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
