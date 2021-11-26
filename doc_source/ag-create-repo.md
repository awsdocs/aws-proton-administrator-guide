# Create and register a link to your repository<a name="ag-create-repo"></a>

You can create and register a link to your repository using the console or CLI\. When you create a repository link, AWS Proton creates a [service linked role](using-service-linked-roles.md) for you\.

------
#### [ AWS Management Console ]

**Create and register a link to your repository as shown in the following console steps\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Repositories**\.

1. Choose **Create repository**\.

1. In the **Link new repository** page, in the **Repository details** section:

   1. Choose your repository provider\.

   1. Choose from your connections\.

   1. Choose from your connected source code repositories\.

1. Choose **Create repository**\.

1. View the detail data for your linked repository\.

------
#### [ AWS CLI ]

**Create and register a link to your repository\.**

Run the following command:

```
aws proton create-repository \
    --name myrepos/environments \
    --connection-arn "arn:aws:codestar-connections:region-id:123456789012:connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111" \
    --provider "GITHUB" \
    --encryption-key "arn:aws:kms:region-id:123456789012:key/bPxRfiCYEXAMPLEKEY
```

Response:

```
{
    "repository": {
        "arn": "arn:aws:proton:region-id:123456789012:repository/github:myrepos/environments",
        "connectionArn": "arn:aws:codestar-connections:region-id:123456789012:connection/2ad03b28-a7c4-EXAMPLE11111",
        "encryptionKey": "arn:aws:kms:region-id:123456789012:key/bPxRfiCYEXAMPLEKEY",
        "name": "myrepos/environments",
        "provider": "GITHUB"
    }
}
```

------