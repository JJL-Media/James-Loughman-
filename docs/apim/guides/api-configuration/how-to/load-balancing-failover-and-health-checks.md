---
description: >-
  This section focuses on configuring load-balancing, failover, and health
  checks as Gravitee backend services.
---

# Load-balancing, failover, and health checks

### Backend services: load-balancing, failover, and health checks

Gravitee API Management (APIM) offers three main backend services for managing your APIs. These services are:&#x20;

* **Load-balancing:** a technique used to distribute incoming traffic across multiple backend servers. The goal of load balancing is to optimize resource utilization, maximize throughput, minimize response time, and avoid overloading any single server.
* **Failover:** a mechanism to ensure high availability and reliability of APIs by redirecting incoming traffic to a secondary server or backup system in the event of a primary server failure.
* **Health checks:** a mechanism used to monitor the availability and health of your endpoints and/or your API gateways.

All of these capabilities are built in to the Gravitee APIM platform. The rest of this article will focus on how to configure these services; if you want more conceptual explanations of the services, please refer to the [Concepts sections on load-balancing, failover, and health checks](../concepts.md#load-balancing).&#x20;

### How to configure load-balancing in Gravitee

To configure load-balancing in Gravitee, follow these steps:

1\. Log in to the Gravitee API Management UI.

2\. Load-balancing (as well other backend services) are configured per API. So, head to the **APIs menu.**

![Load-balancing: select the APIs menu.](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/95d2995f-b5b8-482a-bdd8-8109315e9bb7/ascreenshot.jpeg?tl\_px=0,38\&br\_px=1493,878\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=39,139)

3\. Find and select the API for which you want to configure load-balancing.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/ffb6f144-5f64-474e-9aec-e636a81093d9/ascreenshot.jpeg?tl\_px=0,0\&br\_px=1493,840\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=232,128)

4\. Select the **Edit API** icon.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/2d11dc86-a65a-4c5d-9b1f-cf9646055f77/ascreenshot.jpeg?tl\_px=1962,146\&br\_px=3455,986\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=477,139)

5\. Select Backend services

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/a87da572-ba67-4258-9d29-3be916be39c1/ascreenshot.jpeg?tl\_px=0,628\&br\_px=1493,1468\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=247,139)

6\. From here, you can either configure load-balancing for existing endpoint groups or, create a new endpoint group for which to configure load-balancing. For the sake of this article, we will create a new endpoint group from scratch. To do so, select **+ Add new endpoint group**.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/9478f6d1-c0fe-4cb9-acef-577b03d234f8/ascreenshot.jpeg?tl\_px=1962,0\&br\_px=3455,840\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=411,132)

7\. You'll be taken to the **General** tab. Here, you will name your endpoint group and select the load-balancing algorithm. For the sake of this article, I will select **Round robin**.

