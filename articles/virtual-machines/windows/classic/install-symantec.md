---
title: Instalar o Symantec Endpoint Protection em uma VM Windows no Azure | Microsoft Docs
description: "Saiba como instalar e configurar a extensão de segurança do Symantec Endpoint Protection em uma VM do Azure nova ou existente criada com o modelo Clássico de implantação."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: 1603ebc7ee3c29277f30fbb802bdd8205b92d648
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="41e5c-103">Como instalar e configurar o Symantec Endpoint Protection em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="41e5c-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="41e5c-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="41e5c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="41e5c-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="41e5c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="41e5c-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="41e5c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="41e5c-107">Este artigo mostra como instalar e configurar o cliente do Symantec Endpoint Protection em uma VM (máquina virtual) existente com o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="41e5c-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="41e5c-108">Este cliente completo inclui serviços como proteção contra vírus e spyware, firewall e prevenção contra intrusão.</span><span class="sxs-lookup"><span data-stu-id="41e5c-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="41e5c-109">O cliente é instalado como uma extensão de segurança usando-se o Agente de VM.</span><span class="sxs-lookup"><span data-stu-id="41e5c-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="41e5c-110">Se tiver uma assinatura da Symantec para uma solução local, você poderá usá-la para proteger as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5c-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="41e5c-111">Se ainda não for cliente, você poderá se inscrever em uma assinatura de avaliação.</span><span class="sxs-lookup"><span data-stu-id="41e5c-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="41e5c-112">Para obter mais informações sobre essa solução, consulte [Symantec Endpoint Protection na plataforma Azure da Microsoft][Symantec].</span><span class="sxs-lookup"><span data-stu-id="41e5c-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="41e5c-113">Essa página também fornece links para informações de licenciamento e instruções para instalar o cliente se você já for um cliente da Symantec.</span><span class="sxs-lookup"><span data-stu-id="41e5c-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="41e5c-114">Instalar o Symantec Endpoint Protection em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="41e5c-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="41e5c-115">Antes de começar, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="41e5c-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="41e5c-116">O módulo Azure PowerShell, versão 0.8.2 ou mais recente, em seu computador de trabalho.</span><span class="sxs-lookup"><span data-stu-id="41e5c-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="41e5c-117">Você pode verificar a versão do PowerShell do Azure instalado com o comando **Get-Module azure | format-table version** .</span><span class="sxs-lookup"><span data-stu-id="41e5c-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="41e5c-118">Para obter instruções e um link para a versão mais recente, consulte [Como instalar e configurar o Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="41e5c-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="41e5c-119">Faça logon em sua assinatura do Azure usando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="41e5c-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="41e5c-120">O Agente de VM em execução na Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5c-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="41e5c-121">Primeiro, verifique se o Agente de VM já está instalado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e5c-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="41e5c-122">Preencha o nome do serviço de nuvem e o nome da máquina virtual e, em seguida, execute os seguintes comandos em um prompt de comando do Azure PowerShell com nível de administrador.</span><span class="sxs-lookup"><span data-stu-id="41e5c-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="41e5c-123">Substitua tudo entre aspas, incluindo os caracteres < e >.</span><span class="sxs-lookup"><span data-stu-id="41e5c-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="41e5c-124">Se você não souber o nome da máquina virtual e do serviço de nuvem, execute **Get-AzureVM** para listar os nomes de todas as máquinas virtuais em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="41e5c-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="41e5c-125">Se o comando **write-host** exibir **True**, o agente de VM está instalado.</span><span class="sxs-lookup"><span data-stu-id="41e5c-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="41e5c-126">Se ele exibir **False**, veja as instruções e um link para download na postagem do blog do Azure [Agente de VM e Extensões ‑ Parte 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="41e5c-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="41e5c-127">Se o Agente de VM Agent estiver instalado, execute estes comandos para instalar o agente Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="41e5c-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="41e5c-128">Para verificar se a extensão de segurança Symantec foi instalada e está atualizada:</span><span class="sxs-lookup"><span data-stu-id="41e5c-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="41e5c-129">Faça logon na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e5c-129">Log on to the virtual machine.</span></span> <span data-ttu-id="41e5c-130">Para obter instruções, veja [Como fazer logon em uma máquina virtual que executa o Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="41e5c-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="41e5c-131">Para Windows Server 2008 R2, clique em **Iniciar > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="41e5c-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="41e5c-132">Para o Windows Server 2012 ou Windows Server 2012 R2, na tela inicial, digite **Symantec** e, em seguida, clique em **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="41e5c-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="41e5c-133">Na guia **Status** da janela de **Status-Symantec Endpoint Protection**, aplique atualizações ou reinicie se necessário.</span><span class="sxs-lookup"><span data-stu-id="41e5c-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41e5c-134">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="41e5c-134">Additional resources</span></span>
<span data-ttu-id="41e5c-135">[Como fazer logon em uma máquina virtual que executa o Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="41e5c-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="41e5c-136">[Recursos e Extensões de VM do Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="41e5c-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
