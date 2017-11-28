---
title: "Solução de erros do pacote de conteúdo dos Logs de atividades do Azure Active Directory | Microsoft Docs"
description: "Fornece uma lista das mensagens de erro do hello atividade do Active Directory do Azure conteúdo pack e as etapas toofix-los."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="84c58-103">Solução de erros do pacote de conteúdo dos Logs de atividades do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84c58-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="84c58-104">Ao trabalhar com o pacote de conteúdo do Power BI de saudação visualização do Azure Active Directory, é possível encontrar hello os erros a seguir:</span><span class="sxs-lookup"><span data-stu-id="84c58-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="84c58-105">Falha na atualização</span><span class="sxs-lookup"><span data-stu-id="84c58-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="84c58-106">Credenciais de fonte de dados tooupdate com falha</span><span class="sxs-lookup"><span data-stu-id="84c58-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="84c58-107">Importação de dados muito demorada</span><span class="sxs-lookup"><span data-stu-id="84c58-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="84c58-108">Este tópico fornece informações sobre as possíveis causas de saudação e como toofix esses erros.</span><span class="sxs-lookup"><span data-stu-id="84c58-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="84c58-109">Falha na atualização</span><span class="sxs-lookup"><span data-stu-id="84c58-109">Refresh failed</span></span> 
 
<span data-ttu-id="84c58-110">**Como esse erro aparece**: Email do Power BI ou status de falha no histórico de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="84c58-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="84c58-111">Causa</span><span class="sxs-lookup"><span data-stu-id="84c58-111">Cause</span></span> | <span data-ttu-id="84c58-112">Como toofix</span><span class="sxs-lookup"><span data-stu-id="84c58-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="84c58-113">Atualize erros podem ser causados quando foram Redefinir credenciais de saudação de usuários de saudação conectando o pacote de conteúdo toohello mas não atualizadas nas configurações de conexão de saudação de saudação do pacote de conteúdo de saudação de falha.</span><span class="sxs-lookup"><span data-stu-id="84c58-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="84c58-114">No Power BI, localize toohello correspondente do conjunto de dados de saudação painel de logs de atividade do Active Directory do Azure (logs de atividade do Azure Active Directory), escolha o agendamento de atualização e, em seguida, insira suas credenciais do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="84c58-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="84c58-115">Uma atualização pode falhar devido a problemas toodata Olá subjacente do pacote de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="84c58-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="84c58-116">Registre um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="84c58-116">File a support ticket.</span></span> <span data-ttu-id="84c58-117">Para obter mais detalhes, consulte [como tooget dão suporte ao Active Directory do Azure](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="84c58-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="84c58-118">Credenciais de fonte de dados tooupdate com falha</span><span class="sxs-lookup"><span data-stu-id="84c58-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="84c58-119">**Como esse erro aparece**: no Power BI, quando você está se conectando o pacote de conteúdo toohello atividade do Active Directory do Azure (visualização) de logs.</span><span class="sxs-lookup"><span data-stu-id="84c58-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="84c58-120">Causa</span><span class="sxs-lookup"><span data-stu-id="84c58-120">Cause</span></span> | <span data-ttu-id="84c58-121">Como toofix</span><span class="sxs-lookup"><span data-stu-id="84c58-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="84c58-122">usuário da conexão Olá não é um administrador global nem um leitor de segurança ou um administrador de segurança.</span><span class="sxs-lookup"><span data-stu-id="84c58-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="84c58-123">Use uma conta que seja um administrador global ou um leitor de segurança ou uma segurança admin tooaccess Olá pacotes de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="84c58-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="84c58-124">Seu locatário não é um locatário Premium ou não tem, pelo menos, um usuário com um Arquivo de licença Premium.</span><span class="sxs-lookup"><span data-stu-id="84c58-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="84c58-125">Registre um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="84c58-125">File a support ticket.</span></span> <span data-ttu-id="84c58-126">Para obter mais detalhes, consulte [como tooget dão suporte ao Active Directory do Azure](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="84c58-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="84c58-127">Importação de dados muito demorada</span><span class="sxs-lookup"><span data-stu-id="84c58-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="84c58-128">**Como esse erro aparece**: no Power BI, depois que você se conectou seu pacote de conteúdo, Olá processo de importação de dados inicia tooprepare seu dashboard para log de atividade do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="84c58-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="84c58-129">Você vê a mensagem de saudação: "*importação de dados...* "</span><span class="sxs-lookup"><span data-stu-id="84c58-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="84c58-130">Causa</span><span class="sxs-lookup"><span data-stu-id="84c58-130">Cause</span></span> | <span data-ttu-id="84c58-131">Como toofix</span><span class="sxs-lookup"><span data-stu-id="84c58-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="84c58-132">Dependendo do tamanho de saudação do seu locatário, esta etapa pode levar de alguns minutos too30 minutos.</span><span class="sxs-lookup"><span data-stu-id="84c58-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="84c58-133">Seja paciente.</span><span class="sxs-lookup"><span data-stu-id="84c58-133">Just be patient.</span></span> <span data-ttu-id="84c58-134">Se a mensagem de saudação não alterar tooshowing seu painel em uma hora, envie um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="84c58-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="84c58-135">Para obter mais detalhes, consulte [como tooget dão suporte ao Active Directory do Azure](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="84c58-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="84c58-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84c58-136">Next steps</span></span>

<span data-ttu-id="84c58-137">Olá tooinstall pacote de conteúdo do Power BI visualização do Azure Active Directory, clique em [aqui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="84c58-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


