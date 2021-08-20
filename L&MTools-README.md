# Logging & Monitoring Tools Usage
Deploying to Google Cloud wasn't as easy as it looks at face value. I had to utilize the cloud logging tool to find out why my application was not deploying successfully the first few times. Take a look below... it took THREE attempts before I realized what the problem was.

![The Errors](https://github.com/MatthewPalmer9/CloudUsageReport/blob/master/images/error-overview.PNG)

# The Problem
I received this exact same error message all three times.

![Error Message](https://github.com/MatthewPalmer9/CloudUsageReport/blob/master/images/error-message.PNG)

When I Googled this error initially, it brought me to this page.
- [First disgnostic attempt I followed...](https://cloud.google.com/sdk/docs/downloads-docker)
I followed these steps for my own case, but this did not solve the problem.

# The Solution
As it turns out, it was my own error during configuration. It wasn't until I left `Build Summary` and went into the final step.... `Deploy`. This is when I noticed... everything is building correctly, so what's going on with the actual deployment? Let's see..

![The Problem](https://github.com/MatthewPalmer9/CloudUsageReport/blob/master/images/the-problem.PNG)

Ahhh... It's the port. Within the project's dockerfile, it defines an exploted port `443`, but the Google Cloud configuration automatically chose `8080`. Since the defined configurations specify `8080:443`, it chose `8080` as the default. But `8080` isn't the port! 

Thanks to the logging tools, I was able to fix this and successfully deploy my application. Now that everything is up and running, I was able to start utilizing the Metrics tool to monitor things like Request counts, latencies, instance counts, and ultimately see that my application is running very healthy right out of the gate with ZERO errors found.

![Zero Errors](https://github.com/MatthewPalmer9/CloudUsageReport/blob/master/images/zero-errors.PNG)



