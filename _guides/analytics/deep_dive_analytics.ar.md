---
layout: page
title: نظرة عميقة على AMP Analytics
order: 1
---

يقدم هذا الدليل رؤية متعمقة على
[مكون amp-analytics](/docs/reference/extended/amp-analytics.html)،
حيث يقسّم نموذج تهيئة `amp-analytics` إلى ثلاثة مكونات أساسية مهمة:

{% include toc.html %}

ويستخدم باقي هذا الدليل نموذج التهيئة هذا،
الذي يتتبع مرات مشاهدة الصفحة ونقرات المستخدم على الروابط
ويرسل بيانات التحليلات إلى مزوّد الجهة الخارجية،
[Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/):

{% highlight html %}
<amp-analytics type="googleanalytics" config="https://example.com/analytics.account.config.json">
<script type="application/json">
{
  "requests": {
    "pageview": "https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}",
    "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
  },
  "vars": {
    "account": "ABC123"
  },
  "extraUrlParams": {
    "cd1": "AMP"
  },
  "triggers": {
    "trackPageview": {
      "on": "visible",
      "request": "pageview"
    },
    "trackAnchorClicks": {
      "on": "click",
      "selector": "a",
      "request": "event",
      "vars": {
        "eventId": "42",
        "eventLabel": "clicked on a link"
      }
    }
  },
  'transport': {
    'beacon': false,
    'xhrpost': false,
    'image': true
  }
}
</script>
</amp-analytics>
{% endhighlight %}

**ملاحظة:** الغرض من نموذج الشفرة أعلاه هو مساعدتك على التعلّم، لكنه ليس نموذجًا حقيقيًا على الإطلاق. إذا كنت تعمل مع مزودي تحليلات، فلن يكون للنموذج أعلاه - على الأرجح - أي معنى؛ فتهيئات المزوّد تزيل التعقيد. راجع مستندات مزوّد التحليلات التابع له للاطلاع على نماذج التهيئات.

## وجهة إرسال بيانات التحليلات: السمة type

تم تصميم AMP لدعم النمطين الشائعين لتجميع البيانات:

