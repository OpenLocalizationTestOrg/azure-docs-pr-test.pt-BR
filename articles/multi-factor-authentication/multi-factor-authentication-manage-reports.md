---
title: "relatórios de uso e aaaAccess para o Azure MFA | Microsoft Docs"
description: "Descreve como toouse Olá recurso de autenticação multifator do Azure - relatórios."
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
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="ae593-103">Relatórios no Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ae593-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="ae593-104">O Azure Multi-Factor Authentication fornece vários relatórios que podem ser usados por você e sua organização.</span><span class="sxs-lookup"><span data-stu-id="ae593-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="ae593-105">Esses relatórios podem ser acessados por meio de saudação Portal de gerenciamento do multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ae593-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="ae593-106">a seguir Olá é uma lista de relatórios disponíveis hello:</span><span class="sxs-lookup"><span data-stu-id="ae593-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="ae593-107">Relatório</span><span class="sxs-lookup"><span data-stu-id="ae593-107">Report</span></span> | <span data-ttu-id="ae593-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae593-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ae593-109">Uso</span><span class="sxs-lookup"><span data-stu-id="ae593-109">Usage</span></span> |<span data-ttu-id="ae593-110">uso de saudação relatórios exibem informações sobre o uso geral, resumo do usuário e detalhes do usuário.</span><span class="sxs-lookup"><span data-stu-id="ae593-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="ae593-111">Status do servidor</span><span class="sxs-lookup"><span data-stu-id="ae593-111">Server Status</span></span> |<span data-ttu-id="ae593-112">Este relatório exibe o status de saudação de servidores de autenticação multifator associado à sua conta.</span><span class="sxs-lookup"><span data-stu-id="ae593-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="ae593-113">Histórico de usuário bloqueado</span><span class="sxs-lookup"><span data-stu-id="ae593-113">Blocked User History</span></span> |<span data-ttu-id="ae593-114">Esses relatórios mostram Olá histórico de solicitações tooblock ou desbloquear usuários.</span><span class="sxs-lookup"><span data-stu-id="ae593-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="ae593-115">Histórico de usuário desviado</span><span class="sxs-lookup"><span data-stu-id="ae593-115">Bypassed User History</span></span> |<span data-ttu-id="ae593-116">Mostra o histórico de saudação de solicitações toobypass multi-Factor Authentication para o número de telefone do usuário.</span><span class="sxs-lookup"><span data-stu-id="ae593-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="ae593-117">Alerta de fraude</span><span class="sxs-lookup"><span data-stu-id="ae593-117">Fraud Alert</span></span> |<span data-ttu-id="ae593-118">Mostra um histórico de alertas de fraude enviados durante o intervalo de datas de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="ae593-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="ae593-119">Em fila</span><span class="sxs-lookup"><span data-stu-id="ae593-119">Queued</span></span> |<span data-ttu-id="ae593-120">Lista os relatórios em fila para processamento e seu status.</span><span class="sxs-lookup"><span data-stu-id="ae593-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="ae593-121">Um relatório de saudação de toodownload ou modo de exibição do link é fornecido quando Olá relatório estiver completo.</span><span class="sxs-lookup"><span data-stu-id="ae593-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="ae593-122">Exibir relatórios</span><span class="sxs-lookup"><span data-stu-id="ae593-122">View reports</span></span>
1. <span data-ttu-id="ae593-123">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ae593-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ae593-124">Olá esquerda, selecione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae593-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="ae593-125">Siga uma destas duas opções, dependendo de se você usa Provedores de Autenticação:</span><span class="sxs-lookup"><span data-stu-id="ae593-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="ae593-126">**Opção 1**: clique Olá guia de provedores de autenticação multifator. Selecione seu provedor MFA e clique em hello **gerenciar** botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ae593-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="ae593-127">**Opção 2**: selecione o diretório e vá toohello **configurar** guia. Na seção de autenticação multifator hello, selecione **gerenciar configurações de serviço**.</span><span class="sxs-lookup"><span data-stu-id="ae593-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="ae593-128">Na parte inferior de saudação da página de configurações do serviço de MFA de saudação, clique em Olá Go toohello portal link.</span><span class="sxs-lookup"><span data-stu-id="ae593-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="ae593-129">Na Olá Portal de gerenciamento do Azure multi-Factor Authentication, selecione o tipo de saudação do relatório que você deseja da saudação **exibir um relatório** seção Olá barra de navegação esquerda.</span><span class="sxs-lookup"><span data-stu-id="ae593-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="ae593-130"><center>![Nuvem](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="ae593-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="ae593-131">**Recursos adicionais**</span><span class="sxs-lookup"><span data-stu-id="ae593-131">**Additional Resources**</span></span>

* [<span data-ttu-id="ae593-132">Para usuários</span><span class="sxs-lookup"><span data-stu-id="ae593-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="ae593-133">Azure Multi-Factor Authentication no MSDN</span><span class="sxs-lookup"><span data-stu-id="ae593-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
