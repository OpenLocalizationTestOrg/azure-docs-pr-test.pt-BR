---
title: aaaCreate uma imagem personalizada do Azure DevTest Labs de um arquivo VHD | Microsoft Docs
description: "Saiba como toocreate uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Criar uma imagem personalizada de um arquivo VHD

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Olá etapas a seguir orientam você durante a criação de uma imagem personalizada de um arquivo VHD usando Olá portal do Azure:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.

1. Saudação de laboratórios, selecione lista laboratório desejado hello.  

1. Na folha do laboratório hello, selecione **configuração**. 

1. Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.

1. Em Olá **imagens personalizadas** folha, selecione **+ adicionar**.

    ![Imagem de Adicionar Personalizado](./media/devtest-lab-create-template/add-custom-image.png)

1. Insira o nome de saudação da imagem personalizada do hello. Esse nome é exibido na lista de saudação de imagens de base ao criar uma VM.

1. Insira a descrição de saudação da imagem personalizada do hello. Essa descrição é exibida na lista de saudação de imagens de base ao criar uma VM.

1. Selecione **VHD**.

1. De saudação **VHD** folha, arquivo VHD selecione Olá desejado.

1. Selecione **Okey** tooclose Olá **VHD** folha.

1. Selecione **Configuração do SO**.

1. Em Olá **configuração do sistema operacional** guia, selecione **Windows** ou **Linux**.

1. Se **Windows** é selecionada, especifique por meio da caixa de seleção de saudação se *Sysprep* foi executado na máquina de saudação. 

1. Selecione **Okey** tooclose Olá **configuração do sistema operacional** folha.

1. Selecione **Okey** imagem personalizada do toocreate hello.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas

- [Imagens personalizadas ou fórmulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copiar imagens personalizadas entre Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Próximas etapas

- [Adicionar um laboratório de tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
