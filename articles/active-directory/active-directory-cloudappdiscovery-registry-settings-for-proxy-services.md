---
title: "Configurações de registro de descoberta do aplicativo para os serviços de Proxy de aaaCloud | Microsoft Docs"
description: "Olá objetivo deste tópico é tooprovide com hello etapas que você precisar de porta de Olá necessário de tooset de tooperform em computadores Olá executando Olá Cloud App Discovery agent."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="3c3f2-103">Configurações de Registro do Cloud App Discovery para serviços de proxy</span><span class="sxs-lookup"><span data-stu-id="3c3f2-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="3c3f2-104">Por padrão, o agente do Cloud App Discovery Olá é toouse configurado somente Olá portas 80 ou 443.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="3c3f2-105">Se você estiver planejando instalar o Cloud App Discovery em um ambiente com um servidor proxy que está usando uma porta personalizada (nem 80 nem 443), você precisa tooconfigure toouse seus agentes essa porta.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="3c3f2-106">configuração de saudação baseia-se em uma chave do registro.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="3c3f2-107">Olá objetivo deste tópico é tooprovide com hello etapas que você precisar de porta de Olá necessário de tooset de tooperform em computadores Olá executando Olá Cloud App Discovery agent.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="3c3f2-108">**porta de saudação toomodify usada pelo computador Olá executando o agente do Cloud App Discovery hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c3f2-109">Inicie o editor do registro hello.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-109">Start hello registry editor.</span></span> <br> ![Executar](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="3c3f2-111">Navegue tooor criar hello chave do registro a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c3f2-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="3c3f2-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="3c3f2-113">Crie um novo valor de **cadeia de caracteres múltipla** chamado **Portas**.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="3c3f2-114">![Novo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="3c3f2-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="3c3f2-115">Olá tooopen **Editar cadeia de caracteres múltipla** caixa de diálogo, clique duas vezes no valor de portas de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="3c3f2-116">No texto de dados de valor hello, digite hello valores a seguir e adicione todas as portas personalizadas que são usadas pela sua organização:</span><span class="sxs-lookup"><span data-stu-id="3c3f2-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="3c3f2-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-117">
   **80**</span></span> <br><span data-ttu-id="3c3f2-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-118">
   **8080**</span></span> <br><span data-ttu-id="3c3f2-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-119">
   **8118**</span></span> <br><span data-ttu-id="3c3f2-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-120">
   **8888**</span></span> <br><span data-ttu-id="3c3f2-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-121">
   **81**</span></span> <br><span data-ttu-id="3c3f2-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-122">
   **12080**</span></span> <br><span data-ttu-id="3c3f2-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-123">
**6999**</span></span> <br><span data-ttu-id="3c3f2-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-124">
**30606**</span></span> <br><span data-ttu-id="3c3f2-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-125">
**31595**</span></span> <br><span data-ttu-id="3c3f2-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-126">
**4080**</span></span> <br><span data-ttu-id="3c3f2-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-127">
**443**</span></span> <br><span data-ttu-id="3c3f2-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-128">
**1110**</span></span> <br><br><span data-ttu-id="3c3f2-129">
![Editar Cadeia de Caracteres Múltipla](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="3c3f2-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="3c3f2-130">Clique em **Okey** tooclose Olá **Editar cadeia de caracteres múltipla** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c3f2-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="3c3f2-131">**Recursos adicionais**</span><span class="sxs-lookup"><span data-stu-id="3c3f2-131">**Additional Resources**</span></span>

* [<span data-ttu-id="3c3f2-132">Como descobrir aplicativos na nuvem não aprovados, usados em minha organização</span><span class="sxs-lookup"><span data-stu-id="3c3f2-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

