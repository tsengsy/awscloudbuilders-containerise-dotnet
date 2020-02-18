+++
title = "Testing"
date = 2020-02-10T14:00:00+11:00
weight = 6
+++

Finally, let's check if the application is running.

Go back to the `EC2` console and then click on `Load balancer`.

Select the load balancer `awsbuilders-alb` and copy the DNS name.

![](/images/pipeline/pipeline_testing_1.png)

Open your browser and try to access the URL copied from the ALB.

Congratulations, the page below confirms that your .NET application is now containerized!

![](/images/pipeline/pipeline_testing_2.png)