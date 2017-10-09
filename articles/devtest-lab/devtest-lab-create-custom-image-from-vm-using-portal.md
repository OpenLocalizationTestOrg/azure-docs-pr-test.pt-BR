---
title: aaaCreate uma imagem personalizada do Azure DevTest Labs de uma VM | Microsoft Docs
description: "Saiba como toocreate uma imagem personalizada no Azure DevTest Labs de uma VM provisionados usando Olá portal do Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Criar uma imagem personalizada de uma VM

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Você pode criar uma imagem personalizada de uma VM provisionada e depois usar essa imagem personalizada toocreate VMs idênticas. Olá, as etapas a seguir ilustra como toocreate um personalizado da imagem de uma VM:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.

1. Saudação de laboratórios, selecione lista laboratório desejado hello.  

1. Na folha do laboratório hello, selecione **minhas máquinas virtuais**.
 
1. Em Olá **minhas máquinas virtuais** folha, selecione Olá VM do qual você deseja imagem personalizada do toocreate hello.

1. Na folha de saudação da VM, selecione **criar imagem personalizada (VHD)**.

    ![Criar item de menu de imagem personalizada](./media/devtest-lab-create-template/create-custom-image.png)

1. Em Olá **criar imagem** folha, insira um nome e uma descrição para sua imagem personalizada. Essa informação é exibida na lista de saudação de bases de dados quando você cria uma máquina virtual.

    ![Criar folha de imagem personalizada](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Selecione se o sysprep foi executado no hello VM. Se sysprep Olá não foi executado no hello VM, especifique se você deseja executar quando uma VM é criada usando essa imagem personalizada do sysprep.

1. Selecione **Okey** quando terminar de toocreate Olá imagem personalizada.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas

- [Imagens personalizadas ou fórmulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copiar imagens personalizadas entre Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Próximas etapas

- [Adicionar um laboratório de tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
