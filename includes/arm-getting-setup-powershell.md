## <a name="setting-up-powershell-for-resource-manager-templates"></a>Configurando o PowerShell para modelos do Gerenciador de recursos
Antes de você pode usar o PowerShell do Azure com o Gerenciador de recursos, você precisará toohave saudação do Windows PowerShell e o Azure PowerShell versões corretas.

### <a name="verify-powershell-versions"></a>Verificar as versões do PowerShell
Verifique se você tem o Windows PowerShell versão 3.0 ou 4.0. versão de hello toofind do Windows PowerShell, digite este comando no prompt de comando do Windows PowerShell.

    $PSVersionTable

Olá, tipo de informações a seguir será exibida:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Verifique se o valor de saudação **PSVersion** é 3.0 ou 4.0. Caso não seja, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Definir sua conta e assinatura do Azure
Se ainda não tiver uma assinatura do Azure, você poderá ativar os [benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

Abra um prompt de comando do PowerShell do Azure e faça logon tooAzure com este comando.

    Login-AzureRmAccount

Se você tiver várias assinaturas do Azure, você pode listar suas assinaturas do Azure com este comando.

    Get-AzureRmSubscription

Olá, tipo de informações a seguir será exibida:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Você pode definir a assinatura do Azure Olá executando esses comandos no prompt de comando do PowerShell do Azure hello. Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com o nome correto da saudação.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Para obter mais informações sobre contas e assinaturas do Azure, consulte [como: conectar-se a assinatura de tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).