{% hint style="info" %}
Please refer to the [load-balancing concepts section](../concepts.md#load-balancing) if you need in-depth explanations of the various load-balancing algorithms that Gravitee supports.
{% endhint %}

![](https://colony-recorder.s3.amazonaws.com/files/2023-03-07/0f165e09-c3b5-43fc-b760-d34585ecd629/stack\_animation.webp)

8\. Now, it's time to configure your endpoint group with any additional HTTP details that might be relevant. To do so, select **Configuration**.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/2bb0a7e1-883c-4a37-9cee-ffad16f3ee17/ascreenshot.jpeg?tl\_px=751,0\&br\_px=2244,840\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=262,111)

9\. Configure your HTTP details to your liking. For example, I might choose to enable **HTTP pipelining,** which will cause requests to be written to connections without waiting for previous responses to return. You can configure many other additional details, such as HTTP protocol version, Connect timeout time (in ms), idle timeout (in ms), SSL options, and more.

![](https://colony-recorder.s3.amazonaws.com/files/2023-03-07/7526630f-4033-4b9d-9d41-0062e12ea856/stack\_animation.webp)

10\. Optional: if you want to enable Service Discovery, select the **Service discovery** tab. Service discovery will enable external endpoints to be dynamically added or removed to or from the group. For more information on Service Discovery, please refer to our documentation on [Gravitee Service discovery.](../concepts.md#service-discovery)

![](https://colony-recorder.s3.amazonaws.com/files/2023-03-07/cf7799b5-28eb-4dff-9895-1e7a6f481edb/stack\_animation.webp)

11\. Once you are done defining and configuring your endpoint group, select **Create**.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/46fa5604-2509-48c7-ae72-7c0176a7e4ef/ascreenshot.jpeg?tl\_px=1962,556\&br\_px=3455,1396\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=417,139)

12\. Now, it's time to add endpoints to your endpoint group. Once you've done this, you'll be able to configure load balancing for your endpoint group. Let's head back to the **Endpoints** section of the **Backend Services** menu.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/e338a81b-8c36-4cf1-b927-3f4b7204cea6/ascreenshot.jpeg?tl\_px=489,0\&br\_px=1982,840\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=262,78)

13\. You'll see your endpoint group. To add endpoints to this group, **select** + Add endpoint.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/323033e1-0584-474a-87f4-4f9ad075a8e8/ascreenshot.jpeg?tl\_px=1823,560\&br\_px=3316,1400\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=262,139)

14\. In the General tab, define your endpoint name, target URL, weight (if you chose a weighted load-balancing algorithm), and your tenants.

![](https://colony-recorder.s3.amazonaws.com/files/2023-03-07/accdc8c6-ee91-4bd6-a351-9c3a2656360f/stack\_animation.webp)

15\. **** Optional: **select** Secondary endpoint to define this endpoint outside the main load balancing pool. This will make the endpoint used for load balancing only if all the primary endpoints are marked as down by the health check.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/49f626c6-5ee4-45df-a8f3-5cb76bbcb15d/ascreenshot.jpeg?tl\_px=763,1098\&br\_px=2256,1938\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=262,141)

16\. Once you're finished specifying endpoint details in the General tab, its time to configure the HTTP configuration for your endpoint.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/da0973c3-44ba-4cd0-a288-e6ce86b4f185/ascreenshot.jpeg?tl\_px=849,166\&br\_px=2342,1006\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=262,139)

17\. By default, the endpoint will inherit configuration from the configuration that you set at the endpoint group level.

<figure><img src="../../../.gitbook/assets/Configure load-balancing - Step 17.jpeg" alt=""><figcaption></figcaption></figure>

18\. However, if you want to set up HTTP configuration specific to that endpoint, toggle the **Inherit configuration** OFF.

<figure><img src="../../../.gitbook/assets/Configure load-balancing - Step 18.jpeg" alt=""><figcaption></figcaption></figure>

19\. Once toggled OFF, you can specify a different HTTP configuration for this endpoint. Once you are done, select **Save**.

<figure><img src="../../../.gitbook/assets/Configure load-balancing - Step 19.jpeg" alt=""><figcaption></figcaption></figure>

20\. For the sake of this example, let's toggle the **Inherit configuration** back ON.&#x20;

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-03-07/fd85c6d5-7a13-4dd2-aab8-443fac87cabe/ascreenshot.jpeg?tl\_px=1962,286\&br\_px=3455,1126\&sharp=0.8\&width=560\&wat\_scale=50\&wat=1\&wat\_opacity=0.7\&wat\_gravity=northwest\&wat\_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark\_default.png\&wat\_pad=443,139)

{% hint style="success" %}
Congrats! Once you're done with your HTTP configuration, you can set up a health check for your endpoint. To learn more about setting up health checks, please refer to the "Health checks" section of this article.
{% endhint %}

### How to configure failover

To configure failover, follow these steps:

1\. First, search for the API whose endpoints you want to configure failover for.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/c49cd12d-c15a-4336-bd9f-c47d12bae8f5/2.5/18.634259259259/19.148284313725?0)

2\. Select the **Edit API** icon.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/45a34f5e-3580-4a1e-8c8a-b0375d25be07/2.5/95.833333333333/49.307436790506?0)

3\. Like load-balancing, failover is a backend service. To make failover configurations, select **Backend services** in the **Proxy** section.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/52c7ec53-d5b7-486c-86ac-e9012ecaa972/1.5/15.046296296296/55.830753353973?0)

