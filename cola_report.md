cola Report for recount2:SRP041885
==================

**Date**: 2019-12-26 00:12:34 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 15884    53
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:skmeans](#SD-skmeans)   |          3| 1.000|           1.000|       1.000|** |2          |
|[SD:mclust](#SD-mclust)     |          3| 1.000|           1.000|       1.000|** |           |
|[SD:NMF](#SD-NMF)           |          3| 1.000|           1.000|       0.999|** |2          |
|[CV:hclust](#CV-hclust)     |          6| 1.000|           0.989|       0.992|** |3,5        |
|[CV:kmeans](#CV-kmeans)     |          3| 1.000|           0.972|       0.971|** |           |
|[MAD:skmeans](#MAD-skmeans) |          3| 1.000|           1.000|       1.000|** |2          |
|[MAD:pam](#MAD-pam)         |          3| 1.000|           1.000|       1.000|** |2          |
|[MAD:mclust](#MAD-mclust)   |          3| 1.000|           1.000|       1.000|** |2          |
|[MAD:NMF](#MAD-NMF)         |          3| 1.000|           1.000|       1.000|** |2          |
|[ATC:hclust](#ATC-hclust)   |          3| 1.000|           1.000|       1.000|** |2          |
|[ATC:pam](#ATC-pam)         |          6| 1.000|           0.988|       0.987|** |2,3,5      |
|[ATC:mclust](#ATC-mclust)   |          5| 1.000|           0.923|       0.971|** |2,3        |
|[ATC:NMF](#ATC-NMF)         |          3| 1.000|           1.000|       1.000|** |2          |
|[ATC:skmeans](#ATC-skmeans) |          4| 0.956|           0.961|       0.968|** |2,3        |
|[SD:hclust](#SD-hclust)     |          5| 0.956|           0.973|       0.975|** |2,3        |
|[CV:NMF](#CV-NMF)           |          5| 0.951|           0.936|       0.950|** |2,3        |
|[MAD:hclust](#MAD-hclust)   |          6| 0.934|           0.940|       0.958|*  |2,3,5      |
|[CV:mclust](#CV-mclust)     |          4| 0.923|           0.841|       0.904|*  |2,3        |
|[SD:pam](#SD-pam)           |          5| 0.922|           0.866|       0.896|*  |2,3        |
|[CV:skmeans](#CV-skmeans)   |          4| 0.915|           0.971|       0.921|*  |2,3        |
|[CV:pam](#CV-pam)           |          6| 0.901|           0.948|       0.927|*  |2,3,5      |
|[ATC:kmeans](#ATC-kmeans)   |          3| 0.804|           0.947|       0.908|   |           |
|[SD:kmeans](#SD-kmeans)     |          3| 0.782|           0.960|       0.915|   |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 0.495|           0.955|       0.911|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; CV:NMF      2 1.000           0.972       0.987          0.508 0.491   0.491
#&gt; MAD:NMF     2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; ATC:NMF     2 1.000           0.974       0.982          0.224 0.795   0.795
#&gt; SD:skmeans  2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; CV:skmeans  2 1.000           1.000       1.000          0.510 0.491   0.491
#&gt; MAD:skmeans 2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; ATC:skmeans 2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; SD:mclust   2 0.853           0.823       0.940          0.502 0.492   0.492
#&gt; CV:mclust   2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; MAD:mclust  2 1.000           0.998       0.999          0.501 0.499   0.499
#&gt; ATC:mclust  2 1.000           0.998       0.999          0.505 0.495   0.495
#&gt; SD:kmeans   2 0.495           0.920       0.859          0.409 0.499   0.499
#&gt; CV:kmeans   2 0.491           0.909       0.872          0.438 0.491   0.491
#&gt; MAD:kmeans  2 0.495           0.955       0.911          0.443 0.499   0.499
#&gt; ATC:kmeans  2 0.495           0.920       0.859          0.409 0.499   0.499
#&gt; SD:pam      2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; CV:pam      2 1.000           0.997       0.998          0.510 0.491   0.491
#&gt; MAD:pam     2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; ATC:pam     2 1.000           1.000       1.000          0.501 0.499   0.499
#&gt; SD:hclust   2 1.000           1.000       1.000          0.205 0.795   0.795
#&gt; CV:hclust   2 0.493           0.836       0.880          0.280 0.795   0.795
#&gt; MAD:hclust  2 1.000           1.000       1.000          0.205 0.795   0.795
#&gt; ATC:hclust  2 1.000           1.000       1.000          0.205 0.795   0.795
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 1.000           1.000       0.999          0.206 0.896   0.791
#&gt; CV:NMF      3 1.000           1.000       1.000          0.192 0.891   0.781
#&gt; MAD:NMF     3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; ATC:NMF     3 1.000           1.000       1.000          1.700 0.599   0.496
#&gt; SD:skmeans  3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; CV:skmeans  3 1.000           1.000       1.000          0.188 0.891   0.781
#&gt; MAD:skmeans 3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; ATC:skmeans 3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; SD:mclust   3 1.000           1.000       1.000          0.205 0.891   0.781
#&gt; CV:mclust   3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; MAD:mclust  3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; ATC:mclust  3 1.000           1.000       1.000          0.199 0.900   0.798
#&gt; SD:kmeans   3 0.782           0.960       0.915          0.430 0.896   0.791
#&gt; CV:kmeans   3 1.000           0.972       0.971          0.345 0.891   0.781
#&gt; MAD:kmeans  3 0.782           0.946       0.901          0.340 0.896   0.791
#&gt; ATC:kmeans  3 0.804           0.947       0.908          0.452 0.896   0.791
#&gt; SD:pam      3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; CV:pam      3 1.000           0.950       0.972          0.144 0.891   0.781
#&gt; MAD:pam     3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; ATC:pam     3 1.000           1.000       1.000          0.208 0.896   0.791
#&gt; SD:hclust   3 1.000           1.000       1.000          1.948 0.599   0.496
#&gt; CV:hclust   3 1.000           0.980       0.986          1.126 0.599   0.496
#&gt; MAD:hclust  3 1.000           1.000       1.000          1.948 0.599   0.496
#&gt; ATC:hclust  3 1.000           1.000       1.000          1.948 0.599   0.496
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.993           0.996       0.963         0.0104 0.993   0.983
#&gt; CV:NMF      4 1.000           0.996       0.996         0.0129 0.993   0.983
#&gt; MAD:NMF     4 1.000           0.999       0.998         0.0112 0.993   0.983
#&gt; ATC:NMF     4 0.993           0.985       0.978         0.0073 1.000   1.000
#&gt; SD:skmeans  4 0.876           0.893       0.912         0.1227 0.922   0.801
#&gt; CV:skmeans  4 0.915           0.971       0.921         0.0903 0.922   0.801
#&gt; MAD:skmeans 4 0.890           0.882       0.898         0.0778 1.000   1.000
#&gt; ATC:skmeans 4 0.956           0.961       0.968         0.1157 0.922   0.801
#&gt; SD:mclust   4 1.000           1.000       1.000         0.0110 0.993   0.983
#&gt; CV:mclust   4 0.923           0.841       0.904         0.0791 0.945   0.860
#&gt; MAD:mclust  4 1.000           1.000       1.000         0.0108 0.993   0.983
#&gt; ATC:mclust  4 0.831           0.911       0.875         0.1383 0.922   0.801
#&gt; SD:kmeans   4 0.642           0.646       0.829         0.1532 0.956   0.890
#&gt; CV:kmeans   4 0.747           0.857       0.888         0.1127 1.000   1.000
#&gt; MAD:kmeans  4 0.642           0.824       0.832         0.1344 1.000   1.000
#&gt; ATC:kmeans  4 0.674           0.903       0.830         0.1326 0.904   0.757
#&gt; SD:pam      4 1.000           1.000       1.000         0.0108 0.993   0.983
#&gt; CV:pam      4 1.000           1.000       1.000         0.0494 0.993   0.983
#&gt; MAD:pam     4 1.000           1.000       1.000         0.0108 0.993   0.983
#&gt; ATC:pam     4 0.898           0.940       0.929         0.0478 0.993   0.983
#&gt; SD:hclust   4 1.000           1.000       1.000         0.0108 0.993   0.983
#&gt; CV:hclust   4 1.000           1.000       1.000         0.0297 0.993   0.983
#&gt; MAD:hclust  4 1.000           1.000       1.000         0.0108 0.993   0.983
#&gt; ATC:hclust  4 1.000           0.984       0.984         0.0216 0.993   0.983
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.993           0.970       0.953         0.0253 1.000   1.000
#&gt; CV:NMF      5 0.951           0.936       0.950         0.0716 0.954   0.882
#&gt; MAD:NMF     5 0.963           0.973       0.970         0.0228 1.000   1.000
#&gt; ATC:NMF     5 0.785           0.856       0.853         0.0979 0.993   0.983
#&gt; SD:skmeans  5 0.804           0.938       0.907         0.0737 0.948   0.835
#&gt; CV:skmeans  5 0.807           0.898       0.885         0.0776 0.993   0.979
#&gt; MAD:skmeans 5 0.797           0.827       0.802         0.0814 0.889   0.719
#&gt; ATC:skmeans 5 0.856           0.905       0.925         0.0586 0.967   0.897
#&gt; SD:mclust   5 0.836           0.851       0.902         0.1125 0.954   0.882
#&gt; CV:mclust   5 0.773           0.810       0.810         0.1133 0.868   0.618
#&gt; MAD:mclust  5 0.814           0.861       0.909         0.1033 1.000   1.000
#&gt; ATC:mclust  5 1.000           0.923       0.971         0.1247 0.913   0.725
#&gt; SD:kmeans   5 0.723           0.719       0.751         0.0795 0.913   0.764
#&gt; CV:kmeans   5 0.736           0.804       0.776         0.0888 0.922   0.801
#&gt; MAD:kmeans  5 0.738           0.577       0.724         0.0827 0.956   0.890
#&gt; ATC:kmeans  5 0.748           0.832       0.810         0.0803 1.000   1.000
#&gt; SD:pam      5 0.922           0.866       0.896         0.1402 0.904   0.753
#&gt; CV:pam      5 1.000           0.992       0.996         0.1300 0.922   0.798
#&gt; MAD:pam     5 0.793           0.819       0.878         0.1212 1.000   1.000
#&gt; ATC:pam     5 1.000           1.000       1.000         0.1155 0.904   0.753
#&gt; SD:hclust   5 0.956           0.973       0.975         0.0803 0.954   0.882
#&gt; CV:hclust   5 1.000           1.000       1.000         0.0746 0.954   0.882
#&gt; MAD:hclust  5 1.000           0.975       0.986         0.0864 0.954   0.882
#&gt; ATC:hclust  5 0.826           0.900       0.873         0.1261 0.922   0.798
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.851           0.931       0.926         0.0328 1.000   1.000
#&gt; CV:NMF      6 0.843           0.873       0.903         0.0740 1.000   1.000
#&gt; MAD:NMF     6 0.904           0.941       0.947         0.0257 1.000   1.000
#&gt; ATC:NMF     6 0.729           0.753       0.855         0.0480 0.954   0.882
#&gt; SD:skmeans  6 0.808           0.600       0.782         0.0717 0.956   0.835
#&gt; CV:skmeans  6 0.767           0.792       0.825         0.0658 1.000   1.000
#&gt; MAD:skmeans 6 0.775           0.845       0.848         0.0618 0.993   0.977
#&gt; ATC:skmeans 6 0.856           0.956       0.884         0.0819 0.904   0.662
#&gt; SD:mclust   6 0.772           0.834       0.877         0.1077 0.880   0.657
#&gt; CV:mclust   6 0.791           0.877       0.863         0.0315 0.901   0.641
#&gt; MAD:mclust  6 0.736           0.771       0.862         0.0906 0.880   0.692
#&gt; ATC:mclust  6 0.880           0.866       0.902         0.0525 0.949   0.784
#&gt; SD:kmeans   6 0.704           0.649       0.748         0.0611 0.911   0.708
#&gt; CV:kmeans   6 0.706           0.754       0.754         0.0629 0.926   0.766
#&gt; MAD:kmeans  6 0.718           0.680       0.725         0.0585 0.858   0.604
#&gt; ATC:kmeans  6 0.691           0.763       0.788         0.0573 0.915   0.716
#&gt; SD:pam      6 0.806           0.755       0.838         0.0889 0.954   0.844
#&gt; CV:pam      6 0.901           0.948       0.927         0.0826 0.926   0.761
#&gt; MAD:pam     6 0.750           0.491       0.771         0.0766 0.878   0.686
#&gt; ATC:pam     6 1.000           0.988       0.987         0.0686 0.954   0.844
#&gt; SD:hclust   6 0.802           0.794       0.844         0.1028 0.961   0.886
#&gt; CV:hclust   6 1.000           0.989       0.992         0.1130 0.926   0.784
#&gt; MAD:hclust  6 0.934           0.940       0.958         0.0610 0.961   0.886
#&gt; ATC:hclust  6 0.848           0.983       0.966         0.1099 0.904   0.691
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2054 0.795   0.795
#> 3 3 1.000           1.000       1.000         1.9479 0.599   0.496
#> 4 4 1.000           1.000       1.000         0.0108 0.993   0.983
#> 5 5 0.956           0.973       0.975         0.0803 0.954   0.882
#> 6 6 0.802           0.794       0.844         0.1028 0.961   0.886
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     2       0          1  0  1
#&gt; SRR1283407     2       0          1  0  1
#&gt; SRR1283408     2       0          1  0  1
#&gt; SRR1283409     2       0          1  0  1
#&gt; SRR1283410     2       0          1  0  1
#&gt; SRR1283411     2       0          1  0  1
#&gt; SRR1283412     2       0          1  0  1
#&gt; SRR1283413     2       0          1  0  1
#&gt; SRR1283414     2       0          1  0  1
#&gt; SRR1283415     2       0          1  0  1
#&gt; SRR1283416     2       0          1  0  1
#&gt; SRR1283417     2       0          1  0  1
#&gt; SRR1283418     2       0          1  0  1
#&gt; SRR1283419     2       0          1  0  1
#&gt; SRR1283420     2       0          1  0  1
#&gt; SRR1283421     2       0          1  0  1
#&gt; SRR1283422     2       0          1  0  1
#&gt; SRR1283423     2       0          1  0  1
#&gt; SRR1283424     2       0          1  0  1
#&gt; SRR1283425     2       0          1  0  1
#&gt; SRR1283426     2       0          1  0  1
#&gt; SRR1283427     2       0          1  0  1
#&gt; SRR1283428     2       0          1  0  1
#&gt; SRR1283429     2       0          1  0  1
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3 p4    p5
#&gt; SRR1283379     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1283385     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283386     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283387     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1283406     1   0.104      0.946 0.960  0  0  0 0.040
#&gt; SRR1283407     1   0.104      0.946 0.960  0  0  0 0.040
#&gt; SRR1283408     1   0.104      0.946 0.960  0  0  0 0.040
#&gt; SRR1283409     1   0.269      0.849 0.844  0  0  0 0.156
#&gt; SRR1283410     1   0.269      0.849 0.844  0  0  0 0.156
#&gt; SRR1283411     1   0.269      0.849 0.844  0  0  0 0.156
#&gt; SRR1283412     1   0.104      0.946 0.960  0  0  0 0.040
#&gt; SRR1283413     1   0.104      0.946 0.960  0  0  0 0.040
#&gt; SRR1283414     1   0.104      0.946 0.960  0  0  0 0.040
#&gt; SRR1283415     5   0.269      1.000 0.156  0  0  0 0.844
#&gt; SRR1283416     5   0.269      1.000 0.156  0  0  0 0.844
#&gt; SRR1283417     5   0.269      1.000 0.156  0  0  0 0.844
#&gt; SRR1283418     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283419     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283420     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283421     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283422     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283423     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283424     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283425     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283426     1   0.000      0.952 1.000  0  0  0 0.000
#&gt; SRR1283427     1   0.112      0.924 0.956  0  0  0 0.044
#&gt; SRR1283428     1   0.112      0.924 0.956  0  0  0 0.044
#&gt; SRR1283429     1   0.112      0.924 0.956  0  0  0 0.044
#&gt; SRR1283430     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000  1  0  0 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5    p6
#&gt; SRR1283379     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1283380     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1283381     3  0.0000     1.0000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1283385     2  0.0000     0.8290 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1283386     2  0.0000     0.8290 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1283387     2  0.0000     0.8290 0.000 1.000  0 0.000 0.000 0.000
#&gt; SRR1283388     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283389     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283390     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283382     2  0.1327     0.8264 0.000 0.936  0 0.064 0.000 0.000
#&gt; SRR1283383     2  0.1327     0.8264 0.000 0.936  0 0.064 0.000 0.000
#&gt; SRR1283384     2  0.1327     0.8264 0.000 0.936  0 0.064 0.000 0.000
#&gt; SRR1283391     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283392     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283393     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283394     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283395     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283396     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283397     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283398     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283399     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283400     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283401     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283402     2  0.3672     0.7472 0.000 0.632  0 0.368 0.000 0.000
#&gt; SRR1283403     4  0.3672     1.0000 0.000 0.000  0 0.632 0.000 0.368
#&gt; SRR1283404     4  0.3672     1.0000 0.000 0.000  0 0.632 0.000 0.368
#&gt; SRR1283405     4  0.3672     1.0000 0.000 0.000  0 0.632 0.000 0.368
#&gt; SRR1283406     1  0.5011    -0.0179 0.620 0.000  0 0.000 0.264 0.116
#&gt; SRR1283407     1  0.5011    -0.0179 0.620 0.000  0 0.000 0.264 0.116
#&gt; SRR1283408     1  0.5011    -0.0179 0.620 0.000  0 0.000 0.264 0.116
#&gt; SRR1283409     5  0.3717     1.0000 0.384 0.000  0 0.000 0.616 0.000
#&gt; SRR1283410     5  0.3717     1.0000 0.384 0.000  0 0.000 0.616 0.000
#&gt; SRR1283411     5  0.3717     1.0000 0.384 0.000  0 0.000 0.616 0.000
#&gt; SRR1283412     1  0.2003     0.7254 0.884 0.000  0 0.000 0.000 0.116
#&gt; SRR1283413     1  0.2003     0.7254 0.884 0.000  0 0.000 0.000 0.116
#&gt; SRR1283414     1  0.2003     0.7254 0.884 0.000  0 0.000 0.000 0.116
#&gt; SRR1283415     6  0.5353     1.0000 0.116 0.000  0 0.000 0.368 0.516
#&gt; SRR1283416     6  0.5353     1.0000 0.116 0.000  0 0.000 0.368 0.516
#&gt; SRR1283417     6  0.5353     1.0000 0.116 0.000  0 0.000 0.368 0.516
#&gt; SRR1283418     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000     0.8233 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1283427     1  0.1610     0.7434 0.916 0.000  0 0.000 0.000 0.084
#&gt; SRR1283428     1  0.1610     0.7434 0.916 0.000  0 0.000 0.000 0.084
#&gt; SRR1283429     1  0.1610     0.7434 0.916 0.000  0 0.000 0.000 0.084
#&gt; SRR1283430     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
#&gt; SRR1283431     2  0.0458     0.8266 0.000 0.984  0 0.000 0.016 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.495           0.920       0.859         0.4091 0.499   0.499
#> 3 3 0.782           0.960       0.915         0.4299 0.896   0.791
#> 4 4 0.642           0.646       0.829         0.1532 0.956   0.890
#> 5 5 0.723           0.719       0.751         0.0795 0.913   0.764
#> 6 6 0.704           0.649       0.748         0.0611 0.911   0.708
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     1   0.000      0.670 1.000 0.000
#&gt; SRR1283380     1   0.000      0.670 1.000 0.000
#&gt; SRR1283381     1   0.000      0.670 1.000 0.000
#&gt; SRR1283385     2   0.000      1.000 0.000 1.000
#&gt; SRR1283386     2   0.000      1.000 0.000 1.000
#&gt; SRR1283387     2   0.000      1.000 0.000 1.000
#&gt; SRR1283388     2   0.000      1.000 0.000 1.000
#&gt; SRR1283389     2   0.000      1.000 0.000 1.000
#&gt; SRR1283390     2   0.000      1.000 0.000 1.000
#&gt; SRR1283382     2   0.000      1.000 0.000 1.000
#&gt; SRR1283383     2   0.000      1.000 0.000 1.000
#&gt; SRR1283384     2   0.000      1.000 0.000 1.000
#&gt; SRR1283391     2   0.000      1.000 0.000 1.000
#&gt; SRR1283392     2   0.000      1.000 0.000 1.000
#&gt; SRR1283393     2   0.000      1.000 0.000 1.000
#&gt; SRR1283394     2   0.000      1.000 0.000 1.000
#&gt; SRR1283395     2   0.000      1.000 0.000 1.000
#&gt; SRR1283396     2   0.000      1.000 0.000 1.000
#&gt; SRR1283397     2   0.000      1.000 0.000 1.000
#&gt; SRR1283398     2   0.000      1.000 0.000 1.000
#&gt; SRR1283399     2   0.000      1.000 0.000 1.000
#&gt; SRR1283400     2   0.000      1.000 0.000 1.000
#&gt; SRR1283401     2   0.000      1.000 0.000 1.000
#&gt; SRR1283402     2   0.000      1.000 0.000 1.000
#&gt; SRR1283403     1   0.000      0.670 1.000 0.000
#&gt; SRR1283404     1   0.000      0.670 1.000 0.000
#&gt; SRR1283405     1   0.000      0.670 1.000 0.000
#&gt; SRR1283406     1   0.895      0.906 0.688 0.312
#&gt; SRR1283407     1   0.895      0.906 0.688 0.312
#&gt; SRR1283408     1   0.895      0.906 0.688 0.312
#&gt; SRR1283409     1   0.895      0.906 0.688 0.312
#&gt; SRR1283410     1   0.895      0.906 0.688 0.312
#&gt; SRR1283411     1   0.895      0.906 0.688 0.312
#&gt; SRR1283412     1   0.895      0.906 0.688 0.312
#&gt; SRR1283413     1   0.895      0.906 0.688 0.312
#&gt; SRR1283414     1   0.895      0.906 0.688 0.312
#&gt; SRR1283415     1   0.895      0.906 0.688 0.312
#&gt; SRR1283416     1   0.895      0.906 0.688 0.312
#&gt; SRR1283417     1   0.895      0.906 0.688 0.312
#&gt; SRR1283418     1   0.895      0.906 0.688 0.312
#&gt; SRR1283419     1   0.895      0.906 0.688 0.312
#&gt; SRR1283420     1   0.895      0.906 0.688 0.312
#&gt; SRR1283421     1   0.895      0.906 0.688 0.312
#&gt; SRR1283422     1   0.895      0.906 0.688 0.312
#&gt; SRR1283423     1   0.895      0.906 0.688 0.312
#&gt; SRR1283424     1   0.895      0.906 0.688 0.312
#&gt; SRR1283425     1   0.895      0.906 0.688 0.312
#&gt; SRR1283426     1   0.895      0.906 0.688 0.312
#&gt; SRR1283427     1   0.895      0.906 0.688 0.312
#&gt; SRR1283428     1   0.895      0.906 0.688 0.312
#&gt; SRR1283429     1   0.895      0.906 0.688 0.312
#&gt; SRR1283430     2   0.000      1.000 0.000 1.000
#&gt; SRR1283431     2   0.000      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1283379     3   0.484      0.985 0.224 0.000 0.776
#&gt; SRR1283380     3   0.484      0.985 0.224 0.000 0.776
#&gt; SRR1283381     3   0.484      0.985 0.224 0.000 0.776
#&gt; SRR1283385     2   0.596      0.892 0.044 0.768 0.188
#&gt; SRR1283386     2   0.596      0.892 0.044 0.768 0.188
#&gt; SRR1283387     2   0.596      0.892 0.044 0.768 0.188
#&gt; SRR1283388     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283389     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283390     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283382     2   0.406      0.902 0.044 0.880 0.076
#&gt; SRR1283383     2   0.406      0.902 0.044 0.880 0.076
#&gt; SRR1283384     2   0.406      0.902 0.044 0.880 0.076
#&gt; SRR1283391     2   0.315      0.917 0.044 0.916 0.040
#&gt; SRR1283392     2   0.315      0.917 0.044 0.916 0.040
#&gt; SRR1283393     2   0.315      0.917 0.044 0.916 0.040
#&gt; SRR1283394     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283395     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283396     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283397     2   0.304      0.917 0.044 0.920 0.036
#&gt; SRR1283398     2   0.304      0.917 0.044 0.920 0.036
#&gt; SRR1283399     2   0.304      0.917 0.044 0.920 0.036
#&gt; SRR1283400     2   0.304      0.917 0.044 0.920 0.036
#&gt; SRR1283401     2   0.304      0.917 0.044 0.920 0.036
#&gt; SRR1283402     2   0.304      0.917 0.044 0.920 0.036
#&gt; SRR1283403     3   0.638      0.985 0.224 0.044 0.732
#&gt; SRR1283404     3   0.638      0.985 0.224 0.044 0.732
#&gt; SRR1283405     3   0.638      0.985 0.224 0.044 0.732
#&gt; SRR1283406     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283407     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283408     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283409     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283410     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283411     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283412     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283413     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283414     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283415     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283416     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283417     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283418     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283419     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283420     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283421     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283422     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283423     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283424     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283425     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283426     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283427     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283428     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283429     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283430     2   0.479      0.918 0.044 0.844 0.112
#&gt; SRR1283431     2   0.479      0.918 0.044 0.844 0.112
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.2868      0.986 0.136 0.000 0.864 0.000
#&gt; SRR1283380     3  0.2868      0.986 0.136 0.000 0.864 0.000
#&gt; SRR1283381     3  0.2868      0.986 0.136 0.000 0.864 0.000
#&gt; SRR1283385     4  0.4981      1.000 0.000 0.464 0.000 0.536
#&gt; SRR1283386     4  0.4981      1.000 0.000 0.464 0.000 0.536
#&gt; SRR1283387     4  0.4981      1.000 0.000 0.464 0.000 0.536
#&gt; SRR1283388     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283389     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283390     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283382     2  0.5090     -0.301 0.000 0.660 0.016 0.324
#&gt; SRR1283383     2  0.5090     -0.301 0.000 0.660 0.016 0.324
#&gt; SRR1283384     2  0.5090     -0.301 0.000 0.660 0.016 0.324
#&gt; SRR1283391     2  0.0469      0.484 0.000 0.988 0.000 0.012
#&gt; SRR1283392     2  0.0469      0.484 0.000 0.988 0.000 0.012
#&gt; SRR1283393     2  0.0469      0.484 0.000 0.988 0.000 0.012
#&gt; SRR1283394     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283395     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283396     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283397     2  0.0000      0.495 0.000 1.000 0.000 0.000
#&gt; SRR1283398     2  0.0000      0.495 0.000 1.000 0.000 0.000
#&gt; SRR1283399     2  0.0000      0.495 0.000 1.000 0.000 0.000
#&gt; SRR1283400     2  0.0000      0.495 0.000 1.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.495 0.000 1.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.495 0.000 1.000 0.000 0.000
#&gt; SRR1283403     3  0.4037      0.986 0.136 0.000 0.824 0.040
#&gt; SRR1283404     3  0.4037      0.986 0.136 0.000 0.824 0.040
#&gt; SRR1283405     3  0.4037      0.986 0.136 0.000 0.824 0.040
#&gt; SRR1283406     1  0.2469      0.874 0.892 0.000 0.000 0.108
#&gt; SRR1283407     1  0.2469      0.874 0.892 0.000 0.000 0.108
#&gt; SRR1283408     1  0.2469      0.874 0.892 0.000 0.000 0.108
#&gt; SRR1283409     1  0.2868      0.852 0.864 0.000 0.000 0.136
#&gt; SRR1283410     1  0.2868      0.852 0.864 0.000 0.000 0.136
#&gt; SRR1283411     1  0.2868      0.852 0.864 0.000 0.000 0.136
#&gt; SRR1283412     1  0.1637      0.893 0.940 0.000 0.000 0.060
#&gt; SRR1283413     1  0.1637      0.893 0.940 0.000 0.000 0.060
#&gt; SRR1283414     1  0.1637      0.893 0.940 0.000 0.000 0.060
#&gt; SRR1283415     1  0.3837      0.776 0.776 0.000 0.000 0.224
#&gt; SRR1283416     1  0.3837      0.776 0.776 0.000 0.000 0.224
#&gt; SRR1283417     1  0.3837      0.776 0.776 0.000 0.000 0.224
#&gt; SRR1283418     1  0.0592      0.899 0.984 0.000 0.000 0.016
#&gt; SRR1283419     1  0.0592      0.899 0.984 0.000 0.000 0.016
#&gt; SRR1283420     1  0.0592      0.899 0.984 0.000 0.000 0.016
#&gt; SRR1283421     1  0.0707      0.899 0.980 0.000 0.000 0.020
#&gt; SRR1283422     1  0.0707      0.899 0.980 0.000 0.000 0.020
#&gt; SRR1283423     1  0.0707      0.899 0.980 0.000 0.000 0.020
#&gt; SRR1283424     1  0.0188      0.899 0.996 0.000 0.000 0.004
#&gt; SRR1283425     1  0.0188      0.899 0.996 0.000 0.000 0.004
#&gt; SRR1283426     1  0.0188      0.899 0.996 0.000 0.000 0.004
#&gt; SRR1283427     1  0.3486      0.804 0.812 0.000 0.000 0.188
#&gt; SRR1283428     1  0.3486      0.804 0.812 0.000 0.000 0.188
#&gt; SRR1283429     1  0.3486      0.804 0.812 0.000 0.000 0.188
#&gt; SRR1283430     2  0.6617      0.142 0.000 0.600 0.120 0.280
#&gt; SRR1283431     2  0.6617      0.142 0.000 0.600 0.120 0.280
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1283379     3  0.4131      0.961 0.076 0.000 0.820 0.060 0.044
#&gt; SRR1283380     3  0.4131      0.961 0.076 0.000 0.820 0.060 0.044
#&gt; SRR1283381     3  0.4137      0.961 0.076 0.000 0.820 0.056 0.048
#&gt; SRR1283385     4  0.6672      0.323 0.000 0.288 0.000 0.440 0.272
#&gt; SRR1283386     4  0.6672      0.323 0.000 0.288 0.000 0.440 0.272
#&gt; SRR1283387     4  0.6672      0.323 0.000 0.288 0.000 0.440 0.272
#&gt; SRR1283388     4  0.4291      0.755 0.000 0.464 0.000 0.536 0.000
#&gt; SRR1283389     4  0.4291      0.755 0.000 0.464 0.000 0.536 0.000
#&gt; SRR1283390     4  0.4291      0.755 0.000 0.464 0.000 0.536 0.000
#&gt; SRR1283382     2  0.7152      0.252 0.000 0.496 0.040 0.204 0.260
#&gt; SRR1283383     2  0.7152      0.252 0.000 0.496 0.040 0.204 0.260
#&gt; SRR1283384     2  0.7152      0.252 0.000 0.496 0.040 0.204 0.260
#&gt; SRR1283391     2  0.1074      0.751 0.000 0.968 0.016 0.012 0.004
#&gt; SRR1283392     2  0.1074      0.751 0.000 0.968 0.016 0.012 0.004
#&gt; SRR1283393     2  0.1074      0.751 0.000 0.968 0.016 0.012 0.004
#&gt; SRR1283394     4  0.4283      0.756 0.000 0.456 0.000 0.544 0.000
#&gt; SRR1283395     4  0.4283      0.756 0.000 0.456 0.000 0.544 0.000
#&gt; SRR1283396     4  0.4283      0.756 0.000 0.456 0.000 0.544 0.000
#&gt; SRR1283397     2  0.1117      0.748 0.000 0.964 0.020 0.000 0.016
#&gt; SRR1283398     2  0.1117      0.748 0.000 0.964 0.020 0.000 0.016
#&gt; SRR1283399     2  0.1117      0.748 0.000 0.964 0.020 0.000 0.016
#&gt; SRR1283400     2  0.0000      0.753 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.753 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.753 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1283403     3  0.1671      0.961 0.076 0.000 0.924 0.000 0.000
#&gt; SRR1283404     3  0.1671      0.961 0.076 0.000 0.924 0.000 0.000
#&gt; SRR1283405     3  0.1671      0.961 0.076 0.000 0.924 0.000 0.000
#&gt; SRR1283406     1  0.5182      0.720 0.680 0.000 0.000 0.112 0.208
#&gt; SRR1283407     1  0.5182      0.720 0.680 0.000 0.000 0.112 0.208
#&gt; SRR1283408     1  0.5182      0.720 0.680 0.000 0.000 0.112 0.208
#&gt; SRR1283409     1  0.5210      0.715 0.684 0.000 0.000 0.132 0.184
#&gt; SRR1283410     1  0.5210      0.715 0.684 0.000 0.000 0.132 0.184
#&gt; SRR1283411     1  0.5210      0.715 0.684 0.000 0.000 0.132 0.184
#&gt; SRR1283412     1  0.1965      0.799 0.924 0.000 0.000 0.024 0.052
#&gt; SRR1283413     1  0.1965      0.799 0.924 0.000 0.000 0.024 0.052
#&gt; SRR1283414     1  0.1965      0.799 0.924 0.000 0.000 0.024 0.052
#&gt; SRR1283415     1  0.4256      0.605 0.564 0.000 0.000 0.000 0.436
#&gt; SRR1283416     1  0.4256      0.605 0.564 0.000 0.000 0.000 0.436
#&gt; SRR1283417     1  0.4256      0.605 0.564 0.000 0.000 0.000 0.436
#&gt; SRR1283418     1  0.0000      0.811 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.811 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.811 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0162      0.811 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1283422     1  0.0162      0.811 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1283423     1  0.0162      0.811 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1283424     1  0.0963      0.812 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1283425     1  0.0963      0.812 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1283426     1  0.0963      0.812 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1283427     1  0.4697      0.661 0.648 0.000 0.000 0.032 0.320
#&gt; SRR1283428     1  0.4697      0.661 0.648 0.000 0.000 0.032 0.320
#&gt; SRR1283429     1  0.4697      0.661 0.648 0.000 0.000 0.032 0.320
#&gt; SRR1283430     4  0.4549      0.753 0.000 0.464 0.008 0.528 0.000
#&gt; SRR1283431     4  0.4549      0.753 0.000 0.464 0.008 0.528 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1283379     3  0.3152      0.947 0.020 0.000 0.864 0.056 0.012 0.048
#&gt; SRR1283380     3  0.3179      0.947 0.020 0.000 0.864 0.056 0.016 0.044
#&gt; SRR1283381     3  0.3152      0.947 0.020 0.000 0.864 0.056 0.012 0.048
#&gt; SRR1283385     5  0.5624      0.597 0.000 0.180 0.000 0.296 0.524 0.000
#&gt; SRR1283386     5  0.5624      0.597 0.000 0.180 0.000 0.296 0.524 0.000
#&gt; SRR1283387     5  0.5624      0.597 0.000 0.180 0.000 0.296 0.524 0.000
#&gt; SRR1283388     4  0.3446      0.976 0.000 0.308 0.000 0.692 0.000 0.000
#&gt; SRR1283389     4  0.3446      0.976 0.000 0.308 0.000 0.692 0.000 0.000
#&gt; SRR1283390     4  0.3446      0.976 0.000 0.308 0.000 0.692 0.000 0.000
#&gt; SRR1283382     5  0.6253      0.630 0.000 0.368 0.000 0.044 0.464 0.124
#&gt; SRR1283383     5  0.6253      0.630 0.000 0.368 0.000 0.044 0.464 0.124
#&gt; SRR1283384     5  0.6253      0.630 0.000 0.368 0.000 0.044 0.464 0.124
#&gt; SRR1283391     2  0.1667      0.923 0.000 0.936 0.008 0.004 0.008 0.044
#&gt; SRR1283392     2  0.1667      0.923 0.000 0.936 0.008 0.004 0.008 0.044
#&gt; SRR1283393     2  0.1667      0.923 0.000 0.936 0.008 0.004 0.008 0.044
#&gt; SRR1283394     4  0.4011      0.970 0.000 0.304 0.000 0.672 0.000 0.024
#&gt; SRR1283395     4  0.4011      0.970 0.000 0.304 0.000 0.672 0.000 0.024
#&gt; SRR1283396     4  0.4011      0.970 0.000 0.304 0.000 0.672 0.000 0.024
#&gt; SRR1283397     2  0.1570      0.925 0.000 0.944 0.008 0.004 0.028 0.016
#&gt; SRR1283398     2  0.1570      0.925 0.000 0.944 0.008 0.004 0.028 0.016
#&gt; SRR1283399     2  0.1570      0.925 0.000 0.944 0.008 0.004 0.028 0.016
#&gt; SRR1283400     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283403     3  0.0692      0.947 0.020 0.000 0.976 0.000 0.000 0.004
#&gt; SRR1283404     3  0.0692      0.947 0.020 0.000 0.976 0.000 0.004 0.000
#&gt; SRR1283405     3  0.0692      0.947 0.020 0.000 0.976 0.000 0.004 0.000
#&gt; SRR1283406     1  0.6997      0.197 0.468 0.000 0.000 0.120 0.168 0.244
#&gt; SRR1283407     1  0.6997      0.197 0.468 0.000 0.000 0.120 0.168 0.244
#&gt; SRR1283408     1  0.6997      0.197 0.468 0.000 0.000 0.120 0.168 0.244
#&gt; SRR1283409     1  0.6653      0.224 0.472 0.000 0.000 0.072 0.304 0.152
#&gt; SRR1283410     1  0.6668      0.224 0.472 0.000 0.000 0.072 0.300 0.156
#&gt; SRR1283411     1  0.6653      0.224 0.472 0.000 0.000 0.072 0.304 0.152
#&gt; SRR1283412     1  0.3282      0.508 0.848 0.000 0.000 0.036 0.048 0.068
#&gt; SRR1283413     1  0.3282      0.508 0.848 0.000 0.000 0.036 0.048 0.068
#&gt; SRR1283414     1  0.3282      0.508 0.848 0.000 0.000 0.036 0.048 0.068
#&gt; SRR1283415     6  0.3851      0.996 0.460 0.000 0.000 0.000 0.000 0.540
#&gt; SRR1283416     6  0.3851      0.996 0.460 0.000 0.000 0.000 0.000 0.540
#&gt; SRR1283417     6  0.4083      0.992 0.460 0.000 0.000 0.008 0.000 0.532
#&gt; SRR1283418     1  0.0260      0.533 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1283419     1  0.0260      0.533 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1283420     1  0.0260      0.533 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1283421     1  0.0146      0.534 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1283422     1  0.0146      0.534 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1283423     1  0.0146      0.534 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1283424     1  0.1007      0.509 0.956 0.000 0.000 0.000 0.000 0.044
#&gt; SRR1283425     1  0.1007      0.509 0.956 0.000 0.000 0.000 0.000 0.044
#&gt; SRR1283426     1  0.1007      0.509 0.956 0.000 0.000 0.000 0.000 0.044
#&gt; SRR1283427     1  0.4569     -0.539 0.616 0.000 0.000 0.028 0.012 0.344
#&gt; SRR1283428     1  0.4569     -0.539 0.616 0.000 0.000 0.028 0.012 0.344
#&gt; SRR1283429     1  0.4569     -0.539 0.616 0.000 0.000 0.028 0.012 0.344
#&gt; SRR1283430     4  0.3990      0.965 0.000 0.304 0.004 0.676 0.000 0.016
#&gt; SRR1283431     4  0.3990      0.965 0.000 0.304 0.004 0.676 0.000 0.016
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 0.876           0.893       0.912         0.1227 0.922   0.801
#> 5 5 0.804           0.938       0.907         0.0737 0.948   0.835
#> 6 6 0.808           0.600       0.782         0.0717 0.956   0.835
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.0188      0.998 0.000 0.000 0.996 0.004
#&gt; SRR1283380     3  0.0188      0.998 0.000 0.000 0.996 0.004
#&gt; SRR1283381     3  0.0188      0.998 0.000 0.000 0.996 0.004
#&gt; SRR1283385     2  0.0817      0.989 0.000 0.976 0.000 0.024
#&gt; SRR1283386     2  0.0817      0.989 0.000 0.976 0.000 0.024
#&gt; SRR1283387     2  0.0817      0.989 0.000 0.976 0.000 0.024
#&gt; SRR1283388     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283389     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283390     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283382     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283383     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283384     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283391     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283392     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283393     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283394     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283395     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283396     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283397     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283398     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283399     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283400     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.990 0.000 1.000 0.000 0.000
#&gt; SRR1283403     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1283404     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1283405     3  0.0000      0.998 0.000 0.000 1.000 0.000
#&gt; SRR1283406     4  0.3266      0.845 0.168 0.000 0.000 0.832
#&gt; SRR1283407     4  0.3266      0.845 0.168 0.000 0.000 0.832
#&gt; SRR1283408     4  0.3266      0.845 0.168 0.000 0.000 0.832
#&gt; SRR1283409     4  0.0921      0.869 0.028 0.000 0.000 0.972
#&gt; SRR1283410     4  0.0921      0.869 0.028 0.000 0.000 0.972
#&gt; SRR1283411     4  0.0921      0.869 0.028 0.000 0.000 0.972
#&gt; SRR1283412     1  0.4643      0.758 0.656 0.000 0.000 0.344
#&gt; SRR1283413     1  0.4643      0.758 0.656 0.000 0.000 0.344
#&gt; SRR1283414     1  0.4643      0.758 0.656 0.000 0.000 0.344
#&gt; SRR1283415     1  0.0000      0.660 1.000 0.000 0.000 0.000
#&gt; SRR1283416     1  0.0000      0.660 1.000 0.000 0.000 0.000
#&gt; SRR1283417     1  0.0000      0.660 1.000 0.000 0.000 0.000
#&gt; SRR1283418     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283419     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283420     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283421     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283422     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283423     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283424     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283425     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283426     1  0.4454      0.799 0.692 0.000 0.000 0.308
#&gt; SRR1283427     1  0.0000      0.660 1.000 0.000 0.000 0.000
#&gt; SRR1283428     1  0.0000      0.660 1.000 0.000 0.000 0.000
#&gt; SRR1283429     1  0.0000      0.660 1.000 0.000 0.000 0.000
#&gt; SRR1283430     2  0.0707      0.990 0.000 0.980 0.000 0.020
#&gt; SRR1283431     2  0.0707      0.990 0.000 0.980 0.000 0.020
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1283379     3  0.1830      0.966 0.000 0.000 0.924 0.068 0.008
#&gt; SRR1283380     3  0.1830      0.966 0.000 0.000 0.924 0.068 0.008
#&gt; SRR1283381     3  0.1830      0.966 0.000 0.000 0.924 0.068 0.008
#&gt; SRR1283385     2  0.3354      0.919 0.000 0.844 0.000 0.088 0.068
#&gt; SRR1283386     2  0.3354      0.919 0.000 0.844 0.000 0.088 0.068
#&gt; SRR1283387     2  0.3354      0.919 0.000 0.844 0.000 0.088 0.068
#&gt; SRR1283388     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283389     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283390     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283382     2  0.1106      0.924 0.000 0.964 0.000 0.024 0.012
#&gt; SRR1283383     2  0.1106      0.924 0.000 0.964 0.000 0.024 0.012
#&gt; SRR1283384     2  0.1106      0.924 0.000 0.964 0.000 0.024 0.012
#&gt; SRR1283391     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283392     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283393     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283394     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283395     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283396     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283397     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283398     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283399     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283400     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283401     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283402     2  0.0162      0.934 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1283403     3  0.0000      0.966 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283404     3  0.0000      0.966 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283405     3  0.0000      0.966 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283406     5  0.5096      0.808 0.272 0.000 0.000 0.072 0.656
#&gt; SRR1283407     5  0.5096      0.808 0.272 0.000 0.000 0.072 0.656
#&gt; SRR1283408     5  0.5096      0.808 0.272 0.000 0.000 0.072 0.656
#&gt; SRR1283409     5  0.2280      0.822 0.120 0.000 0.000 0.000 0.880
#&gt; SRR1283410     5  0.2280      0.822 0.120 0.000 0.000 0.000 0.880
#&gt; SRR1283411     5  0.2280      0.822 0.120 0.000 0.000 0.000 0.880
#&gt; SRR1283412     1  0.0898      0.966 0.972 0.000 0.000 0.008 0.020
#&gt; SRR1283413     1  0.0898      0.966 0.972 0.000 0.000 0.008 0.020
#&gt; SRR1283414     1  0.0898      0.966 0.972 0.000 0.000 0.008 0.020
#&gt; SRR1283415     4  0.3395      0.977 0.236 0.000 0.000 0.764 0.000
#&gt; SRR1283416     4  0.3395      0.977 0.236 0.000 0.000 0.764 0.000
#&gt; SRR1283417     4  0.3395      0.977 0.236 0.000 0.000 0.764 0.000
#&gt; SRR1283418     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.989 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283427     4  0.3586      0.977 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1283428     4  0.3586      0.977 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1283429     4  0.3586      0.977 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1283430     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
#&gt; SRR1283431     2  0.2859      0.929 0.000 0.876 0.000 0.068 0.056
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2   p3    p4    p5    p6
#&gt; SRR1283379     3   0.000      0.911 0.000 0.000 1.00 0.000 0.000 0.000
#&gt; SRR1283380     3   0.000      0.911 0.000 0.000 1.00 0.000 0.000 0.000
#&gt; SRR1283381     3   0.000      0.911 0.000 0.000 1.00 0.000 0.000 0.000
#&gt; SRR1283385     2   0.245      0.263 0.000 0.840 0.00 0.000 0.160 0.000
#&gt; SRR1283386     2   0.245      0.263 0.000 0.840 0.00 0.000 0.160 0.000
#&gt; SRR1283387     2   0.245      0.263 0.000 0.840 0.00 0.000 0.160 0.000
#&gt; SRR1283388     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283389     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283390     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283382     5   0.385      1.000 0.000 0.460 0.00 0.000 0.540 0.000
#&gt; SRR1283383     5   0.385      1.000 0.000 0.460 0.00 0.000 0.540 0.000
#&gt; SRR1283384     5   0.385      1.000 0.000 0.460 0.00 0.000 0.540 0.000
#&gt; SRR1283391     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283392     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283393     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283394     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283395     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283396     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283397     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283398     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283399     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283400     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283401     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283402     2   0.382     -0.308 0.000 0.564 0.00 0.000 0.436 0.000
#&gt; SRR1283403     3   0.338      0.911 0.000 0.000 0.82 0.008 0.124 0.048
#&gt; SRR1283404     3   0.338      0.911 0.000 0.000 0.82 0.008 0.124 0.048
#&gt; SRR1283405     3   0.338      0.911 0.000 0.000 0.82 0.008 0.124 0.048
#&gt; SRR1283406     4   0.653      0.698 0.208 0.000 0.00 0.464 0.288 0.040
#&gt; SRR1283407     4   0.653      0.698 0.208 0.000 0.00 0.464 0.288 0.040
#&gt; SRR1283408     4   0.653      0.698 0.208 0.000 0.00 0.464 0.288 0.040
#&gt; SRR1283409     4   0.114      0.690 0.052 0.000 0.00 0.948 0.000 0.000
#&gt; SRR1283410     4   0.114      0.690 0.052 0.000 0.00 0.948 0.000 0.000
#&gt; SRR1283411     4   0.114      0.690 0.052 0.000 0.00 0.948 0.000 0.000
#&gt; SRR1283412     1   0.126      0.950 0.956 0.000 0.00 0.008 0.016 0.020
#&gt; SRR1283413     1   0.126      0.950 0.956 0.000 0.00 0.008 0.016 0.020
#&gt; SRR1283414     1   0.126      0.950 0.956 0.000 0.00 0.008 0.016 0.020
#&gt; SRR1283415     6   0.166      0.970 0.088 0.000 0.00 0.000 0.000 0.912
#&gt; SRR1283416     6   0.166      0.970 0.088 0.000 0.00 0.000 0.000 0.912
#&gt; SRR1283417     6   0.166      0.970 0.088 0.000 0.00 0.000 0.000 0.912
#&gt; SRR1283418     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283419     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283420     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283421     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283422     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283423     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283424     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283425     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283426     1   0.000      0.984 1.000 0.000 0.00 0.000 0.000 0.000
#&gt; SRR1283427     6   0.209      0.970 0.124 0.000 0.00 0.000 0.000 0.876
#&gt; SRR1283428     6   0.209      0.970 0.124 0.000 0.00 0.000 0.000 0.876
#&gt; SRR1283429     6   0.209      0.970 0.124 0.000 0.00 0.000 0.000 0.876
#&gt; SRR1283430     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
#&gt; SRR1283431     2   0.000      0.452 0.000 1.000 0.00 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 1.000           1.000       1.000         0.0108 0.993   0.983
#> 5 5 0.922           0.866       0.896         0.1402 0.904   0.753
#> 6 6 0.806           0.755       0.838         0.0889 0.954   0.844
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1283379     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283385     5   0.418      0.500 0.000 0.400  0  0 0.600
#&gt; SRR1283386     5   0.423      0.483 0.000 0.420  0  0 0.580
#&gt; SRR1283387     5   0.418      0.500 0.000 0.400  0  0 0.600
#&gt; SRR1283388     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283389     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283390     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283382     2   0.148      0.472 0.000 0.936  0  0 0.064
#&gt; SRR1283383     2   0.148      0.472 0.000 0.936  0  0 0.064
#&gt; SRR1283384     2   0.148      0.472 0.000 0.936  0  0 0.064
#&gt; SRR1283391     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283392     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283393     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283394     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283395     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283396     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283397     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283398     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283399     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283400     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283401     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283402     2   0.429      0.810 0.000 0.536  0  0 0.464
#&gt; SRR1283403     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283406     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283407     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283408     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283409     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283410     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283411     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283412     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283413     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283414     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283415     1   0.148      0.951 0.936 0.064  0  0 0.000
#&gt; SRR1283416     1   0.148      0.951 0.936 0.064  0  0 0.000
#&gt; SRR1283417     1   0.148      0.951 0.936 0.064  0  0 0.000
#&gt; SRR1283418     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283419     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283420     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283421     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283422     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283423     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283424     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283425     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283426     1   0.000      0.984 1.000 0.000  0  0 0.000
#&gt; SRR1283427     1   0.148      0.951 0.936 0.064  0  0 0.000
#&gt; SRR1283428     1   0.148      0.951 0.936 0.064  0  0 0.000
#&gt; SRR1283429     1   0.148      0.951 0.936 0.064  0  0 0.000
#&gt; SRR1283430     5   0.000      0.787 0.000 0.000  0  0 1.000
#&gt; SRR1283431     5   0.000      0.787 0.000 0.000  0  0 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1   p2 p3    p4    p5   p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.00  1 0.000 0.000 0.00
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.00  1 0.000 0.000 0.00
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.00  1 0.000 0.000 0.00
#&gt; SRR1283385     6  0.0000      0.494 0.000 0.00  0 0.000 0.000 1.00
#&gt; SRR1283386     6  0.0547      0.484 0.000 0.02  0 0.000 0.000 0.98
#&gt; SRR1283387     6  0.0000      0.494 0.000 0.00  0 0.000 0.000 1.00
#&gt; SRR1283388     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283389     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283390     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283382     2  0.3756      0.497 0.000 0.60  0 0.000 0.000 0.40
#&gt; SRR1283383     2  0.3756      0.497 0.000 0.60  0 0.000 0.000 0.40
#&gt; SRR1283384     2  0.3756      0.497 0.000 0.60  0 0.000 0.000 0.40
#&gt; SRR1283391     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283392     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283393     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283394     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283395     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283396     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283397     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283398     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283399     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283400     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283401     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283402     2  0.0000      0.828 0.000 1.00  0 0.000 0.000 0.00
#&gt; SRR1283403     4  0.3857      1.000 0.000 0.00  0 0.532 0.468 0.00
#&gt; SRR1283404     4  0.3857      1.000 0.000 0.00  0 0.532 0.468 0.00
#&gt; SRR1283405     4  0.3857      1.000 0.000 0.00  0 0.532 0.468 0.00
#&gt; SRR1283406     1  0.3857      0.715 0.532 0.00  0 0.468 0.000 0.00
#&gt; SRR1283407     1  0.3857      0.715 0.532 0.00  0 0.468 0.000 0.00
#&gt; SRR1283408     1  0.3857      0.715 0.532 0.00  0 0.468 0.000 0.00
#&gt; SRR1283409     5  0.3857      1.000 0.000 0.00  0 0.468 0.532 0.00
#&gt; SRR1283410     5  0.3857      1.000 0.000 0.00  0 0.468 0.532 0.00
#&gt; SRR1283411     5  0.3857      1.000 0.000 0.00  0 0.468 0.532 0.00
#&gt; SRR1283412     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283413     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283414     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283415     1  0.0000      0.477 1.000 0.00  0 0.000 0.000 0.00
#&gt; SRR1283416     1  0.0000      0.477 1.000 0.00  0 0.000 0.000 0.00
#&gt; SRR1283417     1  0.0000      0.477 1.000 0.00  0 0.000 0.000 0.00
#&gt; SRR1283418     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283419     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283420     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283421     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283422     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283423     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283424     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283425     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283426     1  0.3817      0.759 0.568 0.00  0 0.432 0.000 0.00
#&gt; SRR1283427     1  0.0000      0.477 1.000 0.00  0 0.000 0.000 0.00
#&gt; SRR1283428     1  0.0000      0.477 1.000 0.00  0 0.000 0.000 0.00
#&gt; SRR1283429     1  0.0000      0.477 1.000 0.00  0 0.000 0.000 0.00
#&gt; SRR1283430     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
#&gt; SRR1283431     6  0.3756      0.808 0.000 0.40  0 0.000 0.000 0.60
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.853           0.823       0.940          0.502 0.492   0.492
#> 3 3 1.000           1.000       1.000          0.205 0.891   0.781
#> 4 4 1.000           1.000       1.000          0.011 0.993   0.983
#> 5 5 0.836           0.851       0.902          0.113 0.954   0.882
#> 6 6 0.772           0.834       0.877          0.108 0.880   0.657
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     2   1.000    -0.1270 0.500 0.500
#&gt; SRR1283380     1   1.000     0.0569 0.500 0.500
#&gt; SRR1283381     1   1.000     0.0569 0.500 0.500
#&gt; SRR1283385     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283386     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283387     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283388     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283389     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283390     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283382     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283383     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283384     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283391     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283392     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283393     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283394     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283395     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283396     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283397     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283398     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283399     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283400     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283401     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283402     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283403     1   1.000     0.0569 0.500 0.500
#&gt; SRR1283404     2   1.000    -0.1270 0.500 0.500
#&gt; SRR1283405     1   1.000     0.0569 0.500 0.500
#&gt; SRR1283406     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283407     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283408     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283409     1   0.311     0.8719 0.944 0.056
#&gt; SRR1283410     1   0.311     0.8719 0.944 0.056
#&gt; SRR1283411     1   0.311     0.8719 0.944 0.056
#&gt; SRR1283412     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283413     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283414     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283415     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283416     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283417     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283418     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283419     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283420     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283421     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283422     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283423     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283424     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283425     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283426     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283427     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283428     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283429     1   0.000     0.9117 1.000 0.000
#&gt; SRR1283430     2   0.000     0.9520 0.000 1.000
#&gt; SRR1283431     2   0.000     0.9520 0.000 1.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3    p4
#&gt; SRR1283379     3  0.0000      1.000 0.000  0  1 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000  0  1 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000  0  1 0.000
#&gt; SRR1283385     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283386     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283387     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283388     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283389     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283390     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283382     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283383     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283384     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283391     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283392     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283393     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283394     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283395     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283396     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283397     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283398     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283399     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283400     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283401     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283402     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000  0  0 1.000
#&gt; SRR1283404     4  0.0000      1.000 0.000  0  0 1.000
#&gt; SRR1283405     4  0.0000      1.000 0.000  0  0 1.000
#&gt; SRR1283406     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283407     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283408     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283409     1  0.0188      0.996 0.996  0  0 0.004
#&gt; SRR1283410     1  0.0188      0.996 0.996  0  0 0.004
#&gt; SRR1283411     1  0.0188      0.996 0.996  0  0 0.004
#&gt; SRR1283412     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283413     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283414     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283415     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283416     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283417     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283418     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283419     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283420     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283421     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283422     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283423     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283424     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283425     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283426     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283427     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283428     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283429     1  0.0000      0.999 1.000  0  0 0.000
#&gt; SRR1283430     2  0.0000      1.000 0.000  1  0 0.000
#&gt; SRR1283431     2  0.0000      1.000 0.000  1  0 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283385     2  0.2605      0.870 0.000 0.852  0 0.000 0.148
#&gt; SRR1283386     2  0.2605      0.870 0.000 0.852  0 0.000 0.148
#&gt; SRR1283387     2  0.2605      0.870 0.000 0.852  0 0.000 0.148
#&gt; SRR1283388     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
#&gt; SRR1283389     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
#&gt; SRR1283390     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
#&gt; SRR1283382     2  0.2605      0.870 0.000 0.852  0 0.000 0.148
#&gt; SRR1283383     2  0.2605      0.870 0.000 0.852  0 0.000 0.148
#&gt; SRR1283384     2  0.2605      0.870 0.000 0.852  0 0.000 0.148
#&gt; SRR1283391     2  0.0404      0.931 0.000 0.988  0 0.000 0.012
#&gt; SRR1283392     2  0.0290      0.932 0.000 0.992  0 0.000 0.008
#&gt; SRR1283393     2  0.0290      0.932 0.000 0.992  0 0.000 0.008
#&gt; SRR1283394     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
#&gt; SRR1283395     2  0.1544      0.922 0.000 0.932  0 0.000 0.068
#&gt; SRR1283396     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
#&gt; SRR1283397     2  0.0000      0.933 0.000 1.000  0 0.000 0.000
#&gt; SRR1283398     2  0.0000      0.933 0.000 1.000  0 0.000 0.000
#&gt; SRR1283399     2  0.0000      0.933 0.000 1.000  0 0.000 0.000
#&gt; SRR1283400     2  0.0000      0.933 0.000 1.000  0 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.933 0.000 1.000  0 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.933 0.000 1.000  0 0.000 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0 1.000 0.000
#&gt; SRR1283406     1  0.3003      0.655 0.812 0.000  0 0.000 0.188
#&gt; SRR1283407     1  0.3003      0.655 0.812 0.000  0 0.000 0.188
#&gt; SRR1283408     1  0.3003      0.655 0.812 0.000  0 0.000 0.188
#&gt; SRR1283409     5  0.3838      1.000 0.280 0.000  0 0.004 0.716
#&gt; SRR1283410     5  0.3838      1.000 0.280 0.000  0 0.004 0.716
#&gt; SRR1283411     5  0.3838      1.000 0.280 0.000  0 0.004 0.716
#&gt; SRR1283412     1  0.0794      0.846 0.972 0.000  0 0.000 0.028
#&gt; SRR1283413     1  0.0794      0.846 0.972 0.000  0 0.000 0.028
#&gt; SRR1283414     1  0.0794      0.846 0.972 0.000  0 0.000 0.028
#&gt; SRR1283415     1  0.4171      0.113 0.604 0.000  0 0.000 0.396
#&gt; SRR1283416     1  0.4171      0.113 0.604 0.000  0 0.000 0.396
#&gt; SRR1283417     1  0.4171      0.113 0.604 0.000  0 0.000 0.396
#&gt; SRR1283418     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283421     1  0.0609      0.852 0.980 0.000  0 0.000 0.020
#&gt; SRR1283422     1  0.0609      0.852 0.980 0.000  0 0.000 0.020
#&gt; SRR1283423     1  0.0609      0.852 0.980 0.000  0 0.000 0.020
#&gt; SRR1283424     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283427     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283428     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283429     1  0.0000      0.859 1.000 0.000  0 0.000 0.000
#&gt; SRR1283430     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
#&gt; SRR1283431     2  0.1608      0.921 0.000 0.928  0 0.000 0.072
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5    p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283385     5  0.1556      1.000 0.000 0.080  0  0 0.920 0.000
#&gt; SRR1283386     5  0.1556      1.000 0.000 0.080  0  0 0.920 0.000
#&gt; SRR1283387     5  0.1556      1.000 0.000 0.080  0  0 0.920 0.000
#&gt; SRR1283388     2  0.0146      0.798 0.000 0.996  0  0 0.004 0.000
#&gt; SRR1283389     2  0.0000      0.801 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283390     2  0.0146      0.798 0.000 0.996  0  0 0.004 0.000
#&gt; SRR1283382     5  0.1556      1.000 0.000 0.080  0  0 0.920 0.000
#&gt; SRR1283383     5  0.1556      1.000 0.000 0.080  0  0 0.920 0.000
#&gt; SRR1283384     5  0.1556      1.000 0.000 0.080  0  0 0.920 0.000
#&gt; SRR1283391     2  0.3371      0.784 0.000 0.708  0  0 0.292 0.000
#&gt; SRR1283392     2  0.3266      0.807 0.000 0.728  0  0 0.272 0.000
#&gt; SRR1283393     2  0.3351      0.789 0.000 0.712  0  0 0.288 0.000
#&gt; SRR1283394     2  0.1387      0.826 0.000 0.932  0  0 0.068 0.000
#&gt; SRR1283395     2  0.1444      0.827 0.000 0.928  0  0 0.072 0.000
#&gt; SRR1283396     2  0.1204      0.823 0.000 0.944  0  0 0.056 0.000
#&gt; SRR1283397     2  0.3101      0.828 0.000 0.756  0  0 0.244 0.000
#&gt; SRR1283398     2  0.3101      0.828 0.000 0.756  0  0 0.244 0.000
#&gt; SRR1283399     2  0.3101      0.828 0.000 0.756  0  0 0.244 0.000
#&gt; SRR1283400     2  0.3151      0.824 0.000 0.748  0  0 0.252 0.000
#&gt; SRR1283401     2  0.3151      0.824 0.000 0.748  0  0 0.252 0.000
#&gt; SRR1283402     2  0.3151      0.824 0.000 0.748  0  0 0.252 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283406     1  0.3647      0.527 0.640 0.000  0  0 0.000 0.360
#&gt; SRR1283407     1  0.3647      0.527 0.640 0.000  0  0 0.000 0.360
#&gt; SRR1283408     1  0.3647      0.527 0.640 0.000  0  0 0.000 0.360
#&gt; SRR1283409     6  0.1444      0.773 0.072 0.000  0  0 0.000 0.928
#&gt; SRR1283410     6  0.1444      0.773 0.072 0.000  0  0 0.000 0.928
#&gt; SRR1283411     6  0.1444      0.773 0.072 0.000  0  0 0.000 0.928
#&gt; SRR1283412     1  0.0458      0.774 0.984 0.000  0  0 0.000 0.016
#&gt; SRR1283413     1  0.0458      0.774 0.984 0.000  0  0 0.000 0.016
#&gt; SRR1283414     1  0.0458      0.774 0.984 0.000  0  0 0.000 0.016
#&gt; SRR1283415     6  0.3266      0.730 0.272 0.000  0  0 0.000 0.728
#&gt; SRR1283416     6  0.3244      0.734 0.268 0.000  0  0 0.000 0.732
#&gt; SRR1283417     6  0.3266      0.730 0.272 0.000  0  0 0.000 0.728
#&gt; SRR1283418     1  0.2454      0.842 0.840 0.000  0  0 0.000 0.160
#&gt; SRR1283419     1  0.2454      0.842 0.840 0.000  0  0 0.000 0.160
#&gt; SRR1283420     1  0.2454      0.842 0.840 0.000  0  0 0.000 0.160
#&gt; SRR1283421     1  0.0000      0.787 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.787 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.787 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283424     1  0.2378      0.845 0.848 0.000  0  0 0.000 0.152
#&gt; SRR1283425     1  0.2378      0.845 0.848 0.000  0  0 0.000 0.152
#&gt; SRR1283426     1  0.2378      0.845 0.848 0.000  0  0 0.000 0.152
#&gt; SRR1283427     1  0.2416      0.844 0.844 0.000  0  0 0.000 0.156
#&gt; SRR1283428     1  0.2416      0.844 0.844 0.000  0  0 0.000 0.156
#&gt; SRR1283429     1  0.2416      0.844 0.844 0.000  0  0 0.000 0.156
#&gt; SRR1283430     2  0.0000      0.801 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283431     2  0.0000      0.801 0.000 1.000  0  0 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       0.999         0.2064 0.896   0.791
#> 4 4 0.993           0.996       0.963         0.0104 0.993   0.983
#> 5 5 0.993           0.970       0.953         0.0253 1.000   1.000
#> 6 6 0.851           0.931       0.926         0.0328 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1283379     3  0.0424      0.998 0.008  0 0.992
#&gt; SRR1283380     3  0.0424      0.998 0.008  0 0.992
#&gt; SRR1283381     3  0.0424      0.998 0.008  0 0.992
#&gt; SRR1283385     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283386     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283387     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283388     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283389     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283390     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283382     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283383     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283384     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283391     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283392     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283393     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283394     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283395     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283396     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283397     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283398     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283399     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283400     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283401     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283402     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283403     3  0.0592      0.998 0.012  0 0.988
#&gt; SRR1283404     3  0.0592      0.998 0.012  0 0.988
#&gt; SRR1283405     3  0.0592      0.998 0.012  0 0.988
#&gt; SRR1283406     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283407     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283408     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283409     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283410     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283411     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283412     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283413     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283414     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283415     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283416     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283417     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283418     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283419     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283420     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283421     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283422     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283423     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283424     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283425     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283426     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283427     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283428     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283429     1  0.0000      1.000 1.000  0 0.000
#&gt; SRR1283430     2  0.0000      1.000 0.000  1 0.000
#&gt; SRR1283431     2  0.0000      1.000 0.000  1 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3   p4
#&gt; SRR1283379     3  0.4948      1.000  0 0.000 0.560 0.44
#&gt; SRR1283380     3  0.4948      1.000  0 0.000 0.560 0.44
#&gt; SRR1283381     3  0.4948      1.000  0 0.000 0.560 0.44
#&gt; SRR1283385     2  0.0707      0.985  0 0.980 0.020 0.00
#&gt; SRR1283386     2  0.0707      0.985  0 0.980 0.020 0.00
#&gt; SRR1283387     2  0.0707      0.985  0 0.980 0.020 0.00
#&gt; SRR1283388     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283389     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283390     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283382     2  0.0707      0.985  0 0.980 0.020 0.00
#&gt; SRR1283383     2  0.0707      0.985  0 0.980 0.020 0.00
#&gt; SRR1283384     2  0.0707      0.985  0 0.980 0.020 0.00
#&gt; SRR1283391     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283392     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283393     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283394     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283395     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283396     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283397     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283398     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283399     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283400     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283401     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283402     2  0.0000      0.994  0 1.000 0.000 0.00
#&gt; SRR1283403     4  0.0000      1.000  0 0.000 0.000 1.00
#&gt; SRR1283404     4  0.0000      1.000  0 0.000 0.000 1.00
#&gt; SRR1283405     4  0.0000      1.000  0 0.000 0.000 1.00
#&gt; SRR1283406     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283407     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283408     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283409     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283410     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283411     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283412     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283413     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283414     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283415     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283416     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283417     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283418     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283419     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283420     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283421     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283422     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283423     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283424     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283425     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283426     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283427     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283428     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283429     1  0.0000      1.000  1 0.000 0.000 0.00
#&gt; SRR1283430     2  0.0188      0.993  0 0.996 0.004 0.00
#&gt; SRR1283431     2  0.0188      0.993  0 0.996 0.004 0.00
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1283379     3  0.3612      1.000 0.000 0.000 0.732 0.268 NA
#&gt; SRR1283380     3  0.3612      1.000 0.000 0.000 0.732 0.268 NA
#&gt; SRR1283381     3  0.3612      1.000 0.000 0.000 0.732 0.268 NA
#&gt; SRR1283385     2  0.1410      0.957 0.000 0.940 0.000 0.000 NA
#&gt; SRR1283386     2  0.1410      0.957 0.000 0.940 0.000 0.000 NA
#&gt; SRR1283387     2  0.1410      0.957 0.000 0.940 0.000 0.000 NA
#&gt; SRR1283388     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283389     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283390     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283382     2  0.1671      0.950 0.000 0.924 0.000 0.000 NA
#&gt; SRR1283383     2  0.1671      0.950 0.000 0.924 0.000 0.000 NA
#&gt; SRR1283384     2  0.1544      0.954 0.000 0.932 0.000 0.000 NA
#&gt; SRR1283391     2  0.0703      0.974 0.000 0.976 0.000 0.000 NA
#&gt; SRR1283392     2  0.0703      0.974 0.000 0.976 0.000 0.000 NA
#&gt; SRR1283393     2  0.0609      0.974 0.000 0.980 0.000 0.000 NA
#&gt; SRR1283394     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283395     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283396     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283397     2  0.0510      0.975 0.000 0.984 0.000 0.000 NA
#&gt; SRR1283398     2  0.0510      0.975 0.000 0.984 0.000 0.000 NA
#&gt; SRR1283399     2  0.0290      0.976 0.000 0.992 0.000 0.000 NA
#&gt; SRR1283400     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283401     2  0.0404      0.975 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283402     2  0.0290      0.976 0.000 0.992 0.000 0.000 NA
#&gt; SRR1283403     4  0.0000      0.997 0.000 0.000 0.000 1.000 NA
#&gt; SRR1283404     4  0.0000      0.997 0.000 0.000 0.000 1.000 NA
#&gt; SRR1283405     4  0.0162      0.995 0.000 0.000 0.004 0.996 NA
#&gt; SRR1283406     1  0.1918      0.949 0.928 0.000 0.036 0.000 NA
#&gt; SRR1283407     1  0.1918      0.949 0.928 0.000 0.036 0.000 NA
#&gt; SRR1283408     1  0.1918      0.949 0.928 0.000 0.036 0.000 NA
#&gt; SRR1283409     1  0.2353      0.937 0.908 0.000 0.060 0.004 NA
#&gt; SRR1283410     1  0.2353      0.937 0.908 0.000 0.060 0.004 NA
#&gt; SRR1283411     1  0.2419      0.934 0.904 0.000 0.064 0.004 NA
#&gt; SRR1283412     1  0.0510      0.971 0.984 0.000 0.000 0.000 NA
#&gt; SRR1283413     1  0.0510      0.971 0.984 0.000 0.000 0.000 NA
#&gt; SRR1283414     1  0.0404      0.972 0.988 0.000 0.000 0.000 NA
#&gt; SRR1283415     1  0.1281      0.961 0.956 0.000 0.032 0.000 NA
#&gt; SRR1283416     1  0.1281      0.961 0.956 0.000 0.032 0.000 NA
#&gt; SRR1283417     1  0.1364      0.961 0.952 0.000 0.036 0.000 NA
#&gt; SRR1283418     1  0.0000      0.973 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0162      0.973 0.996 0.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0000      0.973 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0000      0.973 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0000      0.973 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0000      0.973 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.0162      0.973 0.996 0.000 0.000 0.000 NA
#&gt; SRR1283425     1  0.0162      0.973 0.996 0.000 0.000 0.000 NA
#&gt; SRR1283426     1  0.0162      0.973 0.996 0.000 0.000 0.000 NA
#&gt; SRR1283427     1  0.0771      0.967 0.976 0.000 0.020 0.000 NA
#&gt; SRR1283428     1  0.0771      0.967 0.976 0.000 0.020 0.000 NA
#&gt; SRR1283429     1  0.0771      0.967 0.976 0.000 0.020 0.000 NA
#&gt; SRR1283430     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283431     2  0.0404      0.976 0.000 0.988 0.000 0.000 NA
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1283379     3  0.3023      1.000 0.000 0.000 0.768 0.232 0.000 NA
#&gt; SRR1283380     3  0.3023      1.000 0.000 0.000 0.768 0.232 0.000 NA
#&gt; SRR1283381     3  0.3023      1.000 0.000 0.000 0.768 0.232 0.000 NA
#&gt; SRR1283385     2  0.2442      0.917 0.000 0.852 0.000 0.000 0.004 NA
#&gt; SRR1283386     2  0.2442      0.917 0.000 0.852 0.000 0.000 0.004 NA
#&gt; SRR1283387     2  0.2482      0.916 0.000 0.848 0.000 0.000 0.004 NA
#&gt; SRR1283388     2  0.1610      0.935 0.000 0.916 0.000 0.000 0.000 NA
#&gt; SRR1283389     2  0.1610      0.935 0.000 0.916 0.000 0.000 0.000 NA
#&gt; SRR1283390     2  0.1610      0.935 0.000 0.916 0.000 0.000 0.000 NA
#&gt; SRR1283382     2  0.1588      0.923 0.000 0.924 0.000 0.000 0.004 NA
#&gt; SRR1283383     2  0.1588      0.923 0.000 0.924 0.000 0.000 0.004 NA
#&gt; SRR1283384     2  0.1644      0.923 0.000 0.920 0.000 0.000 0.004 NA
#&gt; SRR1283391     2  0.0806      0.934 0.000 0.972 0.000 0.000 0.020 NA
#&gt; SRR1283392     2  0.0806      0.934 0.000 0.972 0.000 0.000 0.020 NA
#&gt; SRR1283393     2  0.0603      0.935 0.000 0.980 0.000 0.000 0.016 NA
#&gt; SRR1283394     2  0.1957      0.932 0.000 0.888 0.000 0.000 0.000 NA
#&gt; SRR1283395     2  0.1910      0.932 0.000 0.892 0.000 0.000 0.000 NA
#&gt; SRR1283396     2  0.1957      0.932 0.000 0.888 0.000 0.000 0.000 NA
#&gt; SRR1283397     2  0.0458      0.936 0.000 0.984 0.000 0.000 0.016 NA
#&gt; SRR1283398     2  0.0458      0.936 0.000 0.984 0.000 0.000 0.016 NA
#&gt; SRR1283399     2  0.0458      0.936 0.000 0.984 0.000 0.000 0.016 NA
#&gt; SRR1283400     2  0.0603      0.936 0.000 0.980 0.000 0.000 0.016 NA
#&gt; SRR1283401     2  0.0458      0.936 0.000 0.984 0.000 0.000 0.016 NA
#&gt; SRR1283402     2  0.0914      0.936 0.000 0.968 0.000 0.000 0.016 NA
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283406     1  0.1700      0.920 0.916 0.000 0.000 0.000 0.080 NA
#&gt; SRR1283407     1  0.1700      0.920 0.916 0.000 0.000 0.000 0.080 NA
#&gt; SRR1283408     1  0.1753      0.919 0.912 0.000 0.000 0.000 0.084 NA
#&gt; SRR1283409     1  0.2100      0.904 0.884 0.000 0.000 0.000 0.112 NA
#&gt; SRR1283410     1  0.2053      0.907 0.888 0.000 0.000 0.000 0.108 NA
#&gt; SRR1283411     1  0.2146      0.902 0.880 0.000 0.000 0.000 0.116 NA
#&gt; SRR1283412     1  0.0260      0.942 0.992 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283413     1  0.0260      0.942 0.992 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283414     1  0.0260      0.942 0.992 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283415     1  0.3298      0.783 0.756 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283416     1  0.3323      0.779 0.752 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283417     1  0.3271      0.788 0.760 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283418     1  0.0146      0.942 0.996 0.000 0.000 0.000 0.004 NA
#&gt; SRR1283419     1  0.0146      0.942 0.996 0.000 0.000 0.000 0.004 NA
#&gt; SRR1283420     1  0.0146      0.942 0.996 0.000 0.000 0.000 0.004 NA
#&gt; SRR1283421     1  0.0146      0.942 0.996 0.000 0.000 0.000 0.004 NA
#&gt; SRR1283422     1  0.0146      0.942 0.996 0.000 0.000 0.000 0.004 NA
#&gt; SRR1283423     1  0.0260      0.942 0.992 0.000 0.000 0.000 0.008 NA
#&gt; SRR1283424     1  0.0260      0.942 0.992 0.000 0.000 0.000 0.000 NA
#&gt; SRR1283425     1  0.0291      0.942 0.992 0.000 0.004 0.000 0.000 NA
#&gt; SRR1283426     1  0.0260      0.942 0.992 0.000 0.000 0.000 0.000 NA
#&gt; SRR1283427     1  0.1075      0.931 0.952 0.000 0.000 0.000 0.000 NA
#&gt; SRR1283428     1  0.1141      0.930 0.948 0.000 0.000 0.000 0.000 NA
#&gt; SRR1283429     1  0.1075      0.931 0.952 0.000 0.000 0.000 0.000 NA
#&gt; SRR1283430     2  0.1765      0.934 0.000 0.904 0.000 0.000 0.000 NA
#&gt; SRR1283431     2  0.1814      0.934 0.000 0.900 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.493           0.836       0.880         0.2796 0.795   0.795
#> 3 3 1.000           0.980       0.986         1.1264 0.599   0.496
#> 4 4 1.000           1.000       1.000         0.0297 0.993   0.983
#> 5 5 1.000           1.000       1.000         0.0746 0.954   0.882
#> 6 6 1.000           0.989       0.992         0.1130 0.926   0.784
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 3 5
```

There is also optional best $k$ = 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     1   0.000      0.812 1.000 0.000
#&gt; SRR1283380     1   0.000      0.812 1.000 0.000
#&gt; SRR1283381     1   0.000      0.812 1.000 0.000
#&gt; SRR1283385     2   0.802      0.835 0.244 0.756
#&gt; SRR1283386     2   0.802      0.835 0.244 0.756
#&gt; SRR1283387     2   0.802      0.835 0.244 0.756
#&gt; SRR1283388     2   0.802      0.835 0.244 0.756
#&gt; SRR1283389     2   0.802      0.835 0.244 0.756
#&gt; SRR1283390     2   0.802      0.835 0.244 0.756
#&gt; SRR1283382     2   0.802      0.835 0.244 0.756
#&gt; SRR1283383     2   0.802      0.835 0.244 0.756
#&gt; SRR1283384     2   0.802      0.835 0.244 0.756
#&gt; SRR1283391     2   0.802      0.835 0.244 0.756
#&gt; SRR1283392     2   0.802      0.835 0.244 0.756
#&gt; SRR1283393     2   0.802      0.835 0.244 0.756
#&gt; SRR1283394     2   0.802      0.835 0.244 0.756
#&gt; SRR1283395     2   0.802      0.835 0.244 0.756
#&gt; SRR1283396     2   0.802      0.835 0.244 0.756
#&gt; SRR1283397     2   0.802      0.835 0.244 0.756
#&gt; SRR1283398     2   0.802      0.835 0.244 0.756
#&gt; SRR1283399     2   0.802      0.835 0.244 0.756
#&gt; SRR1283400     2   0.802      0.835 0.244 0.756
#&gt; SRR1283401     2   0.802      0.835 0.244 0.756
#&gt; SRR1283402     2   0.802      0.835 0.244 0.756
#&gt; SRR1283403     1   0.802      0.811 0.756 0.244
#&gt; SRR1283404     1   0.802      0.811 0.756 0.244
#&gt; SRR1283405     1   0.802      0.811 0.756 0.244
#&gt; SRR1283406     2   0.000      0.843 0.000 1.000
#&gt; SRR1283407     2   0.000      0.843 0.000 1.000
#&gt; SRR1283408     2   0.000      0.843 0.000 1.000
#&gt; SRR1283409     2   0.000      0.843 0.000 1.000
#&gt; SRR1283410     2   0.000      0.843 0.000 1.000
#&gt; SRR1283411     2   0.000      0.843 0.000 1.000
#&gt; SRR1283412     2   0.000      0.843 0.000 1.000
#&gt; SRR1283413     2   0.000      0.843 0.000 1.000
#&gt; SRR1283414     2   0.000      0.843 0.000 1.000
#&gt; SRR1283415     2   0.000      0.843 0.000 1.000
#&gt; SRR1283416     2   0.000      0.843 0.000 1.000
#&gt; SRR1283417     2   0.000      0.843 0.000 1.000
#&gt; SRR1283418     2   0.000      0.843 0.000 1.000
#&gt; SRR1283419     2   0.000      0.843 0.000 1.000
#&gt; SRR1283420     2   0.000      0.843 0.000 1.000
#&gt; SRR1283421     2   0.000      0.843 0.000 1.000
#&gt; SRR1283422     2   0.000      0.843 0.000 1.000
#&gt; SRR1283423     2   0.000      0.843 0.000 1.000
#&gt; SRR1283424     2   0.000      0.843 0.000 1.000
#&gt; SRR1283425     2   0.000      0.843 0.000 1.000
#&gt; SRR1283426     2   0.000      0.843 0.000 1.000
#&gt; SRR1283427     2   0.000      0.843 0.000 1.000
#&gt; SRR1283428     2   0.000      0.843 0.000 1.000
#&gt; SRR1283429     2   0.000      0.843 0.000 1.000
#&gt; SRR1283430     2   0.802      0.835 0.244 0.756
#&gt; SRR1283431     2   0.802      0.835 0.244 0.756
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1283379     3   0.000      0.848 0.000  0 1.000
#&gt; SRR1283380     3   0.000      0.848 0.000  0 1.000
#&gt; SRR1283381     3   0.000      0.848 0.000  0 1.000
#&gt; SRR1283385     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283386     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283387     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283403     3   0.506      0.806 0.244  0 0.756
#&gt; SRR1283404     3   0.506      0.806 0.244  0 0.756
#&gt; SRR1283405     3   0.506      0.806 0.244  0 0.756
#&gt; SRR1283406     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283407     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283408     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283409     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283410     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283411     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283412     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283413     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283414     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283415     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283416     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283417     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283418     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283419     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283420     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283421     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283422     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283423     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283424     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283425     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283426     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283427     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283428     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283429     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1283430     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000  1 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5
#&gt; SRR1283379     3       0          1  0  0  1  0  0
#&gt; SRR1283380     3       0          1  0  0  1  0  0
#&gt; SRR1283381     3       0          1  0  0  1  0  0
#&gt; SRR1283385     2       0          1  0  1  0  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1  0
#&gt; SRR1283404     4       0          1  0  0  0  1  0
#&gt; SRR1283405     4       0          1  0  0  0  1  0
#&gt; SRR1283406     1       0          1  1  0  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0  0
#&gt; SRR1283415     5       0          1  0  0  0  0  1
#&gt; SRR1283416     5       0          1  0  0  0  0  1
#&gt; SRR1283417     5       0          1  0  0  0  0  1
#&gt; SRR1283418     1       0          1  1  0  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2 p3 p4    p5 p6
#&gt; SRR1283379     3  0.0000      1.000  0 0.000  1  0 0.000  0
#&gt; SRR1283380     3  0.0000      1.000  0 0.000  1  0 0.000  0
#&gt; SRR1283381     3  0.0000      1.000  0 0.000  1  0 0.000  0
#&gt; SRR1283385     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283386     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283387     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283388     2  0.0937      0.966  0 0.960  0  0 0.040  0
#&gt; SRR1283389     2  0.0937      0.966  0 0.960  0  0 0.040  0
#&gt; SRR1283390     2  0.0937      0.966  0 0.960  0  0 0.040  0
#&gt; SRR1283382     2  0.0000      0.979  0 1.000  0  0 0.000  0
#&gt; SRR1283383     2  0.0000      0.979  0 1.000  0  0 0.000  0
#&gt; SRR1283384     2  0.0000      0.979  0 1.000  0  0 0.000  0
#&gt; SRR1283391     5  0.0146      0.977  0 0.004  0  0 0.996  0
#&gt; SRR1283392     5  0.0146      0.977  0 0.004  0  0 0.996  0
#&gt; SRR1283393     5  0.0146      0.977  0 0.004  0  0 0.996  0
#&gt; SRR1283394     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283395     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283396     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283397     2  0.1204      0.956  0 0.944  0  0 0.056  0
#&gt; SRR1283398     2  0.1075      0.962  0 0.952  0  0 0.048  0
#&gt; SRR1283399     2  0.1204      0.956  0 0.944  0  0 0.056  0
#&gt; SRR1283400     5  0.0713      0.977  0 0.028  0  0 0.972  0
#&gt; SRR1283401     5  0.0713      0.977  0 0.028  0  0 0.972  0
#&gt; SRR1283402     5  0.0713      0.977  0 0.028  0  0 0.972  0
#&gt; SRR1283403     4  0.0000      1.000  0 0.000  0  1 0.000  0
#&gt; SRR1283404     4  0.0000      1.000  0 0.000  0  1 0.000  0
#&gt; SRR1283405     4  0.0000      1.000  0 0.000  0  1 0.000  0
#&gt; SRR1283406     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283407     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283408     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283409     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283410     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283411     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283412     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283413     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283414     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283415     6  0.0000      1.000  0 0.000  0  0 0.000  1
#&gt; SRR1283416     6  0.0000      1.000  0 0.000  0  0 0.000  1
#&gt; SRR1283417     6  0.0000      1.000  0 0.000  0  0 0.000  1
#&gt; SRR1283418     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283419     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283420     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283421     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283422     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283423     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283424     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283425     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283426     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283427     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283428     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283429     1  0.0000      1.000  1 0.000  0  0 0.000  0
#&gt; SRR1283430     2  0.0146      0.979  0 0.996  0  0 0.004  0
#&gt; SRR1283431     2  0.0146      0.979  0 0.996  0  0 0.004  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.491           0.909       0.872         0.4384 0.491   0.491
#> 3 3 1.000           0.972       0.971         0.3448 0.891   0.781
#> 4 4 0.747           0.857       0.888         0.1127 1.000   1.000
#> 5 5 0.736           0.804       0.776         0.0888 0.922   0.801
#> 6 6 0.706           0.754       0.754         0.0629 0.926   0.766
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     2   1.000      0.395 0.492 0.508
#&gt; SRR1283380     2   1.000      0.395 0.492 0.508
#&gt; SRR1283381     2   1.000      0.395 0.492 0.508
#&gt; SRR1283385     2   0.000      0.942 0.000 1.000
#&gt; SRR1283386     2   0.000      0.942 0.000 1.000
#&gt; SRR1283387     2   0.000      0.942 0.000 1.000
#&gt; SRR1283388     2   0.000      0.942 0.000 1.000
#&gt; SRR1283389     2   0.000      0.942 0.000 1.000
#&gt; SRR1283390     2   0.000      0.942 0.000 1.000
#&gt; SRR1283382     2   0.000      0.942 0.000 1.000
#&gt; SRR1283383     2   0.000      0.942 0.000 1.000
#&gt; SRR1283384     2   0.000      0.942 0.000 1.000
#&gt; SRR1283391     2   0.000      0.942 0.000 1.000
#&gt; SRR1283392     2   0.000      0.942 0.000 1.000
#&gt; SRR1283393     2   0.000      0.942 0.000 1.000
#&gt; SRR1283394     2   0.000      0.942 0.000 1.000
#&gt; SRR1283395     2   0.000      0.942 0.000 1.000
#&gt; SRR1283396     2   0.000      0.942 0.000 1.000
#&gt; SRR1283397     2   0.000      0.942 0.000 1.000
#&gt; SRR1283398     2   0.000      0.942 0.000 1.000
#&gt; SRR1283399     2   0.000      0.942 0.000 1.000
#&gt; SRR1283400     2   0.000      0.942 0.000 1.000
#&gt; SRR1283401     2   0.000      0.942 0.000 1.000
#&gt; SRR1283402     2   0.000      0.942 0.000 1.000
#&gt; SRR1283403     1   0.000      0.722 1.000 0.000
#&gt; SRR1283404     1   0.000      0.722 1.000 0.000
#&gt; SRR1283405     1   0.000      0.722 1.000 0.000
#&gt; SRR1283406     1   0.775      0.964 0.772 0.228
#&gt; SRR1283407     1   0.775      0.964 0.772 0.228
#&gt; SRR1283408     1   0.775      0.964 0.772 0.228
#&gt; SRR1283409     1   0.775      0.964 0.772 0.228
#&gt; SRR1283410     1   0.775      0.964 0.772 0.228
#&gt; SRR1283411     1   0.775      0.964 0.772 0.228
#&gt; SRR1283412     1   0.775      0.964 0.772 0.228
#&gt; SRR1283413     1   0.775      0.964 0.772 0.228
#&gt; SRR1283414     1   0.775      0.964 0.772 0.228
#&gt; SRR1283415     1   0.775      0.964 0.772 0.228
#&gt; SRR1283416     1   0.775      0.964 0.772 0.228
#&gt; SRR1283417     1   0.775      0.964 0.772 0.228
#&gt; SRR1283418     1   0.775      0.964 0.772 0.228
#&gt; SRR1283419     1   0.775      0.964 0.772 0.228
#&gt; SRR1283420     1   0.775      0.964 0.772 0.228
#&gt; SRR1283421     1   0.775      0.964 0.772 0.228
#&gt; SRR1283422     1   0.775      0.964 0.772 0.228
#&gt; SRR1283423     1   0.775      0.964 0.772 0.228
#&gt; SRR1283424     1   0.775      0.964 0.772 0.228
#&gt; SRR1283425     1   0.775      0.964 0.772 0.228
#&gt; SRR1283426     1   0.775      0.964 0.772 0.228
#&gt; SRR1283427     1   0.775      0.964 0.772 0.228
#&gt; SRR1283428     1   0.775      0.964 0.772 0.228
#&gt; SRR1283429     1   0.775      0.964 0.772 0.228
#&gt; SRR1283430     2   0.000      0.942 0.000 1.000
#&gt; SRR1283431     2   0.000      0.942 0.000 1.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1283379     3  0.1774      0.835 0.024 0.016 0.960
#&gt; SRR1283380     3  0.1774      0.835 0.024 0.016 0.960
#&gt; SRR1283381     3  0.1774      0.835 0.024 0.016 0.960
#&gt; SRR1283385     2  0.0237      0.993 0.000 0.996 0.004
#&gt; SRR1283386     2  0.0237      0.993 0.000 0.996 0.004
#&gt; SRR1283387     2  0.0237      0.993 0.000 0.996 0.004
#&gt; SRR1283388     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283389     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283390     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283382     2  0.0000      0.993 0.000 1.000 0.000
#&gt; SRR1283383     2  0.0000      0.993 0.000 1.000 0.000
#&gt; SRR1283384     2  0.0000      0.993 0.000 1.000 0.000
#&gt; SRR1283391     2  0.0747      0.988 0.000 0.984 0.016
#&gt; SRR1283392     2  0.0747      0.988 0.000 0.984 0.016
#&gt; SRR1283393     2  0.0747      0.988 0.000 0.984 0.016
#&gt; SRR1283394     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283395     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283396     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283397     2  0.0000      0.993 0.000 1.000 0.000
#&gt; SRR1283398     2  0.0000      0.993 0.000 1.000 0.000
#&gt; SRR1283399     2  0.0000      0.993 0.000 1.000 0.000
#&gt; SRR1283400     2  0.0747      0.988 0.000 0.984 0.016
#&gt; SRR1283401     2  0.0747      0.988 0.000 0.984 0.016
#&gt; SRR1283402     2  0.0747      0.988 0.000 0.984 0.016
#&gt; SRR1283403     3  0.5497      0.786 0.292 0.000 0.708
#&gt; SRR1283404     3  0.5497      0.786 0.292 0.000 0.708
#&gt; SRR1283405     3  0.5497      0.786 0.292 0.000 0.708
#&gt; SRR1283406     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283407     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283408     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283409     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283410     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283411     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283412     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283413     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283414     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283415     1  0.1337      0.986 0.972 0.012 0.016
#&gt; SRR1283416     1  0.1337      0.986 0.972 0.012 0.016
#&gt; SRR1283417     1  0.1337      0.986 0.972 0.012 0.016
#&gt; SRR1283418     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283419     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283420     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283421     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283422     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283423     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283424     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283425     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283426     1  0.0592      0.995 0.988 0.012 0.000
#&gt; SRR1283427     1  0.1337      0.986 0.972 0.012 0.016
#&gt; SRR1283428     1  0.1337      0.986 0.972 0.012 0.016
#&gt; SRR1283429     1  0.1337      0.986 0.972 0.012 0.016
#&gt; SRR1283430     2  0.0424      0.992 0.000 0.992 0.008
#&gt; SRR1283431     2  0.0424      0.992 0.000 0.992 0.008
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1283379     3  0.4277      0.850 0.000 0.000 0.720 NA
#&gt; SRR1283380     3  0.4277      0.850 0.000 0.000 0.720 NA
#&gt; SRR1283381     3  0.4277      0.850 0.000 0.000 0.720 NA
#&gt; SRR1283385     2  0.2530      0.884 0.000 0.888 0.000 NA
#&gt; SRR1283386     2  0.2530      0.884 0.000 0.888 0.000 NA
#&gt; SRR1283387     2  0.2530      0.884 0.000 0.888 0.000 NA
#&gt; SRR1283388     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283389     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283390     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283382     2  0.2281      0.885 0.000 0.904 0.000 NA
#&gt; SRR1283383     2  0.2281      0.885 0.000 0.904 0.000 NA
#&gt; SRR1283384     2  0.2281      0.885 0.000 0.904 0.000 NA
#&gt; SRR1283391     2  0.3801      0.819 0.000 0.780 0.000 NA
#&gt; SRR1283392     2  0.3801      0.819 0.000 0.780 0.000 NA
#&gt; SRR1283393     2  0.3801      0.819 0.000 0.780 0.000 NA
#&gt; SRR1283394     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283395     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283396     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283397     2  0.0000      0.909 0.000 1.000 0.000 NA
#&gt; SRR1283398     2  0.0000      0.909 0.000 1.000 0.000 NA
#&gt; SRR1283399     2  0.0000      0.909 0.000 1.000 0.000 NA
#&gt; SRR1283400     2  0.3726      0.820 0.000 0.788 0.000 NA
#&gt; SRR1283401     2  0.3764      0.820 0.000 0.784 0.000 NA
#&gt; SRR1283402     2  0.3764      0.820 0.000 0.784 0.000 NA
#&gt; SRR1283403     3  0.2760      0.831 0.128 0.000 0.872 NA
#&gt; SRR1283404     3  0.2760      0.831 0.128 0.000 0.872 NA
#&gt; SRR1283405     3  0.2760      0.831 0.128 0.000 0.872 NA
#&gt; SRR1283406     1  0.1792      0.863 0.932 0.000 0.000 NA
#&gt; SRR1283407     1  0.1792      0.863 0.932 0.000 0.000 NA
#&gt; SRR1283408     1  0.1792      0.863 0.932 0.000 0.000 NA
#&gt; SRR1283409     1  0.0707      0.891 0.980 0.000 0.000 NA
#&gt; SRR1283410     1  0.0707      0.891 0.980 0.000 0.000 NA
#&gt; SRR1283411     1  0.0707      0.891 0.980 0.000 0.000 NA
#&gt; SRR1283412     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283413     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283414     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283415     1  0.4543      0.685 0.676 0.000 0.000 NA
#&gt; SRR1283416     1  0.4543      0.685 0.676 0.000 0.000 NA
#&gt; SRR1283417     1  0.4543      0.685 0.676 0.000 0.000 NA
#&gt; SRR1283418     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283425     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283426     1  0.0000      0.898 1.000 0.000 0.000 NA
#&gt; SRR1283427     1  0.4543      0.685 0.676 0.000 0.000 NA
#&gt; SRR1283428     1  0.4543      0.685 0.676 0.000 0.000 NA
#&gt; SRR1283429     1  0.4543      0.685 0.676 0.000 0.000 NA
#&gt; SRR1283430     2  0.0817      0.910 0.000 0.976 0.000 NA
#&gt; SRR1283431     2  0.0817      0.910 0.000 0.976 0.000 NA
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1283379     3  0.0162      0.814 0.000 0.000 0.996 0.004 NA
#&gt; SRR1283380     3  0.0000      0.814 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283381     3  0.0000      0.814 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283385     2  0.3966      0.723 0.000 0.664 0.000 0.000 NA
#&gt; SRR1283386     2  0.3966      0.723 0.000 0.664 0.000 0.000 NA
#&gt; SRR1283387     2  0.3966      0.723 0.000 0.664 0.000 0.000 NA
#&gt; SRR1283388     2  0.0162      0.777 0.000 0.996 0.000 0.000 NA
#&gt; SRR1283389     2  0.0162      0.777 0.000 0.996 0.000 0.000 NA
#&gt; SRR1283390     2  0.0162      0.777 0.000 0.996 0.000 0.000 NA
#&gt; SRR1283382     2  0.3895      0.727 0.000 0.680 0.000 0.000 NA
#&gt; SRR1283383     2  0.3895      0.727 0.000 0.680 0.000 0.000 NA
#&gt; SRR1283384     2  0.3895      0.727 0.000 0.680 0.000 0.000 NA
#&gt; SRR1283391     2  0.6478      0.595 0.000 0.488 0.000 0.292 NA
#&gt; SRR1283392     2  0.6478      0.595 0.000 0.488 0.000 0.292 NA
#&gt; SRR1283393     2  0.6478      0.595 0.000 0.488 0.000 0.292 NA
#&gt; SRR1283394     2  0.0693      0.776 0.000 0.980 0.000 0.012 NA
#&gt; SRR1283395     2  0.0451      0.776 0.000 0.988 0.000 0.004 NA
#&gt; SRR1283396     2  0.0404      0.776 0.000 0.988 0.000 0.000 NA
#&gt; SRR1283397     2  0.2077      0.785 0.000 0.908 0.000 0.008 NA
#&gt; SRR1283398     2  0.2077      0.785 0.000 0.908 0.000 0.008 NA
#&gt; SRR1283399     2  0.2077      0.785 0.000 0.908 0.000 0.008 NA
#&gt; SRR1283400     2  0.6459      0.602 0.000 0.500 0.000 0.256 NA
#&gt; SRR1283401     2  0.6477      0.601 0.000 0.496 0.000 0.256 NA
#&gt; SRR1283402     2  0.6477      0.601 0.000 0.496 0.000 0.256 NA
#&gt; SRR1283403     3  0.6732      0.800 0.068 0.000 0.560 0.092 NA
#&gt; SRR1283404     3  0.6784      0.800 0.068 0.000 0.560 0.100 NA
#&gt; SRR1283405     3  0.6732      0.800 0.068 0.000 0.560 0.092 NA
#&gt; SRR1283406     1  0.3724      0.723 0.788 0.000 0.000 0.028 NA
#&gt; SRR1283407     1  0.3724      0.723 0.788 0.000 0.000 0.028 NA
#&gt; SRR1283408     1  0.3724      0.723 0.788 0.000 0.000 0.028 NA
#&gt; SRR1283409     1  0.2685      0.834 0.880 0.000 0.000 0.028 NA
#&gt; SRR1283410     1  0.2685      0.834 0.880 0.000 0.000 0.028 NA
#&gt; SRR1283411     1  0.2685      0.834 0.880 0.000 0.000 0.028 NA
#&gt; SRR1283412     1  0.0865      0.893 0.972 0.000 0.000 0.004 NA
#&gt; SRR1283413     1  0.0865      0.893 0.972 0.000 0.000 0.004 NA
#&gt; SRR1283414     1  0.0865      0.893 0.972 0.000 0.000 0.004 NA
#&gt; SRR1283415     4  0.4542      0.979 0.456 0.000 0.000 0.536 NA
#&gt; SRR1283416     4  0.4542      0.979 0.456 0.000 0.000 0.536 NA
#&gt; SRR1283417     4  0.4283      0.981 0.456 0.000 0.000 0.544 NA
#&gt; SRR1283418     1  0.0000      0.897 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0000      0.897 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0000      0.897 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0000      0.897 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0000      0.897 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0000      0.897 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.0290      0.892 0.992 0.000 0.000 0.000 NA
#&gt; SRR1283425     1  0.0290      0.892 0.992 0.000 0.000 0.000 NA
#&gt; SRR1283426     1  0.0290      0.892 0.992 0.000 0.000 0.000 NA
#&gt; SRR1283427     4  0.4552      0.982 0.468 0.000 0.000 0.524 NA
#&gt; SRR1283428     4  0.4552      0.982 0.468 0.000 0.000 0.524 NA
#&gt; SRR1283429     4  0.4552      0.982 0.468 0.000 0.000 0.524 NA
#&gt; SRR1283430     2  0.0162      0.777 0.000 0.996 0.000 0.000 NA
#&gt; SRR1283431     2  0.0162      0.777 0.000 0.996 0.000 0.000 NA
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1283379     3  0.3847      0.772 0.000 0.000 0.544 0.000 NA 0.000
#&gt; SRR1283380     3  0.4284      0.772 0.004 0.012 0.544 0.000 NA 0.000
#&gt; SRR1283381     3  0.3847      0.772 0.000 0.000 0.544 0.000 NA 0.000
#&gt; SRR1283385     2  0.7328      0.461 0.180 0.360 0.000 0.324 NA 0.000
#&gt; SRR1283386     2  0.7328      0.461 0.180 0.360 0.000 0.324 NA 0.000
#&gt; SRR1283387     2  0.7328      0.461 0.180 0.360 0.000 0.324 NA 0.000
#&gt; SRR1283388     2  0.3244      0.699 0.000 0.732 0.000 0.268 NA 0.000
#&gt; SRR1283389     2  0.3244      0.699 0.000 0.732 0.000 0.268 NA 0.000
#&gt; SRR1283390     2  0.3244      0.699 0.000 0.732 0.000 0.268 NA 0.000
#&gt; SRR1283382     2  0.7179      0.497 0.184 0.396 0.000 0.308 NA 0.000
#&gt; SRR1283383     2  0.7179      0.497 0.184 0.396 0.000 0.308 NA 0.000
#&gt; SRR1283384     2  0.7179      0.497 0.184 0.396 0.000 0.308 NA 0.000
#&gt; SRR1283391     4  0.0858      0.913 0.004 0.000 0.000 0.968 NA 0.000
#&gt; SRR1283392     4  0.0858      0.913 0.004 0.000 0.000 0.968 NA 0.000
#&gt; SRR1283393     4  0.0858      0.913 0.004 0.000 0.000 0.968 NA 0.000
#&gt; SRR1283394     2  0.4528      0.678 0.012 0.680 0.000 0.260 NA 0.000
#&gt; SRR1283395     2  0.4130      0.684 0.012 0.704 0.000 0.260 NA 0.000
#&gt; SRR1283396     2  0.4405      0.680 0.012 0.688 0.000 0.260 NA 0.000
#&gt; SRR1283397     2  0.3986      0.656 0.004 0.608 0.000 0.384 NA 0.000
#&gt; SRR1283398     2  0.3986      0.656 0.004 0.608 0.000 0.384 NA 0.000
#&gt; SRR1283399     2  0.3986      0.656 0.004 0.608 0.000 0.384 NA 0.000
#&gt; SRR1283400     4  0.2566      0.910 0.020 0.028 0.000 0.888 NA 0.000
#&gt; SRR1283401     4  0.2566      0.910 0.020 0.028 0.000 0.888 NA 0.000
#&gt; SRR1283402     4  0.2566      0.910 0.020 0.028 0.000 0.888 NA 0.000
#&gt; SRR1283403     3  0.1074      0.770 0.012 0.000 0.960 0.000 NA 0.028
#&gt; SRR1283404     3  0.1074      0.770 0.012 0.000 0.960 0.000 NA 0.028
#&gt; SRR1283405     3  0.1074      0.770 0.012 0.000 0.960 0.000 NA 0.028
#&gt; SRR1283406     1  0.6550      0.599 0.512 0.064 0.000 0.000 NA 0.236
#&gt; SRR1283407     1  0.6550      0.599 0.512 0.064 0.000 0.000 NA 0.236
#&gt; SRR1283408     1  0.6550      0.599 0.512 0.064 0.000 0.000 NA 0.236
#&gt; SRR1283409     1  0.5670      0.727 0.608 0.060 0.000 0.000 NA 0.256
#&gt; SRR1283410     1  0.5670      0.727 0.608 0.060 0.000 0.000 NA 0.256
#&gt; SRR1283411     1  0.5670      0.727 0.608 0.060 0.000 0.000 NA 0.256
#&gt; SRR1283412     1  0.4025      0.825 0.668 0.016 0.000 0.000 NA 0.312
#&gt; SRR1283413     1  0.4025      0.825 0.668 0.016 0.000 0.000 NA 0.312
#&gt; SRR1283414     1  0.4025      0.825 0.668 0.016 0.000 0.000 NA 0.312
#&gt; SRR1283415     6  0.2001      0.941 0.000 0.048 0.000 0.000 NA 0.912
#&gt; SRR1283416     6  0.2134      0.938 0.000 0.052 0.000 0.000 NA 0.904
#&gt; SRR1283417     6  0.1765      0.943 0.000 0.052 0.000 0.000 NA 0.924
#&gt; SRR1283418     1  0.4034      0.829 0.624 0.008 0.000 0.000 NA 0.364
#&gt; SRR1283419     1  0.4034      0.829 0.624 0.008 0.000 0.000 NA 0.364
#&gt; SRR1283420     1  0.4034      0.829 0.624 0.008 0.000 0.000 NA 0.364
#&gt; SRR1283421     1  0.3659      0.829 0.636 0.000 0.000 0.000 NA 0.364
#&gt; SRR1283422     1  0.3659      0.829 0.636 0.000 0.000 0.000 NA 0.364
#&gt; SRR1283423     1  0.3659      0.829 0.636 0.000 0.000 0.000 NA 0.364
#&gt; SRR1283424     1  0.3774      0.805 0.592 0.000 0.000 0.000 NA 0.408
#&gt; SRR1283425     1  0.3774      0.805 0.592 0.000 0.000 0.000 NA 0.408
#&gt; SRR1283426     1  0.3774      0.805 0.592 0.000 0.000 0.000 NA 0.408
#&gt; SRR1283427     6  0.0146      0.946 0.004 0.000 0.000 0.000 NA 0.996
#&gt; SRR1283428     6  0.0146      0.946 0.004 0.000 0.000 0.000 NA 0.996
#&gt; SRR1283429     6  0.0146      0.946 0.004 0.000 0.000 0.000 NA 0.996
#&gt; SRR1283430     2  0.3198      0.700 0.000 0.740 0.000 0.260 NA 0.000
#&gt; SRR1283431     2  0.3198      0.700 0.000 0.740 0.000 0.260 NA 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5099 0.491   0.491
#> 3 3 1.000           1.000       1.000         0.1877 0.891   0.781
#> 4 4 0.915           0.971       0.921         0.0903 0.922   0.801
#> 5 5 0.807           0.898       0.885         0.0776 0.993   0.979
#> 6 6 0.767           0.792       0.825         0.0658 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     2       0          1  0  1
#&gt; SRR1283380     2       0          1  0  1
#&gt; SRR1283381     2       0          1  0  1
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2   p3    p4
#&gt; SRR1283379     3  0.0000      0.869 0.000 0.000 1.00 0.000
#&gt; SRR1283380     3  0.0000      0.869 0.000 0.000 1.00 0.000
#&gt; SRR1283381     3  0.0000      0.869 0.000 0.000 1.00 0.000
#&gt; SRR1283385     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283386     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283387     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283388     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283389     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283390     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283382     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283383     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283384     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283391     2  0.0817      0.983 0.000 0.976 0.00 0.024
#&gt; SRR1283392     2  0.0817      0.983 0.000 0.976 0.00 0.024
#&gt; SRR1283393     2  0.0817      0.983 0.000 0.976 0.00 0.024
#&gt; SRR1283394     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283395     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283396     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283397     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283398     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283399     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283400     2  0.0817      0.983 0.000 0.976 0.00 0.024
#&gt; SRR1283401     2  0.0817      0.983 0.000 0.976 0.00 0.024
#&gt; SRR1283402     2  0.0817      0.983 0.000 0.976 0.00 0.024
#&gt; SRR1283403     3  0.4522      0.869 0.000 0.000 0.68 0.320
#&gt; SRR1283404     3  0.4522      0.869 0.000 0.000 0.68 0.320
#&gt; SRR1283405     3  0.4522      0.869 0.000 0.000 0.68 0.320
#&gt; SRR1283406     1  0.1118      0.951 0.964 0.000 0.00 0.036
#&gt; SRR1283407     1  0.1118      0.951 0.964 0.000 0.00 0.036
#&gt; SRR1283408     1  0.1118      0.951 0.964 0.000 0.00 0.036
#&gt; SRR1283409     1  0.0707      0.966 0.980 0.000 0.00 0.020
#&gt; SRR1283410     1  0.0707      0.966 0.980 0.000 0.00 0.020
#&gt; SRR1283411     1  0.0707      0.966 0.980 0.000 0.00 0.020
#&gt; SRR1283412     1  0.0000      0.977 1.000 0.000 0.00 0.000
#&gt; SRR1283413     1  0.0000      0.977 1.000 0.000 0.00 0.000
#&gt; SRR1283414     1  0.0000      0.977 1.000 0.000 0.00 0.000
#&gt; SRR1283415     4  0.4790      0.996 0.380 0.000 0.00 0.620
#&gt; SRR1283416     4  0.4790      0.996 0.380 0.000 0.00 0.620
#&gt; SRR1283417     4  0.4790      0.996 0.380 0.000 0.00 0.620
#&gt; SRR1283418     1  0.0336      0.977 0.992 0.000 0.00 0.008
#&gt; SRR1283419     1  0.0336      0.977 0.992 0.000 0.00 0.008
#&gt; SRR1283420     1  0.0336      0.977 0.992 0.000 0.00 0.008
#&gt; SRR1283421     1  0.0336      0.977 0.992 0.000 0.00 0.008
#&gt; SRR1283422     1  0.0336      0.977 0.992 0.000 0.00 0.008
#&gt; SRR1283423     1  0.0336      0.977 0.992 0.000 0.00 0.008
#&gt; SRR1283424     1  0.0469      0.975 0.988 0.000 0.00 0.012
#&gt; SRR1283425     1  0.0469      0.975 0.988 0.000 0.00 0.012
#&gt; SRR1283426     1  0.0469      0.975 0.988 0.000 0.00 0.012
#&gt; SRR1283427     4  0.4804      0.996 0.384 0.000 0.00 0.616
#&gt; SRR1283428     4  0.4804      0.996 0.384 0.000 0.00 0.616
#&gt; SRR1283429     4  0.4804      0.996 0.384 0.000 0.00 0.616
#&gt; SRR1283430     2  0.0000      0.994 0.000 1.000 0.00 0.000
#&gt; SRR1283431     2  0.0000      0.994 0.000 1.000 0.00 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2  p3    p4    p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000 1.0 0.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000 1.0 0.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000 1.0 0.000 0.000
#&gt; SRR1283385     2  0.1597      0.897 0.000 0.940 0.0 0.012 0.048
#&gt; SRR1283386     2  0.1670      0.897 0.000 0.936 0.0 0.012 0.052
#&gt; SRR1283387     2  0.1597      0.897 0.000 0.940 0.0 0.012 0.048
#&gt; SRR1283388     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283389     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283390     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283382     2  0.1281      0.898 0.000 0.956 0.0 0.012 0.032
#&gt; SRR1283383     2  0.1281      0.898 0.000 0.956 0.0 0.012 0.032
#&gt; SRR1283384     2  0.1281      0.898 0.000 0.956 0.0 0.012 0.032
#&gt; SRR1283391     2  0.3707      0.760 0.000 0.716 0.0 0.000 0.284
#&gt; SRR1283392     2  0.3707      0.760 0.000 0.716 0.0 0.000 0.284
#&gt; SRR1283393     2  0.3707      0.760 0.000 0.716 0.0 0.000 0.284
#&gt; SRR1283394     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283395     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283396     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283397     2  0.0162      0.910 0.000 0.996 0.0 0.000 0.004
#&gt; SRR1283398     2  0.0162      0.910 0.000 0.996 0.0 0.000 0.004
#&gt; SRR1283399     2  0.0290      0.909 0.000 0.992 0.0 0.000 0.008
#&gt; SRR1283400     2  0.3684      0.760 0.000 0.720 0.0 0.000 0.280
#&gt; SRR1283401     2  0.3707      0.760 0.000 0.716 0.0 0.000 0.284
#&gt; SRR1283402     2  0.3707      0.760 0.000 0.716 0.0 0.000 0.284
#&gt; SRR1283403     4  0.4182      1.000 0.000 0.000 0.4 0.600 0.000
#&gt; SRR1283404     4  0.4182      1.000 0.000 0.000 0.4 0.600 0.000
#&gt; SRR1283405     4  0.4182      1.000 0.000 0.000 0.4 0.600 0.000
#&gt; SRR1283406     1  0.3750      0.755 0.756 0.000 0.0 0.012 0.232
#&gt; SRR1283407     1  0.3750      0.755 0.756 0.000 0.0 0.012 0.232
#&gt; SRR1283408     1  0.3750      0.755 0.756 0.000 0.0 0.012 0.232
#&gt; SRR1283409     1  0.2464      0.856 0.888 0.000 0.0 0.016 0.096
#&gt; SRR1283410     1  0.2464      0.856 0.888 0.000 0.0 0.016 0.096
#&gt; SRR1283411     1  0.2464      0.856 0.888 0.000 0.0 0.016 0.096
#&gt; SRR1283412     1  0.0000      0.901 1.000 0.000 0.0 0.000 0.000
#&gt; SRR1283413     1  0.0000      0.901 1.000 0.000 0.0 0.000 0.000
#&gt; SRR1283414     1  0.0000      0.901 1.000 0.000 0.0 0.000 0.000
#&gt; SRR1283415     5  0.6428      1.000 0.180 0.000 0.0 0.364 0.456
#&gt; SRR1283416     5  0.6428      1.000 0.180 0.000 0.0 0.364 0.456
#&gt; SRR1283417     5  0.6428      1.000 0.180 0.000 0.0 0.364 0.456
#&gt; SRR1283418     1  0.1195      0.904 0.960 0.000 0.0 0.012 0.028
#&gt; SRR1283419     1  0.1195      0.904 0.960 0.000 0.0 0.012 0.028
#&gt; SRR1283420     1  0.1195      0.904 0.960 0.000 0.0 0.012 0.028
#&gt; SRR1283421     1  0.1195      0.904 0.960 0.000 0.0 0.012 0.028
#&gt; SRR1283422     1  0.1300      0.903 0.956 0.000 0.0 0.016 0.028
#&gt; SRR1283423     1  0.1300      0.903 0.956 0.000 0.0 0.016 0.028
#&gt; SRR1283424     1  0.1582      0.897 0.944 0.000 0.0 0.028 0.028
#&gt; SRR1283425     1  0.1661      0.892 0.940 0.000 0.0 0.024 0.036
#&gt; SRR1283426     1  0.1399      0.901 0.952 0.000 0.0 0.020 0.028
#&gt; SRR1283427     5  0.6428      1.000 0.180 0.000 0.0 0.364 0.456
#&gt; SRR1283428     5  0.6428      1.000 0.180 0.000 0.0 0.364 0.456
#&gt; SRR1283429     5  0.6428      1.000 0.180 0.000 0.0 0.364 0.456
#&gt; SRR1283430     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
#&gt; SRR1283431     2  0.0162      0.910 0.000 0.996 0.0 0.004 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000 1.000 0.000 NA 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000 1.000 0.000 NA 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000 1.000 0.000 NA 0.000
#&gt; SRR1283385     2  0.4278      0.714 0.000 0.720 0.000 0.016 NA 0.040
#&gt; SRR1283386     2  0.4304      0.713 0.000 0.716 0.000 0.016 NA 0.040
#&gt; SRR1283387     2  0.4278      0.714 0.000 0.720 0.000 0.016 NA 0.040
#&gt; SRR1283388     2  0.0146      0.796 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283389     2  0.0146      0.796 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283390     2  0.0146      0.796 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283382     2  0.4083      0.718 0.000 0.748 0.000 0.016 NA 0.040
#&gt; SRR1283383     2  0.4112      0.718 0.000 0.744 0.000 0.016 NA 0.040
#&gt; SRR1283384     2  0.4083      0.718 0.000 0.748 0.000 0.016 NA 0.040
#&gt; SRR1283391     2  0.3868      0.547 0.000 0.508 0.000 0.000 NA 0.000
#&gt; SRR1283392     2  0.3868      0.547 0.000 0.508 0.000 0.000 NA 0.000
#&gt; SRR1283393     2  0.3868      0.547 0.000 0.508 0.000 0.000 NA 0.000
#&gt; SRR1283394     2  0.0146      0.796 0.000 0.996 0.000 0.004 NA 0.000
#&gt; SRR1283395     2  0.0000      0.796 0.000 1.000 0.000 0.000 NA 0.000
#&gt; SRR1283396     2  0.0000      0.796 0.000 1.000 0.000 0.000 NA 0.000
#&gt; SRR1283397     2  0.1007      0.795 0.000 0.956 0.000 0.000 NA 0.000
#&gt; SRR1283398     2  0.0790      0.796 0.000 0.968 0.000 0.000 NA 0.000
#&gt; SRR1283399     2  0.0865      0.796 0.000 0.964 0.000 0.000 NA 0.000
#&gt; SRR1283400     2  0.3854      0.565 0.000 0.536 0.000 0.000 NA 0.000
#&gt; SRR1283401     2  0.3862      0.557 0.000 0.524 0.000 0.000 NA 0.000
#&gt; SRR1283402     2  0.3854      0.562 0.000 0.536 0.000 0.000 NA 0.000
#&gt; SRR1283403     4  0.2854      1.000 0.000 0.000 0.208 0.792 NA 0.000
#&gt; SRR1283404     4  0.2854      1.000 0.000 0.000 0.208 0.792 NA 0.000
#&gt; SRR1283405     4  0.2854      1.000 0.000 0.000 0.208 0.792 NA 0.000
#&gt; SRR1283406     1  0.6378      0.465 0.488 0.000 0.000 0.172 NA 0.040
#&gt; SRR1283407     1  0.6422      0.449 0.476 0.000 0.000 0.176 NA 0.040
#&gt; SRR1283408     1  0.6367      0.470 0.492 0.000 0.000 0.172 NA 0.040
#&gt; SRR1283409     1  0.4462      0.733 0.756 0.000 0.000 0.088 NA 0.036
#&gt; SRR1283410     1  0.4462      0.733 0.756 0.000 0.000 0.088 NA 0.036
#&gt; SRR1283411     1  0.4502      0.731 0.752 0.000 0.000 0.088 NA 0.036
#&gt; SRR1283412     1  0.0260      0.836 0.992 0.000 0.000 0.000 NA 0.000
#&gt; SRR1283413     1  0.0260      0.836 0.992 0.000 0.000 0.000 NA 0.000
#&gt; SRR1283414     1  0.0146      0.837 0.996 0.000 0.000 0.000 NA 0.000
#&gt; SRR1283415     6  0.1958      0.997 0.100 0.000 0.000 0.000 NA 0.896
#&gt; SRR1283416     6  0.1958      0.997 0.100 0.000 0.000 0.000 NA 0.896
#&gt; SRR1283417     6  0.1958      0.997 0.100 0.000 0.000 0.000 NA 0.896
#&gt; SRR1283418     1  0.0935      0.839 0.964 0.000 0.000 0.000 NA 0.032
#&gt; SRR1283419     1  0.0858      0.839 0.968 0.000 0.000 0.000 NA 0.028
#&gt; SRR1283420     1  0.1010      0.839 0.960 0.000 0.000 0.000 NA 0.036
#&gt; SRR1283421     1  0.1007      0.838 0.956 0.000 0.000 0.000 NA 0.044
#&gt; SRR1283422     1  0.1007      0.838 0.956 0.000 0.000 0.000 NA 0.044
#&gt; SRR1283423     1  0.1075      0.836 0.952 0.000 0.000 0.000 NA 0.048
#&gt; SRR1283424     1  0.1267      0.831 0.940 0.000 0.000 0.000 NA 0.060
#&gt; SRR1283425     1  0.1327      0.829 0.936 0.000 0.000 0.000 NA 0.064
#&gt; SRR1283426     1  0.1327      0.829 0.936 0.000 0.000 0.000 NA 0.064
#&gt; SRR1283427     6  0.1814      0.997 0.100 0.000 0.000 0.000 NA 0.900
#&gt; SRR1283428     6  0.1814      0.997 0.100 0.000 0.000 0.000 NA 0.900
#&gt; SRR1283429     6  0.1814      0.997 0.100 0.000 0.000 0.000 NA 0.900
#&gt; SRR1283430     2  0.0000      0.796 0.000 1.000 0.000 0.000 NA 0.000
#&gt; SRR1283431     2  0.0000      0.796 0.000 1.000 0.000 0.000 NA 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.997       0.998         0.5097 0.491   0.491
#> 3 3 1.000           0.950       0.972         0.1444 0.891   0.781
#> 4 4 1.000           1.000       1.000         0.0494 0.993   0.983
#> 5 5 1.000           0.992       0.996         0.1300 0.922   0.798
#> 6 6 0.901           0.948       0.927         0.0826 0.926   0.761
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 5
```

There is also optional best $k$ = 2 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     2  0.0376      0.993 0.004 0.996
#&gt; SRR1283380     2  0.2603      0.956 0.044 0.956
#&gt; SRR1283381     2  0.2603      0.956 0.044 0.956
#&gt; SRR1283385     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283386     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283387     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283388     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283389     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283390     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283382     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283383     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283384     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283391     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283392     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283393     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283394     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283395     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283396     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283397     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283398     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283399     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283400     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283401     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283402     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283403     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283404     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283405     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283406     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283407     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283408     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283409     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283410     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283411     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283412     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283413     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283414     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283415     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283416     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283417     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283418     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283419     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283420     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283421     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283422     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283423     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283424     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283425     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283426     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283427     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283428     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283429     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283430     2  0.0000      0.996 0.000 1.000
#&gt; SRR1283431     2  0.0000      0.996 0.000 1.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1283379     3   0.631      0.690 0.488  0 0.512
#&gt; SRR1283380     3   0.631      0.690 0.488  0 0.512
#&gt; SRR1283381     3   0.631      0.690 0.488  0 0.512
#&gt; SRR1283385     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283386     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283387     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283403     3   0.000      0.428 0.000  0 1.000
#&gt; SRR1283404     3   0.000      0.428 0.000  0 1.000
#&gt; SRR1283405     3   0.000      0.428 0.000  0 1.000
#&gt; SRR1283406     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283407     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283408     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283409     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283410     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283411     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283412     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283413     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283414     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283415     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283416     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283417     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283418     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283419     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283420     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283421     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283422     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283423     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283424     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283425     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283426     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283427     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283428     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283429     1   0.631      1.000 0.512  0 0.488
#&gt; SRR1283430     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000  1 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283385     2  0.0162      0.997 0.000 0.996  0  0 0.004
#&gt; SRR1283386     2  0.0162      0.997 0.000 0.996  0  0 0.004
#&gt; SRR1283387     2  0.0162      0.997 0.000 0.996  0  0 0.004
#&gt; SRR1283388     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283389     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283390     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283382     2  0.0162      0.997 0.000 0.996  0  0 0.004
#&gt; SRR1283383     2  0.0162      0.997 0.000 0.996  0  0 0.004
#&gt; SRR1283384     2  0.0162      0.997 0.000 0.996  0  0 0.004
#&gt; SRR1283391     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283392     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283393     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283394     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283395     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283396     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283397     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283398     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283399     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283400     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283401     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283402     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283406     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283407     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283408     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283409     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283410     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283411     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283412     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283413     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283414     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283415     5  0.0162      1.000 0.004 0.000  0  0 0.996
#&gt; SRR1283416     5  0.0162      1.000 0.004 0.000  0  0 0.996
#&gt; SRR1283417     5  0.0162      1.000 0.004 0.000  0  0 0.996
#&gt; SRR1283418     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283419     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283420     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283421     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283422     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283423     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283424     1  0.0000      0.989 1.000 0.000  0  0 0.000
#&gt; SRR1283425     1  0.1544      0.926 0.932 0.000  0  0 0.068
#&gt; SRR1283426     1  0.2127      0.881 0.892 0.000  0  0 0.108
#&gt; SRR1283427     5  0.0162      1.000 0.004 0.000  0  0 0.996
#&gt; SRR1283428     5  0.0162      1.000 0.004 0.000  0  0 0.996
#&gt; SRR1283429     5  0.0162      1.000 0.004 0.000  0  0 0.996
#&gt; SRR1283430     2  0.0000      0.999 0.000 1.000  0  0 0.000
#&gt; SRR1283431     2  0.0000      0.999 0.000 1.000  0  0 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR1283379     3   0.377      1.000 0.000 0.000 0.592  0 0.408 0.000
#&gt; SRR1283380     3   0.377      1.000 0.000 0.000 0.592  0 0.408 0.000
#&gt; SRR1283381     3   0.377      1.000 0.000 0.000 0.592  0 0.408 0.000
#&gt; SRR1283385     5   0.377      1.000 0.000 0.408 0.000  0 0.592 0.000
#&gt; SRR1283386     5   0.377      1.000 0.000 0.408 0.000  0 0.592 0.000
#&gt; SRR1283387     5   0.377      1.000 0.000 0.408 0.000  0 0.592 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283382     5   0.377      1.000 0.000 0.408 0.000  0 0.592 0.000
#&gt; SRR1283383     5   0.377      1.000 0.000 0.408 0.000  0 0.592 0.000
#&gt; SRR1283384     5   0.377      1.000 0.000 0.408 0.000  0 0.592 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283406     1   0.377      0.546 0.592 0.000 0.408  0 0.000 0.000
#&gt; SRR1283407     1   0.377      0.546 0.592 0.000 0.408  0 0.000 0.000
#&gt; SRR1283408     1   0.377      0.546 0.592 0.000 0.408  0 0.000 0.000
#&gt; SRR1283409     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283410     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283411     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283412     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283413     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283414     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283415     6   0.000      1.000 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1283416     6   0.000      1.000 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1283417     6   0.000      1.000 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1283418     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283419     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283420     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283421     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283422     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283423     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283424     1   0.000      0.918 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR1283425     1   0.139      0.867 0.932 0.000 0.000  0 0.000 0.068
#&gt; SRR1283426     1   0.196      0.824 0.888 0.000 0.000  0 0.000 0.112
#&gt; SRR1283427     6   0.000      1.000 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1283428     6   0.000      1.000 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1283429     6   0.000      1.000 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR1283430     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000 1.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 0.923           0.841       0.904         0.0791 0.945   0.860
#> 5 5 0.773           0.810       0.810         0.1133 0.868   0.618
#> 6 6 0.791           0.877       0.863         0.0315 0.901   0.641
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.4898      0.836 0.000 0.000 0.584 0.416
#&gt; SRR1283380     3  0.4898      0.836 0.000 0.000 0.584 0.416
#&gt; SRR1283381     3  0.4898      0.836 0.000 0.000 0.584 0.416
#&gt; SRR1283385     2  0.2921      0.694 0.000 0.860 0.000 0.140
#&gt; SRR1283386     2  0.2704      0.725 0.000 0.876 0.000 0.124
#&gt; SRR1283387     2  0.2814      0.709 0.000 0.868 0.000 0.132
#&gt; SRR1283388     2  0.0592      0.832 0.000 0.984 0.000 0.016
#&gt; SRR1283389     2  0.0592      0.832 0.000 0.984 0.000 0.016
#&gt; SRR1283390     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283382     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283383     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283384     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283391     4  0.4972      0.980 0.000 0.456 0.000 0.544
#&gt; SRR1283392     4  0.4972      0.980 0.000 0.456 0.000 0.544
#&gt; SRR1283393     4  0.4972      0.980 0.000 0.456 0.000 0.544
#&gt; SRR1283394     2  0.1022      0.826 0.000 0.968 0.000 0.032
#&gt; SRR1283395     2  0.2081      0.784 0.000 0.916 0.000 0.084
#&gt; SRR1283396     2  0.1716      0.801 0.000 0.936 0.000 0.064
#&gt; SRR1283397     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283398     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283399     2  0.0188      0.832 0.000 0.996 0.000 0.004
#&gt; SRR1283400     2  0.4992     -0.854 0.000 0.524 0.000 0.476
#&gt; SRR1283401     2  0.4977     -0.832 0.000 0.540 0.000 0.460
#&gt; SRR1283402     4  0.4996      0.938 0.000 0.484 0.000 0.516
#&gt; SRR1283403     3  0.0000      0.836 0.000 0.000 1.000 0.000
#&gt; SRR1283404     3  0.0000      0.836 0.000 0.000 1.000 0.000
#&gt; SRR1283405     3  0.0000      0.836 0.000 0.000 1.000 0.000
#&gt; SRR1283406     1  0.1022      0.979 0.968 0.000 0.000 0.032
#&gt; SRR1283407     1  0.1022      0.979 0.968 0.000 0.000 0.032
#&gt; SRR1283408     1  0.1022      0.979 0.968 0.000 0.000 0.032
#&gt; SRR1283409     1  0.0592      0.986 0.984 0.000 0.000 0.016
#&gt; SRR1283410     1  0.0000      0.989 1.000 0.000 0.000 0.000
#&gt; SRR1283411     1  0.0592      0.986 0.984 0.000 0.000 0.016
#&gt; SRR1283412     1  0.1022      0.979 0.968 0.000 0.000 0.032
#&gt; SRR1283413     1  0.1022      0.979 0.968 0.000 0.000 0.032
#&gt; SRR1283414     1  0.1022      0.979 0.968 0.000 0.000 0.032
#&gt; SRR1283415     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283416     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283417     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283418     1  0.0000      0.989 1.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0592      0.986 0.984 0.000 0.000 0.016
#&gt; SRR1283420     1  0.0000      0.989 1.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.989 1.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.989 1.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.989 1.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283425     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283426     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283427     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283428     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283429     1  0.0188      0.989 0.996 0.000 0.000 0.004
#&gt; SRR1283430     2  0.1118      0.824 0.000 0.964 0.000 0.036
#&gt; SRR1283431     2  0.1022      0.826 0.000 0.968 0.000 0.032
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1283379     3  0.5922      0.793 0.108 0.000 0.504 0.000 0.388
#&gt; SRR1283380     3  0.5922      0.793 0.108 0.000 0.504 0.000 0.388
#&gt; SRR1283381     3  0.5922      0.793 0.108 0.000 0.504 0.000 0.388
#&gt; SRR1283385     2  0.0404      0.976 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1283386     2  0.0566      0.974 0.004 0.984 0.000 0.000 0.012
#&gt; SRR1283387     2  0.0566      0.974 0.004 0.984 0.000 0.000 0.012
#&gt; SRR1283388     2  0.0404      0.979 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1283389     2  0.0162      0.980 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283390     2  0.0404      0.980 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1283382     2  0.0404      0.976 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1283383     2  0.0404      0.976 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1283384     2  0.0404      0.976 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1283391     5  0.4182      0.982 0.000 0.400 0.000 0.000 0.600
#&gt; SRR1283392     5  0.4182      0.982 0.000 0.400 0.000 0.000 0.600
#&gt; SRR1283393     5  0.4182      0.982 0.000 0.400 0.000 0.000 0.600
#&gt; SRR1283394     2  0.0510      0.976 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1283395     2  0.0290      0.978 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1283396     2  0.0290      0.979 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1283397     2  0.0880      0.965 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1283398     2  0.0880      0.965 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1283399     2  0.0880      0.965 0.000 0.968 0.000 0.000 0.032
#&gt; SRR1283400     5  0.4171      0.968 0.000 0.396 0.000 0.000 0.604
#&gt; SRR1283401     5  0.4227      0.944 0.000 0.420 0.000 0.000 0.580
#&gt; SRR1283402     5  0.4171      0.980 0.000 0.396 0.000 0.000 0.604
#&gt; SRR1283403     3  0.0000      0.793 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283404     3  0.0000      0.793 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283405     3  0.0000      0.793 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283406     4  0.0290      0.725 0.008 0.000 0.000 0.992 0.000
#&gt; SRR1283407     4  0.0404      0.728 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1283408     4  0.0404      0.728 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1283409     4  0.1965      0.710 0.096 0.000 0.000 0.904 0.000
#&gt; SRR1283410     4  0.3999      0.118 0.344 0.000 0.000 0.656 0.000
#&gt; SRR1283411     4  0.1792      0.716 0.084 0.000 0.000 0.916 0.000
#&gt; SRR1283412     4  0.2852      0.663 0.172 0.000 0.000 0.828 0.000
#&gt; SRR1283413     4  0.2852      0.663 0.172 0.000 0.000 0.828 0.000
#&gt; SRR1283414     4  0.2852      0.663 0.172 0.000 0.000 0.828 0.000
#&gt; SRR1283415     1  0.3003      0.784 0.812 0.000 0.000 0.188 0.000
#&gt; SRR1283416     1  0.2690      0.750 0.844 0.000 0.000 0.156 0.000
#&gt; SRR1283417     1  0.2690      0.750 0.844 0.000 0.000 0.156 0.000
#&gt; SRR1283418     1  0.4273      0.614 0.552 0.000 0.000 0.448 0.000
#&gt; SRR1283419     4  0.4304     -0.450 0.484 0.000 0.000 0.516 0.000
#&gt; SRR1283420     1  0.4249      0.648 0.568 0.000 0.000 0.432 0.000
#&gt; SRR1283421     1  0.4201      0.703 0.592 0.000 0.000 0.408 0.000
#&gt; SRR1283422     1  0.4201      0.703 0.592 0.000 0.000 0.408 0.000
#&gt; SRR1283423     1  0.4138      0.731 0.616 0.000 0.000 0.384 0.000
#&gt; SRR1283424     1  0.3752      0.803 0.708 0.000 0.000 0.292 0.000
#&gt; SRR1283425     1  0.3837      0.798 0.692 0.000 0.000 0.308 0.000
#&gt; SRR1283426     1  0.3796      0.802 0.700 0.000 0.000 0.300 0.000
#&gt; SRR1283427     1  0.3177      0.798 0.792 0.000 0.000 0.208 0.000
#&gt; SRR1283428     1  0.3143      0.797 0.796 0.000 0.000 0.204 0.000
#&gt; SRR1283429     1  0.3143      0.797 0.796 0.000 0.000 0.204 0.000
#&gt; SRR1283430     2  0.0162      0.979 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283431     2  0.0290      0.979 0.000 0.992 0.000 0.000 0.008
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5    p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283385     2  0.0790      0.951 0.000 0.968  0  0 0.032 0.000
#&gt; SRR1283386     2  0.0937      0.948 0.000 0.960  0  0 0.040 0.000
#&gt; SRR1283387     2  0.0790      0.950 0.000 0.968  0  0 0.032 0.000
#&gt; SRR1283388     2  0.0790      0.951 0.000 0.968  0  0 0.032 0.000
#&gt; SRR1283389     2  0.0363      0.954 0.000 0.988  0  0 0.012 0.000
#&gt; SRR1283390     2  0.0260      0.953 0.000 0.992  0  0 0.008 0.000
#&gt; SRR1283382     2  0.1007      0.928 0.000 0.956  0  0 0.044 0.000
#&gt; SRR1283383     2  0.1007      0.928 0.000 0.956  0  0 0.044 0.000
#&gt; SRR1283384     2  0.1007      0.928 0.000 0.956  0  0 0.044 0.000
#&gt; SRR1283391     5  0.2969      0.896 0.000 0.224  0  0 0.776 0.000
#&gt; SRR1283392     5  0.3050      0.903 0.000 0.236  0  0 0.764 0.000
#&gt; SRR1283393     5  0.2969      0.896 0.000 0.224  0  0 0.776 0.000
#&gt; SRR1283394     2  0.1501      0.920 0.000 0.924  0  0 0.076 0.000
#&gt; SRR1283395     2  0.0458      0.953 0.000 0.984  0  0 0.016 0.000
#&gt; SRR1283396     2  0.0146      0.953 0.000 0.996  0  0 0.004 0.000
#&gt; SRR1283397     2  0.1444      0.912 0.000 0.928  0  0 0.072 0.000
#&gt; SRR1283398     2  0.1387      0.916 0.000 0.932  0  0 0.068 0.000
#&gt; SRR1283399     2  0.1387      0.916 0.000 0.932  0  0 0.068 0.000
#&gt; SRR1283400     5  0.3547      0.875 0.000 0.332  0  0 0.668 0.000
#&gt; SRR1283401     5  0.3789      0.745 0.000 0.416  0  0 0.584 0.000
#&gt; SRR1283402     5  0.3330      0.901 0.000 0.284  0  0 0.716 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283406     1  0.0405      0.701 0.988 0.000  0  0 0.004 0.008
#&gt; SRR1283407     1  0.0508      0.703 0.984 0.000  0  0 0.004 0.012
#&gt; SRR1283408     1  0.0508      0.703 0.984 0.000  0  0 0.004 0.012
#&gt; SRR1283409     1  0.2294      0.680 0.892 0.000  0  0 0.072 0.036
#&gt; SRR1283410     1  0.2294      0.680 0.892 0.000  0  0 0.072 0.036
#&gt; SRR1283411     1  0.2221      0.678 0.896 0.000  0  0 0.072 0.032
#&gt; SRR1283412     1  0.4301      0.774 0.696 0.000  0  0 0.064 0.240
#&gt; SRR1283413     1  0.4301      0.774 0.696 0.000  0  0 0.064 0.240
#&gt; SRR1283414     1  0.4301      0.774 0.696 0.000  0  0 0.064 0.240
#&gt; SRR1283415     6  0.1075      0.992 0.048 0.000  0  0 0.000 0.952
#&gt; SRR1283416     6  0.1075      0.992 0.048 0.000  0  0 0.000 0.952
#&gt; SRR1283417     6  0.1075      0.992 0.048 0.000  0  0 0.000 0.952
#&gt; SRR1283418     1  0.3371      0.787 0.708 0.000  0  0 0.000 0.292
#&gt; SRR1283419     1  0.3371      0.787 0.708 0.000  0  0 0.000 0.292
#&gt; SRR1283420     1  0.3371      0.787 0.708 0.000  0  0 0.000 0.292
#&gt; SRR1283421     1  0.3409      0.784 0.700 0.000  0  0 0.000 0.300
#&gt; SRR1283422     1  0.3428      0.782 0.696 0.000  0  0 0.000 0.304
#&gt; SRR1283423     1  0.3619      0.771 0.680 0.000  0  0 0.004 0.316
#&gt; SRR1283424     1  0.3795      0.727 0.632 0.000  0  0 0.004 0.364
#&gt; SRR1283425     1  0.3819      0.720 0.624 0.000  0  0 0.004 0.372
#&gt; SRR1283426     1  0.3830      0.715 0.620 0.000  0  0 0.004 0.376
#&gt; SRR1283427     6  0.1204      0.992 0.056 0.000  0  0 0.000 0.944
#&gt; SRR1283428     6  0.1204      0.992 0.056 0.000  0  0 0.000 0.944
#&gt; SRR1283429     6  0.1204      0.992 0.056 0.000  0  0 0.000 0.944
#&gt; SRR1283430     2  0.0363      0.954 0.000 0.988  0  0 0.012 0.000
#&gt; SRR1283431     2  0.0790      0.950 0.000 0.968  0  0 0.032 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.972       0.987         0.5080 0.491   0.491
#> 3 3 1.000           1.000       1.000         0.1921 0.891   0.781
#> 4 4 1.000           0.996       0.996         0.0129 0.993   0.983
#> 5 5 0.951           0.936       0.950         0.0716 0.954   0.882
#> 6 6 0.843           0.873       0.903         0.0740 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     2   0.697      0.780 0.188 0.812
#&gt; SRR1283380     2   0.821      0.682 0.256 0.744
#&gt; SRR1283381     2   0.795      0.708 0.240 0.760
#&gt; SRR1283385     2   0.000      0.972 0.000 1.000
#&gt; SRR1283386     2   0.000      0.972 0.000 1.000
#&gt; SRR1283387     2   0.000      0.972 0.000 1.000
#&gt; SRR1283388     2   0.000      0.972 0.000 1.000
#&gt; SRR1283389     2   0.000      0.972 0.000 1.000
#&gt; SRR1283390     2   0.000      0.972 0.000 1.000
#&gt; SRR1283382     2   0.000      0.972 0.000 1.000
#&gt; SRR1283383     2   0.000      0.972 0.000 1.000
#&gt; SRR1283384     2   0.000      0.972 0.000 1.000
#&gt; SRR1283391     2   0.000      0.972 0.000 1.000
#&gt; SRR1283392     2   0.000      0.972 0.000 1.000
#&gt; SRR1283393     2   0.000      0.972 0.000 1.000
#&gt; SRR1283394     2   0.000      0.972 0.000 1.000
#&gt; SRR1283395     2   0.000      0.972 0.000 1.000
#&gt; SRR1283396     2   0.000      0.972 0.000 1.000
#&gt; SRR1283397     2   0.000      0.972 0.000 1.000
#&gt; SRR1283398     2   0.000      0.972 0.000 1.000
#&gt; SRR1283399     2   0.000      0.972 0.000 1.000
#&gt; SRR1283400     2   0.000      0.972 0.000 1.000
#&gt; SRR1283401     2   0.000      0.972 0.000 1.000
#&gt; SRR1283402     2   0.000      0.972 0.000 1.000
#&gt; SRR1283403     1   0.000      1.000 1.000 0.000
#&gt; SRR1283404     1   0.000      1.000 1.000 0.000
#&gt; SRR1283405     1   0.000      1.000 1.000 0.000
#&gt; SRR1283406     1   0.000      1.000 1.000 0.000
#&gt; SRR1283407     1   0.000      1.000 1.000 0.000
#&gt; SRR1283408     1   0.000      1.000 1.000 0.000
#&gt; SRR1283409     1   0.000      1.000 1.000 0.000
#&gt; SRR1283410     1   0.000      1.000 1.000 0.000
#&gt; SRR1283411     1   0.000      1.000 1.000 0.000
#&gt; SRR1283412     1   0.000      1.000 1.000 0.000
#&gt; SRR1283413     1   0.000      1.000 1.000 0.000
#&gt; SRR1283414     1   0.000      1.000 1.000 0.000
#&gt; SRR1283415     1   0.000      1.000 1.000 0.000
#&gt; SRR1283416     1   0.000      1.000 1.000 0.000
#&gt; SRR1283417     1   0.000      1.000 1.000 0.000
#&gt; SRR1283418     1   0.000      1.000 1.000 0.000
#&gt; SRR1283419     1   0.000      1.000 1.000 0.000
#&gt; SRR1283420     1   0.000      1.000 1.000 0.000
#&gt; SRR1283421     1   0.000      1.000 1.000 0.000
#&gt; SRR1283422     1   0.000      1.000 1.000 0.000
#&gt; SRR1283423     1   0.000      1.000 1.000 0.000
#&gt; SRR1283424     1   0.000      1.000 1.000 0.000
#&gt; SRR1283425     1   0.000      1.000 1.000 0.000
#&gt; SRR1283426     1   0.000      1.000 1.000 0.000
#&gt; SRR1283427     1   0.000      1.000 1.000 0.000
#&gt; SRR1283428     1   0.000      1.000 1.000 0.000
#&gt; SRR1283429     1   0.000      1.000 1.000 0.000
#&gt; SRR1283430     2   0.000      0.972 0.000 1.000
#&gt; SRR1283431     2   0.000      0.972 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.0921      1.000 0.000 0.000 0.972 0.028
#&gt; SRR1283380     3  0.0921      1.000 0.000 0.000 0.972 0.028
#&gt; SRR1283381     3  0.0921      1.000 0.000 0.000 0.972 0.028
#&gt; SRR1283385     2  0.0336      0.995 0.000 0.992 0.008 0.000
#&gt; SRR1283386     2  0.0336      0.995 0.000 0.992 0.008 0.000
#&gt; SRR1283387     2  0.0336      0.995 0.000 0.992 0.008 0.000
#&gt; SRR1283388     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283389     2  0.0188      0.997 0.000 0.996 0.004 0.000
#&gt; SRR1283390     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283382     2  0.0336      0.995 0.000 0.992 0.008 0.000
#&gt; SRR1283383     2  0.0336      0.995 0.000 0.992 0.008 0.000
#&gt; SRR1283384     2  0.0336      0.995 0.000 0.992 0.008 0.000
#&gt; SRR1283391     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283392     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283393     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283394     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283395     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283396     2  0.0188      0.997 0.000 0.996 0.004 0.000
#&gt; SRR1283397     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283398     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283399     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283400     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1283406     1  0.0188      0.995 0.996 0.000 0.000 0.004
#&gt; SRR1283407     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283408     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283409     1  0.0707      0.983 0.980 0.000 0.000 0.020
#&gt; SRR1283410     1  0.0592      0.987 0.984 0.000 0.000 0.016
#&gt; SRR1283411     1  0.0592      0.987 0.984 0.000 0.000 0.016
#&gt; SRR1283412     1  0.0188      0.995 0.996 0.000 0.000 0.004
#&gt; SRR1283413     1  0.0188      0.995 0.996 0.000 0.000 0.004
#&gt; SRR1283414     1  0.0188      0.995 0.996 0.000 0.000 0.004
#&gt; SRR1283415     1  0.0188      0.995 0.996 0.000 0.004 0.000
#&gt; SRR1283416     1  0.0188      0.995 0.996 0.000 0.004 0.000
#&gt; SRR1283417     1  0.0188      0.995 0.996 0.000 0.004 0.000
#&gt; SRR1283418     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283427     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283428     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283429     1  0.0000      0.997 1.000 0.000 0.000 0.000
#&gt; SRR1283430     2  0.0188      0.997 0.000 0.996 0.004 0.000
#&gt; SRR1283431     2  0.0188      0.997 0.000 0.996 0.004 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1283385     2  0.1732      0.948 0.000 0.920  0  0 0.080
#&gt; SRR1283386     2  0.1732      0.948 0.000 0.920  0  0 0.080
#&gt; SRR1283387     2  0.1732      0.948 0.000 0.920  0  0 0.080
#&gt; SRR1283388     2  0.0290      0.970 0.000 0.992  0  0 0.008
#&gt; SRR1283389     2  0.0404      0.970 0.000 0.988  0  0 0.012
#&gt; SRR1283390     2  0.0290      0.970 0.000 0.992  0  0 0.008
#&gt; SRR1283382     2  0.1732      0.948 0.000 0.920  0  0 0.080
#&gt; SRR1283383     2  0.1732      0.948 0.000 0.920  0  0 0.080
#&gt; SRR1283384     2  0.1732      0.948 0.000 0.920  0  0 0.080
#&gt; SRR1283391     2  0.0880      0.967 0.000 0.968  0  0 0.032
#&gt; SRR1283392     2  0.0880      0.967 0.000 0.968  0  0 0.032
#&gt; SRR1283393     2  0.0880      0.967 0.000 0.968  0  0 0.032
#&gt; SRR1283394     2  0.0404      0.970 0.000 0.988  0  0 0.012
#&gt; SRR1283395     2  0.0404      0.971 0.000 0.988  0  0 0.012
#&gt; SRR1283396     2  0.0794      0.969 0.000 0.972  0  0 0.028
#&gt; SRR1283397     2  0.0290      0.970 0.000 0.992  0  0 0.008
#&gt; SRR1283398     2  0.0162      0.971 0.000 0.996  0  0 0.004
#&gt; SRR1283399     2  0.0162      0.971 0.000 0.996  0  0 0.004
#&gt; SRR1283400     2  0.0510      0.968 0.000 0.984  0  0 0.016
#&gt; SRR1283401     2  0.0609      0.969 0.000 0.980  0  0 0.020
#&gt; SRR1283402     2  0.0609      0.968 0.000 0.980  0  0 0.020
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1283406     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283407     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283408     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283409     1  0.0404      0.929 0.988 0.000  0  0 0.012
#&gt; SRR1283410     1  0.0290      0.933 0.992 0.000  0  0 0.008
#&gt; SRR1283411     1  0.0404      0.929 0.988 0.000  0  0 0.012
#&gt; SRR1283412     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283413     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283414     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283415     5  0.4161      0.926 0.392 0.000  0  0 0.608
#&gt; SRR1283416     5  0.4030      0.963 0.352 0.000  0  0 0.648
#&gt; SRR1283417     5  0.4030      0.963 0.352 0.000  0  0 0.648
#&gt; SRR1283418     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283419     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283420     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283421     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283422     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283423     1  0.0000      0.939 1.000 0.000  0  0 0.000
#&gt; SRR1283424     1  0.0880      0.912 0.968 0.000  0  0 0.032
#&gt; SRR1283425     1  0.0880      0.912 0.968 0.000  0  0 0.032
#&gt; SRR1283426     1  0.0880      0.912 0.968 0.000  0  0 0.032
#&gt; SRR1283427     1  0.3143      0.595 0.796 0.000  0  0 0.204
#&gt; SRR1283428     1  0.3143      0.595 0.796 0.000  0  0 0.204
#&gt; SRR1283429     1  0.3143      0.595 0.796 0.000  0  0 0.204
#&gt; SRR1283430     2  0.0963      0.966 0.000 0.964  0  0 0.036
#&gt; SRR1283431     2  0.0794      0.969 0.000 0.972  0  0 0.028
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1283379     3  0.0146      1.000 0.000 0.000 0.996 0.004 NA 0.000
#&gt; SRR1283380     3  0.0146      1.000 0.000 0.000 0.996 0.004 NA 0.000
#&gt; SRR1283381     3  0.0146      1.000 0.000 0.000 0.996 0.004 NA 0.000
#&gt; SRR1283385     2  0.0146      0.739 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283386     2  0.0146      0.739 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283387     2  0.0146      0.739 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283388     2  0.3592      0.855 0.000 0.656 0.000 0.000 NA 0.000
#&gt; SRR1283389     2  0.3578      0.855 0.000 0.660 0.000 0.000 NA 0.000
#&gt; SRR1283390     2  0.3634      0.854 0.000 0.644 0.000 0.000 NA 0.000
#&gt; SRR1283382     2  0.0146      0.739 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283383     2  0.0146      0.739 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283384     2  0.0000      0.741 0.000 1.000 0.000 0.000 NA 0.000
#&gt; SRR1283391     2  0.3565      0.820 0.000 0.692 0.000 0.000 NA 0.004
#&gt; SRR1283392     2  0.3468      0.814 0.000 0.712 0.000 0.000 NA 0.004
#&gt; SRR1283393     2  0.3565      0.820 0.000 0.692 0.000 0.000 NA 0.004
#&gt; SRR1283394     2  0.3592      0.855 0.000 0.656 0.000 0.000 NA 0.000
#&gt; SRR1283395     2  0.3515      0.855 0.000 0.676 0.000 0.000 NA 0.000
#&gt; SRR1283396     2  0.3446      0.852 0.000 0.692 0.000 0.000 NA 0.000
#&gt; SRR1283397     2  0.3841      0.849 0.000 0.616 0.000 0.000 NA 0.004
#&gt; SRR1283398     2  0.3634      0.855 0.000 0.644 0.000 0.000 NA 0.000
#&gt; SRR1283399     2  0.3695      0.851 0.000 0.624 0.000 0.000 NA 0.000
#&gt; SRR1283400     2  0.3915      0.838 0.000 0.584 0.000 0.000 NA 0.004
#&gt; SRR1283401     2  0.3872      0.840 0.000 0.604 0.000 0.000 NA 0.004
#&gt; SRR1283402     2  0.3907      0.840 0.000 0.588 0.000 0.000 NA 0.004
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA 0.000
#&gt; SRR1283406     1  0.0858      0.923 0.968 0.000 0.000 0.000 NA 0.004
#&gt; SRR1283407     1  0.0858      0.923 0.968 0.000 0.000 0.000 NA 0.004
#&gt; SRR1283408     1  0.0972      0.924 0.964 0.000 0.000 0.000 NA 0.008
#&gt; SRR1283409     1  0.1074      0.921 0.960 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283410     1  0.0891      0.924 0.968 0.000 0.000 0.000 NA 0.008
#&gt; SRR1283411     1  0.1074      0.921 0.960 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283412     1  0.0508      0.928 0.984 0.000 0.000 0.000 NA 0.004
#&gt; SRR1283413     1  0.0405      0.929 0.988 0.000 0.000 0.000 NA 0.004
#&gt; SRR1283414     1  0.0508      0.930 0.984 0.000 0.000 0.000 NA 0.004
#&gt; SRR1283415     6  0.1588      0.984 0.072 0.000 0.000 0.000 NA 0.924
#&gt; SRR1283416     6  0.1327      0.987 0.064 0.000 0.000 0.000 NA 0.936
#&gt; SRR1283417     6  0.1531      0.989 0.068 0.000 0.000 0.000 NA 0.928
#&gt; SRR1283418     1  0.0820      0.929 0.972 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283419     1  0.0603      0.929 0.980 0.000 0.000 0.000 NA 0.004
#&gt; SRR1283420     1  0.0993      0.928 0.964 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283421     1  0.0725      0.929 0.976 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283422     1  0.0520      0.929 0.984 0.000 0.000 0.000 NA 0.008
#&gt; SRR1283423     1  0.0725      0.929 0.976 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283424     1  0.1082      0.920 0.956 0.000 0.000 0.000 NA 0.040
#&gt; SRR1283425     1  0.0937      0.920 0.960 0.000 0.000 0.000 NA 0.040
#&gt; SRR1283426     1  0.0865      0.922 0.964 0.000 0.000 0.000 NA 0.036
#&gt; SRR1283427     1  0.3528      0.610 0.700 0.000 0.000 0.000 NA 0.296
#&gt; SRR1283428     1  0.3508      0.615 0.704 0.000 0.000 0.000 NA 0.292
#&gt; SRR1283429     1  0.3468      0.629 0.712 0.000 0.000 0.000 NA 0.284
#&gt; SRR1283430     2  0.3288      0.845 0.000 0.724 0.000 0.000 NA 0.000
#&gt; SRR1283431     2  0.3531      0.855 0.000 0.672 0.000 0.000 NA 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2054 0.795   0.795
#> 3 3 1.000           1.000       1.000         1.9479 0.599   0.496
#> 4 4 1.000           1.000       1.000         0.0108 0.993   0.983
#> 5 5 1.000           0.975       0.986         0.0864 0.954   0.882
#> 6 6 0.934           0.940       0.958         0.0610 0.961   0.886
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 5
```

There is also optional best $k$ = 2 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     2       0          1  0  1
#&gt; SRR1283407     2       0          1  0  1
#&gt; SRR1283408     2       0          1  0  1
#&gt; SRR1283409     2       0          1  0  1
#&gt; SRR1283410     2       0          1  0  1
#&gt; SRR1283411     2       0          1  0  1
#&gt; SRR1283412     2       0          1  0  1
#&gt; SRR1283413     2       0          1  0  1
#&gt; SRR1283414     2       0          1  0  1
#&gt; SRR1283415     2       0          1  0  1
#&gt; SRR1283416     2       0          1  0  1
#&gt; SRR1283417     2       0          1  0  1
#&gt; SRR1283418     2       0          1  0  1
#&gt; SRR1283419     2       0          1  0  1
#&gt; SRR1283420     2       0          1  0  1
#&gt; SRR1283421     2       0          1  0  1
#&gt; SRR1283422     2       0          1  0  1
#&gt; SRR1283423     2       0          1  0  1
#&gt; SRR1283424     2       0          1  0  1
#&gt; SRR1283425     2       0          1  0  1
#&gt; SRR1283426     2       0          1  0  1
#&gt; SRR1283427     2       0          1  0  1
#&gt; SRR1283428     2       0          1  0  1
#&gt; SRR1283429     2       0          1  0  1
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3 p4    p5
#&gt; SRR1283379     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1283385     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283386     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283387     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1283406     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283407     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283408     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283409     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283410     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283411     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283412     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283413     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283414     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283415     5   0.000      1.000 0.000  0  0  0 1.000
#&gt; SRR1283416     5   0.000      1.000 0.000  0  0  0 1.000
#&gt; SRR1283417     5   0.000      1.000 0.000  0  0  0 1.000
#&gt; SRR1283418     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283419     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283420     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283421     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283422     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283423     1   0.000      0.963 1.000  0  0  0 0.000
#&gt; SRR1283424     1   0.112      0.940 0.956  0  0  0 0.044
#&gt; SRR1283425     1   0.112      0.940 0.956  0  0  0 0.044
#&gt; SRR1283426     1   0.112      0.940 0.956  0  0  0 0.044
#&gt; SRR1283427     1   0.307      0.797 0.804  0  0  0 0.196
#&gt; SRR1283428     1   0.307      0.797 0.804  0  0  0 0.196
#&gt; SRR1283429     1   0.307      0.797 0.804  0  0  0 0.196
#&gt; SRR1283430     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000  1  0  0 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3 p4    p5    p6
#&gt; SRR1283379     3   0.000      1.000 0.000  0  1  0 0.000 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000  0  1  0 0.000 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000  0  1  0 0.000 0.000
#&gt; SRR1283385     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283386     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283387     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000  0  0  1 0.000 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000  0  0  1 0.000 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000  0  0  1 0.000 0.000
#&gt; SRR1283406     5   0.276      1.000 0.196  0  0  0 0.804 0.000
#&gt; SRR1283407     5   0.276      1.000 0.196  0  0  0 0.804 0.000
#&gt; SRR1283408     5   0.276      1.000 0.196  0  0  0 0.804 0.000
#&gt; SRR1283409     1   0.345      0.641 0.692  0  0  0 0.308 0.000
#&gt; SRR1283410     1   0.345      0.641 0.692  0  0  0 0.308 0.000
#&gt; SRR1283411     1   0.345      0.641 0.692  0  0  0 0.308 0.000
#&gt; SRR1283412     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283413     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283414     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283415     6   0.000      1.000 0.000  0  0  0 0.000 1.000
#&gt; SRR1283416     6   0.000      1.000 0.000  0  0  0 0.000 1.000
#&gt; SRR1283417     6   0.000      1.000 0.000  0  0  0 0.000 1.000
#&gt; SRR1283418     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283419     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283420     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283421     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283422     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283423     1   0.000      0.886 1.000  0  0  0 0.000 0.000
#&gt; SRR1283424     1   0.101      0.871 0.956  0  0  0 0.000 0.044
#&gt; SRR1283425     1   0.101      0.871 0.956  0  0  0 0.000 0.044
#&gt; SRR1283426     1   0.101      0.871 0.956  0  0  0 0.000 0.044
#&gt; SRR1283427     1   0.276      0.775 0.804  0  0  0 0.000 0.196
#&gt; SRR1283428     1   0.276      0.775 0.804  0  0  0 0.000 0.196
#&gt; SRR1283429     1   0.276      0.775 0.804  0  0  0 0.000 0.196
#&gt; SRR1283430     2   0.000      1.000 0.000  1  0  0 0.000 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000  1  0  0 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.495           0.955       0.911         0.4434 0.499   0.499
#> 3 3 0.782           0.946       0.901         0.3401 0.896   0.791
#> 4 4 0.642           0.824       0.832         0.1344 1.000   1.000
#> 5 5 0.738           0.577       0.724         0.0827 0.956   0.890
#> 6 6 0.718           0.680       0.725         0.0585 0.858   0.604
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     1   0.000      0.808 1.000 0.000
#&gt; SRR1283380     1   0.000      0.808 1.000 0.000
#&gt; SRR1283381     1   0.000      0.808 1.000 0.000
#&gt; SRR1283385     2   0.000      1.000 0.000 1.000
#&gt; SRR1283386     2   0.000      1.000 0.000 1.000
#&gt; SRR1283387     2   0.000      1.000 0.000 1.000
#&gt; SRR1283388     2   0.000      1.000 0.000 1.000
#&gt; SRR1283389     2   0.000      1.000 0.000 1.000
#&gt; SRR1283390     2   0.000      1.000 0.000 1.000
#&gt; SRR1283382     2   0.000      1.000 0.000 1.000
#&gt; SRR1283383     2   0.000      1.000 0.000 1.000
#&gt; SRR1283384     2   0.000      1.000 0.000 1.000
#&gt; SRR1283391     2   0.000      1.000 0.000 1.000
#&gt; SRR1283392     2   0.000      1.000 0.000 1.000
#&gt; SRR1283393     2   0.000      1.000 0.000 1.000
#&gt; SRR1283394     2   0.000      1.000 0.000 1.000
#&gt; SRR1283395     2   0.000      1.000 0.000 1.000
#&gt; SRR1283396     2   0.000      1.000 0.000 1.000
#&gt; SRR1283397     2   0.000      1.000 0.000 1.000
#&gt; SRR1283398     2   0.000      1.000 0.000 1.000
#&gt; SRR1283399     2   0.000      1.000 0.000 1.000
#&gt; SRR1283400     2   0.000      1.000 0.000 1.000
#&gt; SRR1283401     2   0.000      1.000 0.000 1.000
#&gt; SRR1283402     2   0.000      1.000 0.000 1.000
#&gt; SRR1283403     1   0.000      0.808 1.000 0.000
#&gt; SRR1283404     1   0.000      0.808 1.000 0.000
#&gt; SRR1283405     1   0.000      0.808 1.000 0.000
#&gt; SRR1283406     1   0.714      0.950 0.804 0.196
#&gt; SRR1283407     1   0.714      0.950 0.804 0.196
#&gt; SRR1283408     1   0.714      0.950 0.804 0.196
#&gt; SRR1283409     1   0.714      0.950 0.804 0.196
#&gt; SRR1283410     1   0.714      0.950 0.804 0.196
#&gt; SRR1283411     1   0.714      0.950 0.804 0.196
#&gt; SRR1283412     1   0.714      0.950 0.804 0.196
#&gt; SRR1283413     1   0.714      0.950 0.804 0.196
#&gt; SRR1283414     1   0.714      0.950 0.804 0.196
#&gt; SRR1283415     1   0.714      0.950 0.804 0.196
#&gt; SRR1283416     1   0.714      0.950 0.804 0.196
#&gt; SRR1283417     1   0.714      0.950 0.804 0.196
#&gt; SRR1283418     1   0.714      0.950 0.804 0.196
#&gt; SRR1283419     1   0.714      0.950 0.804 0.196
#&gt; SRR1283420     1   0.714      0.950 0.804 0.196
#&gt; SRR1283421     1   0.714      0.950 0.804 0.196
#&gt; SRR1283422     1   0.714      0.950 0.804 0.196
#&gt; SRR1283423     1   0.714      0.950 0.804 0.196
#&gt; SRR1283424     1   0.714      0.950 0.804 0.196
#&gt; SRR1283425     1   0.714      0.950 0.804 0.196
#&gt; SRR1283426     1   0.714      0.950 0.804 0.196
#&gt; SRR1283427     1   0.714      0.950 0.804 0.196
#&gt; SRR1283428     1   0.714      0.950 0.804 0.196
#&gt; SRR1283429     1   0.714      0.950 0.804 0.196
#&gt; SRR1283430     2   0.000      1.000 0.000 1.000
#&gt; SRR1283431     2   0.000      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1283379     3   0.642      0.994 0.324 0.016 0.660
#&gt; SRR1283380     3   0.642      0.994 0.324 0.016 0.660
#&gt; SRR1283381     3   0.642      0.994 0.324 0.016 0.660
#&gt; SRR1283385     2   0.392      0.853 0.016 0.872 0.112
#&gt; SRR1283386     2   0.392      0.853 0.016 0.872 0.112
#&gt; SRR1283387     2   0.392      0.853 0.016 0.872 0.112
#&gt; SRR1283388     2   0.191      0.881 0.016 0.956 0.028
#&gt; SRR1283389     2   0.191      0.881 0.016 0.956 0.028
#&gt; SRR1283390     2   0.191      0.881 0.016 0.956 0.028
#&gt; SRR1283382     2   0.588      0.862 0.016 0.728 0.256
#&gt; SRR1283383     2   0.588      0.862 0.016 0.728 0.256
#&gt; SRR1283384     2   0.588      0.862 0.016 0.728 0.256
#&gt; SRR1283391     2   0.512      0.887 0.016 0.796 0.188
#&gt; SRR1283392     2   0.512      0.887 0.016 0.796 0.188
#&gt; SRR1283393     2   0.512      0.887 0.016 0.796 0.188
#&gt; SRR1283394     2   0.227      0.879 0.016 0.944 0.040
#&gt; SRR1283395     2   0.227      0.879 0.016 0.944 0.040
#&gt; SRR1283396     2   0.227      0.879 0.016 0.944 0.040
#&gt; SRR1283397     2   0.506      0.887 0.016 0.800 0.184
#&gt; SRR1283398     2   0.506      0.887 0.016 0.800 0.184
#&gt; SRR1283399     2   0.506      0.887 0.016 0.800 0.184
#&gt; SRR1283400     2   0.512      0.887 0.016 0.796 0.188
#&gt; SRR1283401     2   0.512      0.887 0.016 0.796 0.188
#&gt; SRR1283402     2   0.512      0.887 0.016 0.796 0.188
#&gt; SRR1283403     3   0.573      0.994 0.324 0.000 0.676
#&gt; SRR1283404     3   0.573      0.994 0.324 0.000 0.676
#&gt; SRR1283405     3   0.573      0.994 0.324 0.000 0.676
#&gt; SRR1283406     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283407     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283408     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283409     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283410     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283411     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283412     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283413     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283414     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283415     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283416     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283417     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283418     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283419     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283420     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283421     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283422     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283423     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283424     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283425     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283426     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283427     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283428     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283429     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283430     2   0.191      0.881 0.016 0.956 0.028
#&gt; SRR1283431     2   0.191      0.881 0.016 0.956 0.028
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1283379     3  0.4462      0.977 0.132 0.000 0.804 NA
#&gt; SRR1283380     3  0.4462      0.977 0.132 0.000 0.804 NA
#&gt; SRR1283381     3  0.4462      0.977 0.132 0.000 0.804 NA
#&gt; SRR1283385     2  0.6953      0.690 0.000 0.476 0.112 NA
#&gt; SRR1283386     2  0.6953      0.690 0.000 0.476 0.112 NA
#&gt; SRR1283387     2  0.6953      0.690 0.000 0.476 0.112 NA
#&gt; SRR1283388     2  0.4866      0.751 0.000 0.596 0.000 NA
#&gt; SRR1283389     2  0.4866      0.751 0.000 0.596 0.000 NA
#&gt; SRR1283390     2  0.4866      0.751 0.000 0.596 0.000 NA
#&gt; SRR1283382     2  0.5964      0.707 0.000 0.684 0.108 NA
#&gt; SRR1283383     2  0.5964      0.707 0.000 0.684 0.108 NA
#&gt; SRR1283384     2  0.5964      0.707 0.000 0.684 0.108 NA
#&gt; SRR1283391     2  0.1004      0.758 0.000 0.972 0.004 NA
#&gt; SRR1283392     2  0.1004      0.758 0.000 0.972 0.004 NA
#&gt; SRR1283393     2  0.1004      0.758 0.000 0.972 0.004 NA
#&gt; SRR1283394     2  0.4877      0.751 0.000 0.592 0.000 NA
#&gt; SRR1283395     2  0.4877      0.751 0.000 0.592 0.000 NA
#&gt; SRR1283396     2  0.4877      0.751 0.000 0.592 0.000 NA
#&gt; SRR1283397     2  0.0188      0.762 0.000 0.996 0.004 NA
#&gt; SRR1283398     2  0.0188      0.762 0.000 0.996 0.004 NA
#&gt; SRR1283399     2  0.0188      0.762 0.000 0.996 0.004 NA
#&gt; SRR1283400     2  0.0000      0.762 0.000 1.000 0.000 NA
#&gt; SRR1283401     2  0.0000      0.762 0.000 1.000 0.000 NA
#&gt; SRR1283402     2  0.0000      0.762 0.000 1.000 0.000 NA
#&gt; SRR1283403     3  0.2814      0.977 0.132 0.000 0.868 NA
#&gt; SRR1283404     3  0.2814      0.977 0.132 0.000 0.868 NA
#&gt; SRR1283405     3  0.2814      0.977 0.132 0.000 0.868 NA
#&gt; SRR1283406     1  0.2868      0.854 0.864 0.000 0.000 NA
#&gt; SRR1283407     1  0.2868      0.854 0.864 0.000 0.000 NA
#&gt; SRR1283408     1  0.2868      0.854 0.864 0.000 0.000 NA
#&gt; SRR1283409     1  0.2216      0.877 0.908 0.000 0.000 NA
#&gt; SRR1283410     1  0.2216      0.877 0.908 0.000 0.000 NA
#&gt; SRR1283411     1  0.2216      0.877 0.908 0.000 0.000 NA
#&gt; SRR1283412     1  0.1637      0.894 0.940 0.000 0.000 NA
#&gt; SRR1283413     1  0.1637      0.894 0.940 0.000 0.000 NA
#&gt; SRR1283414     1  0.1637      0.894 0.940 0.000 0.000 NA
#&gt; SRR1283415     1  0.3726      0.794 0.788 0.000 0.000 NA
#&gt; SRR1283416     1  0.3726      0.794 0.788 0.000 0.000 NA
#&gt; SRR1283417     1  0.3726      0.794 0.788 0.000 0.000 NA
#&gt; SRR1283418     1  0.1211      0.897 0.960 0.000 0.000 NA
#&gt; SRR1283419     1  0.1211      0.897 0.960 0.000 0.000 NA
#&gt; SRR1283420     1  0.1211      0.897 0.960 0.000 0.000 NA
#&gt; SRR1283421     1  0.1211      0.897 0.960 0.000 0.000 NA
#&gt; SRR1283422     1  0.1211      0.897 0.960 0.000 0.000 NA
#&gt; SRR1283423     1  0.1211      0.897 0.960 0.000 0.000 NA
#&gt; SRR1283424     1  0.0188      0.897 0.996 0.000 0.000 NA
#&gt; SRR1283425     1  0.0188      0.897 0.996 0.000 0.000 NA
#&gt; SRR1283426     1  0.0188      0.897 0.996 0.000 0.000 NA
#&gt; SRR1283427     1  0.3444      0.813 0.816 0.000 0.000 NA
#&gt; SRR1283428     1  0.3444      0.813 0.816 0.000 0.000 NA
#&gt; SRR1283429     1  0.3444      0.813 0.816 0.000 0.000 NA
#&gt; SRR1283430     2  0.4866      0.751 0.000 0.596 0.000 NA
#&gt; SRR1283431     2  0.4866      0.751 0.000 0.596 0.000 NA
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1283379     3  0.1041     0.9483 0.032 0.000 0.964 0.004 NA
#&gt; SRR1283380     3  0.1202     0.9481 0.032 0.004 0.960 0.000 NA
#&gt; SRR1283381     3  0.1041     0.9483 0.032 0.000 0.964 0.004 NA
#&gt; SRR1283385     4  0.3884     1.0000 0.004 0.288 0.000 0.708 NA
#&gt; SRR1283386     4  0.3884     1.0000 0.004 0.288 0.000 0.708 NA
#&gt; SRR1283387     4  0.3884     1.0000 0.004 0.288 0.000 0.708 NA
#&gt; SRR1283388     2  0.6836     0.0528 0.004 0.428 0.000 0.284 NA
#&gt; SRR1283389     2  0.6836     0.0528 0.004 0.428 0.000 0.284 NA
#&gt; SRR1283390     2  0.6836     0.0528 0.004 0.428 0.000 0.284 NA
#&gt; SRR1283382     2  0.6095    -0.3028 0.004 0.516 0.024 0.400 NA
#&gt; SRR1283383     2  0.6095    -0.3028 0.004 0.516 0.024 0.400 NA
#&gt; SRR1283384     2  0.6095    -0.3028 0.004 0.516 0.024 0.400 NA
#&gt; SRR1283391     2  0.0613     0.4699 0.004 0.984 0.004 0.008 NA
#&gt; SRR1283392     2  0.0613     0.4699 0.004 0.984 0.004 0.008 NA
#&gt; SRR1283393     2  0.0613     0.4699 0.004 0.984 0.004 0.008 NA
#&gt; SRR1283394     2  0.6965     0.0457 0.004 0.428 0.004 0.292 NA
#&gt; SRR1283395     2  0.6965     0.0457 0.004 0.428 0.004 0.292 NA
#&gt; SRR1283396     2  0.6965     0.0457 0.004 0.428 0.004 0.292 NA
#&gt; SRR1283397     2  0.0833     0.4705 0.004 0.976 0.004 0.000 NA
#&gt; SRR1283398     2  0.0833     0.4705 0.004 0.976 0.004 0.000 NA
#&gt; SRR1283399     2  0.0833     0.4705 0.004 0.976 0.004 0.000 NA
#&gt; SRR1283400     2  0.0162     0.4737 0.004 0.996 0.000 0.000 NA
#&gt; SRR1283401     2  0.0162     0.4737 0.004 0.996 0.000 0.000 NA
#&gt; SRR1283402     2  0.0162     0.4737 0.004 0.996 0.000 0.000 NA
#&gt; SRR1283403     3  0.3622     0.9487 0.032 0.000 0.844 0.032 NA
#&gt; SRR1283404     3  0.3594     0.9488 0.032 0.000 0.844 0.028 NA
#&gt; SRR1283405     3  0.3594     0.9488 0.032 0.000 0.844 0.028 NA
#&gt; SRR1283406     1  0.5182     0.6927 0.632 0.000 0.000 0.068 NA
#&gt; SRR1283407     1  0.5182     0.6927 0.632 0.000 0.000 0.068 NA
#&gt; SRR1283408     1  0.5182     0.6927 0.632 0.000 0.000 0.068 NA
#&gt; SRR1283409     1  0.3966     0.7094 0.664 0.000 0.000 0.000 NA
#&gt; SRR1283410     1  0.3966     0.7094 0.664 0.000 0.000 0.000 NA
#&gt; SRR1283411     1  0.3966     0.7094 0.664 0.000 0.000 0.000 NA
#&gt; SRR1283412     1  0.1430     0.8118 0.944 0.000 0.000 0.004 NA
#&gt; SRR1283413     1  0.1430     0.8118 0.944 0.000 0.000 0.004 NA
#&gt; SRR1283414     1  0.1430     0.8118 0.944 0.000 0.000 0.004 NA
#&gt; SRR1283415     1  0.5904     0.6606 0.600 0.000 0.000 0.204 NA
#&gt; SRR1283416     1  0.5904     0.6606 0.600 0.000 0.000 0.204 NA
#&gt; SRR1283417     1  0.5904     0.6606 0.600 0.000 0.000 0.204 NA
#&gt; SRR1283418     1  0.0000     0.8216 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0000     0.8216 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0000     0.8216 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0000     0.8216 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0000     0.8216 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0000     0.8216 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.1106     0.8219 0.964 0.000 0.000 0.012 NA
#&gt; SRR1283425     1  0.1106     0.8219 0.964 0.000 0.000 0.012 NA
#&gt; SRR1283426     1  0.1106     0.8219 0.964 0.000 0.000 0.012 NA
#&gt; SRR1283427     1  0.5268     0.7070 0.680 0.000 0.000 0.148 NA
#&gt; SRR1283428     1  0.5268     0.7070 0.680 0.000 0.000 0.148 NA
#&gt; SRR1283429     1  0.5268     0.7070 0.680 0.000 0.000 0.148 NA
#&gt; SRR1283430     2  0.6836     0.0528 0.004 0.428 0.000 0.284 NA
#&gt; SRR1283431     2  0.6836     0.0528 0.004 0.428 0.000 0.284 NA
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1283379     3  0.0632      0.934 0.024 0.000 0.976 0.000 0.000 0.000
#&gt; SRR1283380     3  0.0777      0.934 0.024 0.000 0.972 0.000 0.004 0.000
#&gt; SRR1283381     3  0.0632      0.934 0.024 0.000 0.976 0.000 0.000 0.000
#&gt; SRR1283385     5  0.7010      0.630 0.000 0.192 0.000 0.248 0.456 0.104
#&gt; SRR1283386     5  0.7010      0.630 0.000 0.192 0.000 0.248 0.456 0.104
#&gt; SRR1283387     5  0.7010      0.630 0.000 0.192 0.000 0.248 0.456 0.104
#&gt; SRR1283388     4  0.3309      0.972 0.000 0.280 0.000 0.720 0.000 0.000
#&gt; SRR1283389     4  0.3309      0.972 0.000 0.280 0.000 0.720 0.000 0.000
#&gt; SRR1283390     4  0.3309      0.972 0.000 0.280 0.000 0.720 0.000 0.000
#&gt; SRR1283382     5  0.4326      0.613 0.000 0.404 0.000 0.024 0.572 0.000
#&gt; SRR1283383     5  0.4326      0.613 0.000 0.404 0.000 0.024 0.572 0.000
#&gt; SRR1283384     5  0.4326      0.613 0.000 0.404 0.000 0.024 0.572 0.000
#&gt; SRR1283391     2  0.1765      0.910 0.000 0.924 0.000 0.000 0.024 0.052
#&gt; SRR1283392     2  0.1765      0.910 0.000 0.924 0.000 0.000 0.024 0.052
#&gt; SRR1283393     2  0.1765      0.910 0.000 0.924 0.000 0.000 0.024 0.052
#&gt; SRR1283394     4  0.4495      0.960 0.000 0.276 0.012 0.676 0.004 0.032
#&gt; SRR1283395     4  0.4495      0.960 0.000 0.276 0.012 0.676 0.004 0.032
#&gt; SRR1283396     4  0.4495      0.960 0.000 0.276 0.012 0.676 0.004 0.032
#&gt; SRR1283397     2  0.1413      0.922 0.000 0.948 0.004 0.004 0.036 0.008
#&gt; SRR1283398     2  0.1413      0.922 0.000 0.948 0.004 0.004 0.036 0.008
#&gt; SRR1283399     2  0.1413      0.922 0.000 0.948 0.004 0.004 0.036 0.008
#&gt; SRR1283400     2  0.0000      0.937 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.937 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.937 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283403     3  0.3889      0.932 0.024 0.000 0.824 0.060 0.032 0.060
#&gt; SRR1283404     3  0.3848      0.932 0.024 0.000 0.824 0.072 0.024 0.056
#&gt; SRR1283405     3  0.3848      0.932 0.024 0.000 0.824 0.072 0.024 0.056
#&gt; SRR1283406     1  0.6321      0.292 0.524 0.000 0.000 0.048 0.264 0.164
#&gt; SRR1283407     1  0.6321      0.292 0.524 0.000 0.000 0.048 0.264 0.164
#&gt; SRR1283408     1  0.6321      0.292 0.524 0.000 0.000 0.048 0.264 0.164
#&gt; SRR1283409     1  0.6570      0.344 0.552 0.000 0.000 0.128 0.168 0.152
#&gt; SRR1283410     1  0.6570      0.344 0.552 0.000 0.000 0.128 0.168 0.152
#&gt; SRR1283411     1  0.6570      0.344 0.552 0.000 0.000 0.128 0.168 0.152
#&gt; SRR1283412     1  0.1666      0.623 0.936 0.000 0.000 0.008 0.020 0.036
#&gt; SRR1283413     1  0.1666      0.623 0.936 0.000 0.000 0.008 0.020 0.036
#&gt; SRR1283414     1  0.1666      0.623 0.936 0.000 0.000 0.008 0.020 0.036
#&gt; SRR1283415     6  0.3727      1.000 0.388 0.000 0.000 0.000 0.000 0.612
#&gt; SRR1283416     6  0.3727      1.000 0.388 0.000 0.000 0.000 0.000 0.612
#&gt; SRR1283417     6  0.3727      1.000 0.388 0.000 0.000 0.000 0.000 0.612
#&gt; SRR1283418     1  0.0260      0.630 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1283419     1  0.0260      0.630 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1283420     1  0.0260      0.630 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.630 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.630 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.630 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.1549      0.606 0.936 0.000 0.000 0.020 0.000 0.044
#&gt; SRR1283425     1  0.1549      0.606 0.936 0.000 0.000 0.020 0.000 0.044
#&gt; SRR1283426     1  0.1549      0.606 0.936 0.000 0.000 0.020 0.000 0.044
#&gt; SRR1283427     1  0.4897     -0.567 0.536 0.000 0.000 0.028 0.020 0.416
#&gt; SRR1283428     1  0.4897     -0.567 0.536 0.000 0.000 0.028 0.020 0.416
#&gt; SRR1283429     1  0.4897     -0.567 0.536 0.000 0.000 0.028 0.020 0.416
#&gt; SRR1283430     4  0.3799      0.969 0.000 0.280 0.008 0.704 0.000 0.008
#&gt; SRR1283431     4  0.3799      0.969 0.000 0.280 0.008 0.704 0.000 0.008
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 0.890           0.882       0.898         0.0778 1.000   1.000
#> 5 5 0.797           0.827       0.802         0.0814 0.889   0.719
#> 6 6 0.775           0.845       0.848         0.0618 0.993   0.977
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1283379     3  0.0000      0.867 0.000 0.000 1.000 NA
#&gt; SRR1283380     3  0.0000      0.867 0.000 0.000 1.000 NA
#&gt; SRR1283381     3  0.0000      0.867 0.000 0.000 1.000 NA
#&gt; SRR1283385     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283386     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283387     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283388     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283389     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283390     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283382     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283383     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283384     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283391     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283392     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283393     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283394     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283395     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283396     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283397     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283398     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283399     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283400     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283401     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283402     2  0.0000      0.985 0.000 1.000 0.000 NA
#&gt; SRR1283403     3  0.4877      0.867 0.000 0.000 0.592 NA
#&gt; SRR1283404     3  0.4877      0.867 0.000 0.000 0.592 NA
#&gt; SRR1283405     3  0.4877      0.867 0.000 0.000 0.592 NA
#&gt; SRR1283406     1  0.4866      0.598 0.596 0.000 0.000 NA
#&gt; SRR1283407     1  0.4866      0.598 0.596 0.000 0.000 NA
#&gt; SRR1283408     1  0.4866      0.598 0.596 0.000 0.000 NA
#&gt; SRR1283409     1  0.4585      0.666 0.668 0.000 0.000 NA
#&gt; SRR1283410     1  0.4585      0.666 0.668 0.000 0.000 NA
#&gt; SRR1283411     1  0.4585      0.666 0.668 0.000 0.000 NA
#&gt; SRR1283412     1  0.0188      0.860 0.996 0.000 0.000 NA
#&gt; SRR1283413     1  0.0188      0.860 0.996 0.000 0.000 NA
#&gt; SRR1283414     1  0.0188      0.860 0.996 0.000 0.000 NA
#&gt; SRR1283415     1  0.3123      0.799 0.844 0.000 0.000 NA
#&gt; SRR1283416     1  0.3123      0.799 0.844 0.000 0.000 NA
#&gt; SRR1283417     1  0.3123      0.799 0.844 0.000 0.000 NA
#&gt; SRR1283418     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283425     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283426     1  0.0000      0.861 1.000 0.000 0.000 NA
#&gt; SRR1283427     1  0.3123      0.799 0.844 0.000 0.000 NA
#&gt; SRR1283428     1  0.3123      0.799 0.844 0.000 0.000 NA
#&gt; SRR1283429     1  0.3123      0.799 0.844 0.000 0.000 NA
#&gt; SRR1283430     2  0.1022      0.984 0.000 0.968 0.000 NA
#&gt; SRR1283431     2  0.1022      0.984 0.000 0.968 0.000 NA
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1283379     3  0.0000      0.710 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283380     3  0.0000      0.710 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283381     3  0.0000      0.710 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283385     2  0.0609      0.913 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1283386     2  0.0609      0.913 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1283387     2  0.0609      0.913 0.000 0.980 0.000 0.000 0.020
#&gt; SRR1283388     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283389     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283390     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283382     2  0.3297      0.920 0.000 0.848 0.000 0.068 0.084
#&gt; SRR1283383     2  0.3297      0.920 0.000 0.848 0.000 0.068 0.084
#&gt; SRR1283384     2  0.3297      0.920 0.000 0.848 0.000 0.068 0.084
#&gt; SRR1283391     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283392     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283393     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283394     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283395     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283396     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283397     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283398     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283399     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283400     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283401     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283402     2  0.3239      0.923 0.000 0.852 0.000 0.068 0.080
#&gt; SRR1283403     3  0.6781      0.710 0.000 0.000 0.376 0.344 0.280
#&gt; SRR1283404     3  0.6781      0.710 0.000 0.000 0.376 0.344 0.280
#&gt; SRR1283405     3  0.6781      0.710 0.000 0.000 0.376 0.344 0.280
#&gt; SRR1283406     5  0.4192      1.000 0.404 0.000 0.000 0.000 0.596
#&gt; SRR1283407     5  0.4192      1.000 0.404 0.000 0.000 0.000 0.596
#&gt; SRR1283408     5  0.4192      1.000 0.404 0.000 0.000 0.000 0.596
#&gt; SRR1283409     1  0.4497     -0.233 0.632 0.000 0.000 0.016 0.352
#&gt; SRR1283410     1  0.4497     -0.233 0.632 0.000 0.000 0.016 0.352
#&gt; SRR1283411     1  0.4497     -0.233 0.632 0.000 0.000 0.016 0.352
#&gt; SRR1283412     1  0.0671      0.833 0.980 0.000 0.000 0.004 0.016
#&gt; SRR1283413     1  0.0671      0.833 0.980 0.000 0.000 0.004 0.016
#&gt; SRR1283414     1  0.0671      0.833 0.980 0.000 0.000 0.004 0.016
#&gt; SRR1283415     4  0.4242      0.996 0.428 0.000 0.000 0.572 0.000
#&gt; SRR1283416     4  0.4242      0.996 0.428 0.000 0.000 0.572 0.000
#&gt; SRR1283417     4  0.4242      0.996 0.428 0.000 0.000 0.572 0.000
#&gt; SRR1283418     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.847 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1283427     4  0.4249      0.996 0.432 0.000 0.000 0.568 0.000
#&gt; SRR1283428     4  0.4249      0.996 0.432 0.000 0.000 0.568 0.000
#&gt; SRR1283429     4  0.4249      0.996 0.432 0.000 0.000 0.568 0.000
#&gt; SRR1283430     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1283431     2  0.0162      0.918 0.000 0.996 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1283379     3  0.2135      1.000 0.000 0.000 0.872 0.128 0.000 0.000
#&gt; SRR1283380     3  0.2135      1.000 0.000 0.000 0.872 0.128 0.000 0.000
#&gt; SRR1283381     3  0.2135      1.000 0.000 0.000 0.872 0.128 0.000 0.000
#&gt; SRR1283385     2  0.5817      0.776 0.000 0.640 0.120 0.000 0.092 0.148
#&gt; SRR1283386     2  0.5817      0.776 0.000 0.640 0.120 0.000 0.092 0.148
#&gt; SRR1283387     2  0.5817      0.776 0.000 0.640 0.120 0.000 0.092 0.148
#&gt; SRR1283388     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283389     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283390     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283382     2  0.2119      0.793 0.000 0.912 0.008 0.000 0.044 0.036
#&gt; SRR1283383     2  0.2119      0.793 0.000 0.912 0.008 0.000 0.044 0.036
#&gt; SRR1283384     2  0.2119      0.793 0.000 0.912 0.008 0.000 0.044 0.036
#&gt; SRR1283391     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283392     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283393     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283394     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283395     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283396     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283397     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283398     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283399     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283400     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283401     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283402     2  0.0632      0.812 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1283406     5  0.2883      1.000 0.212 0.000 0.000 0.000 0.788 0.000
#&gt; SRR1283407     5  0.2883      1.000 0.212 0.000 0.000 0.000 0.788 0.000
#&gt; SRR1283408     5  0.2883      1.000 0.212 0.000 0.000 0.000 0.788 0.000
#&gt; SRR1283409     1  0.4909      0.278 0.588 0.000 0.008 0.000 0.348 0.056
#&gt; SRR1283410     1  0.4909      0.278 0.588 0.000 0.008 0.000 0.348 0.056
#&gt; SRR1283411     1  0.4909      0.278 0.588 0.000 0.008 0.000 0.348 0.056
#&gt; SRR1283412     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283413     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283414     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283415     6  0.3052      0.986 0.216 0.000 0.000 0.000 0.004 0.780
#&gt; SRR1283416     6  0.3052      0.986 0.216 0.000 0.000 0.000 0.004 0.780
#&gt; SRR1283417     6  0.3052      0.986 0.216 0.000 0.000 0.000 0.004 0.780
#&gt; SRR1283418     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1283427     6  0.3023      0.986 0.232 0.000 0.000 0.000 0.000 0.768
#&gt; SRR1283428     6  0.3023      0.986 0.232 0.000 0.000 0.000 0.000 0.768
#&gt; SRR1283429     6  0.3023      0.986 0.232 0.000 0.000 0.000 0.000 0.768
#&gt; SRR1283430     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
#&gt; SRR1283431     2  0.5227      0.799 0.000 0.692 0.112 0.000 0.056 0.140
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 1.000           1.000       1.000         0.0108 0.993   0.983
#> 5 5 0.793           0.819       0.878         0.1212 1.000   1.000
#> 6 6 0.750           0.491       0.771         0.0766 0.878   0.686
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4 p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 NA
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 NA
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 NA
#&gt; SRR1283385     2  0.3796      0.827 0.000 0.700  0  0 NA
#&gt; SRR1283386     2  0.3707      0.834 0.000 0.716  0  0 NA
#&gt; SRR1283387     2  0.3816      0.826 0.000 0.696  0  0 NA
#&gt; SRR1283388     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283389     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283390     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283382     2  0.1270      0.841 0.000 0.948  0  0 NA
#&gt; SRR1283383     2  0.1270      0.841 0.000 0.948  0  0 NA
#&gt; SRR1283384     2  0.1270      0.841 0.000 0.948  0  0 NA
#&gt; SRR1283391     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283392     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283393     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283394     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283395     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283396     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283397     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283398     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283399     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283400     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283401     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283402     2  0.0000      0.861 0.000 1.000  0  0 NA
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 NA
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 NA
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 NA
#&gt; SRR1283406     1  0.3305      0.675 0.776 0.000  0  0 NA
#&gt; SRR1283407     1  0.3305      0.675 0.776 0.000  0  0 NA
#&gt; SRR1283408     1  0.3305      0.675 0.776 0.000  0  0 NA
#&gt; SRR1283409     1  0.0703      0.833 0.976 0.000  0  0 NA
#&gt; SRR1283410     1  0.0703      0.833 0.976 0.000  0  0 NA
#&gt; SRR1283411     1  0.0703      0.833 0.976 0.000  0  0 NA
#&gt; SRR1283412     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283413     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283414     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283415     1  0.4273      0.539 0.552 0.000  0  0 NA
#&gt; SRR1283416     1  0.4273      0.539 0.552 0.000  0  0 NA
#&gt; SRR1283417     1  0.4273      0.539 0.552 0.000  0  0 NA
#&gt; SRR1283418     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283419     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283420     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283421     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283422     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283423     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283424     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283425     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283426     1  0.0000      0.842 1.000 0.000  0  0 NA
#&gt; SRR1283427     1  0.4273      0.539 0.552 0.000  0  0 NA
#&gt; SRR1283428     1  0.4273      0.539 0.552 0.000  0  0 NA
#&gt; SRR1283429     1  0.4273      0.539 0.552 0.000  0  0 NA
#&gt; SRR1283430     2  0.3508      0.846 0.000 0.748  0  0 NA
#&gt; SRR1283431     2  0.3508      0.846 0.000 0.748  0  0 NA
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5    p6
#&gt; SRR1283379     3   0.000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283385     2   0.214      0.356 0.000 0.872  0  0 0.128 0.000
#&gt; SRR1283386     2   0.230      0.343 0.000 0.856  0  0 0.144 0.000
#&gt; SRR1283387     2   0.214      0.356 0.000 0.872  0  0 0.128 0.000
#&gt; SRR1283388     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283389     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283390     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283382     5   0.386      1.000 0.000 0.480  0  0 0.520 0.000
#&gt; SRR1283383     5   0.386      1.000 0.000 0.480  0  0 0.520 0.000
#&gt; SRR1283384     5   0.386      1.000 0.000 0.480  0  0 0.520 0.000
#&gt; SRR1283391     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283392     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283393     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283394     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283395     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283396     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283397     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283398     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283399     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283400     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283401     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283402     2   0.374     -0.442 0.000 0.608  0  0 0.392 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283406     1   0.447     -0.127 0.584 0.000  0  0 0.380 0.036
#&gt; SRR1283407     1   0.447     -0.127 0.584 0.000  0  0 0.380 0.036
#&gt; SRR1283408     1   0.447     -0.127 0.584 0.000  0  0 0.380 0.036
#&gt; SRR1283409     1   0.525      0.567 0.512 0.000  0  0 0.100 0.388
#&gt; SRR1283410     1   0.525      0.567 0.512 0.000  0  0 0.100 0.388
#&gt; SRR1283411     1   0.525      0.567 0.512 0.000  0  0 0.100 0.388
#&gt; SRR1283412     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283413     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283414     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283415     6   0.000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283416     6   0.000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283417     6   0.000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283418     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283419     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283420     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283421     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283422     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283423     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283424     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283425     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283426     1   0.382      0.721 0.564 0.000  0  0 0.000 0.436
#&gt; SRR1283427     6   0.000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283428     6   0.000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283429     6   0.000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283430     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283431     2   0.000      0.494 0.000 1.000  0  0 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.5013 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2082 0.896   0.791
#> 4 4 1.000           1.000       1.000         0.0108 0.993   0.983
#> 5 5 0.814           0.861       0.909         0.1033 1.000   1.000
#> 6 6 0.736           0.771       0.862         0.0906 0.880   0.692
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     1  0.0672      0.993 0.992 0.008
#&gt; SRR1283380     1  0.0672      0.993 0.992 0.008
#&gt; SRR1283381     1  0.0672      0.993 0.992 0.008
#&gt; SRR1283385     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283386     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283387     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283388     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283389     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283390     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283382     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283383     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283384     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283391     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283392     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283393     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283394     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283395     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283396     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283397     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283398     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283399     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283400     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283401     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283402     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283403     1  0.0672      0.993 0.992 0.008
#&gt; SRR1283404     1  0.0672      0.993 0.992 0.008
#&gt; SRR1283405     1  0.0672      0.993 0.992 0.008
#&gt; SRR1283406     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283407     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283408     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283409     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283410     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283411     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283412     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283413     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283414     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283415     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283416     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283417     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283418     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283419     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283420     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283421     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283422     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283423     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283424     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283425     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283426     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283427     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283428     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283429     1  0.0000      0.998 1.000 0.000
#&gt; SRR1283430     2  0.0000      1.000 0.000 1.000
#&gt; SRR1283431     2  0.0000      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1283379     3       0          1  0  0  1  0
#&gt; SRR1283380     3       0          1  0  0  1  0
#&gt; SRR1283381     3       0          1  0  0  1  0
#&gt; SRR1283385     2       0          1  0  1  0  0
#&gt; SRR1283386     2       0          1  0  1  0  0
#&gt; SRR1283387     2       0          1  0  1  0  0
#&gt; SRR1283388     2       0          1  0  1  0  0
#&gt; SRR1283389     2       0          1  0  1  0  0
#&gt; SRR1283390     2       0          1  0  1  0  0
#&gt; SRR1283382     2       0          1  0  1  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0
#&gt; SRR1283394     2       0          1  0  1  0  0
#&gt; SRR1283395     2       0          1  0  1  0  0
#&gt; SRR1283396     2       0          1  0  1  0  0
#&gt; SRR1283397     2       0          1  0  1  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1
#&gt; SRR1283404     4       0          1  0  0  0  1
#&gt; SRR1283405     4       0          1  0  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0
#&gt; SRR1283430     2       0          1  0  1  0  0
#&gt; SRR1283431     2       0          1  0  1  0  0
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4 p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 NA
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 NA
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 NA
#&gt; SRR1283385     2  0.3210      0.822 0.000 0.788  0  0 NA
#&gt; SRR1283386     2  0.3210      0.822 0.000 0.788  0  0 NA
#&gt; SRR1283387     2  0.3210      0.822 0.000 0.788  0  0 NA
#&gt; SRR1283388     2  0.0162      0.941 0.000 0.996  0  0 NA
#&gt; SRR1283389     2  0.0162      0.941 0.000 0.996  0  0 NA
#&gt; SRR1283390     2  0.0162      0.941 0.000 0.996  0  0 NA
#&gt; SRR1283382     2  0.3210      0.822 0.000 0.788  0  0 NA
#&gt; SRR1283383     2  0.3210      0.822 0.000 0.788  0  0 NA
#&gt; SRR1283384     2  0.3210      0.822 0.000 0.788  0  0 NA
#&gt; SRR1283391     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283392     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283393     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283394     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283395     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283396     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283397     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283398     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283399     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283400     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283401     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283402     2  0.0000      0.942 0.000 1.000  0  0 NA
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 NA
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 NA
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 NA
#&gt; SRR1283406     1  0.2929      0.796 0.820 0.000  0  0 NA
#&gt; SRR1283407     1  0.2929      0.796 0.820 0.000  0  0 NA
#&gt; SRR1283408     1  0.2929      0.796 0.820 0.000  0  0 NA
#&gt; SRR1283409     1  0.3707      0.713 0.716 0.000  0  0 NA
#&gt; SRR1283410     1  0.3707      0.713 0.716 0.000  0  0 NA
#&gt; SRR1283411     1  0.3707      0.713 0.716 0.000  0  0 NA
#&gt; SRR1283412     1  0.2929      0.785 0.820 0.000  0  0 NA
#&gt; SRR1283413     1  0.2929      0.785 0.820 0.000  0  0 NA
#&gt; SRR1283414     1  0.2929      0.785 0.820 0.000  0  0 NA
#&gt; SRR1283415     1  0.4268      0.549 0.556 0.000  0  0 NA
#&gt; SRR1283416     1  0.4268      0.549 0.556 0.000  0  0 NA
#&gt; SRR1283417     1  0.4268      0.549 0.556 0.000  0  0 NA
#&gt; SRR1283418     1  0.0000      0.853 1.000 0.000  0  0 NA
#&gt; SRR1283419     1  0.0000      0.853 1.000 0.000  0  0 NA
#&gt; SRR1283420     1  0.0000      0.853 1.000 0.000  0  0 NA
#&gt; SRR1283421     1  0.1851      0.828 0.912 0.000  0  0 NA
#&gt; SRR1283422     1  0.1851      0.828 0.912 0.000  0  0 NA
#&gt; SRR1283423     1  0.1851      0.828 0.912 0.000  0  0 NA
#&gt; SRR1283424     1  0.0000      0.853 1.000 0.000  0  0 NA
#&gt; SRR1283425     1  0.0000      0.853 1.000 0.000  0  0 NA
#&gt; SRR1283426     1  0.0000      0.853 1.000 0.000  0  0 NA
#&gt; SRR1283427     1  0.0162      0.853 0.996 0.000  0  0 NA
#&gt; SRR1283428     1  0.0162      0.853 0.996 0.000  0  0 NA
#&gt; SRR1283429     1  0.0162      0.853 0.996 0.000  0  0 NA
#&gt; SRR1283430     2  0.0162      0.941 0.000 0.996  0  0 NA
#&gt; SRR1283431     2  0.0162      0.941 0.000 0.996  0  0 NA
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5    p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283385     5  0.3578      0.960 0.000 0.340  0  0 0.660 0.000
#&gt; SRR1283386     5  0.3578      0.960 0.000 0.340  0  0 0.660 0.000
#&gt; SRR1283387     5  0.3578      0.960 0.000 0.340  0  0 0.660 0.000
#&gt; SRR1283388     2  0.2003      0.870 0.000 0.884  0  0 0.116 0.000
#&gt; SRR1283389     2  0.2003      0.870 0.000 0.884  0  0 0.116 0.000
#&gt; SRR1283390     2  0.2003      0.870 0.000 0.884  0  0 0.116 0.000
#&gt; SRR1283382     5  0.3390      0.960 0.000 0.296  0  0 0.704 0.000
#&gt; SRR1283383     5  0.3390      0.960 0.000 0.296  0  0 0.704 0.000
#&gt; SRR1283384     5  0.3390      0.960 0.000 0.296  0  0 0.704 0.000
#&gt; SRR1283391     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283392     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283393     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283394     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283395     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283396     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283397     2  0.0260      0.942 0.000 0.992  0  0 0.008 0.000
#&gt; SRR1283398     2  0.0260      0.942 0.000 0.992  0  0 0.008 0.000
#&gt; SRR1283399     2  0.0260      0.942 0.000 0.992  0  0 0.008 0.000
#&gt; SRR1283400     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.947 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283402     2  0.0146      0.945 0.000 0.996  0  0 0.004 0.000
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283406     1  0.3337      0.297 0.736 0.000  0  0 0.004 0.260
#&gt; SRR1283407     1  0.3337      0.297 0.736 0.000  0  0 0.004 0.260
#&gt; SRR1283408     1  0.3337      0.297 0.736 0.000  0  0 0.004 0.260
#&gt; SRR1283409     1  0.3747      0.137 0.604 0.000  0  0 0.000 0.396
#&gt; SRR1283410     1  0.3747      0.137 0.604 0.000  0  0 0.000 0.396
#&gt; SRR1283411     1  0.3747      0.137 0.604 0.000  0  0 0.000 0.396
#&gt; SRR1283412     1  0.4821      0.404 0.668 0.000  0  0 0.148 0.184
#&gt; SRR1283413     1  0.4821      0.404 0.668 0.000  0  0 0.148 0.184
#&gt; SRR1283414     1  0.4821      0.404 0.668 0.000  0  0 0.148 0.184
#&gt; SRR1283415     6  0.3864      1.000 0.480 0.000  0  0 0.000 0.520
#&gt; SRR1283416     6  0.3864      1.000 0.480 0.000  0  0 0.000 0.520
#&gt; SRR1283417     6  0.3864      1.000 0.480 0.000  0  0 0.000 0.520
#&gt; SRR1283418     1  0.0260      0.672 0.992 0.000  0  0 0.000 0.008
#&gt; SRR1283419     1  0.0260      0.672 0.992 0.000  0  0 0.000 0.008
#&gt; SRR1283420     1  0.0260      0.672 0.992 0.000  0  0 0.000 0.008
#&gt; SRR1283421     1  0.2178      0.607 0.868 0.000  0  0 0.000 0.132
#&gt; SRR1283422     1  0.2178      0.607 0.868 0.000  0  0 0.000 0.132
#&gt; SRR1283423     1  0.2178      0.607 0.868 0.000  0  0 0.000 0.132
#&gt; SRR1283424     1  0.0000      0.673 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.673 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.673 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283427     1  0.0000      0.673 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283428     1  0.0000      0.673 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283429     1  0.0000      0.673 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283430     2  0.1814      0.884 0.000 0.900  0  0 0.100 0.000
#&gt; SRR1283431     2  0.1814      0.884 0.000 0.900  0  0 0.100 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 1.000           0.999       0.998         0.0112 0.993   0.983
#> 5 5 0.963           0.973       0.970         0.0228 1.000   1.000
#> 6 6 0.904           0.941       0.947         0.0257 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1283385     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283386     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283387     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283388     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283389     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283390     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR1283382     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283383     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283384     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283391     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283392     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283393     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283394     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283395     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283396     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283397     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283398     2  0.0188      0.997 0.000 0.996 0.000 0.004
#&gt; SRR1283399     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283400     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283401     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283402     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283403     4  0.0657      1.000 0.004 0.000 0.012 0.984
#&gt; SRR1283404     4  0.0657      1.000 0.004 0.000 0.012 0.984
#&gt; SRR1283405     4  0.0657      1.000 0.004 0.000 0.012 0.984
#&gt; SRR1283406     1  0.0188      0.996 0.996 0.000 0.000 0.004
#&gt; SRR1283407     1  0.0188      0.996 0.996 0.000 0.000 0.004
#&gt; SRR1283408     1  0.0188      0.996 0.996 0.000 0.000 0.004
#&gt; SRR1283409     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283410     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283411     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283412     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283413     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283414     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283415     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283416     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283417     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283418     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283427     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283428     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283429     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283430     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1283431     2  0.0000      0.998 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1283379     3  0.1341      1.000 0.000 0.000 0.944 0.056 NA
#&gt; SRR1283380     3  0.1341      1.000 0.000 0.000 0.944 0.056 NA
#&gt; SRR1283381     3  0.1341      1.000 0.000 0.000 0.944 0.056 NA
#&gt; SRR1283385     2  0.2020      0.945 0.000 0.900 0.000 0.000 NA
#&gt; SRR1283386     2  0.1965      0.946 0.000 0.904 0.000 0.000 NA
#&gt; SRR1283387     2  0.2127      0.944 0.000 0.892 0.000 0.000 NA
#&gt; SRR1283388     2  0.1341      0.951 0.000 0.944 0.000 0.000 NA
#&gt; SRR1283389     2  0.1341      0.951 0.000 0.944 0.000 0.000 NA
#&gt; SRR1283390     2  0.1410      0.949 0.000 0.940 0.000 0.000 NA
#&gt; SRR1283382     2  0.1544      0.942 0.000 0.932 0.000 0.000 NA
#&gt; SRR1283383     2  0.1544      0.942 0.000 0.932 0.000 0.000 NA
#&gt; SRR1283384     2  0.1544      0.942 0.000 0.932 0.000 0.000 NA
#&gt; SRR1283391     2  0.1732      0.936 0.000 0.920 0.000 0.000 NA
#&gt; SRR1283392     2  0.1544      0.942 0.000 0.932 0.000 0.000 NA
#&gt; SRR1283393     2  0.1121      0.950 0.000 0.956 0.000 0.000 NA
#&gt; SRR1283394     2  0.1341      0.951 0.000 0.944 0.000 0.000 NA
#&gt; SRR1283395     2  0.1341      0.951 0.000 0.944 0.000 0.000 NA
#&gt; SRR1283396     2  0.1410      0.949 0.000 0.940 0.000 0.000 NA
#&gt; SRR1283397     2  0.0510      0.955 0.000 0.984 0.000 0.000 NA
#&gt; SRR1283398     2  0.0510      0.955 0.000 0.984 0.000 0.000 NA
#&gt; SRR1283399     2  0.0290      0.955 0.000 0.992 0.000 0.000 NA
#&gt; SRR1283400     2  0.0290      0.955 0.000 0.992 0.000 0.000 NA
#&gt; SRR1283401     2  0.0290      0.955 0.000 0.992 0.000 0.000 NA
#&gt; SRR1283402     2  0.0000      0.956 0.000 1.000 0.000 0.000 NA
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR1283406     1  0.0404      0.989 0.988 0.000 0.000 0.000 NA
#&gt; SRR1283407     1  0.0404      0.989 0.988 0.000 0.000 0.000 NA
#&gt; SRR1283408     1  0.0404      0.989 0.988 0.000 0.000 0.000 NA
#&gt; SRR1283409     1  0.0566      0.987 0.984 0.000 0.000 0.004 NA
#&gt; SRR1283410     1  0.0566      0.987 0.984 0.000 0.000 0.004 NA
#&gt; SRR1283411     1  0.0566      0.987 0.984 0.000 0.000 0.004 NA
#&gt; SRR1283412     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283413     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283414     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283415     1  0.0703      0.980 0.976 0.000 0.000 0.000 NA
#&gt; SRR1283416     1  0.0703      0.980 0.976 0.000 0.000 0.000 NA
#&gt; SRR1283417     1  0.0703      0.980 0.976 0.000 0.000 0.000 NA
#&gt; SRR1283418     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0162      0.991 0.996 0.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0290      0.990 0.992 0.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0290      0.990 0.992 0.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0290      0.990 0.992 0.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283425     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283426     1  0.0000      0.992 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283427     1  0.0162      0.991 0.996 0.000 0.000 0.004 NA
#&gt; SRR1283428     1  0.0324      0.991 0.992 0.000 0.000 0.004 NA
#&gt; SRR1283429     1  0.0162      0.991 0.996 0.000 0.000 0.004 NA
#&gt; SRR1283430     2  0.1341      0.951 0.000 0.944 0.000 0.000 NA
#&gt; SRR1283431     2  0.1410      0.950 0.000 0.940 0.000 0.000 NA
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5 p6
#&gt; SRR1283379     3  0.1141      1.000 0.000 0.000 0.948 0.052 NA NA
#&gt; SRR1283380     3  0.1141      1.000 0.000 0.000 0.948 0.052 NA NA
#&gt; SRR1283381     3  0.1141      1.000 0.000 0.000 0.948 0.052 NA NA
#&gt; SRR1283385     2  0.1285      0.932 0.000 0.944 0.000 0.000 NA NA
#&gt; SRR1283386     2  0.1349      0.934 0.000 0.940 0.000 0.000 NA NA
#&gt; SRR1283387     2  0.1398      0.931 0.000 0.940 0.000 0.000 NA NA
#&gt; SRR1283388     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283389     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283390     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283382     2  0.2100      0.930 0.000 0.884 0.000 0.000 NA NA
#&gt; SRR1283383     2  0.2100      0.930 0.000 0.884 0.000 0.000 NA NA
#&gt; SRR1283384     2  0.2006      0.932 0.000 0.892 0.000 0.000 NA NA
#&gt; SRR1283391     2  0.2402      0.917 0.000 0.856 0.000 0.000 NA NA
#&gt; SRR1283392     2  0.2402      0.917 0.000 0.856 0.000 0.000 NA NA
#&gt; SRR1283393     2  0.1957      0.932 0.000 0.888 0.000 0.000 NA NA
#&gt; SRR1283394     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283395     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283396     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283397     2  0.1501      0.939 0.000 0.924 0.000 0.000 NA NA
#&gt; SRR1283398     2  0.1556      0.939 0.000 0.920 0.000 0.000 NA NA
#&gt; SRR1283399     2  0.1501      0.939 0.000 0.924 0.000 0.000 NA NA
#&gt; SRR1283400     2  0.1610      0.940 0.000 0.916 0.000 0.000 NA NA
#&gt; SRR1283401     2  0.1501      0.939 0.000 0.924 0.000 0.000 NA NA
#&gt; SRR1283402     2  0.1387      0.941 0.000 0.932 0.000 0.000 NA NA
#&gt; SRR1283403     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA NA
#&gt; SRR1283404     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA NA
#&gt; SRR1283405     4  0.0000      1.000 0.000 0.000 0.000 1.000 NA NA
#&gt; SRR1283406     1  0.1863      0.921 0.920 0.000 0.000 0.000 NA NA
#&gt; SRR1283407     1  0.1720      0.927 0.928 0.000 0.000 0.000 NA NA
#&gt; SRR1283408     1  0.1863      0.921 0.920 0.000 0.000 0.000 NA NA
#&gt; SRR1283409     1  0.0935      0.948 0.964 0.000 0.000 0.004 NA NA
#&gt; SRR1283410     1  0.0865      0.948 0.964 0.000 0.000 0.000 NA NA
#&gt; SRR1283411     1  0.0937      0.946 0.960 0.000 0.000 0.000 NA NA
#&gt; SRR1283412     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283413     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283414     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283415     1  0.2933      0.813 0.796 0.000 0.000 0.000 NA NA
#&gt; SRR1283416     1  0.2964      0.809 0.792 0.000 0.000 0.000 NA NA
#&gt; SRR1283417     1  0.3023      0.800 0.784 0.000 0.000 0.000 NA NA
#&gt; SRR1283418     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283419     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283420     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283421     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283422     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283423     1  0.0000      0.958 1.000 0.000 0.000 0.000 NA NA
#&gt; SRR1283424     1  0.0405      0.956 0.988 0.000 0.000 0.000 NA NA
#&gt; SRR1283425     1  0.0405      0.956 0.988 0.000 0.000 0.000 NA NA
#&gt; SRR1283426     1  0.0260      0.957 0.992 0.000 0.000 0.000 NA NA
#&gt; SRR1283427     1  0.0692      0.953 0.976 0.000 0.000 0.000 NA NA
#&gt; SRR1283428     1  0.0692      0.953 0.976 0.000 0.000 0.000 NA NA
#&gt; SRR1283429     1  0.0692      0.953 0.976 0.000 0.000 0.000 NA NA
#&gt; SRR1283430     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
#&gt; SRR1283431     2  0.0777      0.937 0.000 0.972 0.000 0.000 NA NA
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2054 0.795   0.795
#> 3 3 1.000           1.000       1.000         1.9479 0.599   0.496
#> 4 4 1.000           0.984       0.984         0.0216 0.993   0.983
#> 5 5 0.826           0.900       0.873         0.1261 0.922   0.798
#> 6 6 0.848           0.983       0.966         0.1099 0.904   0.691
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     2       0          1  0  1
#&gt; SRR1283407     2       0          1  0  1
#&gt; SRR1283408     2       0          1  0  1
#&gt; SRR1283409     2       0          1  0  1
#&gt; SRR1283410     2       0          1  0  1
#&gt; SRR1283411     2       0          1  0  1
#&gt; SRR1283412     2       0          1  0  1
#&gt; SRR1283413     2       0          1  0  1
#&gt; SRR1283414     2       0          1  0  1
#&gt; SRR1283415     2       0          1  0  1
#&gt; SRR1283416     2       0          1  0  1
#&gt; SRR1283417     2       0          1  0  1
#&gt; SRR1283418     2       0          1  0  1
#&gt; SRR1283419     2       0          1  0  1
#&gt; SRR1283420     2       0          1  0  1
#&gt; SRR1283421     2       0          1  0  1
#&gt; SRR1283422     2       0          1  0  1
#&gt; SRR1283423     2       0          1  0  1
#&gt; SRR1283424     2       0          1  0  1
#&gt; SRR1283425     2       0          1  0  1
#&gt; SRR1283426     2       0          1  0  1
#&gt; SRR1283427     2       0          1  0  1
#&gt; SRR1283428     2       0          1  0  1
#&gt; SRR1283429     2       0          1  0  1
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3    p4
#&gt; SRR1283379     3   0.222      1.000 0.000  0 0.908 0.092
#&gt; SRR1283380     3   0.222      1.000 0.000  0 0.908 0.092
#&gt; SRR1283381     3   0.222      1.000 0.000  0 0.908 0.092
#&gt; SRR1283385     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283386     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283387     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283388     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283389     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283390     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283394     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283395     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283396     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000  0 0.000 1.000
#&gt; SRR1283404     4   0.000      1.000 0.000  0 0.000 1.000
#&gt; SRR1283405     4   0.000      1.000 0.000  0 0.000 1.000
#&gt; SRR1283406     1   0.222      0.928 0.908  0 0.092 0.000
#&gt; SRR1283407     1   0.222      0.928 0.908  0 0.092 0.000
#&gt; SRR1283408     1   0.222      0.928 0.908  0 0.092 0.000
#&gt; SRR1283409     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283410     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283411     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283412     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283413     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283414     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283415     1   0.222      0.928 0.908  0 0.092 0.000
#&gt; SRR1283416     1   0.222      0.928 0.908  0 0.092 0.000
#&gt; SRR1283417     1   0.222      0.928 0.908  0 0.092 0.000
#&gt; SRR1283418     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283419     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283420     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283421     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283422     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283423     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283424     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283425     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283426     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283427     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283428     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283429     1   0.000      0.977 1.000  0 0.000 0.000
#&gt; SRR1283430     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; SRR1283431     2   0.000      1.000 0.000  1 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1283379     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283385     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283386     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283387     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283388     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283389     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283390     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283382     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283383     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283384     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283391     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283392     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283393     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283394     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283395     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283396     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283397     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283398     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283399     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283400     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283401     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283402     2   0.000      0.785 0.000 1.000  0 0.000 0.000
#&gt; SRR1283403     4   0.416      1.000 0.392 0.000  0 0.608 0.000
#&gt; SRR1283404     4   0.416      1.000 0.392 0.000  0 0.608 0.000
#&gt; SRR1283405     4   0.416      1.000 0.392 0.000  0 0.608 0.000
#&gt; SRR1283406     5   0.051      0.984 0.016 0.000  0 0.000 0.984
#&gt; SRR1283407     5   0.051      0.984 0.016 0.000  0 0.000 0.984
#&gt; SRR1283408     5   0.051      0.984 0.016 0.000  0 0.000 0.984
#&gt; SRR1283409     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283410     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283411     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283412     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283413     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283414     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283415     5   0.000      0.984 0.000 0.000  0 0.000 1.000
#&gt; SRR1283416     5   0.000      0.984 0.000 0.000  0 0.000 1.000
#&gt; SRR1283417     5   0.000      0.984 0.000 0.000  0 0.000 1.000
#&gt; SRR1283418     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283419     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283420     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283421     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283422     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283423     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283424     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283425     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283426     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283427     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283428     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283429     1   0.416      1.000 0.608 0.000  0 0.000 0.392
#&gt; SRR1283430     2   0.416      0.761 0.000 0.608  0 0.392 0.000
#&gt; SRR1283431     2   0.416      0.761 0.000 0.608  0 0.392 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5    p6
#&gt; SRR1283379     3   0.000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283380     3   0.000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283381     3   0.000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1283385     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283386     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283387     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283388     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283389     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283390     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283382     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283383     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283384     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283391     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283392     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283393     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283394     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283395     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283396     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283397     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283398     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283399     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283400     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283401     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283402     2   0.000      1.000 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1283403     4   0.000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283404     4   0.000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283405     4   0.000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1283406     6   0.375      0.850 0.112 0.000  0  0 0.104 0.784
#&gt; SRR1283407     6   0.375      0.850 0.112 0.000  0  0 0.104 0.784
#&gt; SRR1283408     6   0.375      0.850 0.112 0.000  0  0 0.104 0.784
#&gt; SRR1283409     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283410     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283411     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283412     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283413     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283414     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283415     6   0.000      0.848 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283416     6   0.000      0.848 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283417     6   0.000      0.848 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1283418     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283419     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283420     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283421     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283422     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283423     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283424     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283425     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283426     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283427     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283428     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283429     1   0.000      1.000 1.000 0.000  0  0 0.000 0.000
#&gt; SRR1283430     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
#&gt; SRR1283431     5   0.186      1.000 0.000 0.104  0  0 0.896 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.495           0.920       0.859         0.4091 0.499   0.499
#> 3 3 0.804           0.947       0.908         0.4516 0.896   0.791
#> 4 4 0.674           0.903       0.830         0.1326 0.904   0.757
#> 5 5 0.748           0.832       0.810         0.0803 1.000   1.000
#> 6 6 0.691           0.763       0.788         0.0573 0.915   0.716
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     1   0.000      0.670 1.000 0.000
#&gt; SRR1283380     1   0.000      0.670 1.000 0.000
#&gt; SRR1283381     1   0.000      0.670 1.000 0.000
#&gt; SRR1283385     2   0.000      1.000 0.000 1.000
#&gt; SRR1283386     2   0.000      1.000 0.000 1.000
#&gt; SRR1283387     2   0.000      1.000 0.000 1.000
#&gt; SRR1283388     2   0.000      1.000 0.000 1.000
#&gt; SRR1283389     2   0.000      1.000 0.000 1.000
#&gt; SRR1283390     2   0.000      1.000 0.000 1.000
#&gt; SRR1283382     2   0.000      1.000 0.000 1.000
#&gt; SRR1283383     2   0.000      1.000 0.000 1.000
#&gt; SRR1283384     2   0.000      1.000 0.000 1.000
#&gt; SRR1283391     2   0.000      1.000 0.000 1.000
#&gt; SRR1283392     2   0.000      1.000 0.000 1.000
#&gt; SRR1283393     2   0.000      1.000 0.000 1.000
#&gt; SRR1283394     2   0.000      1.000 0.000 1.000
#&gt; SRR1283395     2   0.000      1.000 0.000 1.000
#&gt; SRR1283396     2   0.000      1.000 0.000 1.000
#&gt; SRR1283397     2   0.000      1.000 0.000 1.000
#&gt; SRR1283398     2   0.000      1.000 0.000 1.000
#&gt; SRR1283399     2   0.000      1.000 0.000 1.000
#&gt; SRR1283400     2   0.000      1.000 0.000 1.000
#&gt; SRR1283401     2   0.000      1.000 0.000 1.000
#&gt; SRR1283402     2   0.000      1.000 0.000 1.000
#&gt; SRR1283403     1   0.000      0.670 1.000 0.000
#&gt; SRR1283404     1   0.000      0.670 1.000 0.000
#&gt; SRR1283405     1   0.000      0.670 1.000 0.000
#&gt; SRR1283406     1   0.895      0.906 0.688 0.312
#&gt; SRR1283407     1   0.895      0.906 0.688 0.312
#&gt; SRR1283408     1   0.895      0.906 0.688 0.312
#&gt; SRR1283409     1   0.895      0.906 0.688 0.312
#&gt; SRR1283410     1   0.895      0.906 0.688 0.312
#&gt; SRR1283411     1   0.895      0.906 0.688 0.312
#&gt; SRR1283412     1   0.895      0.906 0.688 0.312
#&gt; SRR1283413     1   0.895      0.906 0.688 0.312
#&gt; SRR1283414     1   0.895      0.906 0.688 0.312
#&gt; SRR1283415     1   0.895      0.906 0.688 0.312
#&gt; SRR1283416     1   0.895      0.906 0.688 0.312
#&gt; SRR1283417     1   0.895      0.906 0.688 0.312
#&gt; SRR1283418     1   0.895      0.906 0.688 0.312
#&gt; SRR1283419     1   0.895      0.906 0.688 0.312
#&gt; SRR1283420     1   0.895      0.906 0.688 0.312
#&gt; SRR1283421     1   0.895      0.906 0.688 0.312
#&gt; SRR1283422     1   0.895      0.906 0.688 0.312
#&gt; SRR1283423     1   0.895      0.906 0.688 0.312
#&gt; SRR1283424     1   0.895      0.906 0.688 0.312
#&gt; SRR1283425     1   0.895      0.906 0.688 0.312
#&gt; SRR1283426     1   0.895      0.906 0.688 0.312
#&gt; SRR1283427     1   0.895      0.906 0.688 0.312
#&gt; SRR1283428     1   0.895      0.906 0.688 0.312
#&gt; SRR1283429     1   0.895      0.906 0.688 0.312
#&gt; SRR1283430     2   0.000      1.000 0.000 1.000
#&gt; SRR1283431     2   0.000      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1283379     3   0.614      0.991 0.256 0.024 0.720
#&gt; SRR1283380     3   0.614      0.991 0.256 0.024 0.720
#&gt; SRR1283381     3   0.614      0.991 0.256 0.024 0.720
#&gt; SRR1283385     2   0.614      0.868 0.024 0.720 0.256
#&gt; SRR1283386     2   0.614      0.868 0.024 0.720 0.256
#&gt; SRR1283387     2   0.614      0.868 0.024 0.720 0.256
#&gt; SRR1283388     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283389     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283390     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283382     2   0.206      0.879 0.024 0.952 0.024
#&gt; SRR1283383     2   0.206      0.879 0.024 0.952 0.024
#&gt; SRR1283384     2   0.206      0.879 0.024 0.952 0.024
#&gt; SRR1283391     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283392     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283393     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283394     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283395     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283396     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283397     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283398     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283399     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283400     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283401     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283402     2   0.103      0.886 0.024 0.976 0.000
#&gt; SRR1283403     3   0.518      0.991 0.256 0.000 0.744
#&gt; SRR1283404     3   0.518      0.991 0.256 0.000 0.744
#&gt; SRR1283405     3   0.518      0.991 0.256 0.000 0.744
#&gt; SRR1283406     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283407     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283408     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283409     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283410     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283411     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283412     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283413     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283414     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283415     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283416     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283417     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283418     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283419     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283420     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283421     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283422     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283423     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283424     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283425     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283426     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283427     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283428     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283429     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1283430     2   0.590      0.875 0.024 0.744 0.232
#&gt; SRR1283431     2   0.590      0.875 0.024 0.744 0.232
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.3266      0.980 0.168 0.000 0.832 0.000
#&gt; SRR1283380     3  0.3266      0.980 0.168 0.000 0.832 0.000
#&gt; SRR1283381     3  0.3266      0.980 0.168 0.000 0.832 0.000
#&gt; SRR1283385     4  0.2319      0.886 0.000 0.040 0.036 0.924
#&gt; SRR1283386     4  0.2319      0.886 0.000 0.040 0.036 0.924
#&gt; SRR1283387     4  0.2319      0.886 0.000 0.040 0.036 0.924
#&gt; SRR1283388     4  0.1302      0.936 0.000 0.000 0.044 0.956
#&gt; SRR1283389     4  0.1302      0.936 0.000 0.000 0.044 0.956
#&gt; SRR1283390     4  0.1302      0.936 0.000 0.000 0.044 0.956
#&gt; SRR1283382     2  0.6407      0.854 0.000 0.520 0.068 0.412
#&gt; SRR1283383     2  0.6407      0.854 0.000 0.520 0.068 0.412
#&gt; SRR1283384     2  0.6407      0.854 0.000 0.520 0.068 0.412
#&gt; SRR1283391     2  0.5925      0.931 0.000 0.512 0.036 0.452
#&gt; SRR1283392     2  0.5925      0.931 0.000 0.512 0.036 0.452
#&gt; SRR1283393     2  0.5925      0.931 0.000 0.512 0.036 0.452
#&gt; SRR1283394     4  0.0000      0.934 0.000 0.000 0.000 1.000
#&gt; SRR1283395     4  0.0000      0.934 0.000 0.000 0.000 1.000
#&gt; SRR1283396     4  0.0000      0.934 0.000 0.000 0.000 1.000
#&gt; SRR1283397     2  0.4967      0.938 0.000 0.548 0.000 0.452
#&gt; SRR1283398     2  0.4967      0.938 0.000 0.548 0.000 0.452
#&gt; SRR1283399     2  0.4967      0.938 0.000 0.548 0.000 0.452
#&gt; SRR1283400     2  0.5488      0.939 0.000 0.532 0.016 0.452
#&gt; SRR1283401     2  0.5488      0.939 0.000 0.532 0.016 0.452
#&gt; SRR1283402     2  0.5488      0.939 0.000 0.532 0.016 0.452
#&gt; SRR1283403     3  0.4746      0.980 0.168 0.056 0.776 0.000
#&gt; SRR1283404     3  0.4746      0.980 0.168 0.056 0.776 0.000
#&gt; SRR1283405     3  0.4746      0.980 0.168 0.056 0.776 0.000
#&gt; SRR1283406     1  0.4454      0.705 0.692 0.308 0.000 0.000
#&gt; SRR1283407     1  0.4454      0.705 0.692 0.308 0.000 0.000
#&gt; SRR1283408     1  0.4454      0.705 0.692 0.308 0.000 0.000
#&gt; SRR1283409     1  0.3074      0.840 0.848 0.152 0.000 0.000
#&gt; SRR1283410     1  0.3074      0.840 0.848 0.152 0.000 0.000
#&gt; SRR1283411     1  0.3074      0.840 0.848 0.152 0.000 0.000
#&gt; SRR1283412     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283413     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283414     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283415     1  0.3123      0.841 0.844 0.156 0.000 0.000
#&gt; SRR1283416     1  0.3123      0.841 0.844 0.156 0.000 0.000
#&gt; SRR1283417     1  0.3123      0.841 0.844 0.156 0.000 0.000
#&gt; SRR1283418     1  0.0188      0.912 0.996 0.004 0.000 0.000
#&gt; SRR1283419     1  0.0188      0.912 0.996 0.004 0.000 0.000
#&gt; SRR1283420     1  0.0188      0.912 0.996 0.004 0.000 0.000
#&gt; SRR1283421     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283422     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283423     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283424     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283425     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283426     1  0.0336      0.912 0.992 0.008 0.000 0.000
#&gt; SRR1283427     1  0.0469      0.911 0.988 0.012 0.000 0.000
#&gt; SRR1283428     1  0.0469      0.911 0.988 0.012 0.000 0.000
#&gt; SRR1283429     1  0.0469      0.911 0.988 0.012 0.000 0.000
#&gt; SRR1283430     4  0.1302      0.936 0.000 0.000 0.044 0.956
#&gt; SRR1283431     4  0.1302      0.936 0.000 0.000 0.044 0.956
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1283379     3  0.1628      0.968 0.056 0.000 0.936 0.000 NA
#&gt; SRR1283380     3  0.1628      0.968 0.056 0.000 0.936 0.000 NA
#&gt; SRR1283381     3  0.1628      0.967 0.056 0.008 0.936 0.000 NA
#&gt; SRR1283385     4  0.3207      0.829 0.000 0.040 0.012 0.864 NA
#&gt; SRR1283386     4  0.3207      0.829 0.000 0.040 0.012 0.864 NA
#&gt; SRR1283387     4  0.3207      0.829 0.000 0.040 0.012 0.864 NA
#&gt; SRR1283388     4  0.2079      0.900 0.000 0.000 0.020 0.916 NA
#&gt; SRR1283389     4  0.2079      0.900 0.000 0.000 0.020 0.916 NA
#&gt; SRR1283390     4  0.2079      0.900 0.000 0.000 0.020 0.916 NA
#&gt; SRR1283382     2  0.6148      0.796 0.000 0.536 0.000 0.304 NA
#&gt; SRR1283383     2  0.6148      0.796 0.000 0.536 0.000 0.304 NA
#&gt; SRR1283384     2  0.6148      0.796 0.000 0.536 0.000 0.304 NA
#&gt; SRR1283391     2  0.5483      0.889 0.000 0.596 0.020 0.344 NA
#&gt; SRR1283392     2  0.5483      0.889 0.000 0.596 0.020 0.344 NA
#&gt; SRR1283393     2  0.5483      0.889 0.000 0.596 0.020 0.344 NA
#&gt; SRR1283394     4  0.0162      0.898 0.000 0.000 0.004 0.996 NA
#&gt; SRR1283395     4  0.0162      0.898 0.000 0.000 0.004 0.996 NA
#&gt; SRR1283396     4  0.0162      0.898 0.000 0.000 0.004 0.996 NA
#&gt; SRR1283397     2  0.4555      0.909 0.000 0.636 0.000 0.344 NA
#&gt; SRR1283398     2  0.4555      0.909 0.000 0.636 0.000 0.344 NA
#&gt; SRR1283399     2  0.4555      0.909 0.000 0.636 0.000 0.344 NA
#&gt; SRR1283400     2  0.3999      0.910 0.000 0.656 0.000 0.344 NA
#&gt; SRR1283401     2  0.3999      0.910 0.000 0.656 0.000 0.344 NA
#&gt; SRR1283402     2  0.3999      0.910 0.000 0.656 0.000 0.344 NA
#&gt; SRR1283403     3  0.3365      0.968 0.056 0.052 0.864 0.000 NA
#&gt; SRR1283404     3  0.3347      0.968 0.056 0.056 0.864 0.000 NA
#&gt; SRR1283405     3  0.3347      0.968 0.056 0.056 0.864 0.000 NA
#&gt; SRR1283406     1  0.6463      0.534 0.496 0.228 0.000 0.000 NA
#&gt; SRR1283407     1  0.6463      0.534 0.496 0.228 0.000 0.000 NA
#&gt; SRR1283408     1  0.6463      0.534 0.496 0.228 0.000 0.000 NA
#&gt; SRR1283409     1  0.5216      0.707 0.660 0.092 0.000 0.000 NA
#&gt; SRR1283410     1  0.5216      0.707 0.660 0.092 0.000 0.000 NA
#&gt; SRR1283411     1  0.5216      0.707 0.660 0.092 0.000 0.000 NA
#&gt; SRR1283412     1  0.1410      0.823 0.940 0.000 0.000 0.000 NA
#&gt; SRR1283413     1  0.1410      0.823 0.940 0.000 0.000 0.000 NA
#&gt; SRR1283414     1  0.1410      0.823 0.940 0.000 0.000 0.000 NA
#&gt; SRR1283415     1  0.4101      0.656 0.628 0.000 0.000 0.000 NA
#&gt; SRR1283416     1  0.4101      0.656 0.628 0.000 0.000 0.000 NA
#&gt; SRR1283417     1  0.4101      0.656 0.628 0.000 0.000 0.000 NA
#&gt; SRR1283418     1  0.0000      0.832 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283419     1  0.0000      0.832 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283420     1  0.0000      0.832 1.000 0.000 0.000 0.000 NA
#&gt; SRR1283421     1  0.0794      0.829 0.972 0.000 0.000 0.000 NA
#&gt; SRR1283422     1  0.0794      0.829 0.972 0.000 0.000 0.000 NA
#&gt; SRR1283423     1  0.0794      0.829 0.972 0.000 0.000 0.000 NA
#&gt; SRR1283424     1  0.1282      0.832 0.952 0.004 0.000 0.000 NA
#&gt; SRR1283425     1  0.1282      0.832 0.952 0.004 0.000 0.000 NA
#&gt; SRR1283426     1  0.1282      0.832 0.952 0.004 0.000 0.000 NA
#&gt; SRR1283427     1  0.1952      0.824 0.912 0.004 0.000 0.000 NA
#&gt; SRR1283428     1  0.1952      0.824 0.912 0.004 0.000 0.000 NA
#&gt; SRR1283429     1  0.1952      0.824 0.912 0.004 0.000 0.000 NA
#&gt; SRR1283430     4  0.2079      0.900 0.000 0.000 0.020 0.916 NA
#&gt; SRR1283431     4  0.2079      0.900 0.000 0.000 0.020 0.916 NA
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1283379     3  0.3789      0.940 0.044 0.000 0.832 0.044 0.024 0.056
#&gt; SRR1283380     3  0.3805      0.940 0.044 0.000 0.832 0.044 0.028 0.052
#&gt; SRR1283381     3  0.3789      0.940 0.044 0.000 0.832 0.044 0.024 0.056
#&gt; SRR1283385     4  0.6057      0.766 0.000 0.176 0.000 0.604 0.144 0.076
#&gt; SRR1283386     4  0.6057      0.766 0.000 0.176 0.000 0.604 0.144 0.076
#&gt; SRR1283387     4  0.6171      0.767 0.000 0.176 0.004 0.604 0.136 0.080
#&gt; SRR1283388     4  0.4701      0.880 0.000 0.196 0.000 0.712 0.056 0.036
#&gt; SRR1283389     4  0.4701      0.880 0.000 0.196 0.000 0.712 0.056 0.036
#&gt; SRR1283390     4  0.4701      0.880 0.000 0.196 0.000 0.712 0.056 0.036
#&gt; SRR1283382     2  0.4327      0.761 0.000 0.700 0.000 0.020 0.028 0.252
#&gt; SRR1283383     2  0.4327      0.761 0.000 0.700 0.000 0.020 0.028 0.252
#&gt; SRR1283384     2  0.4327      0.761 0.000 0.700 0.000 0.020 0.028 0.252
#&gt; SRR1283391     2  0.2486      0.858 0.000 0.896 0.024 0.000 0.040 0.040
#&gt; SRR1283392     2  0.2486      0.858 0.000 0.896 0.024 0.000 0.040 0.040
#&gt; SRR1283393     2  0.2486      0.858 0.000 0.896 0.024 0.000 0.040 0.040
#&gt; SRR1283394     4  0.3200      0.877 0.000 0.196 0.000 0.788 0.000 0.016
#&gt; SRR1283395     4  0.3200      0.877 0.000 0.196 0.000 0.788 0.000 0.016
#&gt; SRR1283396     4  0.3200      0.877 0.000 0.196 0.000 0.788 0.000 0.016
#&gt; SRR1283397     2  0.0972      0.883 0.000 0.964 0.000 0.000 0.008 0.028
#&gt; SRR1283398     2  0.0972      0.883 0.000 0.964 0.000 0.000 0.008 0.028
#&gt; SRR1283399     2  0.0972      0.883 0.000 0.964 0.000 0.000 0.008 0.028
#&gt; SRR1283400     2  0.0914      0.881 0.000 0.968 0.016 0.000 0.016 0.000
#&gt; SRR1283401     2  0.0914      0.881 0.000 0.968 0.016 0.000 0.016 0.000
#&gt; SRR1283402     2  0.0914      0.881 0.000 0.968 0.016 0.000 0.016 0.000
#&gt; SRR1283403     3  0.1152      0.940 0.044 0.000 0.952 0.004 0.000 0.000
#&gt; SRR1283404     3  0.1152      0.940 0.044 0.000 0.952 0.000 0.000 0.004
#&gt; SRR1283405     3  0.1152      0.940 0.044 0.000 0.952 0.000 0.000 0.004
#&gt; SRR1283406     5  0.6720      1.000 0.316 0.000 0.000 0.096 0.464 0.124
#&gt; SRR1283407     5  0.6720      1.000 0.316 0.000 0.000 0.096 0.464 0.124
#&gt; SRR1283408     5  0.6720      1.000 0.316 0.000 0.000 0.096 0.464 0.124
#&gt; SRR1283409     1  0.4407     -0.139 0.496 0.000 0.000 0.000 0.480 0.024
#&gt; SRR1283410     1  0.4407     -0.139 0.496 0.000 0.000 0.000 0.480 0.024
#&gt; SRR1283411     1  0.4407     -0.139 0.496 0.000 0.000 0.000 0.480 0.024
#&gt; SRR1283412     1  0.1536      0.685 0.940 0.000 0.000 0.016 0.040 0.004
#&gt; SRR1283413     1  0.1536      0.685 0.940 0.000 0.000 0.016 0.040 0.004
#&gt; SRR1283414     1  0.1536      0.685 0.940 0.000 0.000 0.016 0.040 0.004
#&gt; SRR1283415     6  0.4852      0.994 0.452 0.000 0.000 0.000 0.056 0.492
#&gt; SRR1283416     6  0.4981      0.993 0.452 0.000 0.000 0.004 0.056 0.488
#&gt; SRR1283417     6  0.5080      0.991 0.452 0.000 0.000 0.008 0.056 0.484
#&gt; SRR1283418     1  0.0603      0.691 0.980 0.000 0.000 0.004 0.000 0.016
#&gt; SRR1283419     1  0.0603      0.691 0.980 0.000 0.000 0.004 0.000 0.016
#&gt; SRR1283420     1  0.0603      0.691 0.980 0.000 0.000 0.004 0.000 0.016
#&gt; SRR1283421     1  0.1053      0.697 0.964 0.000 0.000 0.012 0.020 0.004
#&gt; SRR1283422     1  0.1053      0.697 0.964 0.000 0.000 0.012 0.020 0.004
#&gt; SRR1283423     1  0.1053      0.697 0.964 0.000 0.000 0.012 0.020 0.004
#&gt; SRR1283424     1  0.2112      0.641 0.896 0.000 0.000 0.000 0.016 0.088
#&gt; SRR1283425     1  0.2112      0.641 0.896 0.000 0.000 0.000 0.016 0.088
#&gt; SRR1283426     1  0.2112      0.641 0.896 0.000 0.000 0.000 0.016 0.088
#&gt; SRR1283427     1  0.2821      0.548 0.832 0.000 0.000 0.000 0.016 0.152
#&gt; SRR1283428     1  0.2821      0.548 0.832 0.000 0.000 0.000 0.016 0.152
#&gt; SRR1283429     1  0.2821      0.548 0.832 0.000 0.000 0.000 0.016 0.152
#&gt; SRR1283430     4  0.4709      0.880 0.000 0.196 0.000 0.712 0.052 0.040
#&gt; SRR1283431     4  0.4709      0.880 0.000 0.196 0.000 0.712 0.052 0.040
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 0.956           0.961       0.968         0.1157 0.922   0.801
#> 5 5 0.856           0.905       0.925         0.0586 0.967   0.897
#> 6 6 0.856           0.956       0.884         0.0819 0.904   0.662
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283385     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283386     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283387     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283388     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283389     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283390     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283382     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283383     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283384     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283391     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283392     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283393     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283394     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283395     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283396     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283397     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283398     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283399     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283400     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283401     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283402     2  0.0000      0.980 0.000 1.000  0 0.000
#&gt; SRR1283403     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283404     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283405     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283406     4  0.1557      0.757 0.056 0.000  0 0.944
#&gt; SRR1283407     4  0.1557      0.757 0.056 0.000  0 0.944
#&gt; SRR1283408     4  0.1557      0.757 0.056 0.000  0 0.944
#&gt; SRR1283409     4  0.4564      0.758 0.328 0.000  0 0.672
#&gt; SRR1283410     4  0.4564      0.758 0.328 0.000  0 0.672
#&gt; SRR1283411     4  0.4564      0.758 0.328 0.000  0 0.672
#&gt; SRR1283412     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283413     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283414     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283415     1  0.0817      0.975 0.976 0.000  0 0.024
#&gt; SRR1283416     1  0.0817      0.975 0.976 0.000  0 0.024
#&gt; SRR1283417     1  0.0817      0.975 0.976 0.000  0 0.024
#&gt; SRR1283418     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283419     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283420     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283421     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283422     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283423     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283424     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283425     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283426     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283427     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283428     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283429     1  0.0000      0.995 1.000 0.000  0 0.000
#&gt; SRR1283430     2  0.1302      0.978 0.000 0.956  0 0.044
#&gt; SRR1283431     2  0.1302      0.978 0.000 0.956  0 0.044
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283385     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283386     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283387     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283388     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283389     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283390     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283382     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283383     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283384     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283391     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283392     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283393     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283394     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283395     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283396     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283397     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283398     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283399     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283400     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283401     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283402     2  0.2891      0.912 0.000 0.824  0 0.000 0.176
#&gt; SRR1283403     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283404     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283405     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1283406     4  0.0000      0.539 0.000 0.000  0 1.000 0.000
#&gt; SRR1283407     4  0.0000      0.539 0.000 0.000  0 1.000 0.000
#&gt; SRR1283408     4  0.0000      0.539 0.000 0.000  0 1.000 0.000
#&gt; SRR1283409     4  0.4882      0.509 0.444 0.000  0 0.532 0.024
#&gt; SRR1283410     4  0.4882      0.509 0.444 0.000  0 0.532 0.024
#&gt; SRR1283411     4  0.4882      0.509 0.444 0.000  0 0.532 0.024
#&gt; SRR1283412     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283413     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283414     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283415     5  0.3074      1.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1283416     5  0.3074      1.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1283417     5  0.3074      1.000 0.196 0.000  0 0.000 0.804
#&gt; SRR1283418     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.997 1.000 0.000  0 0.000 0.000
#&gt; SRR1283424     1  0.0162      0.995 0.996 0.000  0 0.000 0.004
#&gt; SRR1283425     1  0.0162      0.995 0.996 0.000  0 0.000 0.004
#&gt; SRR1283426     1  0.0162      0.995 0.996 0.000  0 0.000 0.004
#&gt; SRR1283427     1  0.0290      0.993 0.992 0.000  0 0.000 0.008
#&gt; SRR1283428     1  0.0290      0.993 0.992 0.000  0 0.000 0.008
#&gt; SRR1283429     1  0.0290      0.993 0.992 0.000  0 0.000 0.008
#&gt; SRR1283430     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
#&gt; SRR1283431     2  0.0000      0.903 0.000 1.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4   p5    p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1283385     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283386     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283387     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283388     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283389     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283390     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283382     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283383     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283384     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283391     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283392     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283393     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283394     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283395     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283396     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283397     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283398     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283399     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283400     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283401     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283402     2  0.0000      1.000 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1283403     3  0.0000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1283404     3  0.0000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1283405     3  0.0000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1283406     5  0.0000      0.615 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1283407     5  0.0000      0.615 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1283408     5  0.0000      0.615 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1283409     5  0.6045      0.633 0.212 0.000  0 0.364 0.42 0.004
#&gt; SRR1283410     5  0.6045      0.633 0.212 0.000  0 0.364 0.42 0.004
#&gt; SRR1283411     5  0.6045      0.633 0.212 0.000  0 0.364 0.42 0.004
#&gt; SRR1283412     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283413     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283414     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283415     6  0.0146      1.000 0.004 0.000  0 0.000 0.00 0.996
#&gt; SRR1283416     6  0.0146      1.000 0.004 0.000  0 0.000 0.00 0.996
#&gt; SRR1283417     6  0.0146      1.000 0.004 0.000  0 0.000 0.00 0.996
#&gt; SRR1283418     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283419     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283420     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283421     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283422     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283423     1  0.0000      0.995 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1283424     1  0.0363      0.992 0.988 0.000  0 0.012 0.00 0.000
#&gt; SRR1283425     1  0.0363      0.992 0.988 0.000  0 0.012 0.00 0.000
#&gt; SRR1283426     1  0.0363      0.992 0.988 0.000  0 0.012 0.00 0.000
#&gt; SRR1283427     1  0.0363      0.992 0.988 0.000  0 0.012 0.00 0.000
#&gt; SRR1283428     1  0.0363      0.992 0.988 0.000  0 0.012 0.00 0.000
#&gt; SRR1283429     1  0.0363      0.992 0.988 0.000  0 0.012 0.00 0.000
#&gt; SRR1283430     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
#&gt; SRR1283431     4  0.3684      1.000 0.000 0.372  0 0.628 0.00 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5012 0.499   0.499
#> 3 3 1.000           1.000       1.000         0.2083 0.896   0.791
#> 4 4 0.898           0.940       0.929         0.0478 0.993   0.983
#> 5 5 1.000           1.000       1.000         0.1155 0.904   0.753
#> 6 6 1.000           0.988       0.987         0.0686 0.954   0.844
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 5
```

There is also optional best $k$ = 2 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1283379     1       0          1  1  0
#&gt; SRR1283380     1       0          1  1  0
#&gt; SRR1283381     1       0          1  1  0
#&gt; SRR1283385     2       0          1  0  1
#&gt; SRR1283386     2       0          1  0  1
#&gt; SRR1283387     2       0          1  0  1
#&gt; SRR1283388     2       0          1  0  1
#&gt; SRR1283389     2       0          1  0  1
#&gt; SRR1283390     2       0          1  0  1
#&gt; SRR1283382     2       0          1  0  1
#&gt; SRR1283383     2       0          1  0  1
#&gt; SRR1283384     2       0          1  0  1
#&gt; SRR1283391     2       0          1  0  1
#&gt; SRR1283392     2       0          1  0  1
#&gt; SRR1283393     2       0          1  0  1
#&gt; SRR1283394     2       0          1  0  1
#&gt; SRR1283395     2       0          1  0  1
#&gt; SRR1283396     2       0          1  0  1
#&gt; SRR1283397     2       0          1  0  1
#&gt; SRR1283398     2       0          1  0  1
#&gt; SRR1283399     2       0          1  0  1
#&gt; SRR1283400     2       0          1  0  1
#&gt; SRR1283401     2       0          1  0  1
#&gt; SRR1283402     2       0          1  0  1
#&gt; SRR1283403     1       0          1  1  0
#&gt; SRR1283404     1       0          1  1  0
#&gt; SRR1283405     1       0          1  1  0
#&gt; SRR1283406     1       0          1  1  0
#&gt; SRR1283407     1       0          1  1  0
#&gt; SRR1283408     1       0          1  1  0
#&gt; SRR1283409     1       0          1  1  0
#&gt; SRR1283410     1       0          1  1  0
#&gt; SRR1283411     1       0          1  1  0
#&gt; SRR1283412     1       0          1  1  0
#&gt; SRR1283413     1       0          1  1  0
#&gt; SRR1283414     1       0          1  1  0
#&gt; SRR1283415     1       0          1  1  0
#&gt; SRR1283416     1       0          1  1  0
#&gt; SRR1283417     1       0          1  1  0
#&gt; SRR1283418     1       0          1  1  0
#&gt; SRR1283419     1       0          1  1  0
#&gt; SRR1283420     1       0          1  1  0
#&gt; SRR1283421     1       0          1  1  0
#&gt; SRR1283422     1       0          1  1  0
#&gt; SRR1283423     1       0          1  1  0
#&gt; SRR1283424     1       0          1  1  0
#&gt; SRR1283425     1       0          1  1  0
#&gt; SRR1283426     1       0          1  1  0
#&gt; SRR1283427     1       0          1  1  0
#&gt; SRR1283428     1       0          1  1  0
#&gt; SRR1283429     1       0          1  1  0
#&gt; SRR1283430     2       0          1  0  1
#&gt; SRR1283431     2       0          1  0  1
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3    p4
#&gt; SRR1283379     3   0.000      1.000  0 0.000 1.000 0.000
#&gt; SRR1283380     3   0.000      1.000  0 0.000 1.000 0.000
#&gt; SRR1283381     3   0.000      1.000  0 0.000 1.000 0.000
#&gt; SRR1283385     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283386     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283387     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283388     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283389     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283390     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283382     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283383     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283384     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283391     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283392     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283393     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283394     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283395     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283396     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283397     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283398     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283399     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283400     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283401     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283402     2   0.000      0.869  0 1.000 0.000 0.000
#&gt; SRR1283403     4   0.407      1.000  0 0.000 0.252 0.748
#&gt; SRR1283404     4   0.407      1.000  0 0.000 0.252 0.748
#&gt; SRR1283405     4   0.407      1.000  0 0.000 0.252 0.748
#&gt; SRR1283406     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283407     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283408     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283409     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283410     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283411     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283412     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283413     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283414     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283415     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283416     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283417     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283418     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283419     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283420     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283421     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283422     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283423     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283424     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283425     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283426     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283427     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283428     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283429     1   0.000      1.000  1 0.000 0.000 0.000
#&gt; SRR1283430     2   0.407      0.856  0 0.748 0.000 0.252
#&gt; SRR1283431     2   0.407      0.856  0 0.748 0.000 0.252
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5
#&gt; SRR1283379     3       0          1  0  0  1  0  0
#&gt; SRR1283380     3       0          1  0  0  1  0  0
#&gt; SRR1283381     3       0          1  0  0  1  0  0
#&gt; SRR1283385     5       0          1  0  0  0  0  1
#&gt; SRR1283386     5       0          1  0  0  0  0  1
#&gt; SRR1283387     5       0          1  0  0  0  0  1
#&gt; SRR1283388     5       0          1  0  0  0  0  1
#&gt; SRR1283389     5       0          1  0  0  0  0  1
#&gt; SRR1283390     5       0          1  0  0  0  0  1
#&gt; SRR1283382     2       0          1  0  1  0  0  0
#&gt; SRR1283383     2       0          1  0  1  0  0  0
#&gt; SRR1283384     2       0          1  0  1  0  0  0
#&gt; SRR1283391     2       0          1  0  1  0  0  0
#&gt; SRR1283392     2       0          1  0  1  0  0  0
#&gt; SRR1283393     2       0          1  0  1  0  0  0
#&gt; SRR1283394     5       0          1  0  0  0  0  1
#&gt; SRR1283395     5       0          1  0  0  0  0  1
#&gt; SRR1283396     5       0          1  0  0  0  0  1
#&gt; SRR1283397     2       0          1  0  1  0  0  0
#&gt; SRR1283398     2       0          1  0  1  0  0  0
#&gt; SRR1283399     2       0          1  0  1  0  0  0
#&gt; SRR1283400     2       0          1  0  1  0  0  0
#&gt; SRR1283401     2       0          1  0  1  0  0  0
#&gt; SRR1283402     2       0          1  0  1  0  0  0
#&gt; SRR1283403     4       0          1  0  0  0  1  0
#&gt; SRR1283404     4       0          1  0  0  0  1  0
#&gt; SRR1283405     4       0          1  0  0  0  1  0
#&gt; SRR1283406     1       0          1  1  0  0  0  0
#&gt; SRR1283407     1       0          1  1  0  0  0  0
#&gt; SRR1283408     1       0          1  1  0  0  0  0
#&gt; SRR1283409     1       0          1  1  0  0  0  0
#&gt; SRR1283410     1       0          1  1  0  0  0  0
#&gt; SRR1283411     1       0          1  1  0  0  0  0
#&gt; SRR1283412     1       0          1  1  0  0  0  0
#&gt; SRR1283413     1       0          1  1  0  0  0  0
#&gt; SRR1283414     1       0          1  1  0  0  0  0
#&gt; SRR1283415     1       0          1  1  0  0  0  0
#&gt; SRR1283416     1       0          1  1  0  0  0  0
#&gt; SRR1283417     1       0          1  1  0  0  0  0
#&gt; SRR1283418     1       0          1  1  0  0  0  0
#&gt; SRR1283419     1       0          1  1  0  0  0  0
#&gt; SRR1283420     1       0          1  1  0  0  0  0
#&gt; SRR1283421     1       0          1  1  0  0  0  0
#&gt; SRR1283422     1       0          1  1  0  0  0  0
#&gt; SRR1283423     1       0          1  1  0  0  0  0
#&gt; SRR1283424     1       0          1  1  0  0  0  0
#&gt; SRR1283425     1       0          1  1  0  0  0  0
#&gt; SRR1283426     1       0          1  1  0  0  0  0
#&gt; SRR1283427     1       0          1  1  0  0  0  0
#&gt; SRR1283428     1       0          1  1  0  0  0  0
#&gt; SRR1283429     1       0          1  1  0  0  0  0
#&gt; SRR1283430     5       0          1  0  0  0  0  1
#&gt; SRR1283431     5       0          1  0  0  0  0  1
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3 p4    p5 p6
#&gt; SRR1283379     3  0.0000      1.000 0.000  0  1  0 0.000  0
#&gt; SRR1283380     3  0.0000      1.000 0.000  0  1  0 0.000  0
#&gt; SRR1283381     3  0.0000      1.000 0.000  0  1  0 0.000  0
#&gt; SRR1283385     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283386     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283387     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283388     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283389     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283390     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283382     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283383     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283384     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283391     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283392     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283393     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283394     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283395     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283396     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283397     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283398     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283399     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283400     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283401     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283402     2  0.0000      1.000 0.000  1  0  0 0.000  0
#&gt; SRR1283403     4  0.0000      1.000 0.000  0  0  1 0.000  0
#&gt; SRR1283404     4  0.0000      1.000 0.000  0  0  1 0.000  0
#&gt; SRR1283405     4  0.0000      1.000 0.000  0  0  1 0.000  0
#&gt; SRR1283406     5  0.1204      1.000 0.056  0  0  0 0.944  0
#&gt; SRR1283407     5  0.1204      1.000 0.056  0  0  0 0.944  0
#&gt; SRR1283408     5  0.1204      1.000 0.056  0  0  0 0.944  0
#&gt; SRR1283409     1  0.1141      0.966 0.948  0  0  0 0.052  0
#&gt; SRR1283410     1  0.1141      0.966 0.948  0  0  0 0.052  0
#&gt; SRR1283411     1  0.1141      0.966 0.948  0  0  0 0.052  0
#&gt; SRR1283412     1  0.1204      0.965 0.944  0  0  0 0.056  0
#&gt; SRR1283413     1  0.1204      0.965 0.944  0  0  0 0.056  0
#&gt; SRR1283414     1  0.1204      0.965 0.944  0  0  0 0.056  0
#&gt; SRR1283415     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283416     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283417     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283418     1  0.0146      0.974 0.996  0  0  0 0.004  0
#&gt; SRR1283419     1  0.0146      0.974 0.996  0  0  0 0.004  0
#&gt; SRR1283420     1  0.0146      0.974 0.996  0  0  0 0.004  0
#&gt; SRR1283421     1  0.1204      0.965 0.944  0  0  0 0.056  0
#&gt; SRR1283422     1  0.1204      0.965 0.944  0  0  0 0.056  0
#&gt; SRR1283423     1  0.1204      0.965 0.944  0  0  0 0.056  0
#&gt; SRR1283424     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283425     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283426     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283427     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283428     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283429     1  0.0000      0.974 1.000  0  0  0 0.000  0
#&gt; SRR1283430     6  0.0000      1.000 0.000  0  0  0 0.000  1
#&gt; SRR1283431     6  0.0000      1.000 0.000  0  0  0 0.000  1
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.5052 0.495   0.495
#> 3 3 1.000           1.000       1.000         0.1987 0.900   0.798
#> 4 4 0.831           0.911       0.875         0.1383 0.922   0.801
#> 5 5 1.000           0.923       0.971         0.1247 0.913   0.725
#> 6 6 0.880           0.866       0.902         0.0525 0.949   0.784
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1   p2
#&gt; SRR1283379     2   0.000      1.000 0.00 1.00
#&gt; SRR1283380     2   0.000      1.000 0.00 1.00
#&gt; SRR1283381     2   0.000      1.000 0.00 1.00
#&gt; SRR1283385     2   0.000      1.000 0.00 1.00
#&gt; SRR1283386     2   0.000      1.000 0.00 1.00
#&gt; SRR1283387     2   0.000      1.000 0.00 1.00
#&gt; SRR1283388     2   0.000      1.000 0.00 1.00
#&gt; SRR1283389     2   0.000      1.000 0.00 1.00
#&gt; SRR1283390     2   0.000      1.000 0.00 1.00
#&gt; SRR1283382     2   0.000      1.000 0.00 1.00
#&gt; SRR1283383     2   0.000      1.000 0.00 1.00
#&gt; SRR1283384     2   0.000      1.000 0.00 1.00
#&gt; SRR1283391     2   0.000      1.000 0.00 1.00
#&gt; SRR1283392     2   0.000      1.000 0.00 1.00
#&gt; SRR1283393     2   0.000      1.000 0.00 1.00
#&gt; SRR1283394     2   0.000      1.000 0.00 1.00
#&gt; SRR1283395     2   0.000      1.000 0.00 1.00
#&gt; SRR1283396     2   0.000      1.000 0.00 1.00
#&gt; SRR1283397     2   0.000      1.000 0.00 1.00
#&gt; SRR1283398     2   0.000      1.000 0.00 1.00
#&gt; SRR1283399     2   0.000      1.000 0.00 1.00
#&gt; SRR1283400     2   0.000      1.000 0.00 1.00
#&gt; SRR1283401     2   0.000      1.000 0.00 1.00
#&gt; SRR1283402     2   0.000      1.000 0.00 1.00
#&gt; SRR1283403     2   0.000      1.000 0.00 1.00
#&gt; SRR1283404     2   0.000      1.000 0.00 1.00
#&gt; SRR1283405     2   0.000      1.000 0.00 1.00
#&gt; SRR1283406     1   0.000      0.997 1.00 0.00
#&gt; SRR1283407     1   0.000      0.997 1.00 0.00
#&gt; SRR1283408     1   0.000      0.997 1.00 0.00
#&gt; SRR1283409     1   0.141      0.981 0.98 0.02
#&gt; SRR1283410     1   0.141      0.981 0.98 0.02
#&gt; SRR1283411     1   0.141      0.981 0.98 0.02
#&gt; SRR1283412     1   0.000      0.997 1.00 0.00
#&gt; SRR1283413     1   0.000      0.997 1.00 0.00
#&gt; SRR1283414     1   0.000      0.997 1.00 0.00
#&gt; SRR1283415     1   0.000      0.997 1.00 0.00
#&gt; SRR1283416     1   0.000      0.997 1.00 0.00
#&gt; SRR1283417     1   0.000      0.997 1.00 0.00
#&gt; SRR1283418     1   0.000      0.997 1.00 0.00
#&gt; SRR1283419     1   0.000      0.997 1.00 0.00
#&gt; SRR1283420     1   0.000      0.997 1.00 0.00
#&gt; SRR1283421     1   0.000      0.997 1.00 0.00
#&gt; SRR1283422     1   0.000      0.997 1.00 0.00
#&gt; SRR1283423     1   0.000      0.997 1.00 0.00
#&gt; SRR1283424     1   0.000      0.997 1.00 0.00
#&gt; SRR1283425     1   0.000      0.997 1.00 0.00
#&gt; SRR1283426     1   0.000      0.997 1.00 0.00
#&gt; SRR1283427     1   0.000      0.997 1.00 0.00
#&gt; SRR1283428     1   0.000      0.997 1.00 0.00
#&gt; SRR1283429     1   0.000      0.997 1.00 0.00
#&gt; SRR1283430     2   0.000      1.000 0.00 1.00
#&gt; SRR1283431     2   0.000      1.000 0.00 1.00
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283385     2  0.2281      0.797 0.096 0.904  0 0.000
#&gt; SRR1283386     2  0.2281      0.797 0.096 0.904  0 0.000
#&gt; SRR1283387     2  0.2281      0.797 0.096 0.904  0 0.000
#&gt; SRR1283388     2  0.0000      0.817 0.000 1.000  0 0.000
#&gt; SRR1283389     2  0.0000      0.817 0.000 1.000  0 0.000
#&gt; SRR1283390     2  0.0000      0.817 0.000 1.000  0 0.000
#&gt; SRR1283382     2  0.4830      0.807 0.392 0.608  0 0.000
#&gt; SRR1283383     2  0.4830      0.807 0.392 0.608  0 0.000
#&gt; SRR1283384     2  0.4830      0.807 0.392 0.608  0 0.000
#&gt; SRR1283391     2  0.4761      0.814 0.372 0.628  0 0.000
#&gt; SRR1283392     2  0.4776      0.813 0.376 0.624  0 0.000
#&gt; SRR1283393     2  0.4382      0.828 0.296 0.704  0 0.000
#&gt; SRR1283394     2  0.0000      0.817 0.000 1.000  0 0.000
#&gt; SRR1283395     2  0.0000      0.817 0.000 1.000  0 0.000
#&gt; SRR1283396     2  0.0000      0.817 0.000 1.000  0 0.000
#&gt; SRR1283397     2  0.4382      0.828 0.296 0.704  0 0.000
#&gt; SRR1283398     2  0.4382      0.828 0.296 0.704  0 0.000
#&gt; SRR1283399     2  0.4477      0.826 0.312 0.688  0 0.000
#&gt; SRR1283400     2  0.4382      0.828 0.296 0.704  0 0.000
#&gt; SRR1283401     2  0.4382      0.828 0.296 0.704  0 0.000
#&gt; SRR1283402     2  0.4277      0.833 0.280 0.720  0 0.000
#&gt; SRR1283403     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283404     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283405     3  0.0000      1.000 0.000 0.000  1 0.000
#&gt; SRR1283406     4  0.0336      0.967 0.008 0.000  0 0.992
#&gt; SRR1283407     4  0.0336      0.967 0.008 0.000  0 0.992
#&gt; SRR1283408     4  0.0336      0.967 0.008 0.000  0 0.992
#&gt; SRR1283409     4  0.1118      0.965 0.036 0.000  0 0.964
#&gt; SRR1283410     4  0.1118      0.965 0.036 0.000  0 0.964
#&gt; SRR1283411     4  0.1211      0.961 0.040 0.000  0 0.960
#&gt; SRR1283412     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283413     1  0.4843      0.988 0.604 0.000  0 0.396
#&gt; SRR1283414     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283415     1  0.4907      0.963 0.580 0.000  0 0.420
#&gt; SRR1283416     1  0.4898      0.969 0.584 0.000  0 0.416
#&gt; SRR1283417     1  0.4898      0.969 0.584 0.000  0 0.416
#&gt; SRR1283418     1  0.4855      0.985 0.600 0.000  0 0.400
#&gt; SRR1283419     1  0.4855      0.985 0.600 0.000  0 0.400
#&gt; SRR1283420     1  0.4843      0.987 0.604 0.000  0 0.396
#&gt; SRR1283421     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283422     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283423     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283424     1  0.4843      0.988 0.604 0.000  0 0.396
#&gt; SRR1283425     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283426     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283427     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283428     1  0.4843      0.988 0.604 0.000  0 0.396
#&gt; SRR1283429     1  0.4830      0.990 0.608 0.000  0 0.392
#&gt; SRR1283430     2  0.0817      0.814 0.024 0.976  0 0.000
#&gt; SRR1283431     2  0.0000      0.817 0.000 1.000  0 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4 p5
#&gt; SRR1283379     3  0.0000     1.0000 0.000 0.000  1 0.000  0
#&gt; SRR1283380     3  0.0000     1.0000 0.000 0.000  1 0.000  0
#&gt; SRR1283381     3  0.0000     1.0000 0.000 0.000  1 0.000  0
#&gt; SRR1283385     2  0.0000     0.1497 0.000 1.000  0 0.000  0
#&gt; SRR1283386     2  0.0000     0.1497 0.000 1.000  0 0.000  0
#&gt; SRR1283387     2  0.0703     0.0714 0.000 0.976  0 0.024  0
#&gt; SRR1283388     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283389     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283390     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283382     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283383     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283384     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283391     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283392     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283393     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283394     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283395     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283396     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283397     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283398     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283399     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283400     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283401     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283402     2  0.4307     0.8807 0.496 0.504  0 0.000  0
#&gt; SRR1283403     3  0.0000     1.0000 0.000 0.000  1 0.000  0
#&gt; SRR1283404     3  0.0000     1.0000 0.000 0.000  1 0.000  0
#&gt; SRR1283405     3  0.0000     1.0000 0.000 0.000  1 0.000  0
#&gt; SRR1283406     5  0.0000     1.0000 0.000 0.000  0 0.000  1
#&gt; SRR1283407     5  0.0000     1.0000 0.000 0.000  0 0.000  1
#&gt; SRR1283408     5  0.0000     1.0000 0.000 0.000  0 0.000  1
#&gt; SRR1283409     5  0.0000     1.0000 0.000 0.000  0 0.000  1
#&gt; SRR1283410     5  0.0000     1.0000 0.000 0.000  0 0.000  1
#&gt; SRR1283411     5  0.0000     1.0000 0.000 0.000  0 0.000  1
#&gt; SRR1283412     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283413     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283414     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283415     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283416     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283417     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283418     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283419     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283420     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283421     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283422     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283423     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283424     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283425     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283426     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283427     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283428     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283429     1  0.4307     1.0000 0.504 0.000  0 0.496  0
#&gt; SRR1283430     4  0.4307     1.0000 0.000 0.496  0 0.504  0
#&gt; SRR1283431     4  0.4307     1.0000 0.000 0.496  0 0.504  0
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4 p5    p6
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1283385     6  0.3499      0.457 0.000 0.320  0 0.000  0 0.680
#&gt; SRR1283386     6  0.3499      0.457 0.000 0.320  0 0.000  0 0.680
#&gt; SRR1283387     2  0.3789      0.138 0.000 0.584  0 0.000  0 0.416
#&gt; SRR1283388     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283389     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283390     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283382     4  0.0000      0.904 0.000 0.000  0 1.000  0 0.000
#&gt; SRR1283383     4  0.0000      0.904 0.000 0.000  0 1.000  0 0.000
#&gt; SRR1283384     4  0.0000      0.904 0.000 0.000  0 1.000  0 0.000
#&gt; SRR1283391     4  0.0000      0.904 0.000 0.000  0 1.000  0 0.000
#&gt; SRR1283392     4  0.0000      0.904 0.000 0.000  0 1.000  0 0.000
#&gt; SRR1283393     4  0.0146      0.902 0.000 0.000  0 0.996  0 0.004
#&gt; SRR1283394     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283395     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283396     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283397     4  0.3221      0.541 0.000 0.000  0 0.736  0 0.264
#&gt; SRR1283398     4  0.2854      0.654 0.000 0.000  0 0.792  0 0.208
#&gt; SRR1283399     6  0.3717      0.565 0.000 0.000  0 0.384  0 0.616
#&gt; SRR1283400     6  0.3464      0.684 0.000 0.000  0 0.312  0 0.688
#&gt; SRR1283401     6  0.3464      0.684 0.000 0.000  0 0.312  0 0.688
#&gt; SRR1283402     6  0.3390      0.686 0.000 0.000  0 0.296  0 0.704
#&gt; SRR1283403     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1283404     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1283405     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1283406     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1283407     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1283408     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1283409     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1283410     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1283411     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1283412     1  0.1663      0.908 0.912 0.000  0 0.000  0 0.088
#&gt; SRR1283413     1  0.1610      0.909 0.916 0.000  0 0.000  0 0.084
#&gt; SRR1283414     1  0.2454      0.885 0.840 0.000  0 0.000  0 0.160
#&gt; SRR1283415     1  0.1141      0.894 0.948 0.000  0 0.000  0 0.052
#&gt; SRR1283416     1  0.1141      0.894 0.948 0.000  0 0.000  0 0.052
#&gt; SRR1283417     1  0.1141      0.894 0.948 0.000  0 0.000  0 0.052
#&gt; SRR1283418     1  0.2178      0.907 0.868 0.000  0 0.000  0 0.132
#&gt; SRR1283419     1  0.2178      0.907 0.868 0.000  0 0.000  0 0.132
#&gt; SRR1283420     1  0.2912      0.881 0.784 0.000  0 0.000  0 0.216
#&gt; SRR1283421     1  0.2969      0.877 0.776 0.000  0 0.000  0 0.224
#&gt; SRR1283422     1  0.2969      0.877 0.776 0.000  0 0.000  0 0.224
#&gt; SRR1283423     1  0.2969      0.877 0.776 0.000  0 0.000  0 0.224
#&gt; SRR1283424     1  0.1141      0.894 0.948 0.000  0 0.000  0 0.052
#&gt; SRR1283425     1  0.1204      0.895 0.944 0.000  0 0.000  0 0.056
#&gt; SRR1283426     1  0.1204      0.895 0.944 0.000  0 0.000  0 0.056
#&gt; SRR1283427     1  0.1327      0.909 0.936 0.000  0 0.000  0 0.064
#&gt; SRR1283428     1  0.1327      0.909 0.936 0.000  0 0.000  0 0.064
#&gt; SRR1283429     1  0.1327      0.909 0.936 0.000  0 0.000  0 0.064
#&gt; SRR1283430     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1283431     2  0.0000      0.938 0.000 1.000  0 0.000  0 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 15884 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.974       0.982         0.2243 0.795   0.795
#> 3 3 1.000           1.000       1.000         1.6997 0.599   0.496
#> 4 4 0.993           0.985       0.978         0.0073 1.000   1.000
#> 5 5 0.785           0.856       0.853         0.0979 0.993   0.983
#> 6 6 0.729           0.753       0.855         0.0480 0.954   0.882
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1283379     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283380     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283381     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283385     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283386     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283387     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283388     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283389     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283390     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283382     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283383     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283384     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283391     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283392     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283393     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283394     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283395     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283396     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283397     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283398     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283399     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283400     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283401     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283402     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283403     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283404     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283405     1  0.0000      1.000 1.000 0.000
#&gt; SRR1283406     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283407     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283408     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283409     2  0.4562      0.921 0.096 0.904
#&gt; SRR1283410     2  0.4562      0.921 0.096 0.904
#&gt; SRR1283411     2  0.4562      0.921 0.096 0.904
#&gt; SRR1283412     2  0.4690      0.917 0.100 0.900
#&gt; SRR1283413     2  0.4431      0.924 0.092 0.908
#&gt; SRR1283414     2  0.4815      0.913 0.104 0.896
#&gt; SRR1283415     2  0.0672      0.979 0.008 0.992
#&gt; SRR1283416     2  0.1414      0.976 0.020 0.980
#&gt; SRR1283417     2  0.0672      0.979 0.008 0.992
#&gt; SRR1283418     2  0.1414      0.976 0.020 0.980
#&gt; SRR1283419     2  0.1414      0.976 0.020 0.980
#&gt; SRR1283420     2  0.1633      0.975 0.024 0.976
#&gt; SRR1283421     2  0.2423      0.966 0.040 0.960
#&gt; SRR1283422     2  0.2423      0.966 0.040 0.960
#&gt; SRR1283423     2  0.2423      0.966 0.040 0.960
#&gt; SRR1283424     2  0.1633      0.975 0.024 0.976
#&gt; SRR1283425     2  0.1633      0.975 0.024 0.976
#&gt; SRR1283426     2  0.1633      0.975 0.024 0.976
#&gt; SRR1283427     2  0.1633      0.975 0.024 0.976
#&gt; SRR1283428     2  0.1414      0.976 0.020 0.980
#&gt; SRR1283429     2  0.1414      0.976 0.020 0.980
#&gt; SRR1283430     2  0.0000      0.981 0.000 1.000
#&gt; SRR1283431     2  0.0000      0.981 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1283379     3       0          1  0  0  1
#&gt; SRR1283380     3       0          1  0  0  1
#&gt; SRR1283381     3       0          1  0  0  1
#&gt; SRR1283385     2       0          1  0  1  0
#&gt; SRR1283386     2       0          1  0  1  0
#&gt; SRR1283387     2       0          1  0  1  0
#&gt; SRR1283388     2       0          1  0  1  0
#&gt; SRR1283389     2       0          1  0  1  0
#&gt; SRR1283390     2       0          1  0  1  0
#&gt; SRR1283382     2       0          1  0  1  0
#&gt; SRR1283383     2       0          1  0  1  0
#&gt; SRR1283384     2       0          1  0  1  0
#&gt; SRR1283391     2       0          1  0  1  0
#&gt; SRR1283392     2       0          1  0  1  0
#&gt; SRR1283393     2       0          1  0  1  0
#&gt; SRR1283394     2       0          1  0  1  0
#&gt; SRR1283395     2       0          1  0  1  0
#&gt; SRR1283396     2       0          1  0  1  0
#&gt; SRR1283397     2       0          1  0  1  0
#&gt; SRR1283398     2       0          1  0  1  0
#&gt; SRR1283399     2       0          1  0  1  0
#&gt; SRR1283400     2       0          1  0  1  0
#&gt; SRR1283401     2       0          1  0  1  0
#&gt; SRR1283402     2       0          1  0  1  0
#&gt; SRR1283403     3       0          1  0  0  1
#&gt; SRR1283404     3       0          1  0  0  1
#&gt; SRR1283405     3       0          1  0  0  1
#&gt; SRR1283406     1       0          1  1  0  0
#&gt; SRR1283407     1       0          1  1  0  0
#&gt; SRR1283408     1       0          1  1  0  0
#&gt; SRR1283409     1       0          1  1  0  0
#&gt; SRR1283410     1       0          1  1  0  0
#&gt; SRR1283411     1       0          1  1  0  0
#&gt; SRR1283412     1       0          1  1  0  0
#&gt; SRR1283413     1       0          1  1  0  0
#&gt; SRR1283414     1       0          1  1  0  0
#&gt; SRR1283415     1       0          1  1  0  0
#&gt; SRR1283416     1       0          1  1  0  0
#&gt; SRR1283417     1       0          1  1  0  0
#&gt; SRR1283418     1       0          1  1  0  0
#&gt; SRR1283419     1       0          1  1  0  0
#&gt; SRR1283420     1       0          1  1  0  0
#&gt; SRR1283421     1       0          1  1  0  0
#&gt; SRR1283422     1       0          1  1  0  0
#&gt; SRR1283423     1       0          1  1  0  0
#&gt; SRR1283424     1       0          1  1  0  0
#&gt; SRR1283425     1       0          1  1  0  0
#&gt; SRR1283426     1       0          1  1  0  0
#&gt; SRR1283427     1       0          1  1  0  0
#&gt; SRR1283428     1       0          1  1  0  0
#&gt; SRR1283429     1       0          1  1  0  0
#&gt; SRR1283430     2       0          1  0  1  0
#&gt; SRR1283431     2       0          1  0  1  0
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1283379     3  0.0000      0.916 0.000 0.000 1.000 0.000
#&gt; SRR1283380     3  0.0000      0.916 0.000 0.000 1.000 0.000
#&gt; SRR1283381     3  0.0000      0.916 0.000 0.000 1.000 0.000
#&gt; SRR1283385     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283386     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283387     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283388     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283389     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283390     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283382     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283383     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283384     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283391     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283392     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283393     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283394     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283395     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283396     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283397     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283398     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283399     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283400     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283401     2  0.0188      0.989 0.000 0.996 0.000 0.004
#&gt; SRR1283402     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1283403     3  0.4382      0.916 0.000 0.000 0.704 0.296
#&gt; SRR1283404     3  0.4382      0.916 0.000 0.000 0.704 0.296
#&gt; SRR1283405     3  0.4382      0.916 0.000 0.000 0.704 0.296
#&gt; SRR1283406     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283407     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283408     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283409     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283410     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283411     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283412     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283413     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283414     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283415     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283416     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283417     1  0.0188      0.998 0.996 0.000 0.000 0.004
#&gt; SRR1283418     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283419     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283420     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283421     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283422     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283423     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283424     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283425     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283426     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283427     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283428     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283429     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1283430     2  0.0707      0.988 0.000 0.980 0.000 0.020
#&gt; SRR1283431     2  0.0707      0.988 0.000 0.980 0.000 0.020
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1283379     3  0.0000      1.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283380     3  0.0000      1.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283381     3  0.0000      1.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR1283385     2  0.0451      0.919 0.004 0.988 0.000 0.000 NA
#&gt; SRR1283386     2  0.0451      0.919 0.004 0.988 0.000 0.000 NA
#&gt; SRR1283387     2  0.0960      0.918 0.016 0.972 0.000 0.004 NA
#&gt; SRR1283388     2  0.1012      0.915 0.020 0.968 0.000 0.012 NA
#&gt; SRR1283389     2  0.0807      0.919 0.012 0.976 0.000 0.012 NA
#&gt; SRR1283390     2  0.1956      0.895 0.052 0.928 0.000 0.012 NA
#&gt; SRR1283382     2  0.3422      0.866 0.004 0.792 0.000 0.004 NA
#&gt; SRR1283383     2  0.3456      0.862 0.004 0.788 0.000 0.004 NA
#&gt; SRR1283384     2  0.2612      0.908 0.000 0.868 0.000 0.008 NA
#&gt; SRR1283391     2  0.3398      0.856 0.004 0.780 0.000 0.000 NA
#&gt; SRR1283392     2  0.3366      0.859 0.004 0.784 0.000 0.000 NA
#&gt; SRR1283393     2  0.2488      0.909 0.000 0.872 0.000 0.004 NA
#&gt; SRR1283394     2  0.0727      0.918 0.012 0.980 0.000 0.004 NA
#&gt; SRR1283395     2  0.0693      0.918 0.012 0.980 0.000 0.008 NA
#&gt; SRR1283396     2  0.2086      0.894 0.048 0.924 0.000 0.020 NA
#&gt; SRR1283397     2  0.2536      0.906 0.000 0.868 0.000 0.004 NA
#&gt; SRR1283398     2  0.2848      0.894 0.000 0.840 0.000 0.004 NA
#&gt; SRR1283399     2  0.1952      0.917 0.000 0.912 0.000 0.004 NA
#&gt; SRR1283400     2  0.1638      0.919 0.000 0.932 0.000 0.004 NA
#&gt; SRR1283401     2  0.1831      0.918 0.000 0.920 0.000 0.004 NA
#&gt; SRR1283402     2  0.1502      0.920 0.000 0.940 0.000 0.004 NA
#&gt; SRR1283403     4  0.4067      0.994 0.008 0.000 0.300 0.692 NA
#&gt; SRR1283404     4  0.4067      0.994 0.008 0.000 0.300 0.692 NA
#&gt; SRR1283405     4  0.4108      0.988 0.008 0.000 0.308 0.684 NA
#&gt; SRR1283406     1  0.4443      0.562 0.524 0.000 0.000 0.004 NA
#&gt; SRR1283407     1  0.4297      0.563 0.528 0.000 0.000 0.000 NA
#&gt; SRR1283408     1  0.4297      0.563 0.528 0.000 0.000 0.000 NA
#&gt; SRR1283409     1  0.4455      0.631 0.588 0.000 0.000 0.008 NA
#&gt; SRR1283410     1  0.4455      0.631 0.588 0.000 0.000 0.008 NA
#&gt; SRR1283411     1  0.4359      0.627 0.584 0.000 0.000 0.004 NA
#&gt; SRR1283412     1  0.0807      0.847 0.976 0.000 0.000 0.012 NA
#&gt; SRR1283413     1  0.1012      0.848 0.968 0.000 0.000 0.012 NA
#&gt; SRR1283414     1  0.1740      0.833 0.932 0.000 0.000 0.012 NA
#&gt; SRR1283415     1  0.2850      0.821 0.872 0.000 0.000 0.036 NA
#&gt; SRR1283416     1  0.2426      0.832 0.900 0.000 0.000 0.036 NA
#&gt; SRR1283417     1  0.3214      0.808 0.844 0.000 0.000 0.036 NA
#&gt; SRR1283418     1  0.0324      0.847 0.992 0.000 0.000 0.004 NA
#&gt; SRR1283419     1  0.0451      0.847 0.988 0.000 0.000 0.004 NA
#&gt; SRR1283420     1  0.1628      0.831 0.936 0.000 0.000 0.008 NA
#&gt; SRR1283421     1  0.2189      0.819 0.904 0.000 0.000 0.012 NA
#&gt; SRR1283422     1  0.2189      0.819 0.904 0.000 0.000 0.012 NA
#&gt; SRR1283423     1  0.2130      0.822 0.908 0.000 0.000 0.012 NA
#&gt; SRR1283424     1  0.1082      0.846 0.964 0.000 0.000 0.008 NA
#&gt; SRR1283425     1  0.0992      0.847 0.968 0.000 0.000 0.008 NA
#&gt; SRR1283426     1  0.1740      0.842 0.932 0.000 0.000 0.012 NA
#&gt; SRR1283427     1  0.0510      0.845 0.984 0.000 0.000 0.000 NA
#&gt; SRR1283428     1  0.0992      0.842 0.968 0.000 0.000 0.008 NA
#&gt; SRR1283429     1  0.0510      0.845 0.984 0.000 0.000 0.000 NA
#&gt; SRR1283430     2  0.0727      0.918 0.012 0.980 0.000 0.004 NA
#&gt; SRR1283431     2  0.0613      0.918 0.008 0.984 0.000 0.004 NA
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1283379     3  0.2597      1.000 0.000 0.000 0.824 0.176 NA 0.000
#&gt; SRR1283380     3  0.2597      1.000 0.000 0.000 0.824 0.176 NA 0.000
#&gt; SRR1283381     3  0.2597      1.000 0.000 0.000 0.824 0.176 NA 0.000
#&gt; SRR1283385     2  0.4120      0.792 0.000 0.728 0.000 0.000 NA 0.068
#&gt; SRR1283386     2  0.3907      0.819 0.000 0.756 0.000 0.000 NA 0.068
#&gt; SRR1283387     2  0.4038      0.783 0.000 0.712 0.000 0.000 NA 0.044
#&gt; SRR1283388     2  0.1643      0.907 0.000 0.924 0.008 0.000 NA 0.000
#&gt; SRR1283389     2  0.1471      0.908 0.000 0.932 0.004 0.000 NA 0.000
#&gt; SRR1283390     2  0.2159      0.905 0.012 0.904 0.012 0.000 NA 0.000
#&gt; SRR1283382     2  0.2633      0.868 0.000 0.864 0.000 0.000 NA 0.104
#&gt; SRR1283383     2  0.2798      0.861 0.000 0.852 0.000 0.000 NA 0.112
#&gt; SRR1283384     2  0.2318      0.896 0.000 0.892 0.000 0.000 NA 0.064
#&gt; SRR1283391     2  0.2660      0.867 0.000 0.868 0.000 0.000 NA 0.084
#&gt; SRR1283392     2  0.2724      0.864 0.000 0.864 0.000 0.000 NA 0.084
#&gt; SRR1283393     2  0.1245      0.903 0.000 0.952 0.000 0.000 NA 0.016
#&gt; SRR1283394     2  0.1814      0.902 0.000 0.900 0.000 0.000 NA 0.000
#&gt; SRR1283395     2  0.1910      0.900 0.000 0.892 0.000 0.000 NA 0.000
#&gt; SRR1283396     2  0.2611      0.894 0.012 0.864 0.008 0.000 NA 0.000
#&gt; SRR1283397     2  0.1498      0.899 0.000 0.940 0.000 0.000 NA 0.028
#&gt; SRR1283398     2  0.1934      0.892 0.000 0.916 0.000 0.000 NA 0.044
#&gt; SRR1283399     2  0.0260      0.908 0.000 0.992 0.000 0.000 NA 0.000
#&gt; SRR1283400     2  0.0291      0.909 0.000 0.992 0.000 0.000 NA 0.004
#&gt; SRR1283401     2  0.0146      0.908 0.000 0.996 0.000 0.000 NA 0.000
#&gt; SRR1283402     2  0.0291      0.909 0.000 0.992 0.000 0.000 NA 0.004
#&gt; SRR1283403     4  0.0146      0.995 0.004 0.000 0.000 0.996 NA 0.000
#&gt; SRR1283404     4  0.0146      0.995 0.004 0.000 0.000 0.996 NA 0.000
#&gt; SRR1283405     4  0.0405      0.990 0.004 0.000 0.008 0.988 NA 0.000
#&gt; SRR1283406     6  0.4026      0.975 0.348 0.000 0.000 0.000 NA 0.636
#&gt; SRR1283407     6  0.4144      0.965 0.360 0.000 0.000 0.000 NA 0.620
#&gt; SRR1283408     6  0.3592      0.966 0.344 0.000 0.000 0.000 NA 0.656
#&gt; SRR1283409     1  0.4977      0.192 0.636 0.000 0.000 0.000 NA 0.236
#&gt; SRR1283410     1  0.4977      0.192 0.636 0.000 0.000 0.000 NA 0.236
#&gt; SRR1283411     1  0.5076      0.136 0.620 0.000 0.000 0.000 NA 0.248
#&gt; SRR1283412     1  0.1434      0.725 0.940 0.000 0.000 0.000 NA 0.012
#&gt; SRR1283413     1  0.1719      0.718 0.924 0.000 0.000 0.000 NA 0.016
#&gt; SRR1283414     1  0.1511      0.727 0.940 0.000 0.000 0.004 NA 0.012
#&gt; SRR1283415     1  0.5896     -0.189 0.480 0.000 0.000 0.004 NA 0.192
#&gt; SRR1283416     1  0.5947     -0.233 0.460 0.000 0.000 0.004 NA 0.196
#&gt; SRR1283417     1  0.5928     -0.213 0.480 0.000 0.000 0.004 NA 0.204
#&gt; SRR1283418     1  0.0260      0.737 0.992 0.000 0.000 0.008 NA 0.000
#&gt; SRR1283419     1  0.0717      0.737 0.976 0.000 0.000 0.016 NA 0.008
#&gt; SRR1283420     1  0.1194      0.731 0.956 0.000 0.000 0.008 NA 0.004
#&gt; SRR1283421     1  0.0870      0.735 0.972 0.000 0.000 0.004 NA 0.012
#&gt; SRR1283422     1  0.0767      0.735 0.976 0.000 0.000 0.004 NA 0.012
#&gt; SRR1283423     1  0.0870      0.735 0.972 0.000 0.000 0.004 NA 0.012
#&gt; SRR1283424     1  0.1899      0.730 0.928 0.000 0.004 0.032 NA 0.008
#&gt; SRR1283425     1  0.1819      0.731 0.932 0.000 0.004 0.032 NA 0.008
#&gt; SRR1283426     1  0.2364      0.721 0.904 0.000 0.004 0.044 NA 0.012
#&gt; SRR1283427     1  0.2476      0.690 0.880 0.000 0.000 0.024 NA 0.004
#&gt; SRR1283428     1  0.2149      0.695 0.888 0.000 0.000 0.004 NA 0.004
#&gt; SRR1283429     1  0.2373      0.701 0.888 0.000 0.000 0.024 NA 0.004
#&gt; SRR1283430     2  0.1556      0.907 0.000 0.920 0.000 0.000 NA 0.000
#&gt; SRR1283431     2  0.1387      0.908 0.000 0.932 0.000 0.000 NA 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


