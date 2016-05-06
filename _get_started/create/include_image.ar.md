---
layout: page
title: تضمين صورة
order: 1
locale: ar
---

يمكن استخدام معظم علامات HTML مباشرةً في AMP HTML، لكن بعض العلامات، مثل علامة `<img>`، يتم استبدالها بمكافئ أو علامات AMP HTML مخصصة محسّنة بعض الشيء (وتم حظر بضع علامات مسببة للأخطاء حظرًا تامًا، انظر [علامات HTML في المواصفة](https://github.com/ampproject/amphtml/blob/master/spec/amp-html-format.md)).

لتوضيح المظهر الذي يمكن أن يبدو عليه الترميز الإضافي، إليك الشفرة المطلوبة لتضمين صورة في الصفحة:

{% highlight html %}
<amp-img src="welcome.jpg" alt="Welcome" height="400" width="800"></amp-img>
{% endhighlight %}

للتعرّف على أسباب إقدامنا على استبدال العلامات، مثل استبدال `<img>` بـ `<amp-img>`، وكم عدد المتاح منها، يُرجى الانتقال إلى [تضمين إطارات Iframe والوسائط](/docs/guides/amp_replacements.html).

{% include button.html title="المتابعة إلى الخطوة 3" link="/docs/get_started/create/presentation_layout.html" %}