4\. Select the **Failover** tab.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/87522d51-7e88-4e61-9f16-6c75c1efd846/2.5/39.467592592593/9.5975232198142?0)

5\. Toggle **Enable Failover** ON.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/213683b2-cd69-4004-83ef-09d68578019c/2.5/36.082175925926/23.735810113519?0)

6\. Next, you'll need to define your Max attempts setting. This setting defines the upper limit for the number of possible Gravitee API Gateway attempts to find a suitable endpoint, according to the load balancing algorithm, before returning an error.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/b35939dc-685a-411b-afe1-fe1320e9a988/1.2507598784195/64.178240740741/36.532507739938?0)

7\. After you define your Max attempts setting, define your Timeout setting. The Timeout setting defines the upper limit for time spent (in ms) between each attempt before timing out.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/c1a1ba3a-bb99-476a-bd25-46adb82564a1/1.2507598784195/64.178240740741/56.883707430341?0)

{% hint style="success" %}
Congrats! Once you hit **Save,** you will have configured failover successfully.&#x20;
{% endhint %}

### Configure Gravitee health checks

To configure health checks in Gravitee, follow these steps:

1\. Select the API whose endpoints you want to configure a health check for.

![](https://dubble-prod-01.s3.amazonaws.com/assets/95835132-46be-42d5-9fa3-9fd374e2b23a.png?0)

2\. Select the **Edit API** icon.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/d5ae9220-2c42-4cd0-9527-b37afe875169/1.5/95.833333333333/49.307436790506?0)

3\. Like load-balancing and failover, health checks are a backend service provided out-of-the-box by Gravitee. Select **Backend services** within the **Proxy** section.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/654ff309-c168-40e0-82e2-a4e38aaed173/1/13.888888888889/56.862745098039?0)

4\. In the Backend services menu, select **Health-check**.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/733bdda1-a849-4ed8-a193-018ff3f14568/1.5/53.356481481481/9.5975232198142?0)

5\. Toggle **Enable health-check** ON.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/8f5b6037-f3b0-4e16-8e63-3d8d52b10335/2.5/36.545138888889/37.203302373581?0)

6\. Now, you'll need to define your Trigger settings. The first step is to define the Trigger schedule, which will define a time interval between each health check.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/1619e966-8fda-407f-bdc8-36f230e805d5/1.2252234684804/64.178240740741/52.671891124871?0)

7\. Next, enter the HTTP method that will trigger the health check.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/a9a03a97-cd64-4b4d-8e03-11b5fafe0d4c/1.2507598784195/64.178240740741/70.915570175439?0)

8\. Next, define the Path that will trigger the health check. Optionally, you can choose to toggle **From root path ('/')** ON. This will apply the path specified at the root URL level. For example, if your endpoint URL is `www.test.com/api`, this option removes /api before appending the path.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f3b66f85-49b5-42fd-bd88-14b51181550c/2.5/35.624757317802/63.466686016512?0)

9\. In the HTTP Headers section, you can specify any headers that you want to trigger a health check. You can use the Gravitee Expression Language to configure a header. Available variables are dictionaries and API’s properties access.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/04225d0c-29bf-4d83-b1c3-7d0e9cbcae6e/2.5/49.956597222222/69.513512641899?0)

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/2b6db031-54e1-42ea-9f65-e668712a835c/2.5/49.956597222222/90.15334752322?0)

11\. In the Assertions section, you can specify any conditions to test for in the API response in order to trigger a health check. Assertions are written in Gravitee Expression Language. An assertion can be a simple 200 response (#response.status == 200), but you can also test for specific content.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/3e574674-2b01-4f8f-bf29-8f9000a86851/1.3402555910543/62.789351851852/72.078173374613?0)

12\. To add an assertion, select **+ Add assertion**.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/fcdc7f5a-01de-4865-bf38-8e09268ef122/2.5/35.9375/80.366357069143?0)

{% hint style="success" %}
To finish up, select **Save**. You can see a visual summary of the health check configuration you specified on the right.
{% endhint %}

