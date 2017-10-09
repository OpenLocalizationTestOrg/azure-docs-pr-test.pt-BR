---
title: "aaaModify DATA 0 configurações de dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Saiba como toouse do Windows PowerShell para StorSimple tooreconfigure Olá interface de rede 0 de dados no seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="a872f-103">Modificar configurações de interface de rede 0 Olá dados em seu dispositivo da série StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="a872f-103">Modify hello DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="a872f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a872f-104">Overview</span></span>

<span data-ttu-id="a872f-105">Seu dispositivo do Microsoft Azure StorSimple possui seis interfaces de rede, de DATA 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="a872f-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="a872f-106">Olá DATA 0 interface é sempre configurada através da interface do Windows PowerShell hello ou console serial hello e será automaticamente habilitado para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="a872f-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="a872f-107">Observe que você não pode configurar a interface de rede 0 de dados por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a872f-107">Note that you cannot configure DATA 0 network interface through hello Azure portal.</span></span>

<span data-ttu-id="a872f-108">Olá interface DATA 0 é primeiro configurada por meio do Assistente de instalação Olá durante a implantação inicial do dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="a872f-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="a872f-109">Quando o dispositivo de saudação estiver em um modo operacional, talvez seja necessário tooreconfigure DATA 0 configurações.</span><span class="sxs-lookup"><span data-stu-id="a872f-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="a872f-110">Este tutorial fornece dois métodos toomodify dados 0 as configurações de rede, tanto por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a872f-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="a872f-111">Depois de ler este tutorial, você poderá:</span><span class="sxs-lookup"><span data-stu-id="a872f-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="a872f-112">Modificar dados 0 configuração por meio do Assistente de instalação de saudação de rede</span><span class="sxs-lookup"><span data-stu-id="a872f-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="a872f-113">Modificar as configurações de rede 0 de dados por meio de saudação `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="a872f-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="a872f-114">Modificar as configurações de rede de DADOS 0 por meio do assistente de instalação</span><span class="sxs-lookup"><span data-stu-id="a872f-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="a872f-115">Você pode reconfigurar as configurações de rede 0 de dados conectando-se a interface do Windows PowerShell toohello do seu dispositivo StorSimple e iniciar uma sessão do Assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="a872f-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="a872f-116">Executar Olá seguindo as etapas toomodify DATA 0 configurações:</span><span class="sxs-lookup"><span data-stu-id="a872f-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="a872f-117">configurações de rede 0 toomodify dados por meio do Assistente de instalação</span><span class="sxs-lookup"><span data-stu-id="a872f-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="a872f-118">No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="a872f-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a872f-119">Quando solicitado forneça Olá **senha de administrador do dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="a872f-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="a872f-120">Olá a senha padrão é `Password1`.</span><span class="sxs-lookup"><span data-stu-id="a872f-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="a872f-121">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="a872f-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="a872f-122">Um Assistente de instalação aparece toohelp configurar Olá DATA 0 interface do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a872f-122">A setup wizard appears toohelp configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="a872f-123">Fornece novos valores de máscara de rede, o gateway e o endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="a872f-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="a872f-124">Olá fixa controladores IPs precisará toobe reconfigurada por meio de saudação **as configurações de rede** folha do dispositivo StorSimple Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a872f-124">hello fixed controllers IPs will need toobe reconfigured through hello **Network settings** blade of hello StorSimple device in hello Azure portal.</span></span> <span data-ttu-id="a872f-125">Para obter mais informações, vá muito[modificar interfaces de rede](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="a872f-125">For more information, go too[Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="a872f-126">Modificar as configurações de rede de DADOS 0 por meio do cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="a872f-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="a872f-127">Tooreconfigure uma maneira alternativa DATA 0 é de interface de rede através do uso de saudação do hello `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a872f-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="a872f-128">Olá cmdlet é executado na interface do Windows PowerShell de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a872f-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="a872f-129">Ao usar esse procedimento, IPs fixos do controlador Olá também pode ser configurado aqui.</span><span class="sxs-lookup"><span data-stu-id="a872f-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="a872f-130">Executar Olá seguindo as etapas toomodify Olá DATA 0 configurações:</span><span class="sxs-lookup"><span data-stu-id="a872f-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="a872f-131">configurações de rede 0 toomodify dados por meio do cmdlet Set-HcsNetInterface de saudação</span><span class="sxs-lookup"><span data-stu-id="a872f-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="a872f-132">No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="a872f-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a872f-133">Quando solicitado forneça a senha de administrador de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a872f-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="a872f-134">Olá a senha padrão é `Password1`.</span><span class="sxs-lookup"><span data-stu-id="a872f-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="a872f-135">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="a872f-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="a872f-136">Olá angular parênteses, digite Olá valores a seguir para DATA 0:</span><span class="sxs-lookup"><span data-stu-id="a872f-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="a872f-137">Endereço IPv4</span><span class="sxs-lookup"><span data-stu-id="a872f-137">IPv4 address</span></span>
   * <span data-ttu-id="a872f-138">Gateway IPv4</span><span class="sxs-lookup"><span data-stu-id="a872f-138">IPv4 gateway</span></span>
   * <span data-ttu-id="a872f-139">Máscara da sub-rede IPv4</span><span class="sxs-lookup"><span data-stu-id="a872f-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="a872f-140">Endereço IPv4 fixo para o controlador 0</span><span class="sxs-lookup"><span data-stu-id="a872f-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="a872f-141">Endereço IPv4 fixo para o controlador 1</span><span class="sxs-lookup"><span data-stu-id="a872f-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="a872f-142">Para obter mais informações sobre o uso de saudação desse cmdlet, vá muito[do Windows PowerShell para referência de cmdlet do StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="a872f-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a872f-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a872f-143">Next steps</span></span>
* <span data-ttu-id="a872f-144">interfaces de rede tooconfigure diferente de DATA 0, você pode usar o hello [definir configurações de rede no portal do Azure de saudação](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="a872f-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure network settings in hello Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="a872f-145">Se você tiver problemas ao configurar as interfaces de rede, consulte muito[solucionar problemas de implantação](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a872f-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

