---
layout: page
title: "JavaScript forward_static_call function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/forward_static_call:861
- /functions/view/forward_static_call
- /functions/view/861
- /functions/forward_static_call:861
- /functions/861
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's forward_static_call

{% codeblock funchand/forward_static_call.js lang:js https://raw.github.com/kvz/phpjs/master/functions/funchand/forward_static_call.js raw on github %}
function forward_static_call (cb, parameters) {
  // http://kevin.vanzonneveld.net
  // +   original by: Brett Zamir (http://brett-zamir.me)
  // %          note 1: No real relevance to late static binding here; might also use call_user_func()
  // *     example 1: forward_static_call('isNaN', 'a');
  // *     returns 1: true

  var func;

  if (typeof cb === 'string') {
    if (typeof this[cb] === 'function') {
      func = this[cb];
    } else {
      func = (new Function(null, 'return ' + cb))();
    }
  }
  else if (Object.prototype.toString.call(cb) === '[object Array]') {
    func = eval(cb[0] + "['" + cb[1] + "']");
  }

  if (typeof func !== 'function') {
    throw new Error(func + ' is not a valid function');
  }

  return func.apply(null, Array.prototype.slice.call(arguments, 1));
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/funchand/forward_static_call.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/funchand/forward_static_call.js)

### Example 1
This code
{% codeblock lang:js example %}
forward_static_call('isNaN', 'a');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
true
{% endcodeblock %}


### Other PHP functions in the funchand extension
{% render_partial _includes/custom/funchand.html %}
