# Test cross domain tracking with WeTravel embeds

1. Concept explanation https://support.google.com/analytics/answer/10071811?hl=en#zippy=%2Cmanual-setup
2. Test website https://gzog-wetravel.github.io/test-ga-embeds/
3. Test analytics account https://analytics.google.com/analytics/web/#/p422530854/reports/dashboard?params=_u..nav%3Dmaui%26_u.dateOption%3Dyesterday&r=advertising-snapshot&ruid=advertising-snapshot&collectionId=user


# Problem
Organizer's are not able to view from what sources users originated from when they proceeded to make the booking. Because of this they are not able to understand the customer journey that led to the completion of the booking.

# Technical Implementation

1. Organizer requires to have the gtag.js tracking framework installed in the website and have to send hits to GA.
2. Organizer should add their webtravel domain (e.g. demo.wetravel.to) to:
    1. Either to their cross domain linking configuration in Google Analytics property ![image](https://github.com/gzog-wetravel/test-ga-embeds/assets/155722895/90c69a53-3b87-48c4-8c44-382cbe2730c3)
    2. Either include the `gtag('set', 'linker', {'domains': ['demo.wetravel.to']});`
3. When the customer in the organizer's website is redirected to the embedded wetravel booking page, the embedded url needs to contain the `_gl` query parameter. This parameter passes the information of the `_ga` cookie for the customer in the organizer's domain
to the wetravel domain.
4. The gtag code in the wetravel domain should be in a position to pick up and read the information from `_gl` query paramater and update the `_ga` cookie bassed on that, so that both domains (the organizer's domain and the wetravel domain) have the same `_ga` cookie.
5. By doing this, Google Analytics will recognize that events originating from both domains will come from the same user. This in turn will fix the conversion attribution reports. In other words, the organizer will be able to see if the customer that made the booking originated from Mailchimp,
Google AdWords, from a referred website or visted the organizer's website directly (by directly typing the website in their browser).