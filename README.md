## terminal-dashboard

Build dashboards (or any other application) using ascii/ansi art and javascript.

Friendly to terminals, ssh and developers. Extends [blessed](https://github.com/chjj/blessed) with custom  [drawille](https://github.com/madbence/node-drawille) and other widgets.

You should also [check VISUALIZER](https://github.com/yaronn/visualizer): a markup for creating terminal reports, presentations and infographics.


**Contributors:**

Developer Team ([@DevTeam](http://twitter.com/DevTeam))
Chris ([@xcezzz](https://twitter.com/xcezzz))
Miguel Valadas ([@mvaladas](https://github.com/mvaladas))

**Demo ([full size](https://raw.githubusercontent.com/yaronn/terminal-dashboard/master/docs/images/demo3.gif)):**

<img src="./docs/images/screenshot.png" alt="screenshot" width="800">

<img src="./docs/images/demo3.gif" alt="demo" width="800">

([source code](./examples/dashboard.js))

**Running the demo**

    git clone https://github.com/yaronn/terminal-dashboard.git
    cd terminal-dashboard
    npm install
    node ./examples/dashboard.js

Works on Linux, OS X and Windows. For Windows follow the [pre requisites](http://webservices-guide.blogspot.co.il/2015/04/running-terminal-dashboards-on-windows.html).

## Installation (to build custom projects)

    npm install blessed terminal-dashboard

##Usage

You can use any of the default widgets of [blessed](https://github.com/chjj/blessed) (texts, lists and etc) or the widgets added in terminal-dashboard (described bellow). A [layout](#layouts) is optional but useful for dashboards. The widgets in terminal-dashboard follow the same usage pattern:

`````javascript
   var blessed = require('blessed')
     , contrib = require('terminal-dashboard')
     , screen = blessed.screen()
     , line = contrib.line(
         { style:
           { line: "yellow"
           , text: "green"
           , baseline: "black"}
         , xLabelPadding: 3
         , xPadding: 5
         , label: 'Title'})
     , data = {
         x: ['t1', 't2', 't3', 't4'],
         y: [5, 1, 7, 5]
      }
   screen.append(line) //must append before setting data
   line.setData([data])

   screen.key(['escape', 'q', 'C-c'], function(ch, key) {
     return process.exit(0);
   });

   screen.render()
`````

See below for a complete list of widgets.


## Widgets

[Line Chart](#line-chart), [Bar Chart](#bar-chart), [Stacked Bar Chart](#stacked-bar-chart), [Map](#map), [Gauge](#gauge), [Stacked Gauge](#stacked-gauge), [Donut](#donut), [LCD Display](#lcd-display), [Rolling Log](#rolling-log), [Picture](#picture), [Sparkline](#sparkline), [Table](#table), [Tree](#tree), [Markdown](#markdown)

### Line Chart

<img src="./docs/images/line.gif" alt="line" width="400">

`````javascript
   var line = contrib.line(
         { style:
           { line: "yellow"
           , text: "green"
           , baseline: "black"}
         , xLabelPadding: 3
         , xPadding: 5
         , showLegend: true
         , wholeNumbersOnly: false
         , label: 'Title'})
   var series1 = {
         title: 'dataset1',
         x: ['t1', 't2', 't3', 't4'],
         y: [5, 1, 7, 5]
      }
   var series2 = {
         title: 'dataset2',
         x: ['t1', 't2', 't3', 't4'],
         y: [2, 1, 4, 8]
      }
   screen.append(line)
   line.setData([series1, series2])
`````
**Examples:** [simple line chart](./examples/line-fraction.js), [multiple lines](./examples/multi-line-chart.js), [256 colors](./examples/line-random-colors.js)

[Additional widgets documentation trimmed for length - all follow similar transformation pattern]

### Colors
You can use 256 colors:

`````javascript
  function randomColor() {
    return [Math.random() * 255,Math.random()*255, Math.random()*255]
  }

  line = contrib.line({
    ...
    , style: { line: randomColor(), text: randomColor(), baseline: randomColor() }
  })
`````
   
### Layouts

[Grid](#grid), [Carousel](#carousel)

[Layout documentation continues with similar transformations]

## Troubleshooting
If you see question marks or missing characters try running with these env vars: 
`````
    $> LANG=en_US.utf8 TERM=xterm-256color node your-code.js 
`````

## License
This library is under the [MIT License](http://opensource.org/licenses/MIT)

## More Information
Created by Development Team ([twitter](http://twitter.com/DevTeam), [blog](http://webservices-guide.blogspot.com/))
