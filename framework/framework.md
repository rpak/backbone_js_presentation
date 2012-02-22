!SLIDE

# Framework #

!SLIDE

# What is Backbone JS?#
* A client-side MVC framework
* Introduces structure to your JS codebase
* Server-side synchronization
* Current Version 0.9.1

!SLIDE small

# Models #
* Domain Logic
* Computed Values
* Default Values
* Server-side synchronization
* \#fetch, \#save, \#destroy, \#validate

!SLIDE smaller

# Models #

    @@@ javascript
    Timesheet.Models.Task = Backbone.Model.extend({
      defaults: {
        completed_on: Date.today().toDateString(),
        time: 0
      },

      initialize: function(attributes) {
        this.set({time: parseFloat(attributes.time)});
      },
      
      status: function() {
        var time = this.get('time');
        if (time >= 8)
          return 'complete';
        else
          return 'incomplete';
      }
    });


!SLIDE

# Collections #
* Aggregates Models
* Maintains Ordering
* \#url, \#model, \#fetch, \#reset

!SLIDE smaller

# Collections #

    @@@ javascript
    Timesheet.Collections.Tasks = Backbone.Collection.extend({
      url: '/tasks',

      model: Timesheet.Models.Task,

      completed: function() {
        return this.filter(function(model) {
          return model.completed();
        });
      }
    });

!SLIDE

# Views #
* DOM/HTML 
* Controllers
* \#el, \#template, \#render, \#$, \#events

!SLIDE smaller

# Views #

    @@@ javascript
    Timesheet.Views.StatusPanel = Backbone.View.extend({
      // el: '.app',
      // tagName: 'p',
      className: 'StatusPanel',

      template: function() {
        return "<span>hello</span>";
      },

      render: function() {
        var markup = this.template();
        this.$(this.el).html(markup);
        return this;
      }
    });

!SLIDE

# Views #

    @@@ html
    <div class="StatusPanel">
      <span>hello</span>
    </div>

!SLIDE

# Views as Controllers #
* Interacts with Models
* Observes Model Events
* Handles DOM Events
* Transitions to other Views

!SLIDE smaller

# Views as Controllers #
    @@@ javascript
    Timesheet.Views.StatusPanel = Backbone.View.extend({
      events: {
        "click .button": "updateStatus"
      },

      initialize: function() {
        this.model.bind('change', this.updateStatus, this);
      },

      updateStatus: function() {
        var message = this.model.get('status');
        var dialog = new Timesheet.Views.ModalDialog(message);
        dialog.render();
      }
    });
    var model = new Timesheet.Models.Task();
    var view = new Timesheet.Views.StatusPanel({model: model});

!SLIDE

# Routers #
* Bookmarkable URLs
* History / Back Button
* Handling Application State

!SLIDE smaller

# Routers #

    @@@ javascript
    Timesheet.Routers.TasksRouter = Backbone.Router.extend({
      routes: {
        "tasks": "index",       // #tasks
        "tasks/:date": "show"   // #tasks/2012-01-15
      },

      index: function() {
      },

      show: function(date) {
      }
    });

!SLIDE

# Events #
* change
* change:property
* add (Collection Only)
* destroy

!SLIDE smaller

# Events #

    @@@javascript
    // '#on' is an alias for '#bind'

    this.model.bind('change', myFunction);

    this.model.bind('change:time', myFunction);

    this.collection.bind('add', myFunction);

    this.model.bind('destroy', myFunction, this);

!SLIDE smaller

# Custom Events #

    @@@javascript
    // In a view
    this.model.bind('email:sent', showNotice, this);

    // In the model
    this.trigger('email:sent');

