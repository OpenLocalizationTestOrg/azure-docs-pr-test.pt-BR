---
title: "aaaAzure perguntas frequentes sobre a integração de Log | Microsoft Docs"
description: "Este artigo de perguntas frequentes responde às perguntas sobre a Integração de Logs do Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="4863e-103">Perguntas frequentes sobre a Integração de Logs do Azure</span><span class="sxs-lookup"><span data-stu-id="4863e-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="4863e-104">Este artigo responde as perguntas frequentes (FAQ) sobre a Integração de Logs do Azure.</span><span class="sxs-lookup"><span data-stu-id="4863e-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="4863e-105">Integração de Log do Azure é um serviço do sistema operacional Windows que você pode usar logs bruto toointegrate de seus recursos do Azure em seus locais segurança informações e eventos (SIEM) sistemas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4863e-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="4863e-106">Essa integração oferece um painel unificado para todos os seus ativos, local ou na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="4863e-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="4863e-107">Você pode então agregar, correlacionar, analisar e alertar sobre eventos de segurança associados a seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4863e-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="4863e-108">Software de integração do Azure Log Olá é gratuito?</span><span class="sxs-lookup"><span data-stu-id="4863e-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="4863e-109">Sim.</span><span class="sxs-lookup"><span data-stu-id="4863e-109">Yes.</span></span> <span data-ttu-id="4863e-110">Não há nenhuma taxa para Olá software de integração de Log do Azure.</span><span class="sxs-lookup"><span data-stu-id="4863e-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="4863e-111">Onde a Integração de log do Azure está disponível?</span><span class="sxs-lookup"><span data-stu-id="4863e-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="4863e-112">Atualmente, ela está disponível atualmente no Azure Comercial e o Azure Governamental e não está disponível na China nem na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="4863e-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="4863e-113">Como posso ver contas de armazenamento de saudação do qual a integração do Azure Log está recebendo logs da VM do Azure?</span><span class="sxs-lookup"><span data-stu-id="4863e-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="4863e-114">Execute o comando Olá **lista de origem azlog**.</span><span class="sxs-lookup"><span data-stu-id="4863e-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="4863e-115">Como saber quais Olá assinatura são logs de integração do Log do Azure?</span><span class="sxs-lookup"><span data-stu-id="4863e-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="4863e-116">No caso de saudação de logs de auditoria que são colocados em Olá **AzureResourcemanagerJson** diretórios, ID de assinatura de saudação é no nome de arquivo de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="4863e-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="4863e-117">Isso também é verdadeiro para logs no hello **AzureSecurityCenterJson** pasta.</span><span class="sxs-lookup"><span data-stu-id="4863e-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="4863e-118">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4863e-118">For example:</span></span>

<span data-ttu-id="4863e-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="4863e-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="4863e-120">Logs de auditoria do Active Directory do Azure incluem hello ID de locatário como parte do nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="4863e-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="4863e-121">Logs de diagnóstico que são lidos a partir de um hub de eventos não incluem hello ID da assinatura como parte do nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="4863e-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="4863e-122">Em vez disso, eles incluem o nome amigável do hello especificado como parte da criação de saudação da origem de hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4863e-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="4863e-123">Como faço para atualizar a configuração de proxy Olá?</span><span class="sxs-lookup"><span data-stu-id="4863e-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="4863e-124">Se a configuração do proxy não permite acesso de armazenamento do Azure diretamente, abra Olá **AZLOG. EXE. CONFIGURAÇÃO** arquivo **c:\Program Files\Microsoft Azure Log integração**.</span><span class="sxs-lookup"><span data-stu-id="4863e-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="4863e-125">Atualização Olá arquivo tooinclude Olá **defaultProxy** seção com o endereço de proxy de saudação da sua organização.</span><span class="sxs-lookup"><span data-stu-id="4863e-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="4863e-126">Após ter feita a atualização Olá, parar e iniciar o serviço de saudação usando comandos Olá **net stop azlog** e **net start-azlog**.</span><span class="sxs-lookup"><span data-stu-id="4863e-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="4863e-127">Como posso ver informações de assinatura de saudação eventos do Windows?</span><span class="sxs-lookup"><span data-stu-id="4863e-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="4863e-128">Acrescente o nome amigável da toohello Olá assinatura ID ao adicionar fonte hello:</span><span class="sxs-lookup"><span data-stu-id="4863e-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="4863e-129">evento de saudação XML tem Olá metadados, incluindo a ID da assinatura Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4863e-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![Evento XML][1]

