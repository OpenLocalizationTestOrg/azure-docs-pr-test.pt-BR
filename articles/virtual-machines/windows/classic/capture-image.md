---
title: aaaCapture uma imagem de uma VM do Windows Azure | Microsoft Docs
description: "Capture uma imagem de uma máquina virtual do Windows Azure criada com o modelo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Capture uma imagem de uma máquina virtual do Windows Azure criada com o modelo de implantação clássico hello.
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações de modelo do Resource Manager, consulte [Capturar uma imagem gerenciada de uma VM generalizada no Azure](../capture-image-resource.md).

Este artigo mostra como toocapture uma máquina virtual do Azure que executam o Windows para que você pode usá-lo como uma imagem toocreate outras máquinas virtuais. Esta imagem inclui o disco do sistema operacional Olá e discos de dados que são anexados toohello máquina de virtual. Não inclui configurações de rede, portanto, você precisará tooset as configurações de rede ao criar outras máquinas virtuais que usam imagem Olá Olá.

Repositórios do Azure Olá imagem em **imagens da VM (clássico)**, um **de computação** Olá de serviço listado quando você exibe todos os serviços do Azure. Isso é hello mesmo local onde as imagens que você carregou são armazenadas. Para obter detalhes sobre imagens, consulte [Sobre as imagens de máquinas virtuais](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Antes de começar
Essas etapas pressupõem que você já criou uma máquina virtual do Azure e configurado o sistema operacional de hello, incluindo anexar discos de dados. Se você ainda não tiver feito isso ainda, consulte Olá seguintes artigos para obter informações sobre como criar e preparar a máquina virtual de saudação:

* [Criar uma máquina virtual de uma imagem](createportal.md)
* [Como tooattach dados de um disco tooa virtual machine](attach-disk.md)
* Verifique se as funções de servidor de saudação são compatíveis com Sysprep. Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Esse processo exclui a máquina virtual original de saudação depois de ser capturada.
>
>

Toocapturing anterior de uma imagem de uma máquina virtual do Azure, é recomendável backup Olá máquina de virtual de destino. O backup das máquinas virtuais do Azure pode ser feito usando o Backup do Azure. Para obter detalhes, veja [Fazer backup de máquinas virtuais do Azure](../../../backup/backup-azure-vms.md). Existem outras soluções de parceiros certificados. toofind o que está disponível no momento, pesquise hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Capturar a máquina virtual de saudação
1. Em Olá [portal do Azure](http://portal.azure.com), **conectar** toohello VM. Para obter instruções, consulte [como toosign na máquina virtual de tooa executando o Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Abra uma janela de Prompt de comando como administrador.
3. Altere o diretório de saudação muito`%windir%\system32\sysprep`, e execute sysprep.exe.
4. Olá **ferramenta de preparação do sistema** caixa de diálogo é exibida. Olá a seguir:

   * Em **Ação de Limpeza do Sistema**, selecione **Entrar na Configuração Inicial pelo Usuário do Sistema (OOBE)** e verifique se a opção **Generalizar** está marcada. Para obter mais informações sobre como usar o Sysprep, consulte [como tooUse Sysprep: uma introdução][How tooUse Sysprep: An Introduction].
   * Em **Opções de Desligamento**, selecione **Desligar**.
   * Clique em **OK**.

   ![Executar o Sysprep](./media/capture-image/SysprepGeneral.png)
5. Sysprep desliga a máquina virtual de saudação, que altera o status de saudação da máquina virtual Olá Olá portal do Azure muito**parado**.
6. No portal do Azure de Olá, clique em **máquinas virtuais (clássicas)** e selecione Olá a máquina virtual que deseja toocapture. Olá **imagens da VM (clássico)** grupo é listado em **de computação** quando você exibir **mais serviços**.

7. Na barra de comandos de saudação, clique em **capturar**.

   ![Capturar a máquina virtual](./media/capture-image/CaptureVM.png)

   Olá **captura Olá Máquina Virtual** caixa de diálogo é exibida.

8. Em **nome da imagem**, digite um nome para a nova imagem de saudação. Em **rótulo da imagem**, digite um rótulo para a nova imagem de saudação.

9. Clique em **executei o Sysprep na máquina virtual de saudação**. Essa caixa de seleção se refere a ações de toohello com Sysprep nas etapas 3 a 5. Uma imagem _deve_ ser generalizado executando o Sysprep antes de adicionar um servidor Windows tooyour o conjunto de imagens de imagens personalizadas.

10. Após a conclusão da captura hello, nova imagem de saudação se torna disponível no hello **Marketplace**, em Olá **de computação**, **imagens da VM (clássico)** contêiner.

    ![Captura de imagem bem-sucedida](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Próximas etapas
imagem de saudação é máquinas de virtuais toocreate toobe pronto usado. toodo isso, você criará uma máquina virtual selecionando Olá **mais serviços** item de menu na parte inferior de saudação do menu de serviços hello, em seguida, **imagens da VM (clássico)** em Olá **computação**grupo. Para obter instruções, consulte [Criar uma máquina virtual de uma imagem](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
