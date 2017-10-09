
## <a name="start-your-powershell-session"></a>Iniciar sua sessão do PowerShell
Primeiro é necessário toohave hello mais recente [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Olá exemplos neste tópico usam [modelo de implantação do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), portanto, os exemplos usam Olá [cmdlets do Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Executar Olá [ **adicionar AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet e você verá uma tela tooenter entrar suas credenciais. Use Olá mesmo credenciais que você use toosign em toohello portal do Azure.

    Add-AzureRmAccount

Se você tiver várias assinaturas usam Olá [ **conjunto AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect cmdlet qual assinatura sua sessão do PowerShell deve usar. toosee qual assinatura Olá PowerShell atual sessão está usando, execute [ **Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). execução de todas as suas assinaturas, toosee [ **Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

