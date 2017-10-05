---
title: "Configurações de Registro do Cloud App Discovery para Serviços de Proxy | Microsoft Docs"
description: "O objetivo deste tópico é fornecer as etapas que você precisa executar para configurar a porta necessária nos computadores que executam o agente Cloud App Discovery."
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="9b4c8-103">Configurações de Registro do Cloud App Discovery para serviços de proxy</span><span class="sxs-lookup"><span data-stu-id="9b4c8-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="9b4c8-104">Por padrão, o agente Cloud App Discovery é configurado para usar somente as portas 80 ou 443.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="9b4c8-105">Se você estiver planejando instalar o Cloud App Discovery em um ambiente com um servidor proxy que está usando uma porta personalizada (nem 80 nem 443), precisa configurar seus agentes para usar essa porta.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="9b4c8-106">A configuração baseia-se em uma chave do Registro.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="9b4c8-107">O objetivo deste tópico é fornecer as etapas que você precisa executar para configurar a porta necessária nos computadores que executam o agente Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="9b4c8-108">**Para modificar a porta usada pelo computador que está executando o agente Cloud App Discovery, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="9b4c8-109">Inicie o editor do Registro.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-109">Start the registry editor.</span></span> <br> ![Executar](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="9b4c8-111">Navegue até ou crie a seguinte chave do Registro: </span><span class="sxs-lookup"><span data-stu-id="9b4c8-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="9b4c8-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="9b4c8-113">Crie um novo valor de **cadeia de caracteres múltipla** chamado **Portas**.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="9b4c8-114">![Novo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="9b4c8-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="9b4c8-115">Para abrir a caixa de diálogo **Editar Cadeia de Caracteres Múltipla** , clique duas vezes no valor Portas.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="9b4c8-116">Na caixa de texto de dados Valor, digite os seguintes valores e adicione todas as portas personalizadas usadas pela sua organização: </span><span class="sxs-lookup"><span data-stu-id="9b4c8-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="9b4c8-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-117">
   **80**</span></span> <br><span data-ttu-id="9b4c8-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-118">
   **8080**</span></span> <br><span data-ttu-id="9b4c8-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-119">
   **8118**</span></span> <br><span data-ttu-id="9b4c8-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-120">
   **8888**</span></span> <br><span data-ttu-id="9b4c8-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-121">
   **81**</span></span> <br><span data-ttu-id="9b4c8-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-122">
   **12080**</span></span> <br><span data-ttu-id="9b4c8-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-123">
**6999**</span></span> <br><span data-ttu-id="9b4c8-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-124">
**30606**</span></span> <br><span data-ttu-id="9b4c8-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-125">
**31595**</span></span> <br><span data-ttu-id="9b4c8-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-126">
**4080**</span></span> <br><span data-ttu-id="9b4c8-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-127">
**443**</span></span> <br><span data-ttu-id="9b4c8-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-128">
**1110**</span></span> <br><br><span data-ttu-id="9b4c8-129">
![Editar Cadeia de Caracteres Múltipla](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="9b4c8-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="9b4c8-130">Clique em **OK** para fechar a caixa de diálogo **Editar Cadeia de Caracteres Múltipla**.</span><span class="sxs-lookup"><span data-stu-id="9b4c8-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="9b4c8-131">**Recursos adicionais**</span><span class="sxs-lookup"><span data-stu-id="9b4c8-131">**Additional Resources**</span></span>

* [<span data-ttu-id="9b4c8-132">Como descobrir aplicativos na nuvem não aprovados, usados em minha organização</span><span class="sxs-lookup"><span data-stu-id="9b4c8-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

