# What can I do if health checks generate an excessive number of logs? {#concept_hpj_h2d_xdb .concept}

SLB can automatically save health check logs generated in three days. If too many health check logs are generated and affect your maintenance, you can reduce health check logs or prevent certain logs from being generated through the following methods.

**Note:** If you reduce health check logs, SLB faults may be missed. Therefore, we recommend that you consider the risks of the following methods and use the methods with caution.

-   [Get access logs](#section_ubj_tgd_xdb)
-   [Adjust health check frequency](#section_a5r_bhd_xdb)
-   [Close Layer-7 health checks](#section_dj2_rjd_xdb)
-   [Change Layer-7 SLB to Layer-4 SLB](#section_ahx_1ld_xdb)
-   [Disable application logs on the health check page](#section_snb_nnd_xdb)

## Get access logs {#section_ubj_tgd_xdb .section}

HTTP health checks use the HEAD request method by default \(the GET method will be supported later\). Therefore, you can obtain access logs by filtering out HEAD requests.

## Adjust health check frequency {#section_a5r_bhd_xdb .section}

You can increase the interval between two health checks to reduce the health check frequency and generated logs.

Potential risks

After you increase the interval, if a backend ECS instance fails, the time needed for SLB to detect the faulty ECS instance is increased accordingly.

Procedure

1.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
2.  On the Server Load Balancer page, click the ID of the target SLB instance.
3.  Click the Listeners tab, find the target listener, and click **Configure** in the **Actions** column.
4.  On the Configure Listener page, click **Next** and then click **Next** again to go to the **Health Check** tab.
5.  Adjust the **Health Check Interval**. Value range: 1 to 50. Unit: seconds. The greater the interval is, the lower the health check frequency is, and the fewer logs are generated by backend servers. Modify the interval according to your actual situation.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/4302/156571647213840_en-US.png)

6.  Click **OK**.

## Close Layer-7 health checks {#section_dj2_rjd_xdb .section}

When Layer-7 \(HTTP or HTTPS\) SLB is used, health checks are performed through HTTP HEAD requests. Application logs of backend servers record the health check requests, leading to a large number of logs.

Potential risks

After you close HTTP/HTTPS health checks, SLB does not check backend servers. If a backend server fails, the traffic cannot be automatically forwarded to other normal backend servers.

Procedure

1.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
2.  On the Server Load Balancer page, click the ID of the target SLB instance.
3.  Click the **Listeners** tab, find the target listener, and click **Configure** in the **Actions** column.
4.  On the Configure Listener page, click **Next** and then click **Next** again to go to the **Health Check** tab.
5.  Turn off **Enable Health Check**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/4302/156571647213841_en-US.png)

6.  Click **OK**.

## Change Layer-7 SLB to Layer-4 SLB {#section_ahx_1ld_xdb .section}

Layer-4 health checks are preformed through TCP three-way handshakes and generate no application logs. If you change Layer-7 SLB to Layer-4 SLB, the number of application logs can be reduced.

Potential risks

After you change the Layer-7 SLB to Layer-4 SLB, SLB checks only the status of the listener port and does not check the HTTP status. In this way, SLB cannot detect the exceptions occurring to HTTP applications in real time.

Procedure

1.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
2.  On the Server Load Balancer page, click the ID of the target SLB instance.
3.  Click the **Listeners** tab, find the target listener, and click **Configure** in the **Actions** column.
4.  On the Configure Listener page, click **Next** and then click **Next** again to go to the **Health Check** tab.
5.  Change the **Health Check Protocol** to **TCP**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/4302/156571647213842_en-US.png)

6.  Click **OK**.

## Disable application logs on the health check page {#section_snb_nnd_xdb .section}

You can configure an independent site for health checks and disable application logs of this site. This method can also reduce the number of health checks. For example, the service site is abc.123.com. You can use test.123.com as the health check site and disable logs of test.123.com.

Potential risks

If the health check site is running normally, but an exception occurs to the service site, health checks cannot detect the exception of the service site.

Procedure

1.  Create a new health check site and health check page on the backend server and disable logs. In this example, NGINX is used.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/4302/15657164723405_en-US.png)

2.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
3.  On the Server Load Balancer page, click the ID of the target SLB instance.
4.  Click the **Listeners** tab, find the target listener, and click **Configure** in the **Actions** column.
5.  On the Configure Listener page, click **Next** and then click **Next** again to go to the **Health Check** tab.
6.  In the **Health Check Domain Name** field, enter the domain name of the health check site. In the **Health Check Path** field, enter the path of the health check page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/4302/156571647213845_en-US.png)

7.  Click **OK**.

