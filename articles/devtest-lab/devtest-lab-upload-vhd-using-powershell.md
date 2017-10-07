---
title: aaaUpload VHD arquivo tooAzure DevTest Labs usando o PowerShell | Microsoft Docs
description: Carregar conta de armazenamento do toolab do arquivo VHD usando o PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Carregar conta de armazenamento do toolab do arquivo VHD usando o PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

No Azure DevTest Labs, arquivos VHD podem ser imagens personalizadas usadas toocreate, que são máquinas virtuais de tooprovision usado. Olá etapas a seguir orientam você durante usando PowerShell tooupload conta de armazenamento de um VHD arquivo tooa lab. Depois de carregar seu arquivo VHD, Olá [próximas etapas seção](#next-steps) lista alguns artigos que ilustram como toocreate uma imagem personalizada do hello carregado o arquivo VHD. Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Instruções passo a passo

as etapas a seguir de saudação da extensão de arquivo por meio de carregar um VHD tooAzure DevTest Labs usando o PowerShell. 

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.

1. Saudação de laboratórios, selecione lista laboratório desejado hello.  

1. Na folha do laboratório hello, selecione **configuração**. 

1. Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.

1. Em Olá **imagens personalizadas** folha, selecione **+ adicionar**. 

1. Em Olá **imagem personalizada** folha, selecione **VHD**.

1. Em Olá **VHD** folha, selecione **carregar um VHD usando o PowerShell**.

    ![Carregar o VHD usando o PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. Em Olá **carregue uma imagem usando o PowerShell** folha, editor de texto cópia Olá gerado do PowerShell script tooa.

1. Modificar Olá **LocalFilePath** parâmetro hello **Add-AzureVhd** cmdlet toopoint toohello local do arquivo VHD que você deseja tooupload de saudação.

1. Em um prompt do PowerShell, execute Olá **Add-AzureVhd** cmdlet (com hello modificado **LocalFilePath** parâmetro).

> [!WARNING] 
> 
> processo de saudação de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho de saudação do arquivo VHD hello e a velocidade de conexão.

## <a name="next-steps"></a>Próximas etapas

- [Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure](devtest-lab-create-template.md)
- [Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