* التحويل بواسطة نقطة نهائية مملوكة للناشر لأجل أنظمة التحليلات الداخلية.
* التحويل بواسطة نقطة نهائية مملوكة لمورّد لإتاحة التوافقية مع حل المورّد
(مثل [Adobe Analytics](https://helpx.adobe.com/marketing-cloud/analytics.html)، أو [Chartbeat](http://support.chartbeat.com/docs/)، أو [Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/)).

لإرسال بيانات التحليلات إلى مزوّد تحليلات،
ضمّن السمة `type` في العلامة `amp-analytics` وعيّن قيمتها
على المورّد المناسب، وذلك على النحو المحدّد في
[مواصفة amp-analytics](/docs/reference/extended/amp-analytics.html).  

على سبيل المثال: يرسل `<amp-analytics type="googleanalytics">` بيانات التحليلات
إلى مزوّد التحليلات الذي يمثل جهة خارجية، وهو Google Analytics.
لإرسال البيانات إلى نقطة نهائية مملوكة لناشر،
ببساطة لا تضمّن السمة `type`.
سيتم إرسال بيانات التحليلات إلى النقاط النهائية المحددة لكل
[طلب](/docs/guides/analytics/deep_dive_analytics.html#what-data-gets-sent-requests-attribute).

تهيئات مورّد Analytics هي وسيلة سريعة
لبدء العمل باستخدام `amp-analytics`.
ينبغي لك الرجوع إلى مستندات المورّد
وموارد المساعدة لمزيد من الإرشادات.
كما ذكرنا سابقًا،
يمكن العثور على قائمة المورّدين الذين نفذوا بالفعل إجراء الدمج مع AMP، وكذلك الروابط
إلى مستنداتهم الخاصة، في
[مواصفة amp-analytics](/docs/reference/extended/amp-analytics.html). 

إذا كنت مورّد تحليلات،
فتعرّف على المزيد بشأن
[دمج تهيئة تحليلاتك في AMP HTML](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/integrating-analytics.md).

## تحميل تهيئة بعيدة: السمة config

لست مضطرًا إلى تضمين كل التهيئة
لأجل `amp-analytics` كاملةً في صفحتك على AMP.
بدلاً من ذلك، يمكنك الاستدعاء إلى عنوان URL بعيد
لكل التهيئات أو جزء منها.

يسمح لك هذا بتنفيذ إجراءات، مثل تغيير التهيئة
استنادًا إلى طلب معين.
إذا كنت تمتلك، بوصفك ناشرًا، إمكانية التحكم في ملف بعيد
يمكنك إجراء أي معالجة من جهة الخادم تكون ضرورية
لإنشاء بيانات التهيئة.
 
الخطوة الأولى لتحميل التهيئات البعيدة هي
تضمين السمة config في العلامة `amp-analytics`:

{% highlight html %}
<amp-analytics config="https://example.com/analytics.account.config.json">
{% endhighlight %}

الخطوة التالية هي إنشاء محتوى JSON المتضمّن في عنوان URL البعيد.
في هذا النموذج البسيط،
لا تمثل التهيئة المضمّنة في كائن JSON سوى قيمة المتغير لحساب التحليلات.

نموذج المحتوى في `https://example.com/analytics.account.config.json`:

{% highlight html %}
{
  "vars": {
    "account": "UA-XXXXX-Y"  // Replace with your property ID.
  }
}
{% endhighlight %}

الخطوة النهائية هي التأكّد من سحب ما يحتويه الملف البعيد
إلى الموضع السليم في تهيئة `amp-analytics`.
في كلّ من طلبي `pageview` و`event` هنا،
يتم تعيين قيمة المتغير `account` تلقائيًا
على قيمة الحساب في عنوان URL البعيد (`"account": "UA-XXXXX-Y"`):

{% highlight html %}
"requests": {
  "pageview": "https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}",
  "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
}
{% endhighlight %}

**مهم:** لا يتم التحقق من AMP مقابل الاستخدامات العديدة للمتغير نفسه.
يتم ملء القيم عبر اتباع ترتيب استبدال متغير حسب التفضيل،
وتكون القيم في عناوين URL البعيدة في قمة ذلك الترتيب 
(انظر [ترتيب استبدال المتغير](/docs/guides/analytics/deep_dive_analytics.html#variable-substitution-ordering)).

## السمات Requests وtriggers وtransports

تحدّد السمة `requests` "ماهية البيانات التي يتم إرسالها"
(على سبيل المثال، `pageviews`، و`events`)،
والموضع الذي يتم إرسالها إليه (عناوين URL المستخدمة لنقل البيانات).

تصف السمة `triggers` الموعد الذي يتعين إرسال بيانات التحليلات فيه،
على سبيل المثال، عندما يعرض مستخدم صفحة، أو عندما ينقر مستخدم فوق رابط. 

تحدد السمة `transport` كيفية إرسال طلب،
وبشكل أكثر تحديدًا، البروتوكول. 

تابع القراءة للتعرّف على المزيد بشأن هذه التهيئات.
(يمكنك أيضًا القراءة بشأن هذه التهيئات في
[مرجع amp-analytics](/docs/reference/extended/amp-analytics.html).)

### ماهية البيانات التي يتم إرسالها: السمة requests

يتم استخدام `request-name` في تهيئة المشغل لتحديد
الطلب الذي ينبغي إرساله ردًا على حدث خاص.
يمثل `request-value` عنوان URL لـ `https`.
يمكن أن تتضمن هذه القيم الرموز المميزة للعنصر النائب
الذي يمكن أن يشير إلى الطلبات أو المتغيرات الأخرى.

{% highlight html %}
"requests": {
  "pageview": "https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}",
  "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
}
{% endhighlight %}

بعض مزوّدي التحليلات (بما في ذلك Google Analytics)
قدموا بالفعل التهيئة
التي تستخدمها عبر السمة `type`.
إذا كنت تستخدم مزوّد تحليلات،
فقد لا تحتاج إلى تضمين معلومات `requests`.
راجع مستندات مورّدك للتعرّف على ما
إذا كانت هناك حاجة لتهيئة `requests` أم لا وكيفية ذلك.

#### إلحاق عنوان URL للطلب: معلمات عنوان URL الإضافية

تحدد السمة [extraUrlParams](https://github.com/ampproject/amphtml/blob/master/extensions/amp-analytics/amp-analytics.md#extra-url-params)
المعلمات الإضافية التي سيتم إلحاقها بسلسلة طلبات البحث لعنوان URL للطلب عبر اصطلاح "&foo=baz" العادي.

يضيف النموذج `amp-analytics` معلمة <code>cd1</code> إضافية
إلى الطلب ويعيّن قيمة المعلمة على "AMP":

{% highlight html %}
  "extraUrlParams": {
    "cd1": "AMP"
  }
{% endhighlight %}

### متى يتم إرسال البيانات: السمة triggers

تعطي السمة `triggers` وصفًا للوقت الذي ينبغي إرسال طلب تحليلات فيه.
وهي تحتوي على زوج قيمة مفتاح يتمثل في اسم المشغل وتهيئة المشغل.
يمكن أن يكون اسم المشغل أي سلسلة تتألف
من حروف هجائية رقمية (a-zA-Z0-9). 

على سبيل المثال،
تتم تهيئة العنصر `amp-analytics` التالي لإرسال طلب إلى
`https://example.com/analytics` عند تحميل المستند لأول مرة،
وكلما تم النقر فوق علامة `a`:

{% highlight html %}
"triggers": {
  "trackPageview": {
    "on": "visible",
    "request": "pageview"
  },
  "trackAnchorClicks": {
    "on": "click",
    "selector": "a",
    "request": "event",
    "vars": {
      "eventId": "42",
      "eventLabel": "clicked on a link"
    }
  }
}
{% endhighlight %}

تدعم AMP تهيئات المشغل التالية:

<table>
  <thead>
    <tr>
      <th data-th="Trigger Config" class="col-thirty">تهيئة المشغل</th>
      <th data-th="Description">الوصف</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Trigger Config"><code>on</code> (مطلوب)</td>
      <td data-th="Description">الحدث الذي سيتم توزيع الرسائل إليه. القيم الصالحة هي <code>click</code>، و<code>scroll</code>، و<code>timer</code>، و<code>visible</code>.</td>
    </tr>
    <tr>
      <td data-th="Trigger Config"><code>request</code> (مطلوب)</td>
      <td data-th="Description">اسم الطلب الذي سيتم إرساله (على النحو المحدد في <a href="/docs/guides/analytics/deep_dive_analytics.html#what-data-gets-sent-requests-attribute">الطلبات</a>).</td>
    </tr>
    <tr>
      <td data-th="Trigger Config"><code>vars</code></td>
      <td data-th="Description">كائن يحتوي على أزواج قيمة مفتاح للاستخدام في تجاوز <code>vars</code> المحدد في تهيئة المستوى الأعلى، أو لتحديد <code>vars</code> فريد لهذا المشغل (انظر أيضًا <a href="/docs/guides/analytics/deep_dive_analytics.html#variable-substitution-ordering">ترتيب استبدال المتغير</a>).</td>
    </tr>
    <tr>
      <td data-th="Trigger Config"><code>selector</code> (مطلوب عند تعيين <code>on</code> على <code>click</code>)</td>
      <td data-th="Description">محدّد CSS الذي يُستخدم لتحسين العناصر التي ينبغي تتبعها. استخدم القيمة <code>*</code> لتتبع كل العناصر. يتم استخدام هذه التهيئة بالتزامن مع المشغل <code>click</code>. تعرّف على كيفية استخدام المحدّد <a href="/docs/guides/analytics/use_cases.html#tracking-page-clicks">لتتبع النقرات على الصفحة</a> وكذلك <a href="/docs/guides/analytics/use_cases.html#tracking-social-interactions">التفاعلات الاجتماعية</a>.</td>
    </tr>
    <tr>
      <td data-th="Trigger Config"><code>scrollSpec</code> (مطلوب عند تعيين <code>on</code> على <code>scroll</code>)</td>
      <td data-th="Description">عناصر التحكم التي يتم تنشيط الحدث <code>scroll</code> بموجب شروطها عند التمرير عبر الصفحة. يمكن أن يحتوي هذا الكائن على <code>verticalBoundaries</code> و<code>horizontalBoundaries</code>. واحدة من الخصيصتين على الأقل مطلوبة لتنشيط حدث <code>scroll</code>. يجب أن تكون قيم كلّ من الخصيصتين صفائف من الأرقام التي تحتوي على حدود يتم إنشاء حدث تمرير فيها. انظر هذا النموذج في <a href="/docs/guides/analytics/use_cases.html#tracking-scrolling">تتبع التمرير</a>.</td>
    </tr>
    <tr>
      <td data-th="Trigger Config"><code>timerSpec</code> (مطلوب عند تعيين <code>on</code> على <code>timer</code>)</td>
      <td data-th="Description">عناصر التحكم عند تنشيط الحدث <code>timer</code>. سيتم تشغيل المؤقّت في الحال، وبعد ذلك عند فاصل زمني محدد. يتم استخدام هذه التهيئة بالتزامن مع المشغل <code>timer</code>.</td>
    </tr>
  </tbody>
</table>

**مهم:** يتم تجاوز المشغلات المأخوذة من تهيئة ذات أسبقية أقل
عبر المشغلات التي تحمل الأسماء نفسها والمأخوذة من تهيئة ذات أسبقية أعلى
(انظر [ترتيب استبدال المتغير](/docs/guides/analytics/deep_dive_analytics.html#variable-substitution-ordering)).

### كيفية إرسال البيانات: السمة transport

تحدد السمة `transport` كيفية إرسال طلب.
ويتم تمكين الأساليب الثلاثة التالية افتراضيًا:

<table>
  <thead>
    <tr>
      <th data-th="Transport Method" class="col-thirty">أسلوب النقل</th>
      <th data-th="Description">الوصف</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Transport Method"><code>beacon</code></td>
      <td data-th="Description">يشير إلى إمكانية استخدام <a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon">navigator.sendBeacon</a> لإرسال الطلب. سيرسل هذا طلب <code>POST</code> مع بيانات اعتماد ونص فارغ.</td>
    </tr>
    <tr>
      <td data-th="Transport Method"><code>xhrpost</code></td>
      <td data-th="Description">يشير إلى إمكانية استخدام <code>XMLHttpRequest</code> لإرسال الطلب. سيرسل هذا طلب <code>POST</code> مع بيانات اعتماد ونص فارغ.</td>
    </tr>
    <tr>
      <td data-th="Transport Method"><code>image</code></td>
      <td data-th="Description">يشير إلى إمكانية إرسال الطلب عبر إنشاء علامة <code>Image</code>. سيرسل هذا طلب <code>GET</code>.</td>
    </tr>
  </tbody>
</table>

يتم استخدام أسلوب نقل واحد فقط،
وهو الأسلوب الذي يتميز بالأسبقية الأعلى
التي يتم تمكينها والسماح بها وتوفيرها.
هذه الأسبقية هي `beacon` > `xhrpost` > `image`.
إذا كان وكيل مستخدم البرنامج لا يدعم أسلوبًا معينًا،
فسوف يتم استخدام الأسلوب الممكّن التالي من علو الأسبقية. 

اجعل السمة `transport` ضمن تهيئتك
في حالة واحدة وهي إذا أردت تحديد خيارات النقل،
وإلا، فقد تتسبب في إيقاف الطلبات.

في النموذج أدناه،
يكون `beacon` و`xhrpost` معينين إلى false،
لذا لن يتم استخدامهما حتى إذا كانت أسبقيتهما أعلى من `image`.
إذا كان وكيل مستخدم البرنامج يدعم الأسلوب `image`،
فسوف يتم استخدامه؛ وإلا، فلن يتم إرسال أي طلب.

{% highlight html %}
'transport': {
  'beacon': false,
  'xhrpost': false,
  'image': true
}
{% endhighlight %}

## ترتيب استبدال المتغير

تملأ AMP المتغيرات بالقيم بترتيب يستند إلى الأسبقية:

1. التهيئات البعيدة (عبر `config`).
2. تكون `vars` مضمّنة داخل مشغل ضمن `triggers`.
3. تكون `vars` - عند المستوى الأعلى - مضمّنة ضمن `amp-analytics`.
4. القيم المقدّمة بواسط النظام الأساسي.

في هذا النموذج، توجد تهيئة بعيدة،
وهي عبارة عن متغيرات محددة عند المستوى الأعلى، وفي المشغلات، وعند مستوى النظام الأساسي:

{% highlight html %}
<amp-analytics config="http://example.com/config.json">
<script type="application/json">
{
  "requests": {
    "pageview": "https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}&clientId=${clientId(cid-scope)}",
  },
  "vars": {
    "account": "ABC123",
    "title": "Homepage"
  },
  "triggers": {
    "some-event": {
      "on": "visible",
      "request": "pageview",
      "vars": {
        "title": "My homepage",
        "clientId": "my user"
      }
  }
}
</script>
</amp-analytics>
{% endhighlight %}

عند تحديد `var` نفسه في مواقع عديدة،
يعيّن ترتيب الأسبقية للمتغير قيمته مرة واحدة.
ولذلك، إذا تم تحديد `account` بواسطة التهيئة البعيدة بوصفه UA-XXXXX-Y في النموذج أعلاه،
فسوف تكون قيم العديد من المتغيرات كما يلي:

<table>
  <thead>
    <tr>
      <th data-th="var" class="col-thirty"><code>var</code></th>
      <th data-th="Value">القيمة</th>
      <th data-th="Defined By" class="col-thirty">يتم تحديدها بواسطة</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="var"><code>canonicalUrl</code></td>
      <td data-th="Value"><code>http://example.com/path/to/the/page</code></td>
      <td data-th="Defined By">النظام الأساسي</td>
    </tr>
    <tr>
      <td data-th="var"><code>title</code></td>
      <td data-th="Value">الصفحة الرئيسية الخاصة بي</td>
      <td data-th="Defined By">المشغل</td>
    </tr>
    <tr>
      <td data-th="var"><code>account</code></td>
      <td data-th="Value"><code>UA-XXXXX-Y</code></td>
      <td data-th="Defined By">التهيئة البعيدة</td>
    </tr>
    <tr>
      <td data-th="var"><code>clientId</code></td>
      <td data-th="Value">my user</td>
      <td data-th="Defined By">المشغل</td>
    </tr>
  </tbody>
</table>
