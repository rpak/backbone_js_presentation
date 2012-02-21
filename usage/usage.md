!SLIDE

# Usage

!SLIDE

# Project Structure

!SLIDE

# Namespacing

    @@@ javascript
    window.Timesheet = {
      Models: {},
      Collections: {},
      Views: {},
      Routers: {},
      init: function() {
        Backbone.history.start();
      }
    }

!SLIDE

# Starting the App

    @@@ javascript
    $(document).ready(function() {
      Timesheet.init();
    });


!SLIDE smaller

# Events

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

# jQuery

* View.$
