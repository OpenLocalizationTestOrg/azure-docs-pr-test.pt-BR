---
title: "Diagnóstico de aaaBoot para máquinas virtuais Linux no Azure | Documento do Microsoft"
description: "Visão geral dos recursos de depuração dois Olá para máquinas virtuais Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="c22e6-103">Como toouse inicializar máquinas virtuais do diagnóstico tootroubleshoot Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="c22e6-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="c22e6-104">O suporte a dois recursos de depuração agora está disponível no Azure: Saída do Console e a Captura de Tela para o modelo de implantação do Resource Manager de Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="c22e6-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="c22e6-105">Ao colocar tooAzure sua própria imagem ou até mesmo inicialização uma das imagens da plataforma Olá, pode haver várias razões por que uma máquina Virtual entra em um estado não inicializável.</span><span class="sxs-lookup"><span data-stu-id="c22e6-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="c22e6-106">Habilitar esses recursos você tooeasily diagnosticar e recuperar suas máquinas virtuais de falhas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c22e6-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="c22e6-107">Para máquinas de virtuais de Linux, você pode facilmente exibir saída de hello de seu log de console da saudação Portal:</span><span class="sxs-lookup"><span data-stu-id="c22e6-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portal do Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="c22e6-109">No entanto, para o Windows e máquinas virtuais do Linux Azure também permite que toosee uma captura de tela de Olá VM do hipervisor hello:</span><span class="sxs-lookup"><span data-stu-id="c22e6-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Erro](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="c22e6-111">Esses dois recursos têm suporte em máquinas virtuais do Azure em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="c22e6-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="c22e6-112">Observe, capturas de tela e saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c22e6-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="c22e6-113">Erros comuns de inicialização</span><span class="sxs-lookup"><span data-stu-id="c22e6-113">Common boot errors</span></span>

- [<span data-ttu-id="c22e6-114">Problemas com o sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="c22e6-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="c22e6-115">Problemas de kernel</span><span class="sxs-lookup"><span data-stu-id="c22e6-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="c22e6-116">Erros de FSTAB</span><span class="sxs-lookup"><span data-stu-id="c22e6-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="c22e6-117">Habilitar o diagnóstico em uma nova máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c22e6-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="c22e6-118">Ao criar uma nova máquina Virtual do Portal de visualização de saudação, selecione Olá **do Azure Resource Manager** na lista suspensa de modelo de implantação de saudação:</span><span class="sxs-lookup"><span data-stu-id="c22e6-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Gerenciador de Recursos](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="c22e6-120">Configure Olá conta de armazenamento de saudação do monitoramento opção tooselect em que você deseja tooplace esses arquivos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c22e6-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Criar VM](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="c22e6-122">Se você estiver implantando um modelo do Azure Resource Manager, navegue tooyour recurso de máquina Virtual e acrescentar a seção de perfil de diagnóstico hello.</span><span class="sxs-lookup"><span data-stu-id="c22e6-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="c22e6-123">Lembre-se o cabeçalho de versão de API do toouse hello "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="c22e6-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="c22e6-124">perfil de diagnóstico Olá permite tooselect conta de armazenamento de saudação onde você deseja tooput esses logs.</span><span class="sxs-lookup"><span data-stu-id="c22e6-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="c22e6-125">Atualizar uma máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="c22e6-125">Update an existing virtual machine</span></span>

<span data-ttu-id="c22e6-126">Diagnóstico de inicialização tooenable por meio do portal hello, você também pode atualizar uma máquina virtual existente por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="c22e6-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="c22e6-127">Selecione Olá opção de diagnóstico de inicialização e salvar.</span><span class="sxs-lookup"><span data-stu-id="c22e6-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="c22e6-128">Reinicie o efeito de tootake VM hello.</span><span class="sxs-lookup"><span data-stu-id="c22e6-128">Restart hello VM tootake effect.</span></span>

![Atualizar VM existente](./media/boot-diagnostics/screenshot5.png)