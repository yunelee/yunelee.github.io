---
layout: page
title: المعاينة والتحقق
order: 3
locale: ar
---

عاين صفحة AMP تمامًا مثلما تعاين أي موقع HTML ثابت آخر. لا توجد خطوة إنشاء أو معالجة مسبقة مطلوبة. إما:

  - **أن تفتحها مباشرةً في المتصفح من نظام الملفات** (قد لا تعمل بعض العناصر بسبب فشل XMLHttpRequests).
  - **أو تستخدم خادم ويب محلي، مثل Apache 2 أو Nginx**.
    *(Tip: لتسريع خادم الويب، قم بتشغيل `python -m SimpleHTTPServer`.)*

بعد ذلك، تأكّد من أن صفحة AMP **صفحة AMP صالحة بالفعل**، وإلا فلن يتم اكتشافها وتوزيعها بواسطة أنظمة أساسية من جهة خارجية، مثل بحث Google. للتحقق:

  1. افتح صفحتك في متصفحك.
  1. أضف "`#development=1`" إلى عنوان URL، على سبيل المثال، `http://localhost:8000/released.amp.html#development=1`.
  1. افتح [وحدة تحكم Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/debug/console/) وابحث عن أخطاء التحقق.

[تعرّف على المزيد بشأن التحقق](/docs/guides/validate.html)، وما يتعين فعله عند مصادفة أخطاء.

{% include button.html title="المتابعة إلى الخطوة 5" link="/docs/get_started/create/prepare_for_discovery.html" %}
