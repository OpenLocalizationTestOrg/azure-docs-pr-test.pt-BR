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
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Mover uma VM do Windows de tooAzure serviços AWS (Amazon Web) usando o PowerShell

Se você estiver avaliando as máquinas virtuais do Azure para hospedar as cargas de trabalho, você pode exportar uma instância existente de VM do Windows EC2 Services AWS (Amazon Web) e carregar Olá tooAzure de disco rígido virtual (VHD). Uma vez Olá que VHD é carregado, você pode criar uma nova VM no Azure de saudação VHD. 

Este tópico aborda a mover uma VM do AWS tooAzure. Se você quiser toomove VMs do AWS tooAzure em grande escala, consulte [migrar máquinas virtuais em tooAzure AWS Amazon Web Services () com o Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Preparar Olá VM 
 
Você pode carregar tooAzure de VHDs generalizado e especializada. Cada tipo requer que você prepare Olá VM antes de exportar do AWS. 

- **VHD Generalizado** – um VHD generalizado teve todas suas informações de conta pessoal removidas usando o Sysprep. Se você pretende toouse Olá VHD como uma imagem toocreate novas VMs do, você deve: 
 
    * [Preparar uma VM do Windows](prepare-for-upload-vhd-image.md).  
    * Generalize a máquina virtual de saudação usando o Sysprep.  

 
- **Especializado VHD** -um VHD especializado mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original. Se você pretende toouse Olá VHD como-é toocreate uma nova VM, certifique-se de saudação etapas forem concluída.  
    * [Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md). **Não** generalizar Olá VM usando o Sysprep. 
    * Remova quaisquer ferramentas de virtualização de convidado e os agentes instalados em Olá VM (ou seja, as ferramentas do VMware). 
    * Certifique-se de saudação VM é configurada toopull seu endereço IP e as configurações de DNS por meio de DHCP. Isso garante que o servidor Olá obtém um endereço IP em redes de saudação quando ele é iniciado.  


## <a name="export-and-download-hello-vhd"></a>Exportar e baixe Olá VHD 

Exporte Olá EC2 instância tooa VHD em um bucket S3 da Amazon. Execute as etapas de saudação descritas no tópico de documentação do Amazon Olá [exportando uma instância como uma VM usando VM importação/exportação](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) e execução hello [criar-instância-export-tarefa](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) saudação do comando tooexport EC2 arquivo VHD de tooa de instância. 

Hello VHD arquivo exportado é salvo no bucket Olá Amazon S3 que você especificar. Olá sintaxe básica para exportar Olá VHD está abaixo, basta substituir texto de espaço reservado Olá <brackets> com suas informações.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Depois que foi exportado Olá VHD, siga as instruções de Olá em [como baixar um objeto de um Bucket S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) arquivo hello toodownload VHD do bucket Olá S3. 

> [!IMPORTANT]
> AWS encargos de taxas de transferência de dados para baixar Olá VHD. Confira [Preços do Amazon S3](https://aws.amazon.com/s3/pricing/) para saber mais.


## <a name="next-steps"></a>Próximas etapas

Agora você pode carregar Olá VHD tooAzure e crie uma nova VM. 

- Se você executar o Sysprep na sua fonte muito**generalizar** -lo antes de exportar, consulte [carregar um VHD generalizado e usá-lo toocreate um novas VMs no Azure](upload-generalized-managed.md)
- Se você não tiver executado o Sysprep antes de exportar, hello VHD é considerado **especializado**, consulte [carregar um tooAzure especializada do VHD e criar uma nova VM](create-vm-specialized.md)

 
