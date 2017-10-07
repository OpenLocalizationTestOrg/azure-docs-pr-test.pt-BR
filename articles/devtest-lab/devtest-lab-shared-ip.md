---
title: "aaaUnderstand compartilhado endereços IP no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como o Azure DevTest Labs usa a compartilhado IP endereços toominimize Olá pública IP endereços necessário tooaccess sua máquinas virtuais do laboratório."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="8b77c-103">Entender os endereços IP compartilhados no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8b77c-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="8b77c-104">Laboratório de permite DevTest Labs Azure VMs compartilhamento Olá mesmo pública toominimize Olá número do endereço IP do público tooaccess necessário endereços IP laboratório VMs individual.</span><span class="sxs-lookup"><span data-stu-id="8b77c-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="8b77c-105">Este artigo descreve como funcionam os IPs compartilhados e suas opções de configuração relacionadas.</span><span class="sxs-lookup"><span data-stu-id="8b77c-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="8b77c-106">Configuração de IP de compartilhado</span><span class="sxs-lookup"><span data-stu-id="8b77c-106">Shared IP setting</span></span>

<span data-ttu-id="8b77c-107">Quando você cria um laboratório, ele reside em uma sub-rede de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="8b77c-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="8b77c-108">Por padrão, essa sub-rede é criada com **habilitar compartilhada IP público** definido muito*Sim*.</span><span class="sxs-lookup"><span data-stu-id="8b77c-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="8b77c-109">Essa configuração cria um endereço IP público sub-rede inteira hello.</span><span class="sxs-lookup"><span data-stu-id="8b77c-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="8b77c-110">Para obter mais informações sobre como configurar redes virtuais e sub-redes, consulte [Configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="8b77c-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nova sub-rede do laboratório](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="8b77c-112">Em laboratórios existentes, você pode habilitar essa opção selecionando **Políticas e configurações > Redes Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="8b77c-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="8b77c-113">Em seguida, selecione uma rede virtual da lista de saudação e escolha **habilitar compartilhado IP público** para uma sub-rede selecionada.</span><span class="sxs-lookup"><span data-stu-id="8b77c-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="8b77c-114">Você também pode desabilitar essa opção no laboratório de nenhuma se você não quiser tooshare um endereço IP público em máquinas virtuais do laboratório.</span><span class="sxs-lookup"><span data-stu-id="8b77c-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="8b77c-115">Todas as máquinas virtuais criados no toousing de padrão neste laboratório um IP compartilhado.</span><span class="sxs-lookup"><span data-stu-id="8b77c-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="8b77c-116">Ao criar hello VM, essa configuração pode ser observada no hello **configurações avançadas** folha sob **configuração do endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="8b77c-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nova VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="8b77c-118">**Compartilhado:** todas as VMs criadas como **Compartilhadas** são colocadas em um grupo de recursos (RG).</span><span class="sxs-lookup"><span data-stu-id="8b77c-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="8b77c-119">Um único endereço IP é atribuído para que RG e todas as VMs em Olá RG usarão esse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="8b77c-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="8b77c-120">**Público:** cada uma das VMs que você cria tem seu próprio endereço IP e é criada em seu próprio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8b77c-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="8b77c-121">**Privado:** todas as VMs que você criar usarão um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="8b77c-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="8b77c-122">Você não será capaz de tooconnect toothis VM diretamente da saudação internet com área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8b77c-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="8b77c-123">Sempre que uma VM com IP compartilhado habilitado é adicionada a sub-rede toohello, DevTest Labs automaticamente adiciona o balanceador de carga Olá VM tooa e atribui um número de porta TCP no endereço IP público de hello, encaminhamento toohello porta RDP em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8b77c-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="8b77c-124">Usando Olá compartilhado de IP</span><span class="sxs-lookup"><span data-stu-id="8b77c-124">Using hello shared IP</span></span>

- <span data-ttu-id="8b77c-125">**Os usuários do Linux:** SSH toohello VM usando o endereço IP de saudação ou nome de domínio totalmente qualificado, seguido por dois-pontos, seguido pela porta hello.</span><span class="sxs-lookup"><span data-stu-id="8b77c-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="8b77c-126">Por exemplo, na imagem de saudação abaixo, Olá RDP endereços toohello tooconnect VM é `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="8b77c-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Exemplo de VM](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="8b77c-128">**Os usuários do Windows:** Olá selecione **conectar** botão Olá toodownload portal do Azure um arquivo RDP pré-configurado e acessar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8b77c-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b77c-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b77c-129">Next steps</span></span>

* [<span data-ttu-id="8b77c-130">Definir políticas de laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8b77c-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="8b77c-131">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8b77c-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





