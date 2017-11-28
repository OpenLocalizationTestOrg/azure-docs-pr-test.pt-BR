---
title: "Relatórios de acesso e uso para o MFA do Azure | Microsoft Docs"
description: "Descreve como usar o recurso de relatórios do Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="673a5-103">Relatórios no Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="673a5-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="673a5-104">O Azure Multi-Factor Authentication fornece vários relatórios que podem ser usados por você e sua organização.</span><span class="sxs-lookup"><span data-stu-id="673a5-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="673a5-105">Esses relatórios podem ser acessados por meio do Portal de Gerenciamento da Autenticação Multifator.</span><span class="sxs-lookup"><span data-stu-id="673a5-105">These reports can be accessed through the Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="673a5-106">Veja a seguir uma lista dos relatórios disponíveis:</span><span class="sxs-lookup"><span data-stu-id="673a5-106">The following is a list of the available reports:</span></span>

| <span data-ttu-id="673a5-107">Relatório</span><span class="sxs-lookup"><span data-stu-id="673a5-107">Report</span></span> | <span data-ttu-id="673a5-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="673a5-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="673a5-109">Uso</span><span class="sxs-lookup"><span data-stu-id="673a5-109">Usage</span></span> |<span data-ttu-id="673a5-110">Os relatórios de uso exibem informações sobre o uso geral, resumo do usuário e detalhes do usuário.</span><span class="sxs-lookup"><span data-stu-id="673a5-110">The usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="673a5-111">Status do servidor</span><span class="sxs-lookup"><span data-stu-id="673a5-111">Server Status</span></span> |<span data-ttu-id="673a5-112">Este relatório exibe o status dos servidores da autenticação multifator associada à sua conta.</span><span class="sxs-lookup"><span data-stu-id="673a5-112">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="673a5-113">Histórico de usuário bloqueado</span><span class="sxs-lookup"><span data-stu-id="673a5-113">Blocked User History</span></span> |<span data-ttu-id="673a5-114">Esses relatórios mostram o histórico de solicitações para bloquear ou desbloquear usuários.</span><span class="sxs-lookup"><span data-stu-id="673a5-114">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="673a5-115">Histórico de usuário desviado</span><span class="sxs-lookup"><span data-stu-id="673a5-115">Bypassed User History</span></span> |<span data-ttu-id="673a5-116">Mostra o histórico de solicitações para desviar da autenticação multifator para o número de telefone de um usuário.</span><span class="sxs-lookup"><span data-stu-id="673a5-116">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="673a5-117">Alerta de fraude</span><span class="sxs-lookup"><span data-stu-id="673a5-117">Fraud Alert</span></span> |<span data-ttu-id="673a5-118">Mostra um histórico dos alertas de fraude apresentados durante o intervalo de datas especificado.</span><span class="sxs-lookup"><span data-stu-id="673a5-118">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="673a5-119">Em fila</span><span class="sxs-lookup"><span data-stu-id="673a5-119">Queued</span></span> |<span data-ttu-id="673a5-120">Lista os relatórios em fila para processamento e seu status.</span><span class="sxs-lookup"><span data-stu-id="673a5-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="673a5-121">Um link para baixar ou exibir o relatório é fornecido quando o relatório é concluído.</span><span class="sxs-lookup"><span data-stu-id="673a5-121">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="673a5-122">Exibir relatórios</span><span class="sxs-lookup"><span data-stu-id="673a5-122">View reports</span></span>
1. <span data-ttu-id="673a5-123">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="673a5-123">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="673a5-124">Selecione Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="673a5-124">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="673a5-125">Siga uma destas duas opções, dependendo de se você usa Provedores de Autenticação:</span><span class="sxs-lookup"><span data-stu-id="673a5-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="673a5-126">**Opção 1**: clique na guia Provedores de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="673a5-126">**Option 1**: Click the Multi-Factor Auth Providers tab.</span></span> <span data-ttu-id="673a5-127">Selecione seu provedor de MFA e clique no botão **Gerenciar** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="673a5-127">Select your MFA provider and click the **Manage** button at the bottom.</span></span>
   * <span data-ttu-id="673a5-128">**Opção 2**: selecione seu diretório e acesse a guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="673a5-128">**Option 2**: Select your directory and go to the **Configure** tab.</span></span> <span data-ttu-id="673a5-129">Na seção da autenticação multifator, escolha **Gerenciar configurações de serviço**.</span><span class="sxs-lookup"><span data-stu-id="673a5-129">Under the multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="673a5-130">Na parte inferior da página Configurações do Serviço de MFA, clique em Ir para o link para portal.</span><span class="sxs-lookup"><span data-stu-id="673a5-130">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="673a5-131">No Portal de Gerenciamento da Autenticação Multifator do Azure, selecione o tipo de relatório desejado na seção **Exibir um Relatório** no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="673a5-131">In the Azure Multi-Factor Authentication Management Portal, select the type of report you want from the **View a Report** section in the left navigation.</span></span>

<span data-ttu-id="673a5-132"><center>![Nuvem](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="673a5-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="673a5-133">**Recursos adicionais**</span><span class="sxs-lookup"><span data-stu-id="673a5-133">**Additional Resources**</span></span>

* [<span data-ttu-id="673a5-134">Para usuários</span><span class="sxs-lookup"><span data-stu-id="673a5-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="673a5-135">Azure Multi-Factor Authentication no MSDN</span><span class="sxs-lookup"><span data-stu-id="673a5-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
