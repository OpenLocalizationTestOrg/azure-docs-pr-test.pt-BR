## <a name="set-up-azure-powershell-for-azure-dns"></a>Configurar o Azure PowerShell para DNS do Azure

### <a name="before-you-begin"></a>Antes de começar

Verifique se você tem Olá itens a seguir antes de começar a configuração.

* Uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Você precisa tooinstall hello mais recente versão do hello cmdlets do PowerShell do Gerenciador de recursos do Azure. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Entrar tooyour conta do Azure

Abra o console do PowerShell e conecte-se a conta de tooyour. Para obter mais informações, confira [Usar o PowerShell com o Gerenciador de Recursos](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Selecione a assinatura de saudação
 
Verificar as assinaturas de saudação para conta de saudação.

```powershell
Get-AzureRmSubscription
```

Escolha qual toouse suas assinaturas do Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos. No entanto, como todos os recursos DNS são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto no DNS do Azure.

Você pode ignorar esta etapa se está usando um grupo de recursos existente.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Registrar provedor de recursos

Olá serviço DNS do Azure é gerenciado pelo provedor de recursos Microsoft. Network hello. Sua assinatura do Azure deve ser registrado toouse este provedor de recursos antes de usar o DNS do Azure. Essa operação deve ser executa apenas uma vez para cada assinatura.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```