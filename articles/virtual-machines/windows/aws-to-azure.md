---
title: aaaMove tooAzure um Windows AWS VMs | Microsoft Docs
description: "Mova uma instância de serviços AWS (Amazon Web) EC2 Windows tooAzure máquinas virtuais usando o PowerShell do Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="cb948-103">Mover uma VM do Windows de tooAzure serviços AWS (Amazon Web) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb948-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="cb948-104">Se você estiver avaliando as máquinas virtuais do Azure para hospedar as cargas de trabalho, você pode exportar uma instância existente de VM do Windows EC2 Services AWS (Amazon Web) e carregar Olá tooAzure de disco rígido virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="cb948-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="cb948-105">Uma vez Olá que VHD é carregado, você pode criar uma nova VM no Azure de saudação VHD.</span><span class="sxs-lookup"><span data-stu-id="cb948-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="cb948-106">Este tópico aborda a mover uma VM do AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cb948-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="cb948-107">Se você quiser toomove VMs do AWS tooAzure em grande escala, consulte [migrar máquinas virtuais em tooAzure AWS Amazon Web Services () com o Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cb948-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="cb948-108">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="cb948-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="cb948-109">Você pode carregar tooAzure de VHDs generalizado e especializada.</span><span class="sxs-lookup"><span data-stu-id="cb948-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="cb948-110">Cada tipo requer que você prepare Olá VM antes de exportar do AWS.</span><span class="sxs-lookup"><span data-stu-id="cb948-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="cb948-111">**VHD Generalizado** – um VHD generalizado teve todas suas informações de conta pessoal removidas usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="cb948-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="cb948-112">Se você pretende toouse Olá VHD como uma imagem toocreate novas VMs do, você deve:</span><span class="sxs-lookup"><span data-stu-id="cb948-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="cb948-113">[Preparar uma VM do Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="cb948-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="cb948-114">Generalize a máquina virtual de saudação usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="cb948-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="cb948-115">**Especializado VHD** -um VHD especializado mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original.</span><span class="sxs-lookup"><span data-stu-id="cb948-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="cb948-116">Se você pretende toouse Olá VHD como-é toocreate uma nova VM, certifique-se de saudação etapas forem concluída.</span><span class="sxs-lookup"><span data-stu-id="cb948-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="cb948-117">[Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="cb948-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="cb948-118">**Não** generalizar Olá VM usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="cb948-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="cb948-119">Remova quaisquer ferramentas de virtualização de convidado e os agentes instalados em Olá VM (ou seja, as ferramentas do VMware).</span><span class="sxs-lookup"><span data-stu-id="cb948-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="cb948-120">Certifique-se de saudação VM é configurada toopull seu endereço IP e as configurações de DNS por meio de DHCP.</span><span class="sxs-lookup"><span data-stu-id="cb948-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="cb948-121">Isso garante que o servidor Olá obtém um endereço IP em redes de saudação quando ele é iniciado.</span><span class="sxs-lookup"><span data-stu-id="cb948-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="cb948-122">Exportar e baixe Olá VHD</span><span class="sxs-lookup"><span data-stu-id="cb948-122">Export and download hello VHD</span></span> 

<span data-ttu-id="cb948-123">Exporte Olá EC2 instância tooa VHD em um bucket S3 da Amazon.</span><span class="sxs-lookup"><span data-stu-id="cb948-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="cb948-124">Execute as etapas de saudação descritas no tópico de documentação do Amazon Olá [exportando uma instância como uma VM usando VM importação/exportação](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) e execução hello [criar-instância-export-tarefa](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) saudação do comando tooexport EC2 arquivo VHD de tooa de instância.</span><span class="sxs-lookup"><span data-stu-id="cb948-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="cb948-125">Hello VHD arquivo exportado é salvo no bucket Olá Amazon S3 que você especificar.</span><span class="sxs-lookup"><span data-stu-id="cb948-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="cb948-126">Olá sintaxe básica para exportar Olá VHD está abaixo, basta substituir texto de espaço reservado Olá <brackets> com suas informações.</span><span class="sxs-lookup"><span data-stu-id="cb948-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="cb948-127">Depois que foi exportado Olá VHD, siga as instruções de Olá em [como baixar um objeto de um Bucket S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) arquivo hello toodownload VHD do bucket Olá S3.</span><span class="sxs-lookup"><span data-stu-id="cb948-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cb948-128">AWS encargos de taxas de transferência de dados para baixar Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="cb948-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="cb948-129">Confira [Preços do Amazon S3](https://aws.amazon.com/s3/pricing/) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="cb948-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb948-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb948-130">Next steps</span></span>

<span data-ttu-id="cb948-131">Agora você pode carregar Olá VHD tooAzure e crie uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="cb948-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="cb948-132">Se você executar o Sysprep na sua fonte muito**generalizar** -lo antes de exportar, consulte [carregar um VHD generalizado e usá-lo toocreate um novas VMs no Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="cb948-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="cb948-133">Se você não tiver executado o Sysprep antes de exportar, hello VHD é considerado **especializado**, consulte [carregar um tooAzure especializada do VHD e criar uma nova VM](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="cb948-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
