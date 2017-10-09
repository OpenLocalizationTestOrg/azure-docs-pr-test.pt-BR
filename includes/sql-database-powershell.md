
## <a name="start-your-powershell-session"></a>Iniciar sua sessão do PowerShell
Primeiro, você deve ter hello Azure PowerShell mais recente instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Muitos novos recursos do banco de dados SQL só têm suporte quando você estiver usando Olá [modelo de implantação do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), portanto, os exemplos usam Olá [cmdlets de banco de dados do SQL Azure PowerShell](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) para o Gerenciador de recursos . modelo de implantação de gerenciamento (clássico) de serviço Olá [cmdlets de gerenciamento de serviço de banco de dados SQL do Azure](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) têm suporte para compatibilidade com versões anteriores, mas é recomendável usar o hello cmdlets do Gerenciador de recursos.
> 
> 

Executar Olá [ **adicionar AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet e você verá uma tela de entrada tooenter suas credenciais. Use Olá mesmo credenciais que você use toosign em toohello portal do Azure.

```PowerShell
Add-AzureRmAccount
```

Se você tiver várias assinaturas, use Olá [ **conjunto AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect cmdlet qual assinatura sua sessão do PowerShell deve usar. toosee qual assinatura Olá PowerShell atual sessão está usando, execute [ **Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). execução de todas as suas assinaturas, toosee [ **Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
