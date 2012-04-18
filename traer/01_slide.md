!SLIDE
# Traer.js
* Based on Jeff Bernstein's lib for Processing
* Particle physics
* Integrator

!SLIDE
# Traer-Backbone Extension
## Particles fire events (like models)
    @@@ javascript
    function Particle(mass) {
      // redacted
      _.extend(this, Backbone.Events);
    }

!SLIDE
# Traer-Backbone Extension
## Every time the integrator computes new state

    @@@ javascript
    RungeKuttaIntegrator.prototype.step = function (deltaT) {
      /* lots of physics stuff redacted */
      p.trigger('change'); // p is the particle
    }

!SLIDE
# Traer-Backbone Model
## Wrap a Prticle
    @@@ javascript
    Node = Backbone.Model.extend({
      initialize: function(attributes) {
        // when the particle changes, we fire a change
        this.get('particle').on('change', function() {
          this.trigger('change'); 
        }, this);
        this.children = new NodeList();
      },
      // proxy some particle attributes
      x:    function() { return this.get('particle').position.x; },
      y:    function() { return this.get('particle').position.y; },
    });

!SLIDE
# Traer-Backbone Model
## Create children
    @@@ javascript
    createChild: function() {
      var mass = 0.4;
      var x = this.x() + Math.random() * 50 - 25;
      var y = this.y() + Math.random() * 50 - 25;
      var particle = traer.makeParticle(mass, x, y, 0);
      var node = new Node({particle: particle, size: 10});
      this.children.add(node);
      var spring = 0.02;
      var damping = 0.10;
      var length = 120;
      traer.makeSpring(
        this.particle(), node.particle(),
        spring, damping, length
      );
      // cont
    },

!SLIDE
# Traer-Backbone Model
## Propagate forces
    @@@ javascript
    // cont
    this.trigger('child', node);
    node.on('child', this.link, this);
    node.on('child', function(child) {
      this.trigger('child', child);
    }, this);

!SLIDE
# Demo
* [http://ngauthier.com/demo/backbone-raphael-traer](http://ngauthier.com/demo/backbone-raphael-traer)
