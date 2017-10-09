---
title: "aaaAzure integração de Log com os logs de auditoria do Active Directory do Azure | Microsoft Docs"
description: "Saiba como tooinstall Olá serviço de integração de Log do Azure e integrar os logs de logs de auditoria do Azure"
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
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3667d-103">Integrar o Azure Active Directory a logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="3667d-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="3667d-104">Eventos de auditoria do Azure AD (Azure Active Directory) ajudam a identificar ações privilegiadas que ocorreram no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3667d-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="3667d-105">Você pode ver Olá tipos de eventos que você pode acompanhar revisando [eventos de relatório de auditoria do Active Directory do Azure](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="3667d-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3667d-106">Antes de tentar etapas Olá neste artigo, você deve revisar Olá [começar](security-azure-log-integration-get-started.md) artigo e concluir as etapas hello.</span><span class="sxs-lookup"><span data-stu-id="3667d-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3667d-107">Logs de auditoria do Azure Active directory do etapas toointegrate</span><span class="sxs-lookup"><span data-stu-id="3667d-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="3667d-108">Abra o prompt de comando hello e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="3667d-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="3667d-109">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="3667d-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="3667d-110">Esse comando solicitará o logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="3667d-111">Olá comando cria um Azure Active Directory entidade de serviço nos locatários de saudação do AD do Azure que hospedam Olá no qual Olá usuário conectado é um administrador, um coadministrador ou um proprietário de assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="3667d-112">comando Olá falhará se o usuário que fez logon Olá é apenas um usuário convidado no locatário do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3667d-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="3667d-113">Autenticação tooAzure é feito por meio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="3667d-114">Criar uma entidade de serviço para a integração do Azure Log cria Olá identidade do AD do Azure que recebe acesso tooread de assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="3667d-115">Comando a seguir de execução Olá tooprovide sua ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="3667d-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="3667d-116">Você precisa de membro toobe do comando de Olá Olá locatário admin função toorun.</span><span class="sxs-lookup"><span data-stu-id="3667d-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="3667d-117">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3667d-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="3667d-118">Verificar Olá tooconfirm pastas que Olá arquivos de JSON de log de auditoria do Azure Active Directory a seguir é criada no-los:</span><span class="sxs-lookup"><span data-stu-id="3667d-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="3667d-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="3667d-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="3667d-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="3667d-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="3667d-121">Hello vídeo a seguir demonstra as etapas de saudação abordadas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="3667d-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="3667d-122">Para obter instruções específicas sobre colocar informações de saudação nos arquivos de JSON de saudação em seu sistema de gerenciamento (SIEM) de eventos e informações de segurança, contate o fornecedor do SIEM.</span><span class="sxs-lookup"><span data-stu-id="3667d-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="3667d-123">Ajuda da comunidade está disponível por meio de saudação [Fórum do MSDN de integração do Azure Log](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="3667d-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="3667d-124">Este fórum permite que as pessoas em hello Azure Log integração da comunidade toosupport uns aos outros com perguntas, respostas, dicas e truques.</span><span class="sxs-lookup"><span data-stu-id="3667d-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="3667d-125">Além disso, a equipe de integração do Azure Log Olá monitora este fórum e ajuda sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="3667d-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="3667d-126">Você também pode abrir uma [solicitação de suporte](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="3667d-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="3667d-127">Selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.</span><span class="sxs-lookup"><span data-stu-id="3667d-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3667d-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3667d-128">Next steps</span></span>
<span data-ttu-id="3667d-129">toolearn mais sobre a integração de Log do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="3667d-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="3667d-130">[Integração de Logs do Microsoft Azure para os logs do Azure](https://www.microsoft.com/download/details.aspx?id=53324): a página Centro de Download oferece os detalhes, os requisitos de sistema e as instruções de instalação da Integração de Logs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="3667d-131">[Introdução tooAzure Log integração](security-azure-log-integration-overview.md): Este artigo apresenta tooAzure integração de Log, seus principais recursos e como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="3667d-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="3667d-132">[Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): esta postagem de blog mostra como o tooconfigure toowork de integração de Log do Azure com soluções Splunk, HP ArcSight e IBM QRadar de parceiros.</span><span class="sxs-lookup"><span data-stu-id="3667d-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="3667d-133">[Perguntas frequentes sobre a Integração do Log do Azure](security-azure-log-integration-faq.md): este artigo responde perguntas sobre a Integração do Log do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="3667d-134">[Integração de alertas da Central de segurança com a integração do Azure Log](../security-center/security-center-integrating-alerts-with-log-integration.md): Este artigo mostra como alertas da Central de segurança toosync, juntamente com coletados pelo diagnóstico do Azure e logs de auditoria do Azure, com a análise de log de eventos de segurança de máquina virtual ou Solução SIEM.</span><span class="sxs-lookup"><span data-stu-id="3667d-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="3667d-135">[Logs de auditoria de novos recursos de diagnóstico do Azure e o Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta postagem de blog apresenta tooAzure os logs de auditoria e outros recursos que ajudarão a obtém ideias sobre operações de saudação de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3667d-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
