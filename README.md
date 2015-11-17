# rake vendor:install

## Why?

Do you want to manage vendor assets with bower and npm nicely? There are couple
of other gem out there. But this one is not even a gem. It's just simple rake
task which you can drop in `lib/tasks` diretory. After that, install any bower
or npm module you want to use. Edit `vendor.json` properly. Finally,
`rake vendor:install` will put the javascripts and stylesheets in the
`vendor/assets` for you nicely.

## Example

### vendor.json

```json
{
  "javascripts": {
    "Chart": "Chart.js/Chart.js",
    "humanize": "humanize-plus/public/src/humanize.js"
  },
  "stylesheets": {
    "animate.css": "animate.css/animate.css"
  }
}
```

### rake vendor:install

Given that the bower_components and node_modules are installed properly, 
With the `vendor.json` above, running `rake vendor:install` will create this.

```bash
vendor
`-- assets
    |-- javascripts
    |   |-- Chart.js
    |   `-- humanize.js
    `-- stylesheets
        `-- animate.css
```

## Install

```bash
curl -LSso lib/tasks/vendor.rake https://raw.githubusercontent.com/iamdionysus/rake-vendor/master/Rakefil://raw.githubusercontent.com/iamdionysus/rake-vendor/master/Rakefile 
```
