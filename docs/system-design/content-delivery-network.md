# Content Delivery Network (CDN)

![image of CDN](/images/cdn.jpeg)
Source: https://github.com/donnemartin/system-design-primer#content-delivery-network

- Globally distributed network of proxy servers, serving content from locations closer to the user such as images/videos
- The site's DNS resolution will tell clients which server to contact.
- Can significantly improve performance in two ways:
    - Users receive content from data centers close to them
    - Your servers do not have to serve requests that the CDN fulfills

- Disadvantages:
    - CDN costs could be significant depending on traffic
    - Content might be stale if it is updated before the TTL expires it.
    - CDNs require changing URLs for static content to point to the CDN.