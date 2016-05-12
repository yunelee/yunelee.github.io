---
layout: page
title: تحضير صفحتك للاكتشاف والتوزيع
order: 4
locale: ar
---

في بعض الحالات، قد تحتاج إلى امتلاك إصدار تابع لـ AMP وآخر غير تابع لها من الصفحة، مثل مقالة إخبارية. ضع هذا في حسبانك: إذا عثر بحث Google على الإصدار غير التابع لـ AMP من تلك الصفحة، *فكيف يعرف بوجود إصدار تابع لـ AMP منها*؟

## ربط الصفحات بـ &lt;link>

لحل هذه المشكلة، نضيف المعلومات بشأن صفحة AMP إلى الصفحة غير التابعة لـ AMP، والعكس صحيح، في شكل علامات `<link>` في `<head>`.

أضف ما يلي إلى الصفحة غير التابعة لـ AMP:

{% highlight html %}
<link rel="amphtml" href="https://www.example.com/url/to/amp/document.html">
{% endhighlight %}

وهذا لصفحة AMP

{% highlight html %}
<link rel="canonical" href="https://www.example.com/url/to/full/document.html">
{% endhighlight %}

## ماذا إن كان المتوفر لدي صفحة واحدة فقط؟

إذا كانت لديك صفحة واحدة فقط، وكانت هذه الصفحة صفحة AMP، يجب عليك مع ذلك إضافة رابط متعارف عليه إليها، وهو ما يجعلها ببساطة تشير إلى نفسها:

{% highlight html %}
<link rel="canonical" href="https://www.example.com/url/to/amp/document.html">
{% endhighlight %}

{% include button.html title="المتابعة إلى الخطوة 6" link="/docs/get_started/create/publish.html" %}
