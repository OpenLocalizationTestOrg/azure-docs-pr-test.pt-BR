---
title: "Redes conhecidas no portal clássico do Azure | Microsoft Docs"
description: "Configurando redes conhecidas, você pode evitar ter endereços IP que pertencem à sua organização incluídos nos relatórios Entradas de várias regiões geográficas e Entradas de endereços IP com atividade suspeita."
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="cfd2c-103">Redes conhecidas</span><span class="sxs-lookup"><span data-stu-id="cfd2c-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cfd2c-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="cfd2c-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="cfd2c-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cfd2c-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="cfd2c-106">Você pode usar os relatórios de uso e de acesso do Active Directory do Azure para obter visibilidade quanto à integridade e a segurança do diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="cfd2c-107">Com essas informações, um administrador de diretório pode determinar melhor onde possíveis riscos de segurança podem estar, de modo que pode fazer planos adequados para mitigar esses riscos.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="cfd2c-108">É possível que os relatórios "*Entradas de várias regiões geográficas*" e "*Entradas de endereços IP com atividade suspeita*" sinalizem incorretamente os endereços IP que realmente pertencem à sua organização.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="cfd2c-109">Por exemplo, isso pode ocorrer quando:</span><span class="sxs-lookup"><span data-stu-id="cfd2c-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="cfd2c-110">Um usuário em um escritório em Boston ao conectar-se remotamente a um data center em San Francisco aciona o relatório "Entradas de várias regiões geográficas"</span><span class="sxs-lookup"><span data-stu-id="cfd2c-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="cfd2c-111">Um usuário de sua organização que tenta entrar diversas vezes com uma senha incorreta aciona o relatório "Entradas de endereços IP com atividade suspeita”</span><span class="sxs-lookup"><span data-stu-id="cfd2c-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="cfd2c-112">Para impedir que esses casos gerem relatórios de segurança enganadores, você deverá adicionar intervalos de endereços IP conhecidos à lista de endereços IP públicos de sua organização.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="cfd2c-113">Para adicionar os intervalos de endereços IP públicos da sua organização, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cfd2c-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="cfd2c-114">Entre no [portal de gerenciamento do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cfd2c-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="cfd2c-115">No painel esquerdo, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-115">In the left pane, click **Active Directory**.</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="cfd2c-117">Na guia **Diretório** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="cfd2c-118">No menu na parte superior, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-118">In the menu on the top, click **Configure**.</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="cfd2c-120">Na guia Configurar, vá para **os intervalos de endereços IP públicos da sua organização**</span><span class="sxs-lookup"><span data-stu-id="cfd2c-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="cfd2c-122">Clique em **Adicionar Intervalos de Endereços IP conhecidos**.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="cfd2c-123">Adicione seus intervalos de endereços na caixa de diálogo que aparece e clique no botão de verificação quando você terminar.</span><span class="sxs-lookup"><span data-stu-id="cfd2c-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="cfd2c-125">**Recursos adicionais:**</span><span class="sxs-lookup"><span data-stu-id="cfd2c-125">**Additional resources:**</span></span>

* [<span data-ttu-id="cfd2c-126">Exibir relatórios de acesso e uso</span><span class="sxs-lookup"><span data-stu-id="cfd2c-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="cfd2c-127">Entradas de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="cfd2c-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="cfd2c-128">Entradas de várias regiões geográficas</span><span class="sxs-lookup"><span data-stu-id="cfd2c-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

