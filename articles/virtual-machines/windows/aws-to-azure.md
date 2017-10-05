---
title: Mover VMs do AWS do Windows para o Azure | Microsoft Docs
description: "Mova uma instância EC2 do AWS (Amazon Web Services) do Windows para Máquinas Virtuais do Azure usando o Azure PowerShell."
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
ms.openlocfilehash: 7d2b498d3f84c4fd6cccf97c6d7781f293f5b395
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-to-azure-using-powershell"></a><span data-ttu-id="8c5ca-103">Mover uma VM do Windows do AWS (Amazon Web Services) para o Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c5ca-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span></span>

<span data-ttu-id="8c5ca-104">Se você estiver avaliando máquinas virtuais do Azure para hospedar suas cargas de trabalho, poderá exportar uma instância existente de VM do Windows EC2 do AWS (Amazon Web Services) e carregar o VHD (disco rígido virtual) no Azure.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span></span> <span data-ttu-id="8c5ca-105">Após o carregamento do VHD, você pode criar uma nova VM no Azure a partir do VHD.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span></span> 

<span data-ttu-id="8c5ca-106">Este tópico aborda a movimentação de uma VM individual do AWS para o Azure.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-106">This topic covers moving a single VM from AWS to Azure.</span></span> <span data-ttu-id="8c5ca-107">Se você quiser migrar VMs do AWS para o Azure em escala, confira [Migrar máquinas virtuais no AWS (Amazon Web Services) para o Azure com o Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8c5ca-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="8c5ca-108">Preparar a VM</span><span class="sxs-lookup"><span data-stu-id="8c5ca-108">Prepare the VM</span></span> 
 
<span data-ttu-id="8c5ca-109">Você pode carregar VHDs generalizados e especializados no Azure.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-109">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="8c5ca-110">Cada tipo exige a preparação da VM antes de exportar do AWS.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-110">Each type requires that you prepare the VM before exporting from AWS.</span></span> 

- <span data-ttu-id="8c5ca-111">**VHD Generalizado** – um VHD generalizado teve todas suas informações de conta pessoal removidas usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="8c5ca-112">Se você pretende criar novas VMs usando o VHD como uma imagem, você deve:</span><span class="sxs-lookup"><span data-stu-id="8c5ca-112">If you intend to use the VHD as an image to create new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="8c5ca-113">[Preparar uma VM do Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="8c5ca-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="8c5ca-114">Generalizar a máquina virtual usando Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-114">Generalize the virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="8c5ca-115">**VHD Especializado** – um VHD especializado mantém as contas de usuário, aplicativos e outros dados de estado de sua VM original.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="8c5ca-116">Se você pretende usar o VHD no estado em que se encontra para criar uma nova VM, certifique-se de que as seguintes etapas sejam concluídas.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span>  
    * <span data-ttu-id="8c5ca-117">[Preparar um VHD do Windows para carregar no Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="8c5ca-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="8c5ca-118">**Não** generalizar a VM usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-118">**Do not** generalize the VM using Sysprep.</span></span> 
    * <span data-ttu-id="8c5ca-119">Remover quaisquer ferramentas e agentes de virtualização de convidado que estejam instalados na VM (ou seja, ferramentas do VMware).</span><span class="sxs-lookup"><span data-stu-id="8c5ca-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="8c5ca-120">Verifique se a VM está configurada para obter o endereço IP e as configurações de DNS por meio de DHCP.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="8c5ca-121">Isso garante que o servidor obtém um endereço IP na VNet quando ele é iniciado.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span>  


## <a name="export-and-download-the-vhd"></a><span data-ttu-id="8c5ca-122">Exportar e baixar o VHD</span><span class="sxs-lookup"><span data-stu-id="8c5ca-122">Export and download the VHD</span></span> 

<span data-ttu-id="8c5ca-123">Exporte a instância do EC2 para um VHD em um bucket do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="8c5ca-124">Execute as etapas descritas no tópico da documentação da Amazon [Exportar uma instância como VM usando Importação/Exportação de VM](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) e execute o comando [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) para exportar a instância do EC2 para um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-124">Follow the steps described in the Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span></span> 

<span data-ttu-id="8c5ca-125">O arquivo VHD exportado é salvo no bucket do Amazon S3 especificado.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span></span> <span data-ttu-id="8c5ca-126">A sintaxe básica para exportar o VHD está abaixo, basta substituir o texto de espaço reservado em <brackets> por suas informações.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="8c5ca-127">Após a exportação do VHD, siga as instruções em [Como baixar um objeto de um bucket S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) para baixar o arquivo VHD do bucket S3.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8c5ca-128">O AWS cobra encargos por transferência de dados para baixar o VHD.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-128">AWS charges data transfer fees for downloading the VHD.</span></span> <span data-ttu-id="8c5ca-129">Confira [Preços do Amazon S3](https://aws.amazon.com/s3/pricing/) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8c5ca-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c5ca-130">Next steps</span></span>

<span data-ttu-id="8c5ca-131">Agora você pode carregar o VHD no Azure e criar uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="8c5ca-131">Now you can upload the VHD to Azure and create a new VM.</span></span> 

- <span data-ttu-id="8c5ca-132">Se você executou o Sysprep em seu código-fonte para **generalizá-lo** antes de exportar, consulte [Carregar um VHD generalizado e usá-lo para criar novas VMs no Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="8c5ca-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="8c5ca-133">Se você não tiver executado o Sysprep antes da exportação, o VHD será considerado **especializado**, consulte [Carregar um VHD especializado no Azure e criar uma nova VM](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="8c5ca-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span></span>

 
