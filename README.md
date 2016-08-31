# Grav Tag Cloud Plugin

The **Tagcloud** Plugin is for [Grav CMS](http://github.com/getgrav/grav). It creates a rudimentary tag cloud that can be easily styled to fit your needs.

# Installation

Installing the Tag Cloud plugin can be done in one of two ways. The GPM (Grav Package Manager) installation method enables you to quickly and easily install the plugin with a simple terminal command, while the manual method enables you to do so via a zip file.

## GPM Installation (Preferred)

The simplest way to install this plugin is via the [Grav Package Manager (GPM)](http://learn.getgrav.org/advanced/grav-gpm) through your system's terminal (also called the command line).  From the root of your Grav install type:

    bin/gpm install tagcloud

This will install the Tag Cloud plugin into your `/user/plugins` directory within Grav. Its files can be found under `/your/site/grav/user/plugins/tagcloud`.

## Manual Installation

To install this plugin, just download the zip version of this repository and unzip it under `/your/site/grav/user/plugins`. Then, rename the folder to `tagcloud`. You can find these files either on [GitHub](https://github.com/getgrav/grav-plugin-taxonomylist) or via [GetGrav.org](http://getgrav.org/downloads/plugins#extras).

You should now have all the plugin files under

    /your/site/grav/user/plugins/tagcloud
	
>> NOTE: This plugin is a modular component for Grav which requires [Grav](http://github.com/getgrav/grav), the [Error](https://github.com/getgrav/grav-plugin-error), [Problems](https://github.com/getgrav/grav-plugin-problems) and [Taxonomy List](https://github.com/getgrav/grav-plugin-taxonomylist) plugins, and a theme to be installed in order to operate.

# Usage

To use `tagcloud` you need to set your pages header with at least a taxonomy tag:

```
taxonomy:
    tag: [tag1, tag2]
```

You will also need to do the following:

  - Copy the `tagcloud.html.twig` file from the plugin folder to your theme and adjust as you see fit.
  - `include` the twig file somewhere in your theme skeleton (usually in `sidebar.html.twig`) along the following lines:
    ```
    {% if config.plugins.tagcloud.enabled %}
      <aside class="widget widget_meta">
        <h2 class="widget-title">{{config.plugins.tagcloud.title|t}}</h2>
        {% include 'partials/tagcloud.html.twig' %}
        </aside>
    {% endif %}

    ```
  - Copy the contents of the CSS in the `assets` folder of the plugin into your theme and adjust as you see fit.

> Remember that the plugin `taxonomylist` must be installed and enabled!

I recognize that you can configure the PHP file to use the files in the plugin folder, but I can't imagine someone using these files as is. If I'm wrong, let me know and I'll go the PHP file route.

# Config Defaults
```
enabled: true
threshold: 0
title: "POPULAR TAGS"
```
The fields `enabled` and `title` are self-explanatory, but `threshold` takes a little explaining. The tags are sized based on how frequently they appear. This is done by first determining the number of times the *most* frequent tag appears (`max`) and then comparing each tag's count (`count`) against it, forming a percentage: `percent = (count/max) * 100`.

That `percent` number is then compared against the different tiers in the twig file to determine how it should be sized. The `threshold` in the config determines the minimum `percent` a tag must be to even be displayed. A value of 0 shows all tags. A value of 100 only shows the tags whose `counts` equal the `max`. Any value between that will show some subset of your tags. You'll need to do some trial and error to find the right number. It really depends on how many different tags your blog uses.

# Support

This is my very first Grav plugin. I welcome any feedback and pull requests.

