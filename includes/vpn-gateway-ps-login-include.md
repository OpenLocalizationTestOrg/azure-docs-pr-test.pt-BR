<span data-ttu-id="60dae-101">Antes de começar essa configuração, você deve fazer logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="60dae-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="60dae-102">Olá cmdlet solicita as credenciais de logon de saudação para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="60dae-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="60dae-103">Após o logon, ele baixa as configurações de conta para que eles fiquem disponível tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60dae-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="60dae-104">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="60dae-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="60dae-105">toolog, abra o console do PowerShell com privilégios elevados e conectar-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="60dae-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="60dae-106">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="60dae-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="60dae-107">Se você tiver várias assinaturas do Azure, verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="60dae-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="60dae-108">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="60dae-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```