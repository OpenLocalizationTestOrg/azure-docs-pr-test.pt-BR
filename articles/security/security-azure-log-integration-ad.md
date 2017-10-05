---
title: "Integração de Log do Azure com os logs de auditoria do Azure Active Directory | Microsoft Docs"
description: "Saiba como instalar o serviço de Integração de Logs do Azure e integre os registros de logs de auditoria do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="bbf58-103">Integrar o Azure Active Directory a logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="bbf58-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="bbf58-104">Eventos de auditoria do Azure AD (Azure Active Directory) ajudam a identificar ações privilegiadas que ocorreram no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bbf58-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="bbf58-105">Você pode ver os tipos de eventos que você pode acompanhar examinando os [eventos de relatório de auditoria do Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="bbf58-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bbf58-106">Antes de experimentar as etapas neste artigo, você deve examinar o artigo [Introdução](security-azure-log-integration-get-started.md) e concluir as etapas dele.</span><span class="sxs-lookup"><span data-stu-id="bbf58-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="bbf58-107">Etapas para integrar os logs de auditoria do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbf58-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="bbf58-108">Abra o prompt de comando e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="bbf58-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="bbf58-109">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="bbf58-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="bbf58-110">Esse comando solicitará o logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf58-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="bbf58-111">O comando cria uma entidade de serviço do Azure Active Directory em locatários do Azure AD que hospedam as assinaturas do Azure nas quais o usuário conectado é um administrador, um coadministrador ou um proprietário.</span><span class="sxs-lookup"><span data-stu-id="bbf58-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="bbf58-112">O comando falhará se o usuário conectado for apenas um usuário convidado no locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbf58-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="bbf58-113">A autenticação do Azure é feita por meio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf58-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="bbf58-114">A criação de uma entidade de serviço para a Integração de Logs do Azure criará a identidade do Azure AD que receberá o acesso de leitura das assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf58-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="bbf58-115">Execute o seguinte comando para fornecer sua ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="bbf58-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="bbf58-116">Você precisa ser membro da função de administrador de locatário para executar o comando.</span><span class="sxs-lookup"><span data-stu-id="bbf58-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="bbf58-117">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="bbf58-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="bbf58-118">Verifique as seguintes pastas para confirmar se os arquivos JSON do Log de Auditoria do Azure Active Directory são criados nelas:</span><span class="sxs-lookup"><span data-stu-id="bbf58-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="bbf58-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="bbf58-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="bbf58-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="bbf58-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="bbf58-121">O vídeo a seguir demonstra as etapas abordadas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="bbf58-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="bbf58-122">Para obter instruções específicas sobre como colocar as informações nos arquivos JSON em seu SIEM (sistema de gerenciamento de eventos e informações de segurança), contate o fornecedor do SIEM.</span><span class="sxs-lookup"><span data-stu-id="bbf58-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="bbf58-123">Ajuda da comunidade está disponível por meio de [Fórum do MSDN de integração de Log do Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="bbf58-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="bbf58-124">Este fórum permite que as pessoas na comunidade de Integração de Log do Azure deem suporte umas às outras com perguntas, respostas, dicas e truques.</span><span class="sxs-lookup"><span data-stu-id="bbf58-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="bbf58-125">Além disso, a equipe de Integração de Logs do Azure monitora esse fórum e ajuda sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="bbf58-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="bbf58-126">Você também pode abrir uma [solicitação de suporte](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="bbf58-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="bbf58-127">Selecione **Integração de Log** como o serviço para o qual você está solicitando suporte.</span><span class="sxs-lookup"><span data-stu-id="bbf58-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbf58-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bbf58-128">Next steps</span></span>
<span data-ttu-id="bbf58-129">Para saber mais sobre a Integração de Log do Azure, veja:</span><span class="sxs-lookup"><span data-stu-id="bbf58-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="bbf58-130">[Integração de Logs do Microsoft Azure para os logs do Azure](https://www.microsoft.com/download/details.aspx?id=53324): a página Centro de Download oferece os detalhes, os requisitos de sistema e as instruções de instalação da Integração de Logs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf58-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="bbf58-131">[Introdução à Integração de Logs do Azure](security-azure-log-integration-overview.md): este documento apresenta a Integração de Logs do Azure, seus principais recursos e como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="bbf58-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="bbf58-132">[Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): esta postagem de blog mostra a você como configurar a Integração de Logs do Azure para trabalhar com as soluções de parceiros Splunk, HP ArcSight e IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="bbf58-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="bbf58-133">[Perguntas frequentes sobre a Integração do Log do Azure](security-azure-log-integration-faq.md): este artigo responde perguntas sobre a Integração do Log do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf58-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="bbf58-134">[Integração dos alertas da Central de Segurança com a Integração de Log do Azure](../security-center/security-center-integrating-alerts-with-log-integration.md): este artigo mostra como sincronizar os alertas da Central de Segurança, juntamente com os eventos de segurança de máquina virtual coletados pelo Diagnóstico do Azure e pelos logs de auditoria do Azure, com o Log Analytics ou com a solução SIEM.</span><span class="sxs-lookup"><span data-stu-id="bbf58-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="bbf58-135">[Novos recursos para o Diagnóstico do Azure e para os Logs de Auditoria do Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta postagem de blog apresenta os logs de auditoria do Azure e outros recursos que ajudam você a obter ideias sobre as operações de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf58-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
