---
title: "Redes aaaKnown Olá portal clássico do Azure | Microsoft Docs"
description: "Configurando redes conhecidos, você pode evitar ter endereços IP que pertencem a sua organização incluída no hello entradas de várias regiões geográficas e entradas de endereços IP com relatórios de atividade suspeita."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="95d7d-103">Redes conhecidas</span><span class="sxs-lookup"><span data-stu-id="95d7d-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="95d7d-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="95d7d-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="95d7d-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95d7d-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="95d7d-106">Você pode usar o acesso do Azure Active Directory e uso relatórios toogain visibilidade Olá integridade e segurança do diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="95d7d-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="95d7d-107">Com essas informações, um administrador de diretório pode determinar melhor onde possíveis riscos de segurança pode para que possa planejar toomitigate adequadamente esses riscos.</span><span class="sxs-lookup"><span data-stu-id="95d7d-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="95d7d-108">É possível que o hello "*entradas de várias regiões geográficas*"e"*entradas de endereços IP com atividade suspeita*" relatórios incorretamente sinalizador endereços IP que são realmente pertencentes a sua organização.</span><span class="sxs-lookup"><span data-stu-id="95d7d-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="95d7d-109">Por exemplo, isso pode ocorrer quando:</span><span class="sxs-lookup"><span data-stu-id="95d7d-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="95d7d-110">Um usuário em seu escritório Boston entrou remotamente tooyour data center em são Francisco gatilhos Olá relatório de "Entradas de várias regiões geográficas"</span><span class="sxs-lookup"><span data-stu-id="95d7d-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="95d7d-111">Um usuário de sua organização tenta toosign em várias vezes com uma saudação de gatilhos de senha incorreta relatório de "Entradas de endereços IP com atividade suspeita"</span><span class="sxs-lookup"><span data-stu-id="95d7d-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="95d7d-112">tooprevent nesses casos de segurança enganosa gerando relatórios, você deve adicionar conhecidos intervalos toohello lista de endereços IP do endereço IP público de sua organização.</span><span class="sxs-lookup"><span data-stu-id="95d7d-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="95d7d-113">intervalos de endereço IP público de sua organização tooadd, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d7d-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="95d7d-114">Logon toohello [portal de gerenciamento do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="95d7d-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="95d7d-115">No painel esquerdo do hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95d7d-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="95d7d-117">Em Olá **diretório** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="95d7d-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="95d7d-118">No menu de saudação na parte superior de saudação, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="95d7d-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="95d7d-120">Na guia Configurar de hello, vá muito**seus intervalos de endereços IP públicos organizações**</span><span class="sxs-lookup"><span data-stu-id="95d7d-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="95d7d-122">Clique em **Adicionar Intervalos de Endereços IP conhecidos**.</span><span class="sxs-lookup"><span data-stu-id="95d7d-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="95d7d-123">Adicione seus intervalos de endereços na caixa de diálogo de saudação que aparece e, em seguida, clique botão de seleção de hello quando você terminar.</span><span class="sxs-lookup"><span data-stu-id="95d7d-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="95d7d-125">**Recursos adicionais:**</span><span class="sxs-lookup"><span data-stu-id="95d7d-125">**Additional resources:**</span></span>

* [<span data-ttu-id="95d7d-126">Exibir relatórios de acesso e uso</span><span class="sxs-lookup"><span data-stu-id="95d7d-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="95d7d-127">Entradas de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="95d7d-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="95d7d-128">Entradas de várias regiões geográficas</span><span class="sxs-lookup"><span data-stu-id="95d7d-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

