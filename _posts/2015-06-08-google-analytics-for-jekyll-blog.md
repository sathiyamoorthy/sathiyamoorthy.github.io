---
layout: post
title: "Google Analytics for Web applications and Blog"
excerpt: "Google Analytics for analyse web traffic"
date: 2015-06-08
status: publish
comments: true
share: true
categories:
- Web Analytics
tags:
- "Web Analytics, Google Analytics"
image:
  feature: google_analytics_banner.jpg
---

###Get Into Google Analytics

Google Analytics is something which every Web developer should have knowledge of it. Google Analytics helps you to get track application and website traffic. Google Analytics is now the most widely used web analytics service on the internet. Its just didn't end up getting the records, gonna be helpful when you want to bring more customer showinfg traffic and getting into <a href="https://www.google.co.in/adwords/" target="_blank">Adwords</a>(Pay Per Click)

### All "U" Need to do!!

Host Web application or Blog anywhere, No seperate server required for google alaytics. It's pure javscript API code which going to play major role to post all web tracking details. All you have to do is Signup into <a href="https://www.google.com/analytics/" target="_blank">Google Analytics</a> with google account.

Once SignIn into Google Analytics, will get landed into page where you can feed Website details like Website name, Url, time zone etc.. and click Get Tracking id. It will generate unique tracking id with Javscript snippet code like similar page.

>
<figure>
	<img src="/images/google_tracking.jpg">
	<figcaption>Google Tracking page</figcaption>
</figure>


Place the Javscript code into HTML page on layout level or default HTMl which loads for every page. So javascript can render in every page and it triggers Googel Analytics API with all the informations.

Once added the javscript snipet into code, host the application.

 ###It's Time to Analyze application

Log into Google analytics, choose the web application and click Reporting to get all the tracking details and website traffic. User can choose your own dashboard and analytic metrics to get details.

>
<figure>
	<img src="/images/google-analytics.jpg">
	<figcaption>Analytics Dashboard</figcaption>
</figure>

### Google Analytics integrating with Blog(Wordpress, Blogspot, Jekyll.. etc)

Every Blog provided way to integrate with google analytics. Just need to configure Tracking ID using third party tool or direct UI level configuration.

> Jekyll Blog Detail Google Analytics Integration.

**For Jekyll Blog User**. Integrating google analytics into Jekyll is completely depends on the theme because some of the theme which can automatically insert the Google Analytics code. I’ll try to explain how to add the Google Analytics in most Jekyll themes and not Jekyll Bootstrap.

It may quite tricky for who don't understand jekyll layout theming.But, you can identify which file by looking under the:

> _includes

This folder basically holds all the layouting in Jekyll. you can check is there any file called _default, header.html, footer.html. And pase the code above the </head>. At the end, it would be exactly like this:

{% highlight javascript %}
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-63861353-2', 'auto');
  ga('send', 'pageview');

</script>
{% endhighlight %}

>
<figure>
	<img src="/images/Google-Analytics-Real-Time-Dashboard.jpg">
	<figcaption>Google Analytics Real Time Dashboard</figcaption>
</figure>




