This will do you fine these days (IE 8 and up):

.group:after {
  content: "";
  display: table;
  clear: both;
}


Apply it to any parent element in which you need to clear the floats. For example:

<div class="group">
  <div class="is-floated"></div>
  <div class="is-floated"></div>
  <div class="is-floated"></div>
</div>
You would use this instead of clearing the float with something like <br style="clear: both;" /> at the bottom of the parent (easy to forget, not handleable right in CSS, non-semantic) or using something like overflow: hidden; on the parent (you don’t always want to hide overflow).

Now for a bit of history!

This was the original popular version, designed to support browsers as far back as it possibly could:

.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}

.clearfix { display: inline-block; }
/* start commented backslash hack \*/
* html .clearfix { height: 1%; }
.clearfix { display: block; }
/* close commented backslash hack */
There then was a bit of a cleaner version documented here by Jeff Starr, based on the fact that nobody uses IE for Mac, which is what the backslash hack was all about.

.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
* html .clearfix             { zoom: 1; } /* IE6 */
*:first-child+html .clearfix { zoom: 1; } /* IE7 */
Then it became popular to use “group” as a class name, which is nicer and more semantic (via Dan Cederholm). Also, the content property doesn’t even need the space, it can be empty string (via Nicolas Gallagher). Then, without any text, font-size is un-needed (Chris Coyier).

.group:after {
  visibility: hidden;
  display: block;
  content: "";
  clear: both;
  height: 0;
}
* html .group             { zoom: 1; } /* IE6 */
*:first-child+html .group { zoom: 1; } /* IE7 */
Of course, if you drop IE 6 or 7 support, remove the associated lines.

Update May 18, 2011: Nicolas Gallagher again with the “micro” clearfix. Also see this additional stuff.
.group:before,
.group:after {
  content: "";
  display: table;
} 
.group:after {
  clear: both;
}
.group {
  zoom: 1; /* For IE 6/7 (trigger hasLayout) */
}
See the top of this page for the most modern version of the clearfix.

In the future, we might be able to do:

.group {
  display: flow-root;
}
