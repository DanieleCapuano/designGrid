#DesignGrid
Given the description of a design (e.g. made in photoshop, illustrator or whatever), made of reference width/height, and a list of pixel values describing where to place columns and rows, DesignGrid generates a css file with this grid system and several helper css classes.

#Reasons
*"Why another css grid system generator? I can use Bootstrap!"*.
Yes of course. Actually most of the time you should...But...

One of the things you learnt at design school is that grid systems aren't so rigid as css frameworks let them appear. The base column isn't necessarily fixed-width for example, but it can vary depending of your design concept, so you can have a 12px-wide first column and a 173px-wide second column.

It's a richness! Why should I bother myself with a fixed column width and multiples of it?

**DesignGrid** allows you to start from your design, taking the design-specific columns and rows measures (widths/heights, vertical/horizontal gutters, etc); and then it converts such measures to percentages in a fluid 100%-based css layout.

#How to use DesignGrid
Design grid is based on Sass and Compass. [Here](http://thesassway.com/beginner/getting-started-with-sass-and-compass) there's a tutorial to configure your base environment.

After you have Sass and Compass installed and configured, you can start configuring you grid system.

#Configuration
DesignGrid uses the Sass partial called *_dg-config.scss*. Here a $gridConfig variable is stored, which is a map where each key is a *max-width* directive to be used in a *@media screen* rule, except for the *default* key which represents the grid configuration to use as default.

The current configuration file contains an example of a possible grid, where a single default and a @media rule is given (for *max-width:500px*).

##Configuration reference
For each max-width rule (*default* is used for no "@media screen" rules) the following keys are available:
* prefix: a string representing the prefix which will be given to the current ruleset. If you use "foo" as the prefix for the *@media screen and (max-width: 500px)* ruleset, you will get rules such as *.dg-foo-col-x-1*
* designWidth: the width of the original design drawing
* designHeight: the width of the original design drawing
* ncols: the number of columns
* nrows: the number of rows
* colsWidths: a list with the columns widths in pixels measured from the design drawing
* rowsHeights: a list with the rows heights (baseline grid) in pixels measured from the design drawing
* colsGutters: a list with the widths of gutters between columns, in pixels, as measured from the design drawing, 0px for no gutter
* rowsGutters: a list with the heights of gutters between rows, in pixels, as measured from the design drawing, 0px for no gutter

#Using DesignGrid
After you filled the configuration, you can start programming using the grid. The *index.html* and *sass/grid1.scss* files give a possible example of a page which simply displays the grid.

The following css classes are created by DesignGrid:
* *< prefix >*-*< type >*-*< index >*, where *prefix* is either *dg* for the default ruleset or *dg-* + "anything you specified as *prefix* in the configuration file" (see above); *type* is either "col" for columns or "row" for rows; and *index* is the incremental index of the element (row/column).

    For example, you can have the rule *dg-col-1* which defines the first column of the grid system (width specified in percentage value). This class generates rows or columns which are extended just as much as the calculation results for the single row or column: in other words, *dg-col-2* doesn't give a column which is wide *dg-col-1 + < gutter-1-2 > + dg-col-2*, but instead gives a column simply wide as *dg-col-2*;

* *< prefix >*-extended-*< type >*-*< index >*, where *prefix* is either *dg* for the default ruleset or *dg-* + "anything you specified as *prefix* in the configuration file" (see above); *type* is either "col" for columns or "row" for rows; and *index* is the incremental index of the element (row/column). For example, you can have the rule *dg-extended-col-2* which defines a column of the grid system which is as wide as *dg-col-1 + < gutter-1-2 > + dg-col-2*;

        Example: .dg-extended-col-2

* *< prefix >*-[x|y]-[col|row]-*< index >*, where *prefix* is either *dg* for the default ruleset or *dg-* + "anything you specified as *prefix* in the configuration file" (see above); and *index* is the incremental index of a [column|row]. This rule gives the [x|y]-coordinate of the starting point of the "index"-th [column|row];

        Example: .dg-x-col-2, .dg-y-row-3

* *< prefix >*-[x|y]-[col|row]-*< index >*-end, where *prefix* is either *dg* for the default ruleset or *dg-* + "anything you specified as *prefix* in the configuration file" (see above); and *index* is the incremental index of a [column|row]. This rule gives the [x|y]-coordinate of the end point of the "index"-th [column|row] (without gutter);

        Example: .dg-x-col-2-end, .dg-y-row-3-end

* *< prefix >*-ext-[col|row]-fromto-*< index1 >*-*< index2 >*, where *prefix* is either *dg* for the default ruleset or *dg-* + "anything you specified as *prefix* in the configuration file" (see above); *index1* is the starting point and *index2* is the end point. This rule gives an element which goes from the element at *index1* to the starting point of the element at *index2*

        Example: .dg-ext-col-fromto-2-5

* *< prefix >*-ext-[col|row]-fromto-*< index1 >*-*< index2 >*-end, where *prefix* is either *dg* for the default ruleset or *dg-* + "anything you specified as *prefix* in the configuration file" (see above); *index1* is the starting point and *index2* is the end point. This rule gives an element which goes from the element at *index1* to the end point of the element at *index2*

        Example: .dg-ext-col-fromto-2-5-end
