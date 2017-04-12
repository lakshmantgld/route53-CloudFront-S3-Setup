## CloudFront cache:

Caching is an important thing to be decided when using cloudFront. We can control cache before CloudFront forwards another request to your origin (In our case origin is S3). Reducing the duration helps to serve the dynamic content. Increasing the duration means your users get better performance because your objects are more likely to be served directly from the edge cache.

Browsers also cache various objects using the **cache-control** header from response. This should be done carefully. Because when new objects are updated, browser may have the old versions. This has to be pre-decided and planned.

In cloudFront, you can control cache using two methods:

####1. Using Minimum, Maximum and Default TTL in cloudFront:

By default, the CloudFront caches the object for 24 hours. After that when any request comes, it forwards the request to S3(origin) and then serve the objects to users. During this process it also caches the object for another 24 hours. Increasing the cache period greatly improves the performance of the web app by decreasing the latency and increasing the throughput.

**Minimum TTL:** Objects may be cached for at least this long, even if **Cache-Control: max-age** has a lower value.

**Maximum TTL:** Objects will not be cached any longer than this, even if **Cache-Control: max-age** has a higher value.

**Default TTL:** Objects may be cached for this long, if **Cache-Control** is not seen on the object. You should not need this, because you should have Cache-Control headers everywhere.

If you are unsure about the caching period of browsers, I would suggest to set the **Default TTL** to 1 year(365) days, so that we get a better performance. If you add any new/updated objects to S3, then you can invalidate the cache in CloudFront so that the CloudFront fetches the new/updated objects from S3 and serves to the users.

This method will affect only the CloudFront caches and not the browser caches.

####2. Having Cache-Control in origin headers:

This method will affect both CloudFront cache and browser cache. To do this add the time(in seconds) to the header as **Cache-Control: (seconds)** to all the objects in S3. In cloudFront, **Use origin cache headers** should be selected. This option will be selected by default.

So, adding those headers affect both the CF and S3 cache. Be Cautions before using it.
