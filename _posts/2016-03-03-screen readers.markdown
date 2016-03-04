---
layout: post
title:  "Screen readers"
date:   2016-03-04 16:17:52 -0600
categories: nvda jaws screenreaders
author:	"James Setaro"
---

Chrome has interesting issues right now with JAWS and NVDA.  Here are a couple of observations. We have really been pushing to offer better support for our Chrome screen reader and AT users.


Here is how we normally structure our content
{% highlight html %}
<label class="radio">
	<div class="int-choice-control"><input type="radio" name="group_RESPONSE2" value="ChoiceB"/></div>
	<div class="int-choice-label">B</div>
	<div class="int-choice-desc"><span><img src="http://test86-tn8.pearsontestcontent.com/refqc/6f31fd123f608529c7c98b00e1dfc377846179cc/360/17213/bluebox.png" alt="blue box" width="88" height="100"></span></div>
</label>

{% endhighlight %}


Better:

{% highlight html %}
    <!--Chrome/NVDA Reads radio button not checked B, then B again, then blue box-->
    <!--Chrome/JAWS Reads radio button not checked B level 0 then B then blue box-->
<label for=ChoiceB class="radio">
	<div class="int-choice-control"><input type="radio" name="group_RESPONSE2" value="ChoiceB"/></div>
	<div class="int-choice-label">B</div>
	<div class="int-choice-desc"><span><img src="http://test86-tn8.pearsontestcontent.com/refqc/6f31fd123f608529c7c98b00e1dfc377846179cc/360/17213/bluebox.png" alt="blue box" width="88" height="100"></span></div>
</label>
{% endhighlight %}

Even Better, but notice level 0 is read JAWS.   

{% highlight html %}

<!--Chrome/NVDA Reads radio button not checked A, then blue box-->
<!--Chrome/JAWS Reads radio button not checked level 0 then A then blue box-->
<!--FF/NVDA Reads radio button not checked then A then blue box-->
<!--FF/JAWS Reads radio button not checked 1 of 3 then A then blue box-->
<div class="int-choice-control">
<input type="radio" name="group_RESPONSE2" value="ChoiceA"/></div>
<label for=ChoiceA class="radio">
<div class="int-choice-label">A</div>
<div class="int-choice-desc">
    <span>
        <img src="http://test86-tn8.pearsontestcontent.com/refqc/6f31fd123f608529c7c98b00e1dfc377846179cc/360/17213/bluebox.png" alt="blue box" width="88" height="100">
    </span>
</div>
</label>

{% endhighlight %}