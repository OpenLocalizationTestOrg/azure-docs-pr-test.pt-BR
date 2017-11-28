---
title: "Modificar as configurações de DATA 0 em um dispositivo StorSimple | Microsoft Docs"
description: Saiba como usar o Windows PowerShell para StorSimple para reconfigurar a interface de rede DATA 0 em seu dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 3a47ff1eed220cede820e8698c3384300e94688d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="65a14-103">Modificar as configurações de interface de rede DADOS 0 em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="65a14-103">Modify the DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="65a14-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="65a14-104">Overview</span></span>
<span data-ttu-id="65a14-105">O dispositivo Microsoft Azure StorSimple tem seis interfaces de rede de DADOS 0 a DADOS 5.</span><span class="sxs-lookup"><span data-stu-id="65a14-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="65a14-106">A interface de DADOS 0 é sempre configurada por meio da interface do Windows PowerShell ou do console serial e é habilitada para a nuvem automaticamente.</span><span class="sxs-lookup"><span data-stu-id="65a14-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="65a14-107">Observe que não é possível configurar a interface de rede de DATA 0 por meio do portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a14-107">Note that you cannot configure DATA 0 network interface through the Azure classic portal.</span></span> 

<span data-ttu-id="65a14-108">A interface de DADOS 0 é configurada primeiramente por meio do assistente de instalação durante a implantação inicial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65a14-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="65a14-109">Quando o dispositivo está em modo operacional, talvez você precise redefinir as configurações de DADOS 0.</span><span class="sxs-lookup"><span data-stu-id="65a14-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="65a14-110">Este tutorial fornece dois métodos para modificar as configurações de rede de DATA 0; os dois por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65a14-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="65a14-111">Depois de ler este tutorial, você poderá:</span><span class="sxs-lookup"><span data-stu-id="65a14-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="65a14-112">Modificar a configuração de rede de DADOS 0 por meio do assistente de instalação</span><span class="sxs-lookup"><span data-stu-id="65a14-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="65a14-113">Modificar as configurações de rede de DATA 0 por meio do cmdlet `Set-HcsNetInterface`</span><span class="sxs-lookup"><span data-stu-id="65a14-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="65a14-114">Modificar as configurações de rede de DADOS 0 por meio do assistente de instalação</span><span class="sxs-lookup"><span data-stu-id="65a14-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="65a14-115">Você pode reconfigurar as definições de rede de DADOS 0 conectando-se à interface do Windows PowerShell de seu dispositivo StorSimple e iniciando uma sessão do assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="65a14-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="65a14-116">Execute as etapas a seguir para modificar as configurações de DADOS 0:</span><span class="sxs-lookup"><span data-stu-id="65a14-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="65a14-117">Para modificar as configurações de rede de DADOS 0 por meio do assistente de instalação</span><span class="sxs-lookup"><span data-stu-id="65a14-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="65a14-118">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="65a14-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="65a14-119">Quando solicitado, forneça a **senha de administrador do dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="65a14-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="65a14-120">A senha padrão é `Password1`.</span><span class="sxs-lookup"><span data-stu-id="65a14-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="65a14-121">No prompt de comando, digite:</span><span class="sxs-lookup"><span data-stu-id="65a14-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="65a14-122">Um assistente de instalação aparecerá para lhe ajudar a configurar a interface dos DADOS 0 do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="65a14-122">A setup wizard will appear to help you configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="65a14-123">Fornece novos valores para o endereço IP, gateway e máscara de rede.</span><span class="sxs-lookup"><span data-stu-id="65a14-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="65a14-124">Os IPs de controladores fixos precisarão ser reconfigurados por meio da página **Configurar** do dispositivo StorSimple no Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a14-124">The fixed controllers IPs will need to be reconfigured through the **Configure** page of the StorSimple device in the Azure classic portal.</span></span> <span data-ttu-id="65a14-125">Para obter mais informações, vá para [Modificar interfaces de rede](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="65a14-125">For more information, go to [Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="65a14-126">Modificar as configurações de rede de DADOS 0 por meio do cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="65a14-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="65a14-127">Uma maneira alternativa de reconfigurar o adaptador de rede DADOS 0 é através do uso do cmdlet `Set-HcsNetInterface`.</span><span class="sxs-lookup"><span data-stu-id="65a14-127">An alternate way to reconfigure DATA 0 network interface is through the use of  the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="65a14-128">O cmdlet é executado na interface do Windows PowerShell do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65a14-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="65a14-129">Ao usar esse procedimento, os IPs fixos pelo controlador também podem ser configurados aqui.</span><span class="sxs-lookup"><span data-stu-id="65a14-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="65a14-130">Execute as etapas a seguir para modificar as configurações de DADOS 0:</span><span class="sxs-lookup"><span data-stu-id="65a14-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="65a14-131">Para modificar as configurações de rede de DADOS 0 por meio do cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="65a14-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="65a14-132">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="65a14-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="65a14-133">Quando solicitado, forneça a senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="65a14-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="65a14-134">A senha padrão é `Password1`.</span><span class="sxs-lookup"><span data-stu-id="65a14-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="65a14-135">No prompt de comando, digite:</span><span class="sxs-lookup"><span data-stu-id="65a14-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="65a14-136">Entre os colchetes angulares, digite os seguintes valores para DATA 0:</span><span class="sxs-lookup"><span data-stu-id="65a14-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="65a14-137">Endereço IPv4</span><span class="sxs-lookup"><span data-stu-id="65a14-137">IPv4 address</span></span>
   * <span data-ttu-id="65a14-138">Gateway IPv4</span><span class="sxs-lookup"><span data-stu-id="65a14-138">IPv4 gateway</span></span>
   * <span data-ttu-id="65a14-139">Máscara da sub-rede IPv4</span><span class="sxs-lookup"><span data-stu-id="65a14-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="65a14-140">Endereço IPv4 fixo para o controlador 0</span><span class="sxs-lookup"><span data-stu-id="65a14-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="65a14-141">Endereço IPv4 fixo para o controlador 1</span><span class="sxs-lookup"><span data-stu-id="65a14-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="65a14-142">Para obter mais informações sobre como usar esse cmdlet, vá para a [Referência de cmdlets do Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="65a14-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65a14-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65a14-143">Next steps</span></span>
* <span data-ttu-id="65a14-144">Para configurar as interfaces de rede que não sejam DATA 0, você pode usar a [página Configurar no Portal clássico do Azure](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="65a14-144">To configure network interfaces other than DATA 0, you can use the [Configure page in the Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="65a14-145">Se você tiver problemas ao configurar suas interfaces de rede, consulte [Solucionar problemas de implantação](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="65a14-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

