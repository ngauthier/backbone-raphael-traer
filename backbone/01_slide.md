!SLIDE
# Backbone
* Models
* Views
* Collections
* Router
* Whole library

!SLIDE execute
# Model Event

    @@@ javascript
    var m = new Backbone.Model({
      value: 10
    });
    m.on('change:value', function(m) {
      alert(m.get('value'));
    });
    m.set({value: 20});

!SLIDE execute
# View binding
    @@@ javascript
    var m = new Backbone.Model({value: 10});
    var v = new (Backbone.View.extend({
      initialize: function() {
        this.model.on('change', this.render, this);
      },
      render: function() {
        this.$el.html(this.model.get('value'));
        return this;
      }
    }))({model: m});
    $('#backbone-view-binding').append(v.render().el);
    setTimeout(function() {m.set({value: 20})}, 1000);
<p id='backbone-view-binding'></p>

!SLIDE
# Raphael View
    @@@ javascript
    render: function() {
      if (this.raphEl) this.raphEl.remove();
      this.paper = this.paper || Raphael(this.el);
      this.raphEl = this.paper.circle(
        25, 25, this.model.get('value')
      );
      return this;
    }

<script>
    var m = new Backbone.Model({value: 10});
    var v = new (Backbone.View.extend({
      initialize: function() {
        this.model.on('change', this.render, this);
      },
      render: function() {
        if (this.raphEl) this.raphEl.remove();
        this.paper = this.paper || Raphael(this.el);
        this.raphEl = this.paper.circle(
          25, 25, this.model.get('value')
        );
        return this;
      }
    }))({model: m});
    $('#raphael-view').append(v.render().el);
    setTimeout(function() {m.set({value: 20})}, 1000);
</script>
<p id='raphael-view'></p>

!SLIDE
# Collections
    @@@ javascript
    var collection = new Backbone.Collection({
      {value: 10},
      {value: 20}
    });
    collection.each(function(model) {
      var view = new ModelView({model: model});
      $('body').append(view.render().el);
    });

!SLIDE
# Enough Backbone for now
