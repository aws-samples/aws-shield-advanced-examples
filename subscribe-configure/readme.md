# AWS Shield Advanced Subscription and Configuration with AWS CloudFormation

Two example templates are provided to help you  subscribe and/or configure AWS Shield Advanced using CloudFormation.


The key different is shield-configure-subscribe.yaml includes a custom lambda backed resource to subscribe (if not already) the account to AWS Shield Advanced.  YOu can also subscribe an account to AWS Shield Advanced via the [console](https://docs.aws.amazon.com/waf/latest/developerguide/enable-ddos-prem.html), [API](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/shield/client/create_subscription.html#), or using [Firewall Manager](https://docs.aws.amazon.com/waf/latest/developerguide/getting-started-fms-shield.html).

Note:
> The custom lambda backed resource to subscribe to AWS Shield will gracefully continue if an account is already subscribed to AWS Shield Advanced.

> If you delete this template, the custom lambda backed resource does **NOT** unsubscribe you from AWS Shield Advanced.  See [here](https://aws.amazon.com/shield/pricing/) for information about when and how to unsubscribe (Note #3)


## shield-configure-subscribe

This template includes a custom lambda backed resource to subscribe (if not already) the account to AWS Shield Advanced.  If you elect to enable SRT Access and/or Proactive Engagement, the account must have Business or Enterprise support before these can be enabled.


## shield-configure-no-subscription

This template assumes you already have subscribe to AWS Shield Advanced outside of this template.  If you elect to enable SRT Access and/or Proactive Engagement, the account must have Business or Enterprise support before these can be enabled.

Note: If you delete this template, it does **NOT** unsubscribe the account from AWS Shield Advanced.  See [here](https://aws.amazon.com/shield/pricing/)for information about when and how to unsubscribe; see Note #3



## StackSets

AWS CloudFormation Stacksets are a native AWS way to deploy a CloudFormation template to many accounts from a single logical entity.  If you choose to use a StackSets to subscribe and configure AWS Shield Advanced, keep the following in mind.

* If using a service managed stack set with auto-deployment enabled, be sure accounts that come into scope of the stackset already have Business or Enterprise Support enabled.
* If using a service managed stack set with auto-deployment enabled and do not use the template that includes creating a Shield subscription fires, ensure you create a Shield subscription before a new account is in scope
* If you use AWS Firewall Manager to subscribe to AWS Shield Advanced for you, you should consider:
    * Use a self managed stack set or service managed stackset with auto-deployment disabled.
    * Target specific OUs with a stackset and create a shield subscription and enable Support before moving an account into scope

