1. <span data-ttu-id="72405-101">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="72405-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="72405-102">Para obter mais informações sobre registro em log, consulte [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72405-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="72405-103">Se você tiver mais de uma assinatura do Azure, liste as assinaturas Olá conta hello.</span><span class="sxs-lookup"><span data-stu-id="72405-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="72405-104">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="72405-104">Specify hello subscription that you want toouse.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```