---
layout: post
title: "Certificate Validity Dates"
date: 2020-02-20 00:00:00 -0500
img: 
---
Back in 2017 the maximum validity lifetime for an HTTPS certificate was [set to 825 days](https://cabforum.org/2017/03/17/ballot-193-825-day-certificate-lifetimes/), a decision that was widely supported by both browsers and certificate authorities. However, since then there have been multiple unsuccessful attempts at reducing the maximum lifetime to one year. [Scott Helme](https://twitter.com/Scott_Helme) has [written about this previously](https://scotthelme.co.uk/ballot-sc22-reduce-certificate-lifetimes/), and his blog post noted that browser vendors unanimously supported this while some certificate authorities objected to it.

Information is still trickling in, but it seems that Safari is planning to enforce a max validity lifetime of 398 days effective September 1st, 2020.



Let’s take a look at the state of certificate validity ranges today, so we can track how this evolves over the next few months. The data for this comes from the [HTTP Archive](https://httparchive.org), which is an open source project that tracks how the web is built. 

**Certificate Validity Dates in the Wild**

The HTTP Archive requests table contains certificate details for every HTTPS request that was served to the 5.3 million websites tracked. The details are in the `$._securityDetails` and the data contains information on 4,397,690 unique hosts. Out of all of these, 136,007 hostnames served a validity date greater than 825 days! That’s 3.09% of all requests!

Certificate validity dates are widely distributed, but there seems to be a few popular ranges. THe most common validity date is 90 days, likely to the popularity of LetsEncrypt Overall 55% of certificates have a validity date of less than 364 days, which I’ve highlighted in green below. An additional 20% of certificates have a validity between 365 and 398 days, which will meet Safari’s requirements. The remaining 25% have a validity range of more than 398 days.

![|624x181](https://lh6.googleusercontent.com/AOBjFo3j8o70P2yGzR0HGLyJ28q1MxwwsLCW3HkDU9_5lCdxPLyRjioJfnKCHGr4sgLQNTS9MDJwQxKb9kcQtDBztwXX1CpIjdvrP_K3fHsKr-3KOeukfoMaWSbmKWll1fkBMM2E)

Looking at this by certificate authority is also quite interesting. The graph below shows the top 15 certificate authorities. LetsEncrypt accounts for 38.4% of all certificates -

![|624x227](https://lh6.googleusercontent.com/tmVhJjeDtjJatp4JQ2G030Xqy4zar5WP3oOq-oXmSNau8yg1uUJLXMpNwTntspj_9myJGGYZ0pwe96YYS47aZBP99TQl7Y00m1WC-YHlOnGIw0BvbMEPjCpnEkFCMBtq5nRQ3xiF)

When we look at certificate validity date ranges for these certificate authorities, we can see that there’s a mix. Certificates issued by LetsEncrypt, Cloudflare, cPanel and Amazon meet the 398 day requirement already. However, Sectigo, GoDaddy, DigiCert, Comodo and RapidSSL have a very large percentage of certificates that exceed 398 days. 

![|624x284](https://lh6.googleusercontent.com/tNsRLp4kNsUJ55xIHvynO_7-pxNKooBth07BFajaVIODH1vZvlvswd_gA72N3rAvj8Ke4Z_DxW6ogi7Sworl4V8SRN0e4MePBE5xsV_nvC8fho0dyKM96GBgh_9R7puv5KE_j0up)

[DigiCert released a public statement](https://www.digicert.com/position-on-1-year-certificates/) yesterday, which confirms that existing certificates with a validity range >398 days will continue to be trusted by Safari, but that certificates issued after August 30th won’t be able to exceed 398 days.

> For your website to be trusted by Safari, you will no longer be able to issue publicly trusted TLS certificates with validities longer than 398 days after Aug. 30, 2020. Any certificates issued before Sept. 1, 2020 will still be valid, regardless of the validity period (up to 825 days). Certificates that are not publicly trusted can still be recognized, up to a maximum validity of 825 days. 

I’m interested in seeing how this will evolve in the coming months, especially once there are more formal announcements about this. If you would like to see the queries used for this analysis, I've detailed them in this [HTTP Archive discussion forum post](https://discuss.httparchive.org/t/certificate-validity-dates/1874).

Many thanks to Scott Helme for reviewing this.
