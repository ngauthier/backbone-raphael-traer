!SLIDE execute
# Raphael
    @@@ javascript
    var paper = Raphael('raphael-circle')
    paper.circle(500,50,30);
<div id='raphael-circle'></div>

!SLIDE execute
# Dom Events
    @@@ javascript
    var paper = Raphael('raphael-circle-event')
    var circle = paper.circle(500,50,30);
    circle.attr({fill: 'white'});
    $(circle.node).bind('click', function() {
      circle.attr({fill: 'red'});
    });
<div id='raphael-circle-event'></div>

!SLIDE
# Lots more
## [raphaeljs.com](http://raphaeljs.com)
