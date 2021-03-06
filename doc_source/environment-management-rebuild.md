# Rebuilding AWS Elastic Beanstalk Environments<a name="environment-management-rebuild"></a>

Your Elastic Beanstalk environment can become unusable if you don't use Elastic Beanstalk functionality to modify or terminate the environment's underlying AWS resources\. If this happens, you can **rebuild** the environment to attempt to restore it to a working state\. Rebuilding an environment terminates all of its resources and replaces them with new resources with the same configuration\.

You can also rebuild terminated environments within six weeks \(42 days\) of their termination\. When you rebuild, Elastic Beanstalk attempts to create a new environment with the same name, ID, and configuration\.

## Rebuilding a Running Environment<a name="environment-management-rebuild-running"></a>

You can rebuild an environment through the Elastic Beanstalk console or by using the `RebuildEnvironment` API\.

**To rebuild a running environment \(console\)**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Navigate to the management page for your environment\.

1. Choose **Actions**, and then choose **Rebuild environment**\.

1. Choose **Rebuild**\.

Rebuilding a running environment creates new resources that have the same configuration as the old resources; however, the resource IDs are different, and any data on the old resources is not restored\. For example, rebuilding an environment with an Amazon RDS database instance creates a new database with the same configuration, but does not apply a snapshot to the new database\.

To rebuild a running environment with the Elastic Beanstalk API, use the [http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_RebuildEnvironment.html](http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_RebuildEnvironment.html) action with the AWS CLI or the AWS SDK\.

```
$ aws elasticbeanstalk rebuild-environment --environment-id e-vdnftxubwq
```

## Rebuilding a Terminated Environment<a name="environment-management-rebuild-terminated"></a>

You can rebuild and restore a terminated environment by using the Elastic Beanstalk console, the EB CLI, or the `RebuildEnvironment` API\.

**Note**  
Unless you are using your own custom domain name with your terminated environment, the environment uses a subdomain of elasticbeanstalk\.com\. These subdomains are shared within an Elastic Beanstalk region\. Therefore, they can be used by any environment created by any customer in the same region\. While your environment was terminated, another environment could use its subdomain\. In this case, the rebuild would fail\.  
You can avoid this issue by using a custom domain\. See  for details\.

Recently terminated environments appear in the application overview for up to an hour\. During this time, you can view events for the environment in its dashboard, and use the **Restore environment** action to rebuild it\.

To rebuild an environment that is no longer visible, use the **Restore terminated environment** option from the application page\.

**To rebuild a terminated environment \(console\)**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Choose your application\.

1. Choose **Actions**, and then choose **Restore terminated environment**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/applications-restoreenvironment.png)

1. Choose a terminated environment\.

1. Choose **Restore**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/applications-restoreenvironment-modal.png)

Elastic Beanstalk attempts to create a new environment with the same name, ID, and configuration\. If an environment with the same name or URL exists when you attempt to rebuild, the rebuild fails\. Deleting the application version that was deployed to the environment will also cause the rebuild to fail\.

If you use the EB CLI to manage your environment, use the `eb restore` command to rebuild a terminated environment\.

```
$ eb restore e-vdnftxubwq
```

See `eb restore` for more information\.

To rebuild a terminated environment with the Elastic Beanstalk API, use the [http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_RebuildEnvironment.html](http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_RebuildEnvironment.html) action with the AWS CLI or the AWS SDK\.

```
$ aws elasticbeanstalk rebuild-environment --environment-id e-vdnftxubwq
```