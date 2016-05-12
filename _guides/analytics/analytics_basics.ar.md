---
layout: page
title: Analytics&#58; الأساسيات
order: 0
locale: ar
---

ابدأ من هنا للتعرّف على أساسيات تحليلات AMP.

{% include toc.html %}

## هل تستخدم amp-pixel أو amp-analytics؟

توفر AMP مكونين للوفاء باحتياجاتك بخصوص التحليلات والقياس:
[amp-pixel](/docs/reference/amp-pixel.html) وأيضًا 
[amp-analytics](/docs/reference/extended/amp-analytics.html).
يرسل كلّ من الخيارين بيانات التحليلات إلى نقطة نهائية محددة.

إذا كنت بصدد البحث عن أداء، مثل 
[بكسل التتبع](https://en.wikipedia.org/wiki/Web_beacon#Implementation) البسيط،
فإن المكون `amp-pixel` يوفر تتبع عرض صفحة أساسية،
ويتم إرسال بيانات مشاهدة الصفحة إلى عنوان URL محدّد.
بعض عمليات الدمج مع المورّد قد تتطلب هذا المكون،
وفي هذه الحالة سوف تحدد هي النقطة النهائية الدقيقة لعنوان URL. 

بالنسبة لغالبية حلول التحليلات، استخدم `amp-analytics`.
يعمل تتبع مشاهدة الصفحة في `amp-analytics` أيضًا.
لكن يمكنك كذلك تتبع تفاعل المستخدم مع أي نوع من أنواع محتوى الصفحة،
بما في ذلك النقرات على الروابط والأزرار.
ويمكنك قياس لأي مدى قام المستخدم بالتمرير عبر الصفحة،
وما إذا كان المستخدم متفاعلاً مع الشبكات الاجتماعية أم لا، والمزيد
(انظر
[نظرة عميقة على AMP Analytics](/docs/guides/analytics/deep_dive_analytics.html)).

كجزء من الدمج مع النظام الأساسي لـ AMP،
قدم المزودون تهيئات `amp-analytics` مسبقة التحديد
لكي يسهُل التقاط البيانات ودفعها إلى أدوات التتبع لديهم.
يمكنك الوصول إلى مستندات المورّد من
[مواصفة amp-analytics](/docs/reference/extended/amp-analytics.html).

يمكنك استخدام كلّ من `amp-pixel` و`amp-analytics` في صفحاتك:
`amp-pixel` لتتبع عرض صفحات يتسم بالبساطة،
و`amp-analytics` لكل الميزات الأخرى.
يمكنك أيضًا إضافة مضاعفات كل علامة.
إذا كنت بصدد العمل مع مزوّدي تحليلات عديدين،
فسوف تحتاج إلى علامة واحدة لكل حل.
ضع في اعتبارك أنه كلما كانت صفحات AMP أكثر بساطة، كان ذلك أفضل للمستخدمين،
ولهذا إذا كنت لا تحتاج علامات إضافية، فلا تستخدمها.

## إنشاء تهيئة تحليلات بسيطة

تعرّف على كيفية إنشاء تهيئة تحليلات
[amp-pixel](/docs/reference/amp-pixel.html) و
[amp-analytics](/docs/reference/extended/amp-analytics.html) بسيطة.

### تهيئة amp-pixel بسيطة

لإنشاء تهيئة `amp-pixel` بسيطة،
أدرج شيئًا ما، مثل ما يلي، في نص صفحتك في AMP:

{% highlight html %}
<amp-pixel src="https://foo.com/pixel?RANDOM"></amp-pixel>
{% endhighlight %}

في هذا النموذج،
يتم إرسال بيانات مشاهدة الصفحة إلى عنوان URL محدد مع رقم عشوائي.
المتغير `RANDOM` هو واحد من كثير من
[متغيرات الاستبدال في النظام الأساسي لـ AMP](https://github.com/ampproject/amphtml/blob/master/spec/amp-var-substitutions.md).
تعرّف على المزيد بشأن 
[استبدال المتغير](/docs/guides/analytics/analytics_basics.html#variable-substitution) هنا.

يتسم المكون [amp-pixel](/docs/reference/amp-pixel.html)
بأنه مدمج،
وبذلك لن تحتاج إلى تصريح تضمين، مثل ما تفعله
لمكونات AMP الموسّعة، بما في ذلك `amp-analytics`.
لكن عليك وضع العلامة `amp-pixel` في أقرب موضع ممكن
من بداية `<body>`.
لن يتم تنشيط بكسل التتبع إلا عند إظهار العلامة لنفسها.
إذا كان موضع `amp-pixel` قريبًا من أسفل الصفحة،
فقد لا يتم تنشيطه.

### تهيئة amp-analytics بسيطة

لإنشاء تهيئة
[amp-analytics](/docs/reference/extended/amp-analytics.html) بسيطة،
يجب عليك تضمين هذا التصريح بشأن `custom-element`
في `<head>` لمستند AMP (انظر أيضًا
[تصريح بشأن تضمين مكون](/docs/reference/extended.html#component-inclusion-declaration)):

{% highlight html %}
<script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
{% endhighlight %}

النموذج التالي مشابه [للنموذج `amp-pixel`](/docs/guides/analytics/analytics_basics.html#simple-amp-pixel-configuration).
كلما تكون صفحة ما مرئية،
يتم تنشيط حدث المشغل ويتم إرسال
بيانات مشاهدة الصفحة إلى عنوان URL محدد مع معرّف عشوائي: 

{% highlight html %}
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "pageview": "https://foo.com/pixel?RANDOM",
  },
  "triggers": {
    "trackPageview": {
      "on": "visible",
      "request": "pageview"
    }
  }
}
</script>
</amp-analytics>
{% endhighlight %}

في النموذج أعلاه، حددنا طلبًا يُسمى مشاهدة الصفحة لكي يكون https://foo.com/pixel?RANDOM. كما قلنا في نقاش سابق، يحل رقم عشوائي محل القيمة RANDOM وبذلك سينتهي الحال بالطلب إلى أن يبدو مثل هذا https://foo.com/pixel?0.23479283687235653498734.

عندما تصبح الصفحة مرئية
(على النحو المحدد عبر استخدام الكلمة الرئيسية للمشغل `visible`)،
يتم تشغيل حدث ويتم إرسال الطلب `pageview`.
تحدد السمة triggers متى يتم تنشيط طلب مشاهدة الصفحة.
تعرّف على المزيد بشأن السمتين [requests وtriggers](/docs/guides/analytics/deep_dive_analytics.html#requests-triggers--transports).

## استبدال المتغير

يسمح كلّ من المكون [amp-pixel](/docs/reference/amp-pixel.html) وكذلك
[amp-analytics](/docs/reference/extended/amp-analytics.html) بكل
عمليات استبدال متغير عنوان URL القياسية (انظر
[عمليات استبدال متغير AMP HTML](https://github.com/ampproject/amphtml/blob/master/spec/amp-var-substitutions.md)).
في النموذج التالي،
يتم إرسال طلب مشاهدة الصفحة إلى عنوان URL،
مع عنوان URL المتعارف عليه لمستند AMP الحالي، وعنوانه، فضلاً عن
[معرّف العميل](/docs/guides/analytics/analytics_basics.html#user-identification):

{% highlight html %}
<amp-pixel src="https://example.com/analytics?url=${canonicalUrl}&title=${title}&clientId=${clientId(site-user-id)}"></amp-pixel>
{% endhighlight %}

نظرًا لبساطتها،
يمكن للعلامة `amp-pixel` أن تتضمن فقط المتغيرات المحددة بواسطة النظام الأساسي
أو تلك التي يمكن لوقت تشغيل AMP تحليلها من صفحة AMP.
في النموذج أعلاه،
يملأ النظام الأساسي القيم لكل من
`canonicalURL` و`clientId(site-user-id)`.
ويمكن أن تتضمن العلامة `amp-analytics` المتغيرات نفسها، مثل `amp-pixel`،
فضلاً عن المتغيرات ذات التحديد الفريد داخل تهيئة العلامة.

استخدم التنسيق `${varName}` في سلسلة طلب لمتغير محدد بواسطة صفحة
أو نظام أساسي.
سوف تستبدل العلامة `amp-analytics` القالب بقيمته الفعلية
في وقت إنشاء طلب التحليلات (انظر أيضًا
[المتغيرات المدعومة في amp-analytics](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/analytics-vars.md)).

في نموذج `amp-analytics` التالي،
يتم إرسال طلب مشاهدة الصفحة إلى عنوان URL،
مع البيانات الإضافية المستخلصة من عمليات استبدال المتغير،
البعض يوفره النظام الأساسي
والبعض الآخر يتم تحديده بشكل مضمّن،
ضمن التهيئة `amp-analytics`:

{% highlight html %}
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "pageview":"https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}&clientId=${clientId(site-user-id)}",
  },
  "vars": {
    "account": "ABC123",
  },
  "triggers": {
    "someEvent": {
      "on": "visible",
      "request": "pageview",
      "vars": {
        "title": "My homepage",
      }
    }
  }  
}
</script>
</amp-analytics>
{% endhighlight %}

في النموذج أعلاه،
يتم تحديد المتغيرين `account` و`title` في
التهيئة `amp-analytics`.
لا يتم تحديد المتغيرين `canonicalUrl` و`clientId` في التهيئة،
وبذلك يتم استبدال قيمهما عن طريق النظام الأساسي.

**مهم:** يتسم استبدال المتغيرات بالمرونة؛
فمن المكن تحديد المتغيرات نفسها في مواقع مختلفة،
وسوف يحلل وقت تشغيل AMP القيم بهذا الترتيب المستند إلى الأسبقية 
(انظر [ترتيب استبدال المتغير](/docs/guides/analytics/deep_dive_analytics.html#variable-substitution-ordering)).

## هوية المستخدم

تستخدم مواقع الويب ملفات تعريف الارتباط لتخزين المعلومات الخاصة بمستخدم ما في المتصفح.
يمكن استخدام ملفات تعريف الارتباط للإخبار بأن مستخدمًا ما زار موقعًا من قبل.
في AMP،
يمكن عرض الصفحات إما من موقع ويب ناشر، أو من ذاكرة التخزين المؤقت
(مثل Google AMP Cache).
من المرجّح أن يكون لموقع ويب الناشر وذاكرة التخزين المؤقت نطاقات مختلفة.
لأسباب تتعلق بالأمان،
يمكن للمتصفحات (وستفعل غالبًا) تحديد إمكانية الوصول إلى ملفات تعريف الارتباط التابعة للنطاق الآخر
(انظر أيضًا
[تتبع المستخدمين عبر الأصول](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/cross-origin-tracking.md)).

افتراضيًا،
سوف تدير AMP توفير معرّف العميل سواء أكان الوصول إلى الصفحة يتم من موقع الويب الأصلي للناشر أم عبر ذاكرة تخزين مؤقت.
يمتلك معرّف العميل الذي يتم إنشاؤه عبر AMP القيمة `"amp-"`
متبوعةً بسلسلة عشوائية مشفرة بواسطة `base64` ويظل الأمر كذلك
للمستخدم إذا كان المستخدم نفسه يزور الموقع مرة أخرى.

تدير AMP عمليتي القراءة والكتابة لمعرّف العميل في كل الأحوال.
ويكون هذا ملحوظًا بصفة خاصة في حالة عرض الصفحة
عبر ذاكرة تخزين مؤقت أو إظهارها بطريقة أخرى خارج سياق العرض
للموقع الأصلي للناشر.
في هذه الحالة، لا يكون الوصول إلى ملفات تعريف الارتباط التابعة لموقع الناشر متاحًا.

عند عرض صفحة AMP من موقع ناشر،
يمكن الإخبار عن إطار عمل معرّف العميل الذي تستخدمه AMP لملف تعريف ارتباط احتياطي
للبحث عنه واستخدامه.
في هذه الحالة،
يتم تفسير وسيطة `cid-scope-cookie-fallback-name` للمتغير `clientId` بوصفها تمثل
اسم ملف تعريف ارتباط.
قد يظهر التنسيق إما مثل
`CLIENT_ID(cid-scope-cookie-fallback-name)` أو
`${clientId(cid-scope-cookie-fallback-name)}`.

على سبيل المثال:

{% highlight html %}
<amp-pixel src="https://foo.com/pixel?cid=CLIENT_ID(site-user-id-cookie-fallback-name)"></amp-pixel>
{% endhighlight %}

إذا وجدت AMP أن ملف تعريف الارتباط هذا تم تعيينه،
فسوف يعرض استبدال معرّف العميل قيمة ملف تعريف الارتباط.
إذا وجدت AMP أن ملف تعريف الارتباط هذا غير معيّن،
فسوف تنشئ AMP قيمة للنموذج `amp-` متبوعةً
بسلسلة عشوائية مشفرة بواسطة base64.

تعرّف على المزيد بشأن استبدال معرّف العميل،
بما في ذلك كيفية إضافة معرّف إشعار مستخدم اختياري، في
[المتغيرات المدعومة في تحليلات AMP](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/analytics-vars.md).
