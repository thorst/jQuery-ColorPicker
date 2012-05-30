Color Picker
==============

Branch of http://www.eyecon.ro/colorpicker/

##Instructions-##

Download package. If you would like examples they are in the original zip. The files that are in my package are the only ones I cared about. See original website for more information.

##History-##

I did quite a bit of research several months ago and liked eyecon's color picker the best. During implementation I hit a couple of snags. I modified it to suite my needs.


##Change Summary-##

1. I've added an X icon for submit instead of the color pinwheel. The pinwheel is still included, so you can swap it back in via css. In my case I wanted the submit button to undo the changes. This way the user isn't forced into choosing a color.

2. I've added the element being returned on onShow, onChange, and onHide instead of just onSubmit. This allows you to bind to a class or multiple elements. Instead of just one id.

3. I've added a fix for when simply click on a color or hue. Previously you needed to click hold and drag to get a color you desired. This is documented in the comments of this thread: http://stackoverflow.com/questions/5717037/eyecon-colorpicker-color-not-changing-in-click-event

##My Code Changes-##
###change function###
   
**Changed to have apply:**

    cal.data('colorpicker').onChange.apply(cal, [col, HSBToHex(col), HSBToRGB(col)]);

**Return the element as well**

    cal.data('colorpicker').onChange.apply(cal, [col, HSBToHex(col), HSBToRGB(col), cal.data('colorpicker').el]);
 			
**Meaning you need to change your function** 

    $('#colorSelector').ColorPicker({
      onChange: function (hsb, hex, rgb, el) {
      }
    });
                
###show function###
**Changed to have apply:**

    if (cal.data('colorpicker').onShow.apply(this, [cal.get(0)]) != false) {
      cal.show();
    }

**Return the element as well**

    if (cal.data('colorpicker').onShow.apply(this, [cal.get(0), cal.data('colorpicker').el]) != false) {
      cal.show();
    }


###hide function###
**Changed to have apply:**

    if (!isChildOf(ev.data.cal.get(0), ev.target, ev.data.cal.get(0))) {
      if (ev.data.cal.data('colorpicker').onHide.apply(this, [ev.data.cal.get(0)]) != false) {
        ev.data.cal.hide();
      }
      $(document).unbind('mousedown', hide);
    }

**Return the element as well**

    if (!isChildOf(ev.data.cal.get(0), ev.target, ev.data.cal.get(0))) {
      if (ev.data.cal.data('colorpicker').onHide.apply(this, [ev.data.cal.get(0), ev.data.cal.data('colorpicker').el]) != false) {
        ev.data.cal.hide();
      }
      $(document).unbind('mousedown', hide);
    }

###uphue function###
**added:**

moveHue(ev);

###upSelector function###

**added**

moveSelector(ev);

###Markdown Help:###

http://www.ctrlshift.net/project/markdowneditor/

http://github.github.com/github-flavored-markdown/