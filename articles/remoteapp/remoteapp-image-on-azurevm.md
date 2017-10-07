---
title: aaaCreate uma imagem do Azure RemoteApp com base em uma VM do Azure | Microsoft Docs
description: "Saiba como toocreate uma imagem do Azure RemoteApp, iniciando com uma máquina virtual do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Criar uma imagem de RemoteApp do Azure com base em uma máquina virtual do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Você pode criar imagens do Azure RemoteApp (que contêm aplicativos Olá que compartilhar em sua coleção) de uma máquina virtual do Azure. Você também pode escolher toouse uma imagem de máquina virtual, adicionamos toohello Galeria de imagens de VM do Azure que atenda a todos os requisitos de imagem do Azure RemoteApp Olá - você pode usar essa imagem VM como um ponto de partida para sua VM, se desejar. Basta procure imagem de "Windows Server Desktop Host da sessão remota" hello na biblioteca de saudação.

Há dois toocreate etapas sua própria imagem com base em uma VM do Azure - criar imagem hello e, em seguida, carregá-lo do tooAzure de biblioteca Olá VM do Azure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Criar uma imagem personalizada com base em uma VM do Azure
Use essas etapas toocreate uma imagem com base em uma VM do Azure.

1. Crie uma máquina virtual do Azure. Você pode usar o hello "Windows Server Desktop Host da sessão remota" ou imagem "Windows Server Remote Desktop sessão Host com o Microsoft Office 365 ProPlus" hello na Galeria de imagens de máquina virtual do Azure hello. Esta imagem atende a todos os requisitos de imagem de modelo para RemoteApp do Azure hello.
   
    Para obter detalhes, consulte [Criar uma VM que executa o Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Conectar toohello VM e instalar e configurar aplicativos Olá que você deseja tooshare por meio do RemoteApp. Verifique se tooperform quaisquer configurações adicionais do Windows necessárias para seus aplicativos.
   
    Para obter detalhes, consulte [como tooLog no tooa Máquina Virtual executando o Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Se você estiver usando uma das imagens do Host de sessão de área de trabalho remota do Windows Server hello, há um script de validação incluído que garantirá a que sua VM atende Olá RemoteApp pre-reqs. script de toorun, clique duas vezes em **ValidateRemoteAppImage** na área de trabalho de saudação. Certifique-se de que todos os erros relatados pelo script hello são corrigidos antes da próxima etapa de toohello de continuar.
4. SYSPREP generalize e capture a imagem de saudação. Consulte [como tooCapture tooUse uma máquina Virtual do Windows como um modelo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obter instruções.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Importar imagem Olá para biblioteca de imagens do Azure RemoteApp Olá
Use a nova imagem essas etapas tooimport Olá no Azure RemoteApp:

1. Em Olá **imagens de modelo** guia:
   
   * Se você não tiver nenhuma imagem existente, clique em **Carregar ou Importar uma Imagem de Modelo**.
   * Se você já tem pelo menos uma imagem, clique em  **+**  tooadd uma nova imagem.
2. Selecione a biblioteca **Importar uma imagem de suas Máquinas Virtuais** e clique em **Avançar**.
3. Na página seguinte do hello, selecione sua imagem personalizada da lista de saudação e confirme se você seguiu as etapas de saudação listadas quando você criou sua imagem. Clique em **Avançar**.
4. Insira um nome para a nova imagem do RemoteApp hello, escolha Olá local e clique em processo de importação do hello marca de seleção toostart hello.

> [!NOTE]
> Você pode importar imagens de qualquer local do Azure tem suportada por máquinas virtuais do Azure tooany local do Azure com suporte pelo Azure RemoteApp. Dependendo de locais de saudação importação Olá pode demorar até too25 minutos.
> 
> 

Agora você está pronto toocreate sua nova coleção, ou um [nuvem](remoteapp-create-cloud-deployment.md) coleção ou [híbrida](remoteapp-create-hybrid-deployment.md), dependendo de suas necessidades.

