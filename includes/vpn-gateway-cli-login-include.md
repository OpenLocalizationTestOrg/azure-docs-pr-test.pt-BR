<span data-ttu-id="d66ba-101">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="d66ba-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="d66ba-102">Para obter mais informações sobre registro em log, consulte [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d66ba-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="d66ba-103">Se tiver mais de uma assinatura do Azure, liste as assinaturas para a conta.</span><span class="sxs-lookup"><span data-stu-id="d66ba-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="d66ba-104">Especifique a assinatura que você quer usar.</span><span class="sxs-lookup"><span data-stu-id="d66ba-104">Specify the subscription that you want to use.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```