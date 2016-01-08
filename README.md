# Jekyll Bootstrap Calendar

Pure **Jekyll layout** to display [bootstrap-calendar](https://github.com/Serhioromano/bootstrap-calendar/) that reads events from a CSV file. No additional service required. No plugin. No gemfile. No bundle. No NPM. No grunt (ARGHH!!!). Just vanilla Jekyll with basic Liquid template code. Most of the processing is done with JavaScript dynamically at client browser.

All dependencies (JS/HTML/CSS) are included in `components` directory. Some of them may already be included by your theme, so you may want to modify the include paths to avoid redundancy. Details of where to modify is explained below.

*Note*: This directory is not a complete Jekyll project. It only contains the files that are needed for the calendar layout and an `example` directory for demonstration. You basically copy these to your own Jekyll project.


# How to set up

1. Download this repository to your machine [manually](https://github.com/NLKNguyen/jekyll-bootstrap-calendar/archive/master.zip) or:
```
git clone https://github.com/NLKNguyen/jekyll-bootstrap-calendar
```

2. Copy `_layouts/calendar.html` into your Jekyll `_layouts/`

3. Copy `components` directory to your Jekyll root directory

4. Modify your `_includes/head.html` to load the CSS files:

Add this right before the closing `</head>` tag

```Liquid
  {{ page.calendar_css | replace: "!PATH_TO_COMPONENTS!", "/components" | prepend: site.baseurl }}
```

If your theme doesn't use Bootstrap, then also add this line:

```Liquid
  {{ page.calendar_bootstrap_css | replace: "!PATH_TO_COMPONENTS!", "/components" | prepend: site.baseurl }}
```

##### In case your have another preferred location for these components

*On step 3*: go to `calendar.html` and find this line near the top:
```Liquid
{% assign PATH_TO_COMPONENTS =  "/components" | prepend: site.baseurl %}
```
and change `"/components"` to your preferred location, relative to your base URL

*On step 4*: similarly, change `"/components"` to your preferred location, relative to your base URL

##### In case your theme already included some of the dependencies

In `calendar.html`, you find a group of script include tags that refers to these components:
* bootstrap
* bootstrap-calendar
* jquery
* lodash
* moment
* papaparse

To avoid redundant includes, simply remove the ones that are always loaded by your theme.

# How to use
See `example` directory for example usage. You can copy this directory to your Jekyll directory to try out.

The post/page, which you want to use the calendar layout, needs to have the Front Matter that sets:

* `layout` to `calendar`
* `calendar_csv` to the events CSV file path from the base url, and 
* `calendar_timezone_offset` to your timezone offset. 

The rest is optional.

```YAML

---

layout: calendar  # required
title: My Calendar

calendar_timezone_offset: -0800   # required
calendar_csv: example/events.csv  # required. Path to CSV file from base url

calendar_focus_date: 2016-01-06   # optional. YYYY-MM-DD. Without it, the default is today
calendar_caption: My calendar caption   # optional

---

Your usual content here

```

#### Create your own CSV file that contains events
You can use any spreadsheet program to create events and export as CSV file. This is an [example with Google Spreadsheet](https://docs.google.com/spreadsheets/d/1S5TvJIQGLtsne52y-WFrsdYT_QQQGS5RQRhamPvqBpo/edit?usp=sharing). Go to menu `File/Make a copy...` and create your own events. Only the first 3 columns (title, start, end) can't be empty, and the date-time format must be exactly like that. After that, `File/Download as csv file` and use it for your calendar.

The options for different `Mark` styles are: `info`, `warning`, `important`, `success`, `special`, and blank.

# License MIT
Copyright (c) Nguyen Nguyen
