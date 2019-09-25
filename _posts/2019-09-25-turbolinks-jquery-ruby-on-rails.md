---
title: "Solving the jQuery/Materialize problem with Turbolinks under Ruby On Rails"
published: true
---

After spending countless hours trying to make JavaScript/CoffeeScript work under Turbolinks, here's my solution to add JavaScript code (with Materialize components) that gets executed every time the page is loaded. Since maybe there's more people out there using Ruby on Rails with Materialize too, the following examples will show how to initialize and destroy Materialized components, but this solution also applies to the use of JQuery under Turbolinks.

```coffeescript
$(document).on 'turbolinks:load', ->
  # Setup sidenav
  $('.sidenav').sidenav()

  return
```

```coffeescript
$(document).on 'turbolinks:before-cache', ->
  # Destroy sidenav
  sidenav = $('.sidenav')
  sidenavInstance = M.Sidenav.getInstance(sidenav)
  sidenavInstance.destroy()

  return
```
So what this CoffeeScript snippet does is set a listener for when turbolinks loads the page (what in vanilla HTML/JS would be the 'onload' event of the window). The second part is only required while using Materialized component system.
