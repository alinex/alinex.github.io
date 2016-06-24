---
title: Modules
layout: default
---

Node.JS
------------------------------------------------------------------------------

This modules are written in CoffeeScript but are already compiled to JavaScript
in the NPM download package. So no need to worry if you aren't familiar with
CoffeeScript. All my module name's has alinex as a namespace prefix and often use
some other alinex modules. But that shouldn't prevent you to use it elsewhere.

To get more information about the code, style and development guidelines see
the [General docs](http://alinex.github.io/node-alinex/).

<div class="row modules">
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>General Helpers</h3>
<p><a href="http://alinex.github.io/node-builder/">builder</a>
    a built tool to help while developing</p>
<p><a href="http://alinex.github.io/node-alinex/">core</a>
    application basics</p>
<p><a href="http://alinex.github.io/node-handlebars/">handlebars</a>
    helper collection for handlebars templates</p>
<p><a href="http://alinex.github.io/node-report/">report</a>
    easy report generation using markdown</p>
<p><a href="http://alinex.github.io/node-sshtunnel/">sshtunnel</a>
    ssh port tunneling made easy</p>
<p><a href="http://alinex.github.io/node-table/">table</a>
    working with table like data</p>
<p><a href="http://alinex.github.io/node-util/">util</a>
    different smaller helpers for string, array and objects</p>
<p><a href="http://alinex.github.io/node-validator/">validator</a>
    validation and sanitize of simple or complex values</p>

  </div>
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>Base Modules</h3>
<p><a href="http://alinex.github.io/node-config/">config</a>
    configuration management</p>
<p><a href="http://alinex.github.io/node-database/">database</a>
    wrapper module supporting mysql and more</p>
<p><a href="http://alinex.github.io/node-exec/">exec</a>
    async execution control for other processes</p>
<p><a href="http://alinex.github.io/node-format/">format</a>
    easy serialization and deserialization of data objects</p>
<p><a href="http://alinex.github.io/node-fs/">fs</a>
    enhancement of the node filesystem library</p>
<p><a href="http://alinex.github.io/node-mail/">mail</a>
    easy mail sending</p>
<p><a href="http://alinex.github.io/node-media/">media</a>
    media file analyzation and manipulation</p>
<p><a href="http://alinex.github.io/node-server/">server</a>
    basic webserver based on express</p>

  </div>
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>Applications</h3>

<p><a href="http://alinex.github.io/node-dbreport/">dbreport</a>
    tool to query database and send results as email attachments</p>
<p><a href="http://alinex.github.io/node-mailman/">mailman</a>
    management console based on email</p>
<p><a href="http://alinex.github.io/node-monitor/">monitor</a>
    server application for monitoring IT systems</p>
<p><a href="http://alinex.github.io/node-scripter/">scripter</a>
    environment to make powerful scripts</p>
<p><a href="http://alinex.github.io/node-worktime/">worktime</a>
    command line application for logging work times</p>

  </div>
</div>

Some more modules are planned or in development but didn't reach a stable
and presentable stage. I will add them as soon as they are ready.

Third Party NodeJS
---------------------------------------------------------------------------

This is used as a quick link to the individual documentation pages helping in
fast lookup of often used packages.

<div class="row modules">
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>General Tools</h3>

<p><a href="https://github.com/caolan/async/blob/master/README.md">async</a> easy asynchronous calls</p>
<p><a href="https://github.com/abbr/deasync">deasync</a> run async functions synchron</p>
<p><a href="https://github.com/visionmedia/debug/blob/master/Readme.md">debug</a> life debugging</p>
<p><a href="https://github.com/pgte/carrier">carrier</a> stream line reader</p>
<p><a href="https://github.com/chalk/chalk/blob/master/readme.md">chalk</a> terminal string styling</p>
<p><a href="http://mathjs.org/docs/index.html">mathjs</a> math library with unit support</p>
<p><a href="https://github.com/medikoo/memoize">Memoizee</a> make a function or method using cache for results</p>
<p><a href="https://github.com/cho45/named-regexp.js/blob/master/README.md">named-regexp</a> named capture feature for RegExp</p>

  </div>
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>Format</h3>

<p><a href="https://github.com/cheeriojs/cheerio">cheerio</a> html parser with easy jQuery like access</p>
<p><a href="https://github.com/wanasit/chrono">Chrono</a> natural language date parser</p>
<p><a href="http://handlebarsjs.com/">handlebars</a> template engine</p>
<p><a href="https://github.com/marcbachmann/node-html-pdf/blob/master/README.md">html-pdf</a> convert html to pdf or image using phantomjs</p>
<p><a href="https://github.com/ashtuchkin/iconv-lite/blob/master/README.md">iconv-lite</a> easy change of encoding</p>
<p><a href="https://github.com/mashpie/i18n-node/blob/master/README.md">i18n</a> simple translation module</p>
<p><a href="https://github.com/zemirco/json2csv/blob/master/README.md">json2csv</a> easy converting</p>
<p><a href="https://github.com/nodeca/js-yaml">js-yaml</a> YAML parser (to read configurations</p>
<p><a href="https://markdown-it.github.io/">markdown-it</a> convert markdown to html</p>
<p><a href="http://momentjs.com/docs/">moment</a> parse and manipulate dates and times</p>
<p><a href="https://github.com/Leonidas-from-XIV/node-xml2js">xml2js</a> Conversion from simple XML to JavaScript objects</p>
<p><a href="http://pdfkit.org/">pdfkit</a> pdf creation toolkit</p>
  </div>
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>IO</h3>

<p><a href="https://github.com/paulmillr/chokidar">chokidar</a> fs-watch wrapper</p>
<p><a href="https://github.com/SBoudrias/Inquirer.js/blob/master/README.md">Inquirer</a> interactive command line user interface</p>
<p><a href="https://github.com/felixge/node-mysql">Mysql</a> easy to use mysql library</p>
<p><a href="http://nodemailer.com/">nodemail</a> sending emails</p>
<p><a href="https://github.com/request/request/blob/master/README.md">request</a> simple http/https requests</p>
<p><a href="https://github.com/flatiron/winston/">Winston</a> extensible multi-transport async logging library</p>
<p><a href="http://yargs.js.org/docs/index.html">yargs</a> parsing option strings from the commandline</p>

  </div>
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>Development</h3>

<p><a href="http://coffeescript.org/">CoffeeScript</a> a language that compiles into JavaScript but is easier to read and write</p>
<p><a href="http://chaijs.com/">chai</a> assertion library that can be paired with mocha</p>  
<p><a href="https://github.com/bnoordhuis/node-heapdump">HeapDump</a> create a heapdump to analyze using Chrome</p>
<p><a href="http://mochajs.org/">mocha</a> simple, flexible test tool</p>

  </div>
  <div class="col-md-4 col-sm-6 col-xs-12">

<h3>Applications</h3>

<p><a href="http://pm2.keymetrics.io/docs/usage/cluster-mode/">pm2</a> production process manager</p>

</div>
<div class="col-md-4 col-sm-6 col-xs-12">

<h3>Webservices</h3>

<p><a href="https://docs.angularjs.org/">AngularJS</a> client library is added here to be compiled into the client scripts</p>

  </div>
</div>
