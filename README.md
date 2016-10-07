# ![inuitcss](http://inuitcss.com/img/logo-small.png)

**Extensible, scalable, Sass-based, OOCSS framework for large and long-lasting
UI projects.**

inuitcss is a framework in its truest sense: it does not provide you with UI and
design out of the box, instead, it provides you with a solid architectural
baseline upon which to complete your own work.

## Full Documentation

You can find full documentation at [inuitcss.com](http://inuitcss.com).

## Installation

You can use inuitcss in your project by installing it using a package manager
(recommended):

**npm:**

```
$ npm install --save-dev inuitcss
```

**Bower:**

```
$ bower install --save-dev inuitcss
```

**Copy/paste (not recommended):**

You can download inuitcss and save it into your project’s `css/` directory. This
method is not recommended because you lose the ability to easily and quickly
manage and update inuitcss as a dependency.

## Getting Started

Once you have got inuitcss into your project using one of the methods outlined
above, there are a handful of things we need to do before we’re ready to go.

Firstly, we need to identify any files whose name contain the word `example`.
These files are demo and/or scaffolding files that inuitcss requires, but that
you are encouraged to create and define yourself. These files, as of v6.0.0,
are:

```
example.main.scss
settings/_example.settings.config.scss
settings/_example.settings.global.scss
components/_example.components.buttons.scss
```

Here’s what we need to do with them:

### [`example.main.scss`](https://github.com/inuitcss/inuitcss/blob/master/example.main.scss)

This is your main, or _manifest_, file. This is the backbone of any inuitcss
project, and it is responsible for `@import`ing all other files. This is the
file that we compile out into a corresponding CSS file.

You need to copy this file from the directory that your package manager
installed it into, and move it to the root of your `css/` directory. Once there,
rename it `main.scss`.

Next, you’ll need to update all of the `@import`s in that file to point at the
new locations of each partial (that will depend on how your project is set up).

Once you’ve done this, you should be able to run the following command on that
file and get a compiled stylesheet without any errors:

```
path/to/css/$ sass main.scss:main.css
```

**N.B.** If you downloaded inuitcss, you do not need to move this file; you
can simply rename it.

### [`_example.settings.config.scss`](https://github.com/inuitcss/inuitcss/blob/master/settings/_example.settings.config.scss)

This is a configuration file that inuitcss uses to handle the state, location,
or environment of your project. This handles very high-level settings that don’t
necessarily affect the CSS itself, but can be used to manipulate things
depending on where you are running things (e.g. turning a debugging mode on, or
telling your CI sever that you’re compiling for production).

Copy this file into your own `css/settings/` directory and rename it
`_settings.config.scss`.

**N.B.** If you downloaded inuitcss, you do not need to move this this file; you
can simply rename it.

### [`_example.settings.global.scss`](https://github.com/inuitcss/inuitcss/blob/master/components/_example.settings.global.scss)

This is an example globals file; it contains any settings that are available to
your entire project. These variables and settings could be font families,
colours, border-radius values, etc.

Copy this file into your own `css/settings/` directory and rename it
`_settings.global.scss`. Now you can begin adding your own project-wide
settings.

### [`_example.components.buttons.scss`](https://github.com/inuitcss/inuitcss/blob/master/components/_example.components.buttons.scss)

You don’t need to really do much with this file other than ensure you don’t let
it into your final project!

This file exists to show you how you might build components into an inuitcss
project, because components are the one thing that inuitcss purposefully refuses
to provide.

You can, if you wish, copy this file to your own `css/components/` directory and
rename it `_components.buttons.scss`. You can now use this file as the basis for
your own buttons component.

## CSS directory structure

inuitcss follows a specific folder structure, which you should follow as well in your own CSS directory:

* `/settings`: Global variables, site-wide settings, config switches, etc.
* `/tools`: Site-wide mixins and functions.
* `/generic`: Low-specificity, far-reaching rulesets (e.g. resets).
* `/elements`: Unclassed HTML elements (e.g. `a {}`, `blockquote {}`, `address {}`).
* `/objects`: Objects, abstractions, and design patterns (e.g. `.o-layout {}`).
* `/components`: Discrete, complete chunks of UI (e.g. `.c-carousel {}`). This is the one layer that inuitcss doesn’t provide code for, as this is completely your terrain.
* `/utilities`: High-specificity, very explicit selectors. Overrides and helper
  classes (e.g. `.u-hidden {}`).

Following this structure allows you to intersperse inuitcss’ code with your own, so that your `main.scss` file might look something like this:

```scss
// SETTINGS
@import "settings/settings.config";
@import "node_modules/inuitcss/settings/settings.core";
@import "settings/settings.global";
@import "settings/settings.colors";

// TOOLS
@import "node_modules/inuitcss/tools/tools.font-size";
@import "node_modules/inuitcss/tools/tools.clearfix";
@import "node_modules/sass-mq/mq";
@import "tools/tools.aliases";

// GENERIC
@import "node_modules/inuitcss/generic/generic.box-sizing";
@import "node_modules/inuitcss/generic/generic.normalize";
@import "node_modules/inuitcss/generic/generic.shared";

// ELEMENTS
@import "node_modules/inuitcss/elements/elements.page";
@import "node_modules/inuitcss/elements/elements.headings";
@import "elements/elements.links";
@import "elements/elements.quotes";

// OBJECTS
@import "node_modules/inuitcss/objects/objects.layout";
@import "node_modules/inuitcss/objects/objects.media";
@import "node_modules/inuitcss/objects/objects.flag";
@import "node_modules/inuitcss/objects/objects.list-bare";
@import "node_modules/inuitcss/objects/objects.list-inline";
@import "node_modules/inuitcss/objects/objects.box";
@import "node_modules/inuitcss/objects/objects.block";
@import "node_modules/inuitcss/objects/objects.tables";

// COMPONENTS
@import "components/components.buttons";
@import "components/components.page-head";
@import "components/components.page-foot";
@import "components/components.site-nav";
@import "components/components.ads";
@import "components/components.promo";

// UTILITIES
@import "node_modules/inuitcss/utilities/utilities.widths";
@import "node_modules/inuitcss/utilities/utilities.headings";
@import "node_modules/inuitcss/utilities/utilities.spacing";
```

**NOTE:** Every `@import` above which begins with "node_modules" is inuitcss core. When you installed inuitcss via bower, these imports would begin with "bower_components".

Having your own and inuitcss’ partials interlaced like this is one of the real strengths of inuitcss.

## Responsive

inuitcss is built with as much extensibility as possible in mind. Adding full responsive functionality for every kind of module would pretty much kill the intended generic concept behind the framework.

The one opinionated decision we made was adding [Sass-MQ](https://github.com/sass-mq/sass-mq) as a dependency, to provide at least a full working responsive grid off-the-shelf. So if you need media-query support in your own Sass code, have a look at the [Sass-MQ documentation on how to use it](https://github.com/sass-mq/sass-mq#how-to-use-it) properly.

**NOTE: If you've installed inuitcss neither with npm nor with bower, make sure that Sass-MQ is properly imported in your `main.scss` in the tools layer.**

If you want to use another media-query library like [@include-media](http://include-media.com/) or [sass-mediaqueries](https://github.com/paranoida/sass-mediaqueries), feel free to do so. But in this case you have to manage your [responsive widths classes](https://github.com/inuitcss/inuitcss/blob/develop/utilities/_utilities.widths.scss) yourself.
