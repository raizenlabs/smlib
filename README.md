# Social Media Influencers Node JS module 

## Description
This module provides a simple API to
- Get insights for you instagram account
- Get metrics for your instagram posts 
- Get posts from other instagram accounts

## Functions

<dl>
<dt><a href="#Get">Get(urlPath, params)</a> ⇒ <code>Promise.&lt;Object, Error&gt;</code></dt>
<dd><p>Get request to Facebook API</p>
</dd>
<dt><a href="#DiscoverPosts">DiscoverPosts(urlPath, fields, token, posts)</a> ⇒ <code>Promise.&lt;Array.&lt;DiscoveryPosts&gt;, Error&gt;</code></dt>
<dd><p>Business discovery request for Facebook API</p>
</dd>
<dt><a href="#GetAll">GetAll(urlPath, params)</a> ⇒ <code>Promise.&lt;Array.&lt;Object&gt;, Error&gt;</code></dt>
<dd><p>Get request to Facebook API reading paginated results.
Results will be read until no more &#39;next&#39; cursor is returned in response</p>
</dd>
<dt><a href="#GetPostContent">GetPostContent(urlPath, token)</a> ⇒ <code>Promise.&lt;Post, Error&gt;</code></dt>
<dd><p>Returns post caption,media_type,media_url,children,media_url,comment_count,like_count, and impressions 
from an Instagram post. Ex. &#39;/v11.0/12437548796&#39; would request post content for post with Id 12437548796</p>
</dd>
<dt><a href="#GetDailyInsights">GetDailyInsights(urlPath, token, daysAgo)</a> ⇒ <code>Promise.&lt;(Metrics|Error)&gt;</code></dt>
<dd><p>Returns reach,impressions,and follower_count metrics of an instagram profile
aggregated over a time range from n days ago up to current date</p>
</dd>
<dt><a href="#GetLifetimeInsights">GetLifetimeInsights(urlPath, token)</a> ⇒ <code>Promise.&lt;Array, Error&gt;</code></dt>
<dd><p>Returns countries and cities for Instagram user followers</p>
</dd>
<dt><a href="#DiscoverUserPosts">DiscoverUserPosts(urlPath, userName, daysAgo, token)</a> ⇒ <code>Promise.&lt;Array.&lt;DiscoveryPosts&gt;, Error&gt;</code></dt>
<dd><p>Returns posts for Instagram user using business dicovery since &#39;daysAgo&#39; till current date</p>
</dd>
</dl>

## Typedefs

<dl>
<dt><a href="#PostChildren">PostChildren</a></dt>
<dd></dd>
<dt><a href="#DiscoveryPosts">DiscoveryPosts</a></dt>
<dd></dd>
<dt><a href="#Children">Children</a></dt>
<dd></dd>
<dt><a href="#Post">Post</a></dt>
<dd></dd>
<dt><a href="#Metrics">Metrics</a></dt>
<dd></dd>
</dl>

<a name="Get"></a>

## Get(urlPath, params) ⇒ <code>Promise.&lt;Object, Error&gt;</code>
Get request to Facebook API

**Kind**: global function  
**Returns**: <code>Promise.&lt;Object, Error&gt;</code> - Promise to the request response  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version ex: /v11.0/.. |
| params | <code>Object</code> | Query parameters as key value pairs.  Check the documentation https://developers.facebook.com/docs/instagram for valid key value pairs |
| params.fields | <code>string</code> | Comma separated list of fields and edges to be returned |
| params.access_token | <code>string</code> | Facebook API access token |
   
**Example:**
```javascript
fb.Get('/v11.0/your_ig_user_id',{
    'fields':'name',
    'access_token':'your_access_token'
}).then((data)=>{
    //Do something with data
}).catch((err)=>{
    //Do something with error
})
```

<a name="DiscoverPosts"></a>

## DiscoverPosts(urlPath, fields, token, posts) ⇒ <code>Promise.&lt;Array.&lt;DiscoveryPosts&gt;, Error&gt;</code>
Business discovery request for Facebook API

**Kind**: global function  
**Returns**: <code>Promise.&lt;Array.&lt;DiscoveryPosts&gt;, Error&gt;</code> - Promise to the request response  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version ex: /v11.0/.. |
| fields | <code>Object</code> | Object with the following properties: userName,startDate,endDate |
| fields.userName | <code>string</code> | The userName of the instagram account to query (required) |
| fields.startDate | <code>string</code> | Start date of request in ISO Layout 'YYYY-MM-DD' |
| fields.endDate | <code>string</code> | End date of request in ISO Layout 'YYYY-MM-DD' |
| token | <code>string</code> | Facebook API access token |
| posts | <code>Array</code> | Array to append results to |
   
**Example:**
```javascript
fb.Discover('/v11.0/your_ig_user_id',{
   userName: 'esmuellert', //Here esmuellert is the instagram user name we want to discover
   startDate: '2021-06-29',
   endDate:'2021-06-30',
},'your_access_token',[]).then((data)=>{
    //Do something with data
}).catch((err)=>{
    //Do something with error
})
```

<a name="GetAll"></a>

## GetAll(urlPath, params) ⇒ <code>Promise.&lt;Array.&lt;Object&gt;, Error&gt;</code>
Get request to Facebook API reading paginated results.
Results will be read until no more 'next' cursor is returned in response

**Kind**: global function  
**Returns**: <code>Promise.&lt;Array.&lt;Object&gt;, Error&gt;</code> - Promise to the request response  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version ex: /v11.0/.. |
| params | <code>string</code> | Query parameters as key value pairs.  Check the documentation https://developers.facebook.com/docs/instagram for valid key value pairs |

