---
title: assinaturas aaaNo encontrou um erro ao tentar toosign no portal de tooAzure ou centro de contas do Azure | Microsoft Docs
description: "Fornece a solução de saudação para um problema no qual a assinaturas não encontram erro ocorre quando se inscreve no portal de tooAzure ou centro de contas do Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="9cdc5-103">Erro Nenhuma assinatura encontrada no Portal do Azure ou no centro de contas do Azure</span><span class="sxs-lookup"><span data-stu-id="9cdc5-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="9cdc5-104">Você poderá receber uma mensagem de erro "Nenhuma assinatura encontrada" ao tentar toosign em toohello [portal do Azure](https://portal.azure.com/) ou hello [Centro de contas do Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="9cdc5-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="9cdc5-105">Este artigo fornece uma solução para esse problema.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="9cdc5-106">Sintoma</span><span class="sxs-lookup"><span data-stu-id="9cdc5-106">Symptom</span></span>

<span data-ttu-id="9cdc5-107">Quando você tentar toosign em toohello [portal do Azure](https://portal.azure.com/) ou hello [Centro de contas do Azure](https://account.windowsazure.com/Subscriptions), você receberá Olá a seguinte mensagem de erro: "Nenhuma assinatura encontrada".</span><span class="sxs-lookup"><span data-stu-id="9cdc5-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="9cdc5-108">Causa</span><span class="sxs-lookup"><span data-stu-id="9cdc5-108">Cause</span></span>

<span data-ttu-id="9cdc5-109">Esse problema ocorrerá se sua conta não tiver permissões suficientes.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="9cdc5-110">Solução</span><span class="sxs-lookup"><span data-stu-id="9cdc5-110">Solution</span></span>

<span data-ttu-id="9cdc5-111">Certifique-se de que você faça login como administrador correto do hello.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="9cdc5-112">Um administrador de conta pode acessar somente o Centro de contas de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="9cdc5-113">Os administradores de serviços (SA) e os coadministradores (CA) têm acesso de permissão somente toohello portal do Azure ou Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="9cdc5-114">Cenário 1: Mensagem de erro é recebida em Olá [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="9cdc5-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="9cdc5-115">toofix esse problema:</span><span class="sxs-lookup"><span data-stu-id="9cdc5-115">toofix this issue:</span></span>

* <span data-ttu-id="9cdc5-116">Certifique-se de que Olá correto de diretório do Azure está selecionado, clicando em sua conta na parte superior de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Diretório selecione Olá Olá parte superior direita da saudação portal do Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="9cdc5-118">Se hello directory à direita do Azure está selecionado, mas você ainda recebe a mensagem de erro Olá, [sua conta como um proprietário](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="9cdc5-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="9cdc5-119">Cenário 2: Mensagem de erro é recebida em Olá [Centro de contas do Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="9cdc5-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="9cdc5-120">Verifique se a conta Olá usada é Olá administrador da conta.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="9cdc5-121">é tooverify que Olá administrador da conta, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9cdc5-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="9cdc5-122">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cdc5-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cdc5-123">No menu de Hub hello, selecione **assinatura**.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="9cdc5-124">Selecione Olá assinatura que você deseja toocheck e, em seguida, selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="9cdc5-125">Selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-125">Select **Properties**.</span></span> <span data-ttu-id="9cdc5-126">Olá administrador da conta Olá assinatura é exibido no hello **administrador da conta** caixa.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="9cdc5-127">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="9cdc5-127">Need help?</span></span> <span data-ttu-id="9cdc5-128">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-128">Contact support.</span></span>
<span data-ttu-id="9cdc5-129">Se você ainda precisar de Ajuda, [entre em contato com o suporte](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="9cdc5-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
