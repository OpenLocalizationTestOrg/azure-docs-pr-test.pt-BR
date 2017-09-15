<span data-ttu-id="3c872-101">Antes de iniciar essa configuração, você deve fazer logon na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c872-101">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="3c872-102">O cmdlet solicita as credenciais de logon para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c872-102">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="3c872-103">Depois de entrar, ele baixa as configurações da conta para que elas estejam disponíveis para o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c872-103">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span> <span data-ttu-id="3c872-104">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3c872-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="3c872-105">Para fazer logon, abra o console do PowerShell com privilégios elevados e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="3c872-105">To log in, open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="3c872-106">Use o exemplo a seguir para ajudar a se conectar:</span><span class="sxs-lookup"><span data-stu-id="3c872-106">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3c872-107">Se você tiver várias assinaturas do Azure, verifique as assinaturas para a conta.</span><span class="sxs-lookup"><span data-stu-id="3c872-107">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="3c872-108">Especifique a assinatura que você quer usar.</span><span class="sxs-lookup"><span data-stu-id="3c872-108">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```