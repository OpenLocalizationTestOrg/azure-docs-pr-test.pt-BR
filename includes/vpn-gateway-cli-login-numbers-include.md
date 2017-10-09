1. Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela. Para obter mais informações sobre registro em log, consulte [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli).

  ```azurecli
  az login
  ```
2. Se você tiver mais de uma assinatura do Azure, liste as assinaturas Olá conta hello.

  ```azurecli
  az account list --all
  ```
3. Especifique que você deseja toouse de assinatura de saudação.

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```