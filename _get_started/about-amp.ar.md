---
layout: page
title: ما المقصود بـ AMP؟
order: 0
locale: ar
---
<amp-youtube
    data-videoid="lBTCB7yLs8Y"
    layout="responsive"
    width="480" height="270">
</amp-youtube>

AMP هي وسيلة لإنشاء صفحات الويب للمحتوى الثابت الذي يتميز بسرعة العرض.
تتألف AMP عند التطبيق من ثلاثة أجزاء مختلفة:

{% include toc.html %}

**AMP HTML** هو HTML مع بعض القيود لإتاحة أداء موثوق به
وبعض الإضافات لإنشاء محتوى منسّق خارج نطاق HTML الأساسي.
تضمن مكتبة **AMP JS** العرض السريع لصفحات AMP HTML.
تعرض **Google AMP Cache** (اختياريًا) صفحات AMP HTML.

## AMP HTML

AMP HTML هو HTML الأساسي مع توسيعه بخصائص AMP المخصصة.
يشبه أبسط ملف AMP HTML هذا:

{% highlight html %}
<!doctype html>
<html ⚡>
 <head>
   <meta charset="utf-8">
   <link rel="canonical" href="hello-world.html">
   <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
   <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
   <script async src="https://cdn.ampproject.org/v0.js"></script>
 </head>
 <body>Hello World!</body>
</html>
{% endhighlight %}

بالرغم من أن غالبية العلامات في صفحة AMP HTML تمثل علامات HTML العادية،
لكنّ بعض علامات HTML يتم استبدالها بعلامات مخصصة لـ AMP (انظر أيضًا
[علامات HTML في مواصفات AMP](https://github.com/ampproject/amphtml/blob/master/spec/amp-html-format.md)).
هذه العناصر المخصصة، التي يُطلق عليها اسم مكونات AMP HTML،
تسهّل تنفيذ الأنماط الشائعة بطريقة فائقة الأداء.

على سبيل المثال، توفر العلامة [`amp-img`](/docs/reference/amp-img.html)
الدعم الكامل لـ `srcset` حتى في المتصفحات التي لا تدعمها حتى الآن.
تعرّف على كيفية [إنشاء صفحة AMP HTML الأولى لك](/docs/get_started/create_page.html).

## AMP JS

تنفّذ [مكتبة AMP JS](https://github.com/ampproject/amphtml/tree/master/src) كلاً من
[أفضل ممارسات الأداء لـ AMP](/docs/get_started/technical_overview.html)،
وتدير تحميل الموارد، وتمنحك العلامات المخصصة المذكورة أعلاه،
وهذا كله بغرض ضمان العرض السريع لصفحتك.

ومن بين أكبر التحسينات أنها تجعل كلّ ما يكون مصدره الموارد الخارجية غير متزامن؛ وبذلك لا يعيق أيُّ مكون في الصفحة عرض أيٍ من عناصرها.

كذلك، فمن بين تقنيات الأداء الأخرى توفير وضع الحماية لإطارات iframe كلها، والحساب المسبق لتنسيق كل عنصر في الصفحة قبل تحميل الموارد، وتعطيل محدّدات CSS البطيئة.

للتعرّف على المزيد بشأن [التحسينات](/docs/get_started/technical_overview.html) والقيود كذلك، [اقرأ مواصفات AMP HTML](https://github.com/ampproject/amphtml/blob/master/spec/amp-html-format.md).

## Google AMP Cache

Google AMP Cache هي شبكة عرض محتوى تستند إلى خادم وكيل
لعرض كل مستندات AMP الصالحة.
فهي تجلب صفحات AMP HTML وتخزّنها في الذاكرة مؤقتًا، وتحسّن أداء الصفحة تلقائيًا.
عند استخدام Google AMP Cache، يتم تحميل المستند وكل ملفات JS وكل الصور
من الأصل نفسه الذي يستخدم
[HTTP 2.0](https://http2.github.io/) لتوفير أقصى حد من الفاعلية.

كذلك تأتي ذاكرة التخزين المؤقت مزوّدة
[بنظام تحقق من الصحة](https://github.com/ampproject/amphtml/tree/master/validator)
مدمج لتأكيد ضمان تشغيل الصفحة،
وعدم استنادها إلى موارد خارجية.
ينفّذ نظام التحقق من الصحة سلسلة من التأكيدات
التي تؤكد توافق ترميز الصفحة مع مواصفات AMP HTML.

وهناك إصدار آخر من أداة التحقق من الصحة يأتي مرفقًا بكل صفحة AMP. هذا الإصدار يمكنه تسجيل أخطاء التحقق من الصحة مباشرةً في وحدة التحكم بالمتصفح عند عرض الصفحة،
مما يتيح لك مشاهدة كيف قد تؤثر التغييرات المعقّدة في نصك البرمجي
على الأداء وانطباع المستخدم.

تعرّف على المزيد بشأن [اختبار صفحات AMP HTML](/docs/guides/validate.html).
