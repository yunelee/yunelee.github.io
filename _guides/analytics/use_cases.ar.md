---
layout: page
title: حالات الاستخدام
order: 2
locale: ar
---

يقدم هذا الدليل مجموعة من حالات الاستخدام الشائعة لتتبع تفاعل المستخدم:

{% include toc.html %}

هل تريد إضافة حالة استخدام؟ 
[أحطنا علمًا.](https://github.com/ampproject/docs/issues/new)

يمكنك أيضًا المساهمة بحالات الاستخدام الخاصة بك،
انظر [كيفية المساهمة](https://www.ampproject.org/docs/support/contribute.html).

## تتبع مشاهدات الصفحة

تعرّف على كيفية تتبع مشاهدات الصفحة باستخدام `amp-pixel` و`amp-analytics`. 

### باستخدام amp-pixel

أرسل بيانات مشاهدة الصفحة إلى عنوان URL محدّد باستخدام
[amp-pixel](/docs/reference/amp-pixel.html):

{% highlight html %}
<amp-pixel src="https://foo.com/pixel?"></amp-pixel>
{% endhighlight %}

### باستخدام amp-analytics - لا مورّد

أرسل بيانات مشاهدة الصفحة إلى عنوان URL محدّد باستخدام
[amp-analytics](/docs/reference/extended/amp-analytics.html):

{% highlight html %}
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "pageview": "https://example.com/analytics?url=${canonicalUrl}&title=${title}&acct=${account}"
  },
  "vars": {
    "account": "ABC123"
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

### باستخدام amp-analytics - googleanalytics

أرسل بيانات مشاهدة الصفحة إلى Google Analytics
(انظر أيضًا [تتبع الصفحة في Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/#page_tracking)): 

{% highlight html %}
<amp-analytics type="googleanalytics" id="analytics1">
<script type="application/json">
{
  "vars": {
    "account": "UA-XXXXX-Y"  // Replace with your property ID.
  },
  "triggers": {
    "trackPageview": {  // Trigger names can be any string. trackPageview is not a required name.
      "on": "visible",
      "request": "pageview"
    }
  }
}
</script>
</amp-analytics>
{% endhighlight %}

## تتبع النقرات على الصفحة

تعرّف على كيفية تتبع النقرات على الصفحة باستخدام
[amp-analytics](/docs/reference/extended/amp-analytics.html)،
وإرسال بيانات الحدث إلى عنوان URL محدّد، وإلى
[Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/).

### إرسال البيانات إلى عنوان URL محدّد

يستخدم النموذج التالي السمة `selector` لإرسال حدث `click`
إلى عنوان URL المحدّد كلما نقر مستخدم على رابط (`<a href>`):

{% highlight html %}
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
  },
  "vars": {
    "account": "ABC123"
  },
  "triggers": {
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
}
</script>
</amp-analytics>
{% endhighlight %}

### إرسال البيانات إلى Google Analytics

يستخدم النموذج التالي السمة `selector` لـ `trigger`
لإرسال حدث `click` إلى Google Analytics عند النقر على عنصر معين
(انظر أيضًا
[تتبع حدث AMP في Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/#event_tracking)):

{% highlight html %}
<amp-analytics type="googleanalytics" id="analytics3">
<script type="application/json">
{
  "vars": {
    "account": "UA-XXXXX-Y"  // Replace with your property ID.
  },
  "triggers": {
    "trackClickOnHeader" : {
      "on": "click",
      "selector": "#header",
      "request": "event",
      "vars": {
        "eventCategory": "ui-components",
        "eventAction": "header-click"
      }
    }
  }
}
</script>
</amp-analytics>
{% endhighlight %}

## تتبع التمرير

تتبع التمرير عبر الصفحة باستخدام [amp-analytics](/docs/reference/extended/amp-analytics.html).
يستخدم النموذج التالي السمة `scrollspec` لإرسال حدث `scroll`
إلى عنوان URL المحدّد عند التمرير عبر الصفحة رأسيًا بنسبة 25%، و50%، و90%.
يتم تنشيط الحدث كذلك عند التمرير عبر الصفحة أفقيًا
إلى نسبة 90% من عرض `scroll`:

{% highlight html %}
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
  },
  "vars": {
    "account": "ABC123"
  },
  "triggers": {
    "scrollPings": {
      "on": "scroll",
      "scrollSpec": {
        "verticalBoundaries": [25, 50, 90],
        "horizontalBoundaries": [90]
      }
    }
  }
}
</script>
</amp-analytics>
{% endhighlight %}

## تتبع التفاعلات الاجتماعية

تعرّف على كيفية تتبع التفاعلات الاجتماعية باستخدام
[amp-analytics](/docs/reference/extended/amp-analytics.html)،
وإرسال بيانات الحدث إلى عنوان URL محدّد، وإلى
[Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/).

### إرسال البيانات إلى عنوان URL محدّد

يستخدم النموذج التالي السمة `selector` لإرسال حدث `click`
إلى عنوان URL المحدّد كلما نقر مستخدم على تغريدة ("#رابط_التغريدة):

{% highlight html %}
<amp-analytics>
<script type="application/json">
{
  "requests": {
    "event": "https://example.com/analytics?eid=${eventId}&elab=${eventLabel}&acct=${account}"
  },
  "vars": {
    "account": "ABC123"
  },
  "triggers": {
    "trackClickOnTwitterLink": {
      "on": "click",
      "selector": "#tweet-link",
      "request": "event",
      "vars": {
        "eventId": "43",
        "eventLabel": "clicked on a tweet link"
      }
    }
  }
}
</script>
</amp-analytics>
{% endhighlight %}

### إرسال البيانات إلى Google Analytics

يستخدم النموذج التالي السمة `selector` لـ `trigger`
لإرسال حدث عند النقر على زر إجراءات اجتماعية معيّن
(انظر أيضًا
[تتبع التفاعلات الاجتماعية في Google Analytics](https://developers.google.com/analytics/devguides/collection/amp-analytics/#social_interactions)):

{% highlight html %}
<amp-analytics type="googleanalytics" id="analytics4">
<script type="application/json">
{
  "vars": {
    "account": "UA-XXXXX-Y" // Replace with your property ID.
  },
  "triggers": {
    "trackClickOnTwitterLink" : {
      "on": "click",
      "selector": "#tweet-link",
      "request": "social",
      "vars": {
          "socialNetwork": "twitter",
          "socialAction": "tweet",
          "socialTarget": "https://www.examplepetstore.com"
      }
    }
  }
}
</script>
</amp-analytics>
{% endhighlight %}
