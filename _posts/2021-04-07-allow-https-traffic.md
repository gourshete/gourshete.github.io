---
layout: post
title:  "Allow HTTPS traffic via AWS Load balancer and EC2"
date:   2021-04-07
keywords: "ruby rails aws load-balancer ec2 instance github learning swapnil gourshete ruby on rails"
image: assets/images/aws-icon.png
categories: [ Rails, AWS, ELB, EC2 ]
---

In this post we will achieve passing only https traffic to EC2 via application load balancer.

Pre-requisites:

1. running EC2 instance
2. SSL certificate added to AWS Certificate Manager

-

First we need to setup an AWS Load balancer. If you have load balancer created, then please skip to 
<a href="#skip-step">this step</a>  
AWS provides three types of LB - application, network and classic, while 
AWS itself promotes application LB for Modern web applications.

<img src="{{ '/assets/images/aws-lb-types.png' | prepend: site.baseurl }}" alt="aws-load-balancer-types">

- <h4>Create Application Load Balancer</h4>

  1. Open the Amazon EC2 console at <a href="https://console.aws.amazon.com/ec2/" target="_blank"> https://console.aws.amazon.com/ec2/ </a>
  2. On the navigation pane, open CREATE LOAD BALANCER.
  3. Choose Create for Application Load Balancer.

-

- <h4>Adding listener configuration</h4>

  We need to add where load balancer is listening. We also need to specify what action should be taken, but it is covered
  later in the post as it has a pre-requisite task. 
  We will listen from both ports 80 and 443.
  1. For port 443 (HTTPS) - On AWS console, for port choose HTTPS and for port choose 443. 
     
  2. For port 80 (HTTP) - On AWS console, for protocol choose HTTP and for port choose 80.
  
-

- <h4>Configure Security Settings</h4> 

  AWS Certificate Manager (ACM) is the preferred tool to provision and store server certificates. If you previously 
  stored a server certificate using IAM, you can deploy it to your load balancer.
  From Certificate type dropdown choose Choose a certificate from ACM (recommended). Select Certificate from Certificate 
  name dropdown.

-

- <h4>Adding VPC and security groups</h4>

  Add appropriate VPC and security groups to your ALB

-

- <h4>Adding target group</h4>

  Create new target group with protocol (HTTP) and port (80). For health check keep default settings or assign any other
  route your application has, it will be used for periodically checking health of target group. Use this target group to
  forward your traffic from listener port 443 (From the above steps).

<img src="{{ '/assets/images/lb-health-check.png' | prepend: site.baseurl }}" alt="load-balancer-health-check">

-
  
- <h4>Listeners & targets settings</h4>

  Open listeners edit option and do changes for following 
  1. For port 80 (HTTP) - Open edit option. For Default action(s), choose Redirect to. Choose HTTPS & 443 and Original host, path, query 
     from dropdown. This will redirect all traffic on port 80 to port 443 (https) on same host.
  2. For port 443 (HTTPS) - Open edit option. Select protocol HTTPS and port 443. For Default action(s), choose Forward 
     to and then select your ALB target group from the drop-down menu. For Default SSL certificate, choose From ACM
     (recommended) and then choose the ACM certificate.
  
-

<div id="skip-step"></div>

- <h5>Already have Application Load Balancer up and running, then</h5>

  1. In the navigation pane, choose Load Balancers and then choose your Application Load Balancer.
  2. Choose Add listener.
  3. For Protocol, choose HTTPS.
  4. For port, choose 443.
  5. For Default action(s), choose Forward to, and then select your ALB target group from the drop-down menu.
  6. For Default SSL certificate, choose From ACM (recommended) and then choose the ACM certificate. 
  7. Choose Save.
  If you are operating classic load balancer, then the process is slightly different. Please refer to this guide -
     <a href="https://aws.amazon.com/premiumsupport/knowledge-center/associate-acm-certificate-alb-nlb/" target="_blank">https://aws.amazon.com/premiumsupport/knowledge-center/associate-acm-certificate-alb-nlb/</a

-

---

References -

- <a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html" target='_blank'>https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html</a>

- <a href="https://aws.amazon.com/premiumsupport/knowledge-center/associate-acm-certificate-alb-nlb/" target="_blank">https://aws.amazon.com/premiumsupport/knowledge-center/associate-acm-certificate-alb-nlb/</a>
