---
title: "Perguntas frequentes sobre a Integração de Logs do Azure | Microsoft Docs"
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
ms.openlocfilehash: bfdc7154160bb6bb7dc9c46eb2352ce74310c4de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="cc821-103">Perguntas frequentes sobre a Integração de Logs do Azure</span><span class="sxs-lookup"><span data-stu-id="cc821-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="cc821-104">Este artigo responde as perguntas frequentes (FAQ) sobre a Integração de Logs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc821-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="cc821-105">A Integração de Logs do Azure é um serviço do sistema operacional Windows que permite integrar logs brutos de recursos do Azure a seus sistemas locais de SIEM (Gerenciamento de Eventos e Informações de Segurança).</span><span class="sxs-lookup"><span data-stu-id="cc821-105">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="cc821-106">Essa integração oferece um painel unificado para todos os seus ativos, locais ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="cc821-106">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="cc821-107">Você pode então agregar, correlacionar, analisar e alertar sobre eventos de segurança associados a seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="cc821-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="cc821-108">O software Integração de Log do Azure é gratuito?</span><span class="sxs-lookup"><span data-stu-id="cc821-108">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="cc821-109">Sim.</span><span class="sxs-lookup"><span data-stu-id="cc821-109">Yes.</span></span> <span data-ttu-id="cc821-110">Não há nenhuma cobrança pelo software Integração de Log do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc821-110">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="cc821-111">Onde a Integração de log do Azure está disponível?</span><span class="sxs-lookup"><span data-stu-id="cc821-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="cc821-112">Atualmente, ela está disponível atualmente no Azure Comercial e o Azure Governamental e não está disponível na China nem na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="cc821-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="cc821-113">Como posso ver as contas de armazenamento nas quais a Integração de Logs do Azure está efetuando pull para extrair os logs da VM do Azure?</span><span class="sxs-lookup"><span data-stu-id="cc821-113">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="cc821-114">Execute o comando **azlog source list**.</span><span class="sxs-lookup"><span data-stu-id="cc821-114">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="cc821-115">Como saber de qual assinatura os logs de Integração de Logs do Azure são provenientes?</span><span class="sxs-lookup"><span data-stu-id="cc821-115">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="cc821-116">No caso de logs de auditoria que são colocados nos diretórios **AzureResourcemanagerJson**, a ID da assinatura está no nome do arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="cc821-116">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="cc821-117">Isso também é verdadeiro para logs na pasta **AzureSecurityCenterJson**.</span><span class="sxs-lookup"><span data-stu-id="cc821-117">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="cc821-118">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cc821-118">For example:</span></span>

<span data-ttu-id="cc821-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="cc821-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="cc821-120">Logs de auditoria do Azure Active Directory incluem a ID do locatário como parte do nome.</span><span class="sxs-lookup"><span data-stu-id="cc821-120">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="cc821-121">Os logs de diagnóstico lidos de um hub de eventos não incluem a ID da assinatura como parte do nome.</span><span class="sxs-lookup"><span data-stu-id="cc821-121">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="cc821-122">Em vez disso, eles incluem o nome amigável especificado como parte da criação da origem do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cc821-122">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="cc821-123">Como atualizo a configuração de proxy?</span><span class="sxs-lookup"><span data-stu-id="cc821-123">How can I update the proxy configuration?</span></span>
<span data-ttu-id="cc821-124">Se a configuração de proxy não permitir acesso ao armazenamento do Azure diretamente, abra o arquivo **AZLOG.EXE.CONFIG** em **c:\Arquivos de Programas\Integração de Log do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="cc821-124">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="cc821-125">Atualize o arquivo para incluir a seção **defaultProxy** com o endereço do proxy da sua organização.</span><span class="sxs-lookup"><span data-stu-id="cc821-125">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="cc821-126">Depois que a atualização for concluída, pare e inicie o serviço usando os comandos **net stop azlog** e **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="cc821-126">After the update is done, stop and start the service by using the commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="cc821-127">Como posso ver as informações de assinatura nos eventos do Windows?</span><span class="sxs-lookup"><span data-stu-id="cc821-127">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="cc821-128">Acrescente a ID da assinatura ao nome amigável ao adicionar a origem:</span><span class="sxs-lookup"><span data-stu-id="cc821-128">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="cc821-129">O evento XML tem os seguintes metadados, incluindo a ID da assinatura:</span><span class="sxs-lookup"><span data-stu-id="cc821-129">The event XML has the following metadata, including the subscription ID:</span></span>

![Evento XML][1]

