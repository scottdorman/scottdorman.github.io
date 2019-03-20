---
layout: post
title: Saving Bootstrap component state
date: '2018-08-18 13:22:00 -05:00'
tags: bootstrap
---

Bootstrap is a great front-end UI framework for web development and has a lot of great components. One of those components is the [collapse component](https://getbootstrap.com/docs/4.1/components/collapse/). This allows you to easily toggle the visibility of content on your site. It also allows you to make really great [accordion](https://getbootstrap.com/docs/4.1/components/collapse/#accordion-example) style content.

One of the issues with the accordion is that when you navigate to another page and then come back, you're back to the default open panel of the accordion. Sometimes that isn't an issue, but there are times when you want to remember the current state of the accordion and return the user to the same open panel they were on before the page navigation.

A similar issue exists with the [tab control (v3.x)](https://getbootstrap.com/docs/3.3/javascript/#tabs) or the [nav component (v4.x)](https://getbootstrap.com/docs/4.1/components/navs/).

You can easily solve these problems with a small amount of Javascript.

[bootstrapHelpers.js](https://gist.github.com/scottdorman/dbe9cb3494e21dd880cf155a89b24622#file-bootstraphelpers-js)

```javascript
function restoreAccordionPanel(storageKey, accordionId) {
    var activeItem = localStorage.getItem(storageKey);
    if (activeItem) {
        //remove default collapse settings
        $(accordionId + " .panel-collapse").removeClass('in');

        //show the account_last visible group
        $("#" + activeItem).addClass("in");
    }
}

function restoreActiveTab(storageKey, tabId) {
    var activeItem = localStorage.getItem(storageKey);
    if (activeItem) {
        $(tabId + ' a[href="' + activeItem + '"]').tab('show');
    }
}

function saveActiveAccordionPanel(storageKey, e) {
    localStorage.setItem(storageKey, e.target.id);
}

function saveActiveTab(storageKey, e) {
    localStorage.setItem(storageKey, $(e.target).attr('href'));
}
```

This uses the [HTML5 web storage feature](https://www.tutorialrepublic.com/html-tutorial/html5-web-storage.php), specifically the `localstorage`, but you can change this to use whatever storage mechanism you want.

Using these functions is just as simple:

[example.html](https://gist.github.com/scottdorman/dbe9cb3494e21dd880cf155a89b24622#file-example-html)
```html
<!DOCTYPE html>
<html>
  <head>
  <title>Page Title</title>
  </head>
  <body>
  <div class="accordion" id="accordionExample">
    <div class="card">
      <div class="card-header" id="headingOne">
        <h5 class="mb-0">
          <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
          Collapsible Group Item #1
          </button>
        </h5>
      </div>
      <div id="collapseOne" class="collapse show" aria-labelledby="headingOne" data-parent="#accordionExample">
        <div class="card-body">
        Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
        </div>
      </div>
    </div>
    <div class="card">
      <div class="card-header" id="headingTwo">
        <h5 class="mb-0">
          <button class="btn btn-link collapsed" type="button" data-toggle="collapse" data-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
          Collapsible Group Item #2
          </button>
        </h5>
      </div>
      <div id="collapseTwo" class="collapse" aria-labelledby="headingTwo" data-parent="#accordionExample">
        <div class="card-body">
        Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
        </div>
      </div>
    </div>
    <div class="card">
      <div class="card-header" id="headingThree">
        <h5 class="mb-0">
          <button class="btn btn-link collapsed" type="button" data-toggle="collapse" data-target="#collapseThree" aria-expanded="false" aria-controls="collapseThree">
            Collapsible Group Item #3
          </button>
        </h5>
      </div>
      <div id="collapseThree" class="collapse" aria-labelledby="headingThree" data-parent="#accordionExample">
        <div class="card-body">
          Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
        </div>
      </div>
    </div>
  </div>
    <script>
      $(function () {
        $('#accordion').on('shown.bs.collapse', function (e) {
            saveActiveAccordionPanel('accordion-activePanel', e);
        })        
      )};
      restoreAccordionPanel('accordion-activePanel', '#accordion');
    </script>
  </body>
</html>
```
