---
title: Nightwatch Test Environments 
description: Learn how to define, manage, & better large-scale projects with multiple test environments in Nightwatch.
summary_image: https://nightwatchjs.org/img/banner.png
---

<div class="page-header"><h2>Test Environments</h2></div>

### Overview

Nightwatch provides `test environments` to maintain a better structure of configuration for large-scale projects.

You can define multiple sections (environments) under the `test_settings` dictionary so you could overwrite specific values per environment.

<p class="alert alert-info">A "default" environment is required. All the other environments are inheriting from default and can overwrite settings as needed.</p>

An environment inherits all the base settings and all the settings defined under the "default" environment.

### Example

In the example below, there are two environments: 
- `default` (always required)
- `integration`

<div class="sample-test">
<i>nightwatch.json</i><pre data-language="javascript"><code class="language-javascript">{
  "src_folders": ["./tests"],

  "test_settings" : {
    "default" : {
      "launch_url" : "http://localhost",
      "globals" : {
        "myGlobalVar" : "some value",
        "otherGlobal" : "some other value"
      }
    },
    "integration" : {
      "launch_url" : "http://staging.host",
      "globals" : {
        "myGlobalVar" : "other value"
      }
    }
  }
}</code></pre></div>

<br>

### Usage
Test environments can be referenced by its key in the command-line test runner, as the  <code>--env</code> argument:

<pre><code class="language-bash">nightwatch --env integration</code></pre>

This can be useful if you need to have different settings for your local machine and the Continuous Integration server.

### Built-in environments
The configuration file which is auto-generated by Nightwatch (`nightwatch.conf.js`) contains several pre-defined test environments for running tests against several browsers (Firefox, Chrome, Edge, Safari), and also for running tests using Selenium Server or popular cloud testing providers Browserstack and Saucelabs.

Here’s an extract from the `nightwatch.conf.js` config file available as part of the <a href="https://github.com/nightwatchjs/nightwatch-examples/">nightwatch-examples</a> project on Github:

<div class="sample-test"><a href="https://github.com/nightwatchjs/nightwatch-examples/blob/main/nightwatch.conf.js"><i>github.com/nightwatchjs/nightwatch-examples/.../nightwatch.conf.js</i></a>

<pre class="line-numbers language-javascript"><code class="language-javascript">module.exports = {
  src_folders: ['tests'],

  test_settings: {
    default: {
      webdriver: {
        start_process: true,
        server_path: ''
      }
    },

    safari: {
      desiredCapabilities : {
        browserName : 'safari',
        alwaysMatch: {
          acceptInsecureCerts: false
        }
      },
      webdriver: {
        port: 4445
      }
    },
    
    firefox: {
      desiredCapabilities : {
        browserName : 'firefox'
      },
      
      webdriver: {
        start_process: true,
        port: 4444
      }
    }
  }
}</code></pre></div>

### Recommended content
 - [Define and use test environments](/guide/running-tests/define-test-environments.html)
