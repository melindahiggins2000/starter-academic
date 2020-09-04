---
title: "Create Rmarkdown Document with SAS Code and Output - SAS engine"
author: "Melinda Higgins"
date: '2019-10-01'
slug: create-rmarkdown-document-with-sas-code-and-output-sas-engine
categories:
- R
- SAS
- Rmarkdown
tags:
- R
- SAS
- Rmarkdown
subtitle: ''
summary: ''
authors: []
lastmod: '2020-09-02'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---




## Getting started - SAS Engine for Rmarkdown

To get started using SAS as your statistical software/data processing "engine" take a look at the following article: [http://www.ssc.wisc.edu/~hemken/SASworkshops/Markdown/SASmarkdown.html](http://www.ssc.wisc.edu/~hemken/SASworkshops/Markdown/SASmarkdown.html).

Also read up on the `SASmarkdown` package [https://cran.r-project.org/web/packages/SASmarkdown/](https://cran.r-project.org/web/packages/SASmarkdown/).

## Display the current `knitr` engine

The following Rmarkdown chunk shows the commands to see what are your current `knitr` engine settings.

Be sure to put `{r}` after the 3 backticks ``` to create the R chunk.

` ```{r} `

```
# see what the initial knitr engine settings are
knitr::opts_chunk$get()$engine
knitr::opts_chunk$get()$engine.path
knitr::opts_chunk$get()$engine.opts
```

` ``` `


```
## [1] "R"
```

```
## NULL
```

```
## NULL
```

## Setup the SAS engine

To get started you need:

1. Have SAS installed locally on your machine (i.e. you need a licensed copy)
2. You need to know where on your local drive that your SAS executable is located. Mine is located at `C:\Program Files\SASHome\SASFoundation\9.4\sas.exe`.
3. Install the `SASmarkdown` package [https://cran.r-project.org/web/packages/SASmarkdown/index.html](https://cran.r-project.org/web/packages/SASmarkdown/index.html).
4. Then setup your `knitr` options as follows (type these commands into an R chunk - see next section below):

```
saspath <- "C:/Program Files/SASHome/SASFoundation/9.4/sas.exe"
sasopts <- "-nosplash -linesize 75"
knitr::opts_chunk$set(engine="sashtml", engine.path=saspath, 
        engine.opts=sasopts, comment=NA)
```

## Change settings to use HTML output from SAS

NOTE: You will need to install the `SASmarkdown` package first. For this exercise we're using `engine="sashtml"` which works well when knitting to HTML. However, this format will not work if you knit to PDF or DOC. This leverages the ODS output from SAS.

The R chunk below loads the `SASmarkdown` package, changes the `knitr` engine to `"sashtml"` and runs the `knitr::opts_chunk$get()` commands again to make sure that the engine has been switched from `"R"` to `"sashtml"`.

` ```{r} `

```
# load the SASmarkdown package
library(SASmarkdown)

# set up the options so that knit knows where you SAS executable is
# set the linesize to be easily readable on letter size paper, portrait
# and set the knir options using opts_chunk$set().
saspath <- "C:/Program Files/SASHome/SASFoundation/9.4/sas.exe"
sasopts <- "-nosplash -linesize 75"
knitr::opts_chunk$set(engine="sashtml", engine.path=saspath, 
        engine.opts=sasopts, comment=NA)

# run these commands to convince yourself that
# within this knitr session the engine changed.
knitr::opts_chunk$get()$engine
knitr::opts_chunk$get()$engine.path
knitr::opts_chunk$get()$engine.opts
```

` ``` `


```
## [1] "sashtml"
```

```
## [1] "C:/Program Files/SASHome/SASFoundation/9.4/sas.exe"
```

```
## [1] "-nosplash -linesize 75"
```

## If you want to use SAS but make PDF or DOC files

If you want to knit to PDF or DOC, you should change the engine to `engine="sas"`. This will NOT use ODS output from SAS.

These R chunk commands are provided for reference but not executed here.

```
saspath <- "C:/Program Files/SASHome/SASFoundation/9.4/sas.exe"
sasopts <- "-nosplash -linesize 75"
knitr::opts_chunk$set(engine="sas", engine.path=saspath, 
        engine.opts=sasopts, comment=NA)
```

## Try some `SAS` code

This code chunk below runs the `PROC MEANS` command from SAS using the built in dataset `sashelp.class`.

` ```{r} `

```
proc means data=sashelp.class;
run;
```

` ``` `

<div class="branch">
<a name="IDX"></a>
<div>
<div align="center">
<!--BEGINTABLE--><table class="table" cellspacing="0" cellpadding="7" rules="groups" frame="hsides" summary="Procedure Means: Summary statistics">
<colgroup>
<col>
</colgroup>
<colgroup>
<col>
<col>
<col>
<col>
<col>
</colgroup>
<thead>
<tr>
<th class="l b header" scope="col">Variable</th>
<th class="r b header" scope="col">N</th>
<th class="r b header" scope="col">Mean</th>
<th class="r b header" scope="col">Std Dev</th>
<th class="r b header" scope="col">Minimum</th>
<th class="r b header" scope="col">Maximum</th>
</tr>
</thead>
<tbody>
<tr>
<th class="l stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<th class="l data top_stacked_value">Age</th>
</tr>
<tr>
<th class="l data middle_stacked_value">Height</th>
</tr>
<tr>
<th class="l data bottom_stacked_value">Weight</th>
</tr>
</table></th>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">19</td>
</tr>
<tr>
<td class="r data middle_stacked_value">19</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">19</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">13.3157895</td>
</tr>
<tr>
<td class="r data middle_stacked_value">62.3368421</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">100.0263158</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">1.4926722</td>
</tr>
<tr>
<td class="r data middle_stacked_value">5.1270752</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">22.7739335</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">11.0000000</td>
</tr>
<tr>
<td class="r data middle_stacked_value">51.3000000</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">50.5000000</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">16.0000000</td>
</tr>
<tr>
<td class="r data middle_stacked_value">72.0000000</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">150.0000000</td>
</tr>
</table></td>
</tr>
</tbody>
</table>
<!--ENDTABLE--></div>
</div>
<br>
</div>

## More SAS code 

Here is another example of SAS code chunk using the `PROC CORR` commands to see correlations between the variables in the `sashelp.class` dataset and  visualize the scatterplot matrix.

` ```{r} `

```
proc corr data=sashelp.class plots=matrix;
run;
```

` ``` `

<div class="branch">
<a name="IDX"></a>
<div>
<div align="center">
<!--BEGINTABLE--><table class="table" cellspacing="0" cellpadding="7" rules="groups" frame="hsides" summary="Procedure Corr: Variables Information">
<colgroup>
<col>
</colgroup>
<colgroup>
<col>
</colgroup>
<tbody>
<tr>
<th class="l rowheader" scope="row">3  Variables:</th>
<td class="l data">Age      Height   Weight</td>
</tr>
</tbody>
</table>
<!--ENDTABLE--></div>
</div>
<br>
<a name="IDX1"></a>
<div>
<div align="center">
<!--BEGINTABLE--><table class="table" cellspacing="0" cellpadding="7" rules="groups" frame="hsides" summary="Procedure Corr: Simple Statistics">
<colgroup>
<col>
</colgroup>
<colgroup>
<col>
<col>
<col>
<col>
<col>
<col>
</colgroup>
<thead>
<tr>
<th class="c b header" colspan="7" scope="colgroup">Simple Statistics</th>
</tr>
<tr>
<th class="l b header" scope="col">Variable</th>
<th class="r b header" scope="col">N</th>
<th class="r b header" scope="col">Mean</th>
<th class="r b header" scope="col">Std Dev</th>
<th class="r b header" scope="col">Sum</th>
<th class="r b header" scope="col">Minimum</th>
<th class="r b header" scope="col">Maximum</th>
</tr>
</thead>
<tbody>
<tr>
<th class="l rowheader" scope="row">Age</th>
<td class="r data">19</td>
<td class="r data">13.31579</td>
<td class="r data">1.49267</td>
<td class="r data">253.00000</td>
<td class="r data">11.00000</td>
<td class="r data">16.00000</td>
</tr>
<tr>
<th class="l rowheader" scope="row">Height</th>
<td class="r data">19</td>
<td class="r data">62.33684</td>
<td class="r data">5.12708</td>
<td class="r data">1184</td>
<td class="r data">51.30000</td>
<td class="r data">72.00000</td>
</tr>
<tr>
<th class="l rowheader" scope="row">Weight</th>
<td class="r data">19</td>
<td class="r data">100.02632</td>
<td class="r data">22.77393</td>
<td class="r data">1901</td>
<td class="r data">50.50000</td>
<td class="r data">150.00000</td>
</tr>
</tbody>
</table>
<!--ENDTABLE--></div>
</div>
<br>
<a name="IDX2"></a>
<div>
<div align="center">
<!--BEGINTABLE--><table class="table" cellspacing="0" cellpadding="7" rules="groups" frame="hsides" summary="Procedure Corr: Pearson Correlations">
<colgroup>
<col>
</colgroup>
<colgroup>
<col>
<col>
<col>
</colgroup>
<thead>
<tr>
<th class="c b header" colspan="4" scope="colgroup">Pearson Correlation Coefficients, N = 19 <br/>Prob &gt; |r| under H0: Rho=0</th>
</tr>
<tr>
<th class="c headerempty" scope="col"> </th>
<th class="r b header" scope="col">Age</th>
<th class="r b header" scope="col">Height</th>
<th class="r b header" scope="col">Weight</th>
</tr>
</thead>
<tbody>
<tr>
<th class="l rowheader" scope="row">Age</th>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">1.00000</td>
</tr>
<tr>
<td class="r data bottom_stacked_value"> </td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">0.81143</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">&lt;.0001</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">0.74089</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">0.0003</td>
</tr>
</table></td>
</tr>
<tr>
<th class="l rowheader" scope="row">Height</th>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">0.81143</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">&lt;.0001</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">1.00000</td>
</tr>
<tr>
<td class="r data bottom_stacked_value"> </td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">0.87779</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">&lt;.0001</td>
</tr>
</table></td>
</tr>
<tr>
<th class="l rowheader" scope="row">Weight</th>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">0.74089</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">0.0003</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">0.87779</td>
</tr>
<tr>
<td class="r data bottom_stacked_value">&lt;.0001</td>
</tr>
</table></td>
<td class="r stacked_cell data"><table width="100%" border="0" cellpadding="7" cellspacing="0">
<tr>
<td class="r data top_stacked_value">1.00000</td>
</tr>
<tr>
<td class="r data bottom_stacked_value"> </td>
</tr>
</table></td>
</tr>
</tbody>
</table>
<!--ENDTABLE--></div>
</div>
<br>
<a name="IDX3"></a>
<div>
<div  class="c">
<img alt="Scatter Plot Matrix" src="unnamed-chunk-5.png" style=" height: 640px; width: 640px;" border="0" class="c">
</div>
</div>
<br>
</div>

## Reset engine to R

While this is great using SAS, if you want to switch back to using R within the same Rmarkdown document, within the same `knitr` session, you'll need to tell `knitr` that you are switching engines.

To get this next chunk to run, you'll need to reset the `knitr` engine within the chunk options directly and then use the command `knitr::opts_chunk$set(engine="R", engine.path=NULL, engine.opts=NULL, comment=NA)` to reset back to R.

Be sure to put `{r, engine='R'}` after the 3 backticks ``` to set this R chunk back to the R engine.

` ```{r, engine='R'} `

```
# this chunk has the engine set back to `R`

# run a short bit of r code
# scatterplot of cars dataset
plot(cars)

# check the current engine
knitr::opts_chunk$get()$engine

# reset the engine globally (i.e. so it will work outside of
# this chunk so you don't have to keep typing engine=`R`)
knitr::opts_chunk$set(engine="R",  engine.path=NULL, 
        engine.opts=NULL, comment=NA)

# confirm that this change was applied
knitr::opts_chunk$get()$engine
knitr::opts_chunk$get()$engine.path
knitr::opts_chunk$get()$engine.opts
```

` ``` `

<img src="/post/2019-10-01-create-rmarkdown-document-with-sas-code-and-output-sas-engine/index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```
[1] "sashtml"
```

```
[1] "R"
```

```
NULL
```

```
NULL
```

...and here is another R chunk with no engine defined but the engine was switched back to R in the previous chunk.

` ```{r} `

```
# this chunk didn't list the engine explicitly, so let's
# make sure the global change carried over into this chunk
knitr::opts_chunk$get()$engine

# and some more R code
# simple linear regression of distance by speed
# for cars dataset
summary(lm(dist ~ speed, data = cars))
```

` ``` `


```
[1] "R"
```

```

Call:
lm(formula = dist ~ speed, data = cars)

Residuals:
    Min      1Q  Median      3Q     Max 
-29.069  -9.525  -2.272   9.215  43.201 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) -17.5791     6.7584  -2.601   0.0123 *  
speed         3.9324     0.4155   9.464 1.49e-12 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 15.38 on 48 degrees of freedom
Multiple R-squared:  0.6511,	Adjusted R-squared:  0.6438 
F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12
```

Good luck creating documents with Rmarkdown for SAS code and output.

#### Read more on R and SAS

* [R-Bloggers](https://www.r-bloggers.com/) 
* [PROC-X SAS Bloggers](http://www.proc-x.com/)
