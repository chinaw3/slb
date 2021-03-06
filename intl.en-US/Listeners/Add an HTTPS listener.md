# Add an HTTPS listener {#task_1563673 .task}

This topic describes how to add an HTTPS listener to a Server Load Balancer \(SLB\) instance. You can add an HTTPS listener to forward requests from the HTTPS protocol.

An SLB instance is created. For more information, see [Create an SLB instance](../reseller.en-US/Instance/Create an SLB instance.md#).

## Step 1 Open the listener configuration wizard {#section_zd7_xi8_xj0 .section}

To open the listener configuration wizard, follow these steps:

1.  Log on to the [Server Load Balancer console](https://partners-intl.console.aliyun.com/#/slb). 
2.  In the left-side navigation pane, choose **Instances** \> **Server Load Balancer**.
3.  Select the region of the target SLB instance.
4.  Select one of the following methods to open the listener configuration wizard: 
    -   On the Server Load Balancer page, find the target SLB instance and then click **Configure Listener** in the **Actions** column.

        ![Listener configuration wizard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16139/156687442610004_en-US.png)

    -   On the Server Load Balancer page, click the ID of the target SLB instance. On the Listeners tab, click **Add Listener**.

        ![Add listener](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16161/15668744277399_en-US.png)


## Step 2 Configure the HTTPS listener {#section_k58_mb2_whz .section}

To configure the HTTPS listener, follow these steps:

1.  On the Protocol and Listener page, configure the HTTPS listener according to the following information: 

    |Configuration|Description|
    |:------------|:----------|
    |**Select Listener Protocol**|Select the protocol type of the listener. In this topic, select **HTTPS**.

 |
    |**Listening Port**|The listening port used to receive requests and forward the requests to backend servers. Value range: 1 to 65535

 **Note:** The listening port must be unique in an SLB instance.

 |
    |**Advanced configurations**|
    |**Scheduling Algorithm**|SLB supports three scheduling algorithms: round robin, weighted round robin \(WRR\), and weighted least connections \(WLC\).     -   **Weighted Round-Robin \(WRR\)**: A backend server with a higher weight receives more requests.
    -   **Round-Robin \(RR\)**: Requests are evenly and sequentially distributed to backend servers.
    -   **Weighted Least Connections \(WLC\)**: A server with a higher weight receives more requests. When the weight values of two backend servers are the same, the backend server with a smaller number of connections is more likely to be polled.
 |
    |**Enable Session Persistence**| Select whether to enable session persistence.

 After you enable session persistence, all session requests from the same client are sent to the same backend server.

 HTTP session persistence is based on cookies. The following two methods are supported:

     -   **Insert cookie**: You only need to specify the cookie timeout period.

SLB adds a cookie to the first response from the backend server \(inserts SERVERID in the HTTP and HTTPS response packet\). The next request will contain the cookie and the listener will distribute the request to the same backend server.

    -   **Rewrite cookie**: You can set the cookie to be inserted to the HTTP or HTTPS response according to your needs. You must maintain the timeout period and lifecycle of the cookie on the backend server.

SLB will overwrite the original cookie when it discovers that a new cookie is set. The next time the client carries the new cookie to access SLB, the listener will distribute the request to the recorded backend server. For more information, see [Configure session persistence](../reseller.en-US/FAQ/Best practices/Configure cookie in the backend server.md#).

 |
    |**Enable HTTP/2**|Select whether to enable HTTP 2.0.|
    |**Enable Access Control**|Select whether to enable the access control function.|
    |**Access Control Method**| Select an access control method after you enable the access control function:

     -   **Whitelist**: Only requests from IP addresses or CIDR blocks in the selected access control list are forwarded. It applies to scenarios where the application only allows access from some specific IP addresses.

Enabling a white access control list poses some risks to your services. After a whitelist is configured, only the IP addresses in the list can access the listener. If you enable the whitelist without adding any IP addresses in the corresponding access control list, all requests are forwarded.

    -   **Blacklist**: Requests from IP addresses or CIDR blocks in the selected access control list are not forwarded. It applies to scenarios where the application only denies access from some specific IP addresses.

If you enable a blacklist without adding any IP addresses in the corresponding access control list, all requests are forwarded.

 |
    |**Access Control List**|Select an access control list as the whitelist or the blacklist. **Note:** An IPv6 instance can only be associated with IPv6 access control lists and an IPv4 instance can only be associated with IPv4 access control lists. For more information, see [Configure an access control list](reseller.en-US/Archives/User Guide (Old Console)/Access control/Configure an access control list.md#).

 |
    |**Enable Peak Bandwidth Limit**| Select whether to configure the listening bandwidth.

 If the SLB instance is charged based on bandwidth, you can set different peak bandwidth values for different listeners to limit the traffic passing through each listener. The sum of the peak bandwidth values of all listeners under an SLB instance cannot exceed the bandwidth value of that SLB instance.

 By default, all listeners share the bandwidth of the SLB instance.

 **Note:** SLB instances billed by traffic have no peak bandwidth limit by default.

 |
    |**Idle Timeout**|Specify the idle connection timeout period. Value range: 1 to 60. Unit: seconds. If no request is received during the specified timeout period, SLB temporarily terminates the connection and restarts the connection when the next request is received.

 This function is available in all regions.

 |
    |**Request Timeout**|Specify the request timeout period. Value range: 1 to 180. Unit: seconds. If no response is received from the backend server during the specified timeout period, SLB stops waiting and sends an HTTP 504 error code to the client.

 Currently, this function is available in all regions.

 |
    |**TLS Security Policy**| Only guaranteed-performance instances support selecting the TLS security policy.

 The TLS security policy contains available TLS protocol versions and supported cipher suites. For more information, see [Manage TLS security policies](reseller.en-US/Listeners/Manage TLS security policies.md#).

 |
    |**Enable Gzip Compression**|Choose whether to enable Gzip compression to compress files of specific formats. Now Gzip supports the following file types: text/xml, text/plain, text/css, application/javascript, application/x-javascript, application/rss+xml, application/atom+xml, and application/xml.

 |
    |**Add HTTP Header Fields**|Select the custom HTTP headers that you want to add:     -   Use the `X-Forwarded-For` field to retrieve client source IP addresses.
    -   Use the `X-Forwarded-Proto` field to retrieve the listener protocol used by the SLB instance.
    -   Use the `SLB-IP` field to retrieve the public IP address of the SLB instance.
    -   Use the `SLB-ID` field to retrieve the ID of the SLB instance.
 |
    |**Get Client Source IP Address**|HTTP listeners use X-Forwarded-For to obtain real IP addresses of clients.|
    |**Automatically Enable Listener After Creation**|Choose whether to start the listener after the listener is configured. The listener is started by default.|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16604/156687442811858_en-US.png)

2.  Click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16604/156687442810035_en-US.png)


## Step 3 Configure the SSL certificate {#section_dk9_0ci_bod .section}

To add an HTTPS listener, you must upload a server certificate or CA certificate, as shown in the following table.

|Certificate|Description|Required for one-way authentication?|Required for mutual authentication?|
|:----------|:----------|:-----------------------------------|:----------------------------------|
|Server certificate|Used to identify a server. The client uses it to check whether the certificate sent by the server is issued by a trusted center.

 |Yes. You need to upload the server certificate to the certificate management system of SLB.

 |Yes. You need to upload the server certificate to the certificate management system of SLB.

 |
|Client certificate|Used to identify a client. The client user can prove its true identity when communicating with the server. You can sign a client certificate with a self-signed CA certificate.

 |No.|Yes. You need to install the client certificate on the client.

 |
|CA certificate|The server uses the CA certificate to authenticate the signature on the client certificate, as part of the authentication before launching a secure connection. If the authentication fails, the connection is rejected.|No.|Yes. You need to upload the CA certificate to the certificate management system of SLB.

 |

Note the following before you upload a certificate:

-   The uploaded certificate must be in the PEM format. For more information, see [Certificate requirements](../reseller.en-US/Certificate management/Certificate requirements.md#).
-   After the certificate is uploaded to SLB, SLB can manage the certificate and you do not need to associate the certificate with backend ECS instances.
-   It usually takes one to three minutes to activate the HTTPS listener because the uploading, loading, and validation of certificates take some time. Normally it takes effect in one minute and it will definitely take effect in three minutes.
-   The ECDHE algorithm cluster used by HTTPS listeners supports forward secrecy, but does not support uploading security enhancement parameter files required by the DHE algorithm cluster, such as strings containing the `BEGIN DH PARAMETERS` field in the PEM certificate file. For more information, see [Certificate requirements](../reseller.en-US/Certificate management/Certificate requirements.md#).
-   Currently, SLB HTTPS listeners do not support SNI \(Server Name Indication\). You can use TCP listeners instead, and then configure SNI on backend ECS instances.
-   The session ticket timeout period of HTTPS listeners is 300 seconds.
-   The actual amount of traffic is larger than the billed traffic amount because some traffic is used for protocol handshaking.
-   In the case of a large number of new connections, HTTPS listeners consume more traffic.

1.  Select the server certificate that has been uploaded, or click **Create Server Certificate** to upload a server certificate. For more information, see [Create a certificate](../reseller.en-US/Certificate management/Create a certificate/Overview.md#).
2.  If you want to enable HTTPS mutual authentication or set a TLS security policy, click **Modify**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16604/156687442847905_en-US.png)

3.  Select an uploaded CA certificate, or click **Create CA Certificate** to upload a CA certificate. You can use a self-signed CA certificate. For more information, see [Create a certificate](../reseller.en-US/Certificate management/Create a certificate/Overview.md#).
4.  Select a TLS security policy. For more information, see [Manage TLS security policies](reseller.en-US/Listeners/Manage TLS security policies.md#).

## Step 4 Add backend servers {#section_ib1_z58_t2l .section}

You need to add backend servers to process requests. You can use the default server group configured for the SLB instance, or configure a VServer group or an active/standby server group for the listener. For more information, see [Backend server overview](../reseller.en-US/Backend servers/Backend server overview.md#).

In this topic, use the default server group.

1.  Select **Default Server Group** and then click **Add More**. 

    ![Add default servers](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16139/156687442910030_en-US.png)

2.  Select the ECS instances to add, and then click **Next: Set Weight and Port**. 

    ![Configure weights](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16139/15668744337499_en-US.png)

3.  Configure ports and weights for the added backend servers \(ECS instances\). 
    -   Port

        The port opened on the backend server to receive requests. The port number is in the range of 1 to 65535. Ports of backend servers can be the same in an SLB instance.

    -   Weight

        The weight of the backend server. A backend server with a higher weight receives more requests.

        **Note:** If the weight is set to 0, no requests are sent to the backend server.

        ![Set weights](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16139/15668744337504_en-US.png)

4.  Click **Next**.

## Step 5 Configure health checks {#section_cut_74n_vc5 .section}

SLB checks the service availability of backend servers by performing health checks. The health check function improves the overall availability of your services and avoids the impact of backend server failures. Click **Modify** to change health check configurations. For more information, see [Health check overview](../reseller.en-US/Health check/Health check overview.md#).

## Step 6 Submit the configurations {#section_k0i_zfp_3ow .section}

To submit the listener configurations, follow these steps:

1.  On the Submit page, check the listener configurations. You can click **Modify** to change the configurations.
2.  Click **Submit**.
3.  On the Submit page, click **OK** after the configurations are successful. 

    After the configurations are successful, you can view the created listener on the **Listeners** page.


[Configure health checks](../reseller.en-US/Health check/Configure health checks.md#)

[Manage a default server group](../reseller.en-US//Manage a default server group.md#)

[Manage a VServer group](../reseller.en-US//Manage a VServer group.md#)

[Manage an active/standby server group](../reseller.en-US//Manage an active__standby server group.md#)

[Configure access control](../reseller.en-US/Access control/Configure access control.md#)

[Traffic forwarding based on domain names or URLs](../reseller.en-US/Tutorials/Traffic forwarding based on domain names or URLs.md#)

[Manage a domain name extension](../reseller.en-US/Listeners/Domain name extensions/Manage a domain name extension.md#)

[CreateLoadBalancerHTTPSListener](../reseller.en-US/Developer Guide/HTTPS listeners/CreateLoadBalancerHTTPSListener.md#)

