## Infrastructure

So you wrote your web server and ui. Now you want to share it, but you also have a limited bandwidth plan with your ISP and don't want to keep your linux machine running 24/7.

Plus do you really want strange web traffic coming through your house?

Probably not. So you need to know where to run it, how to get a domain name, and how to get an HTTPS certificate. Plus those HTTPS certificates expire every so often and no one remembers to renew them by hand.

There are services for this! AWS and Azure are two enterprise grade services which specialize in providing infrastructure, and Digital Ocean is a simpler alternative for folks who just want it easy.

Typically you rent a linux server e.g. from digital ocean for $5 a month, and `ssh` into it to set up the backend server.

Alternatively use a framework like AWS Lambda to avoid remote linux servers entirely.

## Build Infrastructure

Sometimes it is super convenient to just push code to github and let the tests run somewhere else.

travis-ci.com is an option for this, and github now has its own CI options (Continuous Integration). The idea is that you push your code and the tests all run and whatnot so its always the same remotely even if your local environment gets busted.

## Static websites are free

If you want to share a static website, you can push it to github and use github pages. There are many options for free website hosting.

## A few options

* $5/month from digital ocean is pretty friendly to beginners. I like digital ocean a lot and they have great documentation.
* AWS Free Tier is friendly as well, but AWS is huge and complicated and it is easy to blow through your free tier if you spin up the wrong server sizes. 
   * CloudFront + S3 + ACM can be used for static website hosting.
   * DynamoDB and Lambda is a common cheap combination for low-cost hosting as long as you don't have much traffic.


Think about it, search around, do not spend money on a service "that will be big" instead find a pay-as-you go service which scales cost and infrastructure with traffic.