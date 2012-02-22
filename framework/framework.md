!SLIDE

# Framework #

!SLIDE small

# Models #
* Synchonization with the Backend
* Computed Values
* Logic
* Model#fetch
* Model#save
* Model#destroy
* Model#validate

!SLIDE smaller

# Models #

    @@@ javascript
    var Timesheet.Models.Task = Backbone.Model.extend({
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
        else if (time < 8)
          return 'incomplete';
        else
          return 'due';
      }
    });


!SLIDE

# Collections #
* Collection#url
* Collection#model
* Collection#fetch
* Collection#reset

!SLIDE smaller

# Collections #

    @@@ javascript
    var Timesheet.Collections.Tasks = Backbone.Collection.extend({
      model: Timesheet.Models.Task,

      url: '/tasks',

      completedOn: function(date) {
        this.filter(function(model) {
          return !model.isNew();
        });
      }
    });

!SLIDE

# Views #
* DOM/HTML 
* CSS
* View#el
* View#template
* View#render
* View#$

!SLIDE smaller

# Views #

    @@@ javascript
    var Timesheet.Views.StatusPanel = Backbone.View.extend({
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

# Views as Presenters #
* Transitions
* Interacting with Models
* Handling Events

!SLIDE smaller

# Views as Presenters #
    @@@ javascript
    var Timesheet.Views.StatusPanel = Backbone.View.extend({
      events: {
        "click .button": "updateStatus"
      },

      initialize: function() {
        this.model.bind('change', this.updateStatus, this);
      },

      updateStatus: function() {
        var message = this.model.get('status');
        var dialog = new Timesheet.Views.ModalDialog();
        dialog.render();
        dialog.showMessage(message);
      }
    });


!SLIDE

# Routers #
* Bookmarkable URLs
* History
* Handling Application State

!SLIDE smaller

# Routers #

    @@@ javascript
    var Timesheet.Routers.TasksRouter = Backbone.Router.extend({
      routes: {
        "tasks": "index",       // #tasks
        "tasks/:date": "show"   // #tasks/2012-01-15
      },

      index: function() {
        // Invoke a method on a view object to show something
      },

      show: function(date) {
        // Invoke a method on a view object to show something
      }
    });

!SLIDE

# Events #
* change
* change:property
* add
* destroy

!SLIDE smaller

# Events #

    @@@javascript
    this.model.bind('change', myFunction);

    this.model.bind('change:time', myFunction);

    this.collection.bind('add', myFunction);

    this.model.bind('destroy', myFunction);

!SLIDE

# Custom Events #

    @@@javascript
    // In a view
    this.model.bind('email:sent', myFunction);

    // In the model
    this.trigger('email:sent');

