!SLIDE

# Usage #

!SLIDE

# Project Structure #

!SLIDE smaller

# Namespacing #

    @@@ javascript
    window.Timesheet = {
      Models: {},
      Collections: {},
      Views: {},
      Routers: {},
      init: function() {
        Backbone.history.start();
        var statusPanel = new Timesheet.Views.StatusPanel();
        statusPanel.render();
      }
    }

!SLIDE

# Starting the App #

    @@@ javascript
    $(document).ready(function() {
      Timesheet.init();
    });


!SLIDE smaller

# Events #

    @@@ javascript
    var Timesheet.Views.StatusPanel = Backbone.View.extend({
      events: {
        "click .button": "updateStatus"
      },

      initialize: function() {
        this.model.bind('change', this.updateStatus, this);
      },

      updateStatus: function() {
        alert("status updated!");
      }

    });

!SLIDE

# Fat Views #

* Composite View Objects
* Sub-views

!SLIDE
![Layout Example](Layout.001.png)

!SLIDE

# Testing #

* Jasmine
* Jasmine jQuery
