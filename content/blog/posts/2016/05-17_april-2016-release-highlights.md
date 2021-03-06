---

date: "2016-05-17"
title: "April 2016 Release Highlights"
description: "Our engineering team spent much of April 2016 focused on quality assurance and framework upgrades, but they still pushed some features we think you’ll love."
category: "Product Updates"
url: "/april-2016-release-highlights/"
layout: "single"
---


Our engineering team spent much of April focused on quality assurance and framework upgrades, but they still had time to push some key features we think you'll love. Check out the April 2016 feature highlights below:

*Our new features are even cooler in person! [Try our demo](/signup) to see them live.*

Amazon Simple Queue Service (SQS) Support
-----------------------------------------

[![April 2016: Amazon SQS Metrics](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-public/wp-content/uploads/2016/05/april-rnh-sqs-1024x470.png)](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-public/wp-content/uploads/2016/05/april-rnh-sqs.png)

The first of new AWS services to come out in the coming weeks, Metricly rolled out a comprehensive analytics set for AWS Simple Queue Service (SQS) elements. Now when you set up an [AWS datasource](https://docs.metricly.com/integrations/aws-integration/) with Metricly, SQS elements are enabled by default (unless you disable by un-checking a box, or filter them.) Monitoring the performance of your SQS queues is as easy as your other AWS elements; just enable collection and let Metricly's behavior learning, pre-configured dashboards, pre-set alerting policies, and out-of-the-box reports do the rest. For more information on the metrics Metricly collects for SQS, visit the [AWS docs](https://docs.metricly.com/integrations/aws-integration/#amazon_metrics).

Updates to the Browser Agent
----------------------------

[![April 2016: browser-changes](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-public/wp-content/uploads/2016/05/april-rnh-browser-changes-1024x335.png)](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-public/wp-content/uploads/2016/05/april-rnh-browser-changes.png)

Previously, a single Browser datasource could only monitor a single web page. With major improvements to a newly designed Browser datasource activation page that leverage functionality improvements in the agent , you can now monitor an entire website using a single datasource. Simply add as many valid URLs or Regex expressions as desired, choose a name for each URL/expression, choose if you want to track the HTTP errors on the page or not, and save the datasource. The browser agent will begin to track the individual URLs/expressions under the same Browser element. Metricly's integration package will provide pre-set dashboards, alerting policies and reports to simplify your day-zero experience.

Generic Cost Reporting for AWS EC2s
-----------------------------------

[![April 2016: Ec2-estimated-costs](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-public/wp-content/uploads/2016/05/april-rnh-ec2-estimated-costs-1024x588.png)](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-public/wp-content/uploads/2016/05/april-rnh-ec2-estimated-costs.png)

About a month ago, Metricly rolled out expansive EC2 cost reporting for customers who activate an AWS Cost datasource that places detailed billing information in an S3 bucket and shares it with Metricly's analytics service via a real-only permission. This report combines billing information with instance utilization data to identify areas of savings. Now Metricly generates generic EC2 cost reporting for your AWS environment so that you can benefit from some of the features of this report without having to activate an AWS Cost datasource. The Estimated EC2 cost report uses estimated instance costs based on current list prices and simple assumptions to fill in missing information.

* * * * *

Want access to all of the April 2016 features and more? Sign up for Metricly's [21-day free trial](/signup)!