**Example**
```javascript
fb.GetAll('/v11.0/your_ig_user_id/media',{
  'fields':'timestamp,caption,media_type,children{media_url}',
  'access_token':'your_access_token',
}).then((data)=>{
    //Do something with data
}).catch((err)=>{
    //Do something with error
})
```
<a name="GetPostContent"></a>

## GetPostContent(urlPath, token) ⇒ <code>Promise.&lt;Post, Error&gt;</code>
Returns post caption,media_type,media_url,children,media_url,comment_count,like_count, and impressions 
from an Instagram post. Ex. '/v11.0/12437548796' would request post content for post with Id 12437548796

**Kind**: global function  
**Returns**: <code>Promise.&lt;Post, Error&gt;</code> - Promise object represents request payload  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version and end with post ID ex: '/v11.0/12341234' where 12341234 is the post ID you want to query |
| token | <code>string</code> | Facebook API access token |

**Exampe**
```javascript
fb.GetPost('/v11.0/your_post_id','your_access_token').then((data)=>{
   //Do something with data
}).catch((err)=>{
   //Do something with error
})
```

<a name="GetDailyInsights"></a>

## GetDailyInsights(urlPath, token, daysAgo) ⇒ <code>Promise.&lt;(Metrics\|Error)&gt;</code>
Returns reach,impressions,and follower_count metrics of an instagram profile
aggregated over a time range from n days ago up to current date

**Kind**: global function  
**Returns**: <code>Promise.&lt;(Metrics\|Error)&gt;</code> - Promise object represents request payload  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version,  then indicate Instagram user ID you want to query, and end with 'insights' path. Ex: '/v11.0/123412345/insights' where 123412345 is the Instagram user Id |
| token | <code>string</code> | access token for Facebook API |
| daysAgo | <code>Number</code> | Number of days you want to query. Ex 2 means you want to query insights from 2 days ago till today |

**Example**
```javascript
fb.GetInsights('/v11.0/your_ig_user/insights','your_access_token',11).then((data)=>{
    //Do something with data
}).catch((err)=>{
    //Do something with error
})
```

<a name="GetLifetimeInsights"></a>

## GetLifetimeInsights(urlPath, token) ⇒ <code>Promise.&lt;Array, Error&gt;</code>
Returns countries and cities for Instagram user followers

**Kind**: global function  
**Returns**: <code>Promise.&lt;Array, Error&gt;</code> - Promise object represents request payload  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version.  then indicate Instagram user ID you want to query, and end with 'insights' path. Ex: '/v11.0/123412345/insights' where 123412345 is the Instagram user Id |
| token | <code>string</code> | access token for Facebook API |

**Example**
```javascript
fb.GetAudiences('/v11.0/your_instagram_id/insights','your_access_token').then((data)=>{
    //Do something with data
}).catch((err)=>{
    //Do something with error
})
```

<a name="DiscoverUserPosts"></a>

## DiscoverUserPosts(urlPath, userName, daysAgo, token) ⇒ <code>Promise.&lt;Array.&lt;DiscoveryPosts&gt;, Error&gt;</code>
Returns posts for Instagram user using business dicovery since 'daysAgo' till current date

**Kind**: global function  
**Returns**: <code>Promise.&lt;Array.&lt;DiscoveryPosts&gt;, Error&gt;</code> - Promise to the request response  

| Param | Type | Description |
| --- | --- | --- |
| urlPath | <code>string</code> | URL path for request. Must start with api version ex: /v11.0/.. |
| userName | <code>string</code> | The userName of the instagram account to query (required) |
| daysAgo | <code>number</code> | Number of days you want to query. Ex 2 means you want to query posts from 2 days ago till today |
| token | <code>string</code> | Facebook API access token |

**Example**
```javascript
fb.DiscoverUserPosts('/v11.0/your_ig_user_id','instagram_user_to_discover',18,'your_acces_token').then((data)=>{
    //Do something with data
}).catch((err)=>{
    //Do something with error
})
```

<a name="PostChildren"></a>

## PostChildren
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| data | [<code>Array.&lt;DiscoveryPosts&gt;</code>](#DiscoveryPosts) | Array with posts children |

<a name="DiscoveryPosts"></a>

## DiscoveryPosts
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| timestamp | <code>string</code> | Date when posts was posted |
| caption | <code>string</code> | Post caption |
| media_type | <code>string</code> | Post type (CAROUSEL_ALBUM, IMAGE, or VIDEO) |
| media_url | <code>string</code> | video or image URL |
| children | [<code>PostChildren</code>](#PostChildren) | Post's children |
| id | <code>string</code> | Post ID |

<a name="Children"></a>

## Children
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| data | [<code>Array.&lt;Post&gt;</code>](#Post) | Array with Post's children |

<a name="Post"></a>

## Post
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| id | <code>string</code> | Post ID |
| timestamp | <code>string</code> | Date |
| caption | <code>string</code> | Post caption |
| media_type | <code>string</code> | Post type (CAROUSEL_ALBUM, IMAGE, or VIDEO) |
| media_url | <code>string</code> | video or image URL |
| comments_count | <code>number</code> | Comment counts on the post |
| like_count | <code>number</code> | Like counts on the post |
| impressions | <code>number</code> | Number of times post has been seen |
| engagement | <code>number</code> | Sum of likes_count, comment_count and saved counts on post |
| insights | <code>Object</code> | Social interaction metrics on the post |
| children | [<code>Children</code>](#Children) | Post's children |

<a name="Metrics"></a>

## Metrics
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| reach | <code>number</code> | Number of unique users ho have viewed at least one post from the Instagram user |
| impressions | <code>number</code> | Number of times posts from the Instagram user have been seen |
| follower_count | <code>number</code> | Sum of new followers within the specified range |

