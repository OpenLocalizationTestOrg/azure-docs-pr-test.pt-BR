---
title: "Solução de erros do pacote de conteúdo dos Logs de atividades do Azure Active Directory | Microsoft Docs"
description: "Fornece uma lista de mensagens de erro do pacote de conteúdo de Atividades do Azure Active Directory e as etapas para corrigi-las."
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
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="3e0ca-103">Solução de erros do pacote de conteúdo dos Logs de atividades do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e0ca-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="3e0ca-104">Ao trabalhar com o Pacote de Conteúdo do Power BI para a Versão Prévia do Azure Active Directory, é possível encontrar os seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="3e0ca-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="3e0ca-105">Falha na atualização</span><span class="sxs-lookup"><span data-stu-id="3e0ca-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="3e0ca-106">Falha ao atualizar as credenciais de fonte de dados</span><span class="sxs-lookup"><span data-stu-id="3e0ca-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="3e0ca-107">Importação de dados muito demorada</span><span class="sxs-lookup"><span data-stu-id="3e0ca-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="3e0ca-108">Este tópico fornece informações sobre as possíveis causas e como corrigir esses erros.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="3e0ca-109">Falha na atualização</span><span class="sxs-lookup"><span data-stu-id="3e0ca-109">Refresh failed</span></span> 
 
<span data-ttu-id="3e0ca-110">**Como esse erro é exibido**: email do Power BI ou status de falha no histórico de atualizações.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="3e0ca-111">Causa</span><span class="sxs-lookup"><span data-stu-id="3e0ca-111">Cause</span></span> | <span data-ttu-id="3e0ca-112">Como corrigir</span><span class="sxs-lookup"><span data-stu-id="3e0ca-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3e0ca-113">Erros de falha na atualização podem ser causados quando as credenciais dos usuários que se conectam ao pacote de conteúdo foram redefinidas, mas não atualizadas nas configurações de conexão do pacote de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="3e0ca-114">No Power BI, localize o conjunto de dados correspondente ao painel dos Logs de atividades do Azure Active Directory (Logs de atividades do Azure Active Directory), escolha Agendar atualização e, em seguida, insira suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="3e0ca-115">Uma atualização poderá falhar devido a problemas de dados no pacote de conteúdo subjacente.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="3e0ca-116">Registre um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-116">File a support ticket.</span></span> <span data-ttu-id="3e0ca-117">Para obter mais detalhes, consulte [Como obter suporte para o Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3e0ca-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="3e0ca-118">Falha ao atualizar as credenciais de fonte de dados</span><span class="sxs-lookup"><span data-stu-id="3e0ca-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="3e0ca-119">**Como esse erro é exibido**: no Power BI, ao se conectar ao pacote de conteúdo dos Logs de atividades do Azure Active Directory (versão prévia).</span><span class="sxs-lookup"><span data-stu-id="3e0ca-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="3e0ca-120">Causa</span><span class="sxs-lookup"><span data-stu-id="3e0ca-120">Cause</span></span> | <span data-ttu-id="3e0ca-121">Como corrigir</span><span class="sxs-lookup"><span data-stu-id="3e0ca-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3e0ca-122">O usuário que está se conectando não é um administrador global nem um leitor de segurança ou administrador de segurança.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="3e0ca-123">Use uma conta que é um administrador global ou um leitor de segurança ou administrador de segurança para acessar os pacotes de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="3e0ca-124">Seu locatário não é um locatário Premium ou não tem, pelo menos, um usuário com um Arquivo de licença Premium.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="3e0ca-125">Registre um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-125">File a support ticket.</span></span> <span data-ttu-id="3e0ca-126">Para obter mais detalhes, consulte [Como obter suporte para o Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3e0ca-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="3e0ca-127">Importação de dados muito demorada</span><span class="sxs-lookup"><span data-stu-id="3e0ca-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="3e0ca-128">**Como esse erro é exibido**: no Power BI, depois de você se conectar ao pacote de conteúdo, o processo de importação de dados começa a preparar o painel para o Log de atividades do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="3e0ca-129">Você vê a mensagem: “*Importando dados...*”</span><span class="sxs-lookup"><span data-stu-id="3e0ca-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="3e0ca-130">Causa</span><span class="sxs-lookup"><span data-stu-id="3e0ca-130">Cause</span></span> | <span data-ttu-id="3e0ca-131">Como corrigir</span><span class="sxs-lookup"><span data-stu-id="3e0ca-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3e0ca-132">Dependendo do tamanho do locatário, esta etapa poderá levar de alguns minutos a 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="3e0ca-133">Seja paciente.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-133">Just be patient.</span></span> <span data-ttu-id="3e0ca-134">Se a mensagem não for alterada para mostrar o painel em até uma hora, registre um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="3e0ca-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="3e0ca-135">Para obter mais detalhes, consulte [Como obter suporte para o Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3e0ca-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3e0ca-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e0ca-136">Next steps</span></span>

<span data-ttu-id="3e0ca-137">Para instalar o Pacote de Conteúdo do Power BI para a Versão Prévia do Azure Active Directory, clique [aqui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="3e0ca-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