## <a name="error-messages"></a><span data-ttu-id="4863e-131">Mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="4863e-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="4863e-132">Ao executar o comando de saudação **azlog createazureid**, por que recebo Olá erro a seguir?</span><span class="sxs-lookup"><span data-stu-id="4863e-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="4863e-133">Erro:</span><span class="sxs-lookup"><span data-stu-id="4863e-133">Error:</span></span>

  <span data-ttu-id="4863e-134">*Falha toocreate aplicativo AAD - locatário 72f988bf-86f1-41af-91ab-2d7cd011db37 - motivo = 'Proibido' - mensagem = 'privilégios insuficientes toocomplete Olá operação'.*</span><span class="sxs-lookup"><span data-stu-id="4863e-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="4863e-135">Olá **azlog createazureid** comando tenta toocreate uma entidade de serviço em todos os locatários de saudação do AD do Azure para assinaturas de Olá Olá logon do Azure tem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="4863e-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="4863e-136">Se o logon do Azure é apenas um usuário convidado no locatário do AD do Azure, Olá falhará com "privilégios insuficientes toocomplete Olá a operação."</span><span class="sxs-lookup"><span data-stu-id="4863e-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="4863e-137">Peça ao locatário Olá administrador tooadd sua conta como um usuário no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="4863e-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="4863e-138">Ao executar o comando de saudação **azlog autorizar**, por que recebo Olá erro a seguir?</span><span class="sxs-lookup"><span data-stu-id="4863e-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="4863e-139">Erro:</span><span class="sxs-lookup"><span data-stu-id="4863e-139">Error:</span></span>

  <span data-ttu-id="4863e-140">*Aviso de criação de atribuição de função - AuthorizationFailed: cliente Olá janedo@microsoft.com' com o objeto id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' não tem autorização tooperform ação 'Microsoft.Authorization/roleAssignments/write' no escopo ' / assinaturas / 70d 95299-d689-4c 97 b971 0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="4863e-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="4863e-141">Olá **azlog autorizar** comando atribui Olá função da entidade de serviço do leitor toohello AD do Azure (criado com **azlog createazureid**) assinaturas toohello fornecido.</span><span class="sxs-lookup"><span data-stu-id="4863e-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="4863e-142">Se Olá logon do Azure não é um coadministrador ou um proprietário de assinatura hello, ele falhará com uma mensagem de erro "Falha de autorização".</span><span class="sxs-lookup"><span data-stu-id="4863e-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="4863e-143">Azure Role-Based Access RBAC (controle) de coadministrador ou o proprietário é necessário toocomplete esta ação.</span><span class="sxs-lookup"><span data-stu-id="4863e-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="4863e-144">Onde encontrar definição Olá propriedades Olá no log de auditoria Olá?</span><span class="sxs-lookup"><span data-stu-id="4863e-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="4863e-145">Consulte:</span><span class="sxs-lookup"><span data-stu-id="4863e-145">See:</span></span>

* [<span data-ttu-id="4863e-146">Operações de auditoria com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4863e-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="4863e-147">Lista de eventos de gerenciamento de saudação em uma assinatura no hello API de REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="4863e-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="4863e-148">Onde posso encontrar detalhes sobre alertas da Central de Segurança do Azure?</span><span class="sxs-lookup"><span data-stu-id="4863e-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="4863e-149">Consulte [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4863e-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="4863e-150">Como posso modificar o que é coletado com o diagnóstico da VM?</span><span class="sxs-lookup"><span data-stu-id="4863e-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="4863e-151">Para obter detalhes sobre como tooget, modificar e definir a configuração de diagnóstico do Azure hello, consulte [tooenable de usar o PowerShell diagnóstico do Azure em uma máquina virtual que executa o Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4863e-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="4863e-152">saudação de exemplo a seguir obtém a configuração de diagnóstico do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4863e-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="4863e-153">saudação de exemplo a seguir modifica a configuração de diagnóstico do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4863e-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="4863e-154">Nessa configuração, somente 4624 ID e do evento ID 4625 são coletados do log de eventos de segurança de saudação.</span><span class="sxs-lookup"><span data-stu-id="4863e-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="4863e-155">O Antimalware da Microsoft para eventos do Azure são coletados do log de eventos do sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="4863e-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="4863e-156">Para obter detalhes sobre o uso de saudação de expressões XPath, consulte [consumindo eventos](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="4863e-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="4863e-157">Olá, exemplo a seguir define configuração de diagnóstico do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4863e-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="4863e-158">Depois de fazer alterações, verifique Olá tooensure de conta de armazenamento que Olá correto de eventos são coletados.</span><span class="sxs-lookup"><span data-stu-id="4863e-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="4863e-159">Se você tiver problemas durante a saudação de instalação e configuração, abra um [solicitação de suporte](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="4863e-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="4863e-160">Selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.</span><span class="sxs-lookup"><span data-stu-id="4863e-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="4863e-161">Pode usar logs do Azure Log integração toointegrate observador de rede em meu SIEM?</span><span class="sxs-lookup"><span data-stu-id="4863e-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="4863e-162">O Observador de Rede do Azure gera grandes quantidades de informações de registro em log.</span><span class="sxs-lookup"><span data-stu-id="4863e-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="4863e-163">Esses logs não são toobe devem enviado tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="4863e-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="4863e-164">destino de saudação só tem suportada para logs do observador de rede é uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4863e-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="4863e-165">Integração de Log do Azure não oferece suporte a ler esses logs e tornando-os disponível tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="4863e-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
