---
title: aaaConfigure SSL descarregar - Gateway de aplicativo do Azure - Portal do Azure | Microsoft Docs
description: "Esta página fornece instruções toocreate descarregar um application gateway com SSL usando o portal de saudação"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="63304-103">Configure um gateway de aplicativo para descarregamento SSL usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="63304-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="63304-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="63304-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="63304-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63304-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="63304-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="63304-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="63304-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="63304-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="63304-108">Gateway de aplicativo do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão Olá gateway tooavoid cara SSL descriptografia tarefas toohappen no farm de web hello.</span><span class="sxs-lookup"><span data-stu-id="63304-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="63304-109">Descarregamento SSL também simplifica a configuração de servidor front-end do hello e gerenciamento de aplicativo da web hello.</span><span class="sxs-lookup"><span data-stu-id="63304-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="63304-110">Cenário</span><span class="sxs-lookup"><span data-stu-id="63304-110">Scenario</span></span>

<span data-ttu-id="63304-111">Olá cenário a seguir vai pela configuração de descarregamento de SSL em um gateway existente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63304-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="63304-112">Olá cenário pressupõe que você já seguiu as etapas de saudação muito[criar um Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="63304-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="63304-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="63304-113">Before you begin</span></span>

<span data-ttu-id="63304-114">Descarregamento SSL tooconfigure com um gateway de aplicativo, é necessário um certificado.</span><span class="sxs-lookup"><span data-stu-id="63304-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="63304-115">Esse certificado é carregado no gateway do aplicativo hello e usado tooencrypt e descriptografar o tráfego de saudação enviado através de SSL.</span><span class="sxs-lookup"><span data-stu-id="63304-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="63304-116">certificado Olá precisa toobe no formato de troca de informações pessoais (pfx).</span><span class="sxs-lookup"><span data-stu-id="63304-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="63304-117">Esse formato de arquivo permite Olá privada toobe chave exportado que é exigido pelo Olá application gateway tooperform Olá criptografia e a descriptografia de tráfego.</span><span class="sxs-lookup"><span data-stu-id="63304-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="63304-118">Adicionar um ouvinte HTTPS</span><span class="sxs-lookup"><span data-stu-id="63304-118">Add an HTTPS listener</span></span>

<span data-ttu-id="63304-119">Ouvinte HTTPS Olá procura o tráfego com base em sua configuração e ajuda a pools de back-end rota Olá tráfego toohello.</span><span class="sxs-lookup"><span data-stu-id="63304-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="63304-120">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="63304-120">Step 1</span></span>

<span data-ttu-id="63304-121">Navegue toohello portal do Azure e selecione um gateway existente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="63304-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="63304-122">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="63304-122">Step 2</span></span>

<span data-ttu-id="63304-123">Clique em ouvintes e Olá adicionar botão tooadd um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="63304-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![folha de visão geral do gateway de aplicativo][1]

### <a name="step-3"></a><span data-ttu-id="63304-125">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="63304-125">Step 3</span></span>

<span data-ttu-id="63304-126">Preencha Olá informações necessárias para o ouvinte de saudação e upload hello. pfx do certificado, quando concluída em Okey.</span><span class="sxs-lookup"><span data-stu-id="63304-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="63304-127">**Nome** -esse valor é um nome amigável do ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="63304-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="63304-128">**Configuração de IP de Frontend** -este valor é a configuração de IP de front-end Olá que é usada para o ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="63304-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="63304-129">**Porta de front-end (nome/porta)** -um nome amigável para a porta Olá usada no front-end do gateway de aplicativo hello e porta real de saudação usada hello.</span><span class="sxs-lookup"><span data-stu-id="63304-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="63304-130">**Protocolo** -toodetermine um comutador se http ou https é usado para o front-end hello.</span><span class="sxs-lookup"><span data-stu-id="63304-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="63304-131">**Certificado (Nome/Senha)** : se o descarregamento SSL for usado, um certificado .pfx for exigido para essa configuração, serão necessários um nome amigável e uma senha.</span><span class="sxs-lookup"><span data-stu-id="63304-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![folha adicionar ouvinte][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="63304-133">Criar uma regra e associá-lo toohello ouvinte</span><span class="sxs-lookup"><span data-stu-id="63304-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="63304-134">ouvinte de saudação foi criado.</span><span class="sxs-lookup"><span data-stu-id="63304-134">hello listener has now been created.</span></span> <span data-ttu-id="63304-135">É hora toocreate um regra toohandle Olá o tráfego do ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="63304-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="63304-136">As regras definem como o tráfego é roteado toohello pools de back-end com base em várias configurações, incluindo se a afinidade de sessão baseada em cookie é usada, protocolo, porta e investigações de integridade.</span><span class="sxs-lookup"><span data-stu-id="63304-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="63304-137">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="63304-137">Step 1</span></span>

<span data-ttu-id="63304-138">Clique em Olá **regras** do gateway de aplicativo hello e, em seguida, clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="63304-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![folha de regras do gateway de aplicativo][3]

### <a name="step-2"></a><span data-ttu-id="63304-140">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="63304-140">Step 2</span></span>

<span data-ttu-id="63304-141">Em Olá **Adicionar regra básica** folha, digite Olá o nome amigável para a regra de saudação e escolha o ouvinte Olá criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="63304-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="63304-142">Escolha o pool de back-end apropriado hello e configuração de http e clique em **Okey**</span><span class="sxs-lookup"><span data-stu-id="63304-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![janela de configurações de https][4]

<span data-ttu-id="63304-144">configurações de saudação agora são salvas toohello gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63304-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="63304-145">Olá processo para essas configurações de gravação pode demorar um pouco antes de serem tooview disponível por meio do portal hello, ou por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63304-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="63304-146">Gateway de aplicativo de uma vez salvo Olá lida com criptografia hello e a descriptografia de tráfego.</span><span class="sxs-lookup"><span data-stu-id="63304-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="63304-147">Todo o tráfego entre o gateway do aplicativo hello e servidores de web de back-end hello será tratado por http.</span><span class="sxs-lookup"><span data-stu-id="63304-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="63304-148">Qualquer cliente de toohello back comunicação se iniciada via https será retornado toohello cliente criptografado.</span><span class="sxs-lookup"><span data-stu-id="63304-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63304-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63304-149">Next steps</span></span>

<span data-ttu-id="63304-150">toolearn como tooconfigure uma integridade personalizado teste com o Gateway de aplicativo do Azure, consulte [criar um teste de integridade personalizado](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="63304-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
