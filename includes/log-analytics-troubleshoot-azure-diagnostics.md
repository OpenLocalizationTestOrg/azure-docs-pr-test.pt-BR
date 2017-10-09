### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="94edc-101">Solucionar problemas de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="94edc-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="94edc-102">Se você receber a seguinte mensagem de erro de saudação, o provedor de recursos do hello Insights não está registrado:</span><span class="sxs-lookup"><span data-stu-id="94edc-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="94edc-103">provedor de recursos do tooregister hello, executar Olá etapas Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="94edc-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="94edc-104">No painel de navegação Olá Olá esquerda, clique em *assinaturas*</span><span class="sxs-lookup"><span data-stu-id="94edc-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="94edc-105">Selecionar assinatura Olá identificada na mensagem de saudação do erro</span><span class="sxs-lookup"><span data-stu-id="94edc-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="94edc-106">Clique em *Provedores de Recursos*</span><span class="sxs-lookup"><span data-stu-id="94edc-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="94edc-107">Localize Olá *Insights* provedor</span><span class="sxs-lookup"><span data-stu-id="94edc-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="94edc-108">Clique em Olá *registrar* link</span><span class="sxs-lookup"><span data-stu-id="94edc-108">Click hello *Register* link</span></span>

![Registrar o provedor de recursos microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="94edc-110">Uma vez Olá *Insights* provedor de recursos está registrado, tente novamente a configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="94edc-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="94edc-111">No PowerShell, se você receber Olá a seguinte mensagem de erro, será necessário tooupdate sua versão do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="94edc-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="94edc-112">Atualize sua versão do PowerShell toohello novembro de 2016 (v2.3.0) ou versão posterior, usando instruções Olá Olá [Introdução aos cmdlets do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artigo.</span><span class="sxs-lookup"><span data-stu-id="94edc-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
