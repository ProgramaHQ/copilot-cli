# AWS Copilot v1.17: Tracing for Request-Driven Web Services.

It's only been a week since v1.16! The AWS Copilot core team, together with AWS App Runner, is announcing support for integrated tracing using AWS X-Ray with OpenTelemetry.
To learn more about App Runner's release, see [here](https://aws.amazon.com/blogs/containers/tracing-an-aws-app-runner-service-using-aws-x-ray-with-opentelemetry/). For
enabling tracing for your Request-Driven Web Services in Copilot, [see detailed section](./#send-your-request-driven-web-services-traces-to-aws-xray).


Special shout-out to [@kangere](https://github.com/kangere)
who contributed to this release. Our public [сommunity сhat](https://gitter.im/aws/copilot-cli) is growing and has over 270 people online,
who help each other daily. Thanks to every one of you who shows love and support for AWS Copilot.

Copilot v1.17 brings a brand-new feature and several improvements:

* **Tracing for Request-Driven Web Service:** With the release of AWS X-Ray tracing support for AWS App Runner services, you can now add `observability.tracing: awsxray` in your Request-Driven Web Service's 
  manifest to send your traces to AWS X-Ray. [See detailed section](./#send-your-request-driven-web-services-traces-to-aws-xray).
* **Allow disabling of Scheduled Jobs**: 
  Easily toggle your Scheduled Job off by setting your schedule to "none" in your manifest, disabling the event rule. ([#3447](https://github.com/aws/copilot-cli/pull/3447))
  ```yaml
  on:
    schedule: "none"
  ```
* **Increased visibility for progress trackers:** Now progress trackers are showing more information, such as the creation of HTTP listener rules. ([#3430](https://github.com/aws/copilot-cli/pull/3430) & [#3432](https://github.com/aws/copilot-cli/pull/3432)).
* **Bug fix:** Remove color formatting of suggested pipeline names ([#3437](https://github.com/aws/copilot-cli/pull/3437)).

There is no breaking change in this release.

## What’s AWS Copilot?

The AWS Copilot CLI is a tool for developers to build, release, and operate production ready containerized applications on AWS.  
From getting started, pushing to staging, and releasing to production, Copilot can help manage the entire lifecycle of your application development.
At the foundation of Copilot is AWS CloudFormation, which enables you to provision infrastructure as code in a single operation.
Copilot provides pre-defined CloudFormation templates and user-friendly workflows for different types of micro services creation and operation,
enabling you to focus on developing your application, instead of writing deployment scripts.

See the section [Overview](../docs/concepts/overview.en.md) for a more detailed introduction to AWS Copilot.

## Send Your Request-Driven Web Service's Traces to AWS X-Ray
_Contributed by [Wanxian Yang](https://github.com/Lou1415926/)_

You can now send traces generated by your Request-Driven Web Services to AWS X-Ray. This allows you to visualize the service map and traces 
through the Amazon CloudWatch console or AWS X-Ray console.

To use this feature, your service needs to be first instrumented with 
[AWS Distro for OpenTelemetry](https://aws.amazon.com/otel/?otel-blogs.sort-by=item.additionalFields.createdDate&otel-blogs.sort-order=desc).
You can either [manually instrument](https://aws-otel.github.io/docs/getting-started/python-sdk/trace-manual-instr) your service, 
or for a quicker, easier set up, [auto-instrument](https://aws-otel.github.io/docs/getting-started/python-sdk/trace-auto-instr) 
your service through your Dockerfile without changing the application code.

After instrumenting your service, simply modify your Request-Driven Web Service's manifest to include the [observability](../docs/manifest/rd-web-service.en.md#observability) configuration:
```yaml
observability:
  tracing: awsxray
```

After running `copilot svc deploy`, traces generated by your service will get sent to AWS X-Ray, allowing you to measure
the current state of your services easily.


## What’s next?

Download the new Copilot CLI version by following the link below and leave your feedback on [GitHub](https://github.com/aws/copilot-cli/) or our [Community Chat](https://gitter.im/aws/copilot-cli):

* Download [the latest CLI version](../docs/getting-started/install.en.md)
* Try our [Getting Started Guide](../docs/getting-started/first-app-tutorial.en.md)
* Read full release notes on [GitHub](https://github.com/aws/copilot-cli/releases/tag/v1.17.0)