## <a name="error-messages"></a><span data-ttu-id="cc821-131">Mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="cc821-131">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="cc821-132">Ao executar o comando **azlog createazureid**, por que obtenho o erro a seguir?</span><span class="sxs-lookup"><span data-stu-id="cc821-132">When I run the command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="cc821-133">Erro:</span><span class="sxs-lookup"><span data-stu-id="cc821-133">Error:</span></span>

  <span data-ttu-id="cc821-134">*Falha ao criar aplicativo AAD - Locatário 72f988bf-86f1-41af-91ab-2d7cd011db37 - Motivo = 'Proibido' - Mensagem = 'Privilégios insuficientes para concluir a operação.'*</span><span class="sxs-lookup"><span data-stu-id="cc821-134">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="cc821-135">O comando **azlog createazureid** tenta criar uma entidade de serviço em todos os locatários do Azure AD para as assinaturas nas quais o logon do Azure tem acesso.</span><span class="sxs-lookup"><span data-stu-id="cc821-135">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="cc821-136">Se o logon do Azure for apenas um usuário Convidado nesse locatário do Azure AD, o comando falhará com “Privilégios insuficientes para concluir a operação”.</span><span class="sxs-lookup"><span data-stu-id="cc821-136">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="cc821-137">Solicite ao administrador do locatário para adicionar sua conta como um usuário no locatário.</span><span class="sxs-lookup"><span data-stu-id="cc821-137">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="cc821-138">Ao executar o comando **azlog authorize**, por que obtenho o erro a seguir?</span><span class="sxs-lookup"><span data-stu-id="cc821-138">When I run the command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="cc821-139">Erro:</span><span class="sxs-lookup"><span data-stu-id="cc821-139">Error:</span></span>

  <span data-ttu-id="cc821-140">*Aviso ao criar Atribuição de Função – AuthorizationFailed: O cliente janedo@microsoft.com' com a id de objeto 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' não tem autorização para executar a ação 'Microsoft.Authorization/roleAssignments/write' além do escopo '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="cc821-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="cc821-141">O comando **azlog authorize** tenta criar a função de leitor para a entidade de serviço do Azure AD (criada com **azlog createazureid**) para as assinaturas fornecidas.</span><span class="sxs-lookup"><span data-stu-id="cc821-141">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="cc821-142">Se o logon do Azure não for um coadministrador nem um proprietário da assinatura, ele falhará com a mensagem de erro “Falha na Autorização”.</span><span class="sxs-lookup"><span data-stu-id="cc821-142">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="cc821-143">O RBAC (Controle de Acesso Baseado em Função) do coadministrador ou proprietário é necessário para concluir essa ação.</span><span class="sxs-lookup"><span data-stu-id="cc821-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="cc821-144">Onde posso encontrar a definição das propriedades no log de auditoria?</span><span class="sxs-lookup"><span data-stu-id="cc821-144">Where can I find the definition of the properties in the audit log?</span></span>
<span data-ttu-id="cc821-145">Consulte:</span><span class="sxs-lookup"><span data-stu-id="cc821-145">See:</span></span>

* [<span data-ttu-id="cc821-146">Operações de auditoria com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc821-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="cc821-147">Listar os eventos de gerenciamento em uma assinatura na API REST do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="cc821-147">List the management events in a subscription in the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="cc821-148">Onde posso encontrar detalhes sobre alertas da Central de Segurança do Azure?</span><span class="sxs-lookup"><span data-stu-id="cc821-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="cc821-149">Confira [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="cc821-149">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="cc821-150">Como posso modificar o que é coletado com o diagnóstico da VM?</span><span class="sxs-lookup"><span data-stu-id="cc821-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="cc821-151">Para obter detalhes sobre como obter, modificar e definir a configuração do Diagnóstico do Azure, veja [Usar o PowerShell para habilitar o Diagnóstico do Azure em uma máquina virtual que executa o Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc821-151">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="cc821-152">O exemplo a seguir obtém a configuração do Diagnóstico do Azure:</span><span class="sxs-lookup"><span data-stu-id="cc821-152">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="cc821-153">O exemplo a seguir modifica a configuração do Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc821-153">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="cc821-154">Nessa configuração, somente a ID de evento 4624 e a ID de evento 4625 são coletadas do log de eventos de segurança.</span><span class="sxs-lookup"><span data-stu-id="cc821-154">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="cc821-155">Os eventos do Microsoft Antimalware para Azure são coletados no log de eventos do sistema.</span><span class="sxs-lookup"><span data-stu-id="cc821-155">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="cc821-156">Para obter detalhes sobre o uso de expressões XPath, veja [Consumo de eventos](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="cc821-156">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="cc821-157">O exemplo a seguir define a configuração do Diagnóstico do Azure:</span><span class="sxs-lookup"><span data-stu-id="cc821-157">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="cc821-158">Depois de fazer alterações, verifique a conta de armazenamento para garantir que os eventos corretos sejam coletados.</span><span class="sxs-lookup"><span data-stu-id="cc821-158">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="cc821-159">Se você tiver problemas durante a instalação e configuração, abra uma [solicitação de suporte](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="cc821-159">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="cc821-160">Selecione **Integração de Log** como o serviço para o qual você está solicitando suporte.</span><span class="sxs-lookup"><span data-stu-id="cc821-160">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="cc821-161">Posso usar a Integração de Logs do Azure para integrar os logs do Observador de Rede em meu SIEM?</span><span class="sxs-lookup"><span data-stu-id="cc821-161">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="cc821-162">O Observador de Rede do Azure gera grandes quantidades de informações de registro em log.</span><span class="sxs-lookup"><span data-stu-id="cc821-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="cc821-163">Esses logs não devem ser enviadas para um SIEM.</span><span class="sxs-lookup"><span data-stu-id="cc821-163">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="cc821-164">O único destino com suporte para logs do Observador de Rede é uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cc821-164">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="cc821-165">A Integração de Logs do Azure não dá suporte à leitura desses logs e disponibilização deles para um SIEM.</span><span class="sxs-lookup"><span data-stu-id="cc821-165">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
