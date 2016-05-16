---
layout: page
title: إنشاء صفحة AMP HTML
order: 0
locale: ar
---

يمثل الترميز التالي نقطة بداية مناسبة أو نصًا معياريًا.
انسخه واحفظه في ملف بإضافة ‎.html.

{% highlight html %}
<!doctype html>
<html amp lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello, AMPs</title>
    <link rel="canonical" href="http://example.ampproject.org/article-metadata.html" />
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
    <script type="application/ld+json">
      {
        "@context": "http://schema.org",
        "@type": "NewsArticle",
        "headline": "Open-source framework for publishing content",
        "datePublished": "2015-10-07T12:02:41Z",
        "image": [
          "logo.jpg"
        ]
      }
    </script>
    <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
    <script async src="https://cdn.ampproject.org/v0.js"></script>
  </head>
  <body>
    <h1>Welcome to the mobile web</h1>
  </body>
</html>
{% endhighlight %}

المحتوى في النص الأساسي واضح حتى الآن. لكن هناك الكثير من الشفرات الإضافية في عنوان الصفحة، والتي قد لا تبدو واضحةً مباشرةً. هيا نحلل الترميز المطلوب.

## الترميز المطلوب

يجب على مستندات AMP HTML:

  - أن تبدأ بـ doctype `<!doctype html>`.
  - أن تحتوي على علامة المستوى الأعلى `<html ⚡>` (تكون `<html amp>` مقبولة كذلك).
  - أن تحتوي على العلامتين `<head>` و`<body>` (هما علامتان اختياريتان في HTML).
  - أن تحتوي على العلامة `<link rel="canonical" href="$SOME_URL" />` داخل عنوانها، والتي تشير إلى إصدار HTML العادي لمستند AMP HTML أو إلى نفسها إذا لم يكن إصدار HTML من هذا القبيل موجودًا.
  - أن تحتوي على العلامة `<meta charset="utf-8">` بوصفها التابع الأول للعلامة head.
  - أن تحتوي على العلامة `<meta name="viewport" content="width=device-width,minimum-scale=1">` داخل العلامة head. من الموصى به أيضًا تضمين initial-scale=1.
  - أن تحتوي على العلامة `<script async src="https://cdn.ampproject.org/v0.js"></script>` بوصفها العنصر الأخير في head (يشمل هذا مكتبة AMP JS ويقوم بتحميلها).
  - أن تحتوي على ما يلي في العلامة `<head>`:
    `<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>`

## البيانات الوصفية الاختيارية

بالإضافة إلى المتطلبات المجرّدة، كذلك يتضمن النموذج تعريف Schema.org في العنوان، والتي لا تمثل متطلبًا صارمًا لـ AMP، لكنها متطلب لتوزيع محتواك في مواقع معينة، على سبيل المثال في [العرض التوضيحي لسلسلة عرض أخبار بحث Google (جرّبه على هاتفك)](https://g.co/ampdemo).

للتعرّف على المزيد بشأن كل البيانات الوصفية التي ستحتاجها في العديد من المواقع الأخرى، أي Twitter, [استكشف نماذجنا](https://github.com/ampproject/amphtml/tree/master/examples/metadata-examples). للتعرّف بصفة خاصة على AMP في بحث Google، انظر [أهم الأخبار باستخدام AMP](https://developers.google.com/structured-data/carousels/top-stories).

<hr>

أخبار سارّة! هذا كل ما نحتاجه لإنشاء صفحتنا الأولى في AMP، لكن ليس هناك الكثير مما يجري، بطبيعة الحال، في النص الأساسي حتى اللحظة. في القسم التالي، سوف نتناول كيفية إضافة أساسيات، مثل الصور وعناصر AMP المخصصة، وكيفية إضفاء نمط على صفحتك، وتطوير تنسيق سريع الاستجابة.

{% include button.html title="المتابعة إلى الخطوة 2" link="/docs/get_started/create/include_image.html" %}
