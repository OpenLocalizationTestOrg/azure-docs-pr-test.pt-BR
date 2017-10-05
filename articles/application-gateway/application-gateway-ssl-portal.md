---
title: Configurar o descarregamento SSL - Gateway de Aplicativo do Azure - Portal do Azure | Microsoft Docs
description: "Esta página fornece instruções para criar um Gateway de Aplicativo com descarregamento SSL usando o portal"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="bacd0-103">Configurar um Gateway de Aplicativo para descarregamento SSL usando o portal</span><span class="sxs-lookup"><span data-stu-id="bacd0-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bacd0-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bacd0-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="bacd0-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bacd0-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="bacd0-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="bacd0-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="bacd0-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="bacd0-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="bacd0-108">O Gateway de Aplicativo do Azure pode ser configurado para encerrar a sessão SSL no gateway para evitar que a onerosa tarefa de descriptografia de SSL aconteça no web farm.</span><span class="sxs-lookup"><span data-stu-id="bacd0-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="bacd0-109">O descarregamento SSL também simplifica a configuração do servidor front-end e o gerenciamento do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bacd0-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="bacd0-110">Cenário</span><span class="sxs-lookup"><span data-stu-id="bacd0-110">Scenario</span></span>

<span data-ttu-id="bacd0-111">O cenário a seguir passa pela configuração do descarregamento SSL em um Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bacd0-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="bacd0-112">O cenário pressupõe que você já seguiu as etapas para [Criar um Gateway de Aplicativo](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bacd0-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bacd0-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bacd0-113">Before you begin</span></span>

<span data-ttu-id="bacd0-114">Para configurar o descarregamento SSL com um Gateway de Aplicativo, é necessário um certificado.</span><span class="sxs-lookup"><span data-stu-id="bacd0-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="bacd0-115">Esse certificado é carregado no Gateway de Aplicativo e usado para criptografar e descriptografar o tráfego enviado via SSL.</span><span class="sxs-lookup"><span data-stu-id="bacd0-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="bacd0-116">O certificado precisa estar no formato pfx (Troca de Informações Pessoais).</span><span class="sxs-lookup"><span data-stu-id="bacd0-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="bacd0-117">Esse formato de arquivo permite que a chave privada seja exportada, o que é exigido pelo Gateway de Aplicativo para executar criptografia e descriptografia de tráfego.</span><span class="sxs-lookup"><span data-stu-id="bacd0-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="bacd0-118">Adicionar um ouvinte HTTPS</span><span class="sxs-lookup"><span data-stu-id="bacd0-118">Add an HTTPS listener</span></span>

<span data-ttu-id="bacd0-119">O ouvinte HTTPS procura o tráfego com base em sua configuração e ajuda a rotear o tráfego para os pools de back-end.</span><span class="sxs-lookup"><span data-stu-id="bacd0-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="bacd0-120">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="bacd0-120">Step 1</span></span>

<span data-ttu-id="bacd0-121">Navegue até o portal do Azure e selecione um gateway de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="bacd0-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="bacd0-122">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="bacd0-122">Step 2</span></span>

<span data-ttu-id="bacd0-123">Clique em Ouvintes e clique no botão Adicionar para adicionar um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="bacd0-123">Click Listeners and click the Add button to add a listener.</span></span>

![folha de visão geral do gateway de aplicativo][1]

### <a name="step-3"></a><span data-ttu-id="bacd0-125">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="bacd0-125">Step 3</span></span>

<span data-ttu-id="bacd0-126">Preencha as informações necessárias para o ouvinte e carregue o certificado .pfx. Quando terminar, clique em OK.</span><span class="sxs-lookup"><span data-stu-id="bacd0-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="bacd0-127">**Nome** : um nome amigável do ouvinte.</span><span class="sxs-lookup"><span data-stu-id="bacd0-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="bacd0-128">**Configuração de IP de front-end** : a configuração de IP de front-end usada para o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="bacd0-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="bacd0-129">**Porta de front-end (Nome/Porta)** : um nome amigável para a porta usada no front-end do Gateway de Aplicativo e a porta real usada.</span><span class="sxs-lookup"><span data-stu-id="bacd0-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="bacd0-130">**Protocolo** : uma opção para determinar se o https ou http é usado para o front-end.</span><span class="sxs-lookup"><span data-stu-id="bacd0-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="bacd0-131">**Certificado (Nome/Senha)** : se o descarregamento SSL for usado, um certificado .pfx for exigido para essa configuração, serão necessários um nome amigável e uma senha.</span><span class="sxs-lookup"><span data-stu-id="bacd0-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![folha adicionar ouvinte][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="bacd0-133">Criar uma regra e associá-la ao ouvinte</span><span class="sxs-lookup"><span data-stu-id="bacd0-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="bacd0-134">O ouvinte foi criado.</span><span class="sxs-lookup"><span data-stu-id="bacd0-134">The listener has now been created.</span></span> <span data-ttu-id="bacd0-135">É hora de criar uma regra para lidar com o tráfego do ouvinte.</span><span class="sxs-lookup"><span data-stu-id="bacd0-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="bacd0-136">As regras definem como o tráfego será roteado para os pools de back-end com base em várias configurações, incluindo se a afinidade de sessão baseada em cookies é usada, protocolo, porta e investigações de integridade.</span><span class="sxs-lookup"><span data-stu-id="bacd0-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="bacd0-137">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="bacd0-137">Step 1</span></span>

<span data-ttu-id="bacd0-138">Clique nas **Regras** do Gateway de Aplicativo e clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="bacd0-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![folha de regras do gateway de aplicativo][3]

### <a name="step-2"></a><span data-ttu-id="bacd0-140">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="bacd0-140">Step 2</span></span>

<span data-ttu-id="bacd0-141">Na folha **Adicionar regra básica** , digite o nome amigável da regra e selecione o ouvinte criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="bacd0-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="bacd0-142">Escolha o pool de back-end apropriado e a configuração de http e clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="bacd0-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![janela de configurações de https][4]

<span data-ttu-id="bacd0-144">Agora as configurações são salvas no Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bacd0-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="bacd0-145">O processo de salvamento dessas configurações pode demorar um pouco antes que elas estejam disponíveis para exibição pelo portal ou pelo PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bacd0-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="bacd0-146">Após salvas, o Gateway de Aplicativo lida com a criptografia e descriptografia do tráfego.</span><span class="sxs-lookup"><span data-stu-id="bacd0-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="bacd0-147">Todo o tráfego entre o Gateway de Aplicativo e os servidores Web de back-end será tratado por http.</span><span class="sxs-lookup"><span data-stu-id="bacd0-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="bacd0-148">Toda a comunicação para o cliente, se iniciada por https, será retornada criptografada para o cliente.</span><span class="sxs-lookup"><span data-stu-id="bacd0-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bacd0-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bacd0-149">Next steps</span></span>

<span data-ttu-id="bacd0-150">Para saber como configurar uma investigação de integridade personalizada com o Gateway de Aplicativo do Azure, consulte [Criar uma investigação de integridade personalizada](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bacd0-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
