---
ms.topic: include
ms.technology: devops-cicd
ms.manager: mijacobs
ms.author: jukullam
author: juliakm
ms.date: 09/19/2022
---

# [Service principal](#tab/userlevel)

Create a [service principal](/azure/active-directory/develop/app-objects-and-service-principals#service-principal-object) with the [az ad sp create-for-rbac](/cli/azure/ad/sp#az-ad-sp-create-for-rbac) command in the [Azure CLI](/cli/azure/). Run this command with [Azure Cloud Shell](https://shell.azure.com/) in the Azure portal or by selecting the **Try it** button.

```azurecli-interactive
az ad sp create-for-rbac --name "myML" --role contributor \
                            --scopes /subscriptions/<subscription-id>/resourceGroups/<group-name> \
                            --sdk-auth
```

In the example above, replace the placeholders with your subscription ID, resource group name, and app name. The output is a JSON object with the role assignment credentials that provide access to your App Service app similar to below. Copy this JSON object for later.

```output 
  {
    "clientId": "<GUID>",
    "clientSecret": "<GUID>",
    "subscriptionId": "<GUID>",
    "tenantId": "<GUID>",
    (...)
  }
```

# [OpenID Connect](#tab/openid)

OpenID Connect is an authentication method that uses short-lived tokens. Setting up [OpenID Connect with GitHub Actions](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect) is more complex process that offers hardened security. 

1.  If you don't have an existing application, register a [new Active Directory application and service principal that can access resources](/azure/active-directory/develop/howto-create-service-principal-portal). Create the Active Directory application. 

    ```azurecli-interactive
    az ad app create --display-name myApp
    ```

    This command will output JSON with an `appId` that is your `client-id`. Save the value to use as the `AZURE_CLIENT_ID` GitHub secret later. 

    You'll use the `objectId` value when creating federated credentials with Graph API and reference it as the `APPLICATION-OBJECT-ID`.

1. Create a service principal. Replace the `$appID` with the appId from your JSON output. 

    This command generates JSON output with a different `objectId` and will be used in the next step. The new  `objectId` is the `assignee-object-id`. 
    
    Copy the `appOwnerTenantId` to use as a GitHub secret for `AZURE_TENANT_ID` later. 

    ```azurecli-interactive
     az ad sp create --id $appId
    ```

1. Create a new role assignment by subscription and object. By default, the role assignment will be tied to your default subscription. Replace `$subscriptionId` with your subscription ID, `$resourceGroupName` with your resource group name, and `$assigneeObjectId` with the generated `assignee-object-id`. Learn [how to manage Azure subscriptions with the Azure CLI](/cli/azure/manage-azure-subscriptions-azure-cli). 

    ```azurecli-interactive
    az role assignment create --role contributor --scope /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName --subscription $subscriptionId --assignee-object-id  $assigneeObjectId --assignee-principal-type ServicePrincipal
    ```

1. Run the following command to [create a new federated identity credential](/graph/api/application-post-federatedidentitycredentials?view=graph-rest-beta&preserve-view=true) for your active directory application.

    * Replace `APPLICATION-OBJECT-ID` with the **objectId (generated while creating app)** for your Active Directory application.
    * Set a value for `CREDENTIAL-NAME` to reference later.
    * Set the `subject`. The value of this is defined by GitHub depending on your workflow:
      * Jobs in your GitHub Actions environment: `repo:< Organization/Repository >:environment:< Name >`
      * For Jobs not tied to an environment, include the ref path for branch/tag based on the ref path used for triggering the workflow: `repo:< Organization/Repository >:ref:< ref path>`.  For example, `repo:n-username/ node_express:ref:refs/heads/my-branch` or `repo:n-username/ node_express:ref:refs/tags/my-tag`.
      * For workflows triggered by a pull request event: `repo:< Organization/Repository >:pull_request`.
    
    ```azurecli
    az rest --method POST --uri 'https://graph.microsoft.com/beta/applications/<APPLICATION-OBJECT-ID>/federatedIdentityCredentials' --body '{"name":"<CREDENTIAL-NAME>","issuer":"https://token.actions.githubusercontent.com","subject":"repo:organization/repository:ref:refs/heads/main","description":"Testing","audiences":["api://AzureADTokenExchange"]}' 
    ```
    
To learn how to create a Create an active directory application, service principal, and federated credentials in Azure portal, see [Connect GitHub and Azure](/azure/developer/github/connect-from-azure#use-the-azure-login-action-with-openid-connect).

---