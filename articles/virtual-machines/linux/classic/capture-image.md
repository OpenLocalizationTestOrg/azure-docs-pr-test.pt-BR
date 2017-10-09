---
title: aaaCapture uma imagem de uma VM do Linux | Microsoft Docs
description: "Saiba como toocapture uma imagem de uma baseados em Linux do Azure máquina virtual (VM) criados com o modelo de implantação clássico hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Como uma máquina de virtual do Linux clássica como uma imagem de toocapture
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este artigo mostra como toocapture uma máquina de virtual do Azure (VM) clássica executando o Linux como uma imagem toocreate outras máquinas virtuais. Esta imagem inclui o disco do sistema operacional hello e discos de dados anexados toohello VM. Não inclui a configuração de rede, portanto, você precisa tooconfigure que quando você cria Olá outra VM da imagem de saudação.

Repositórios do Azure Olá imagem em **imagens**, junto com as imagens que você carregou. Para saber mais sobre imagens, confira [Sobre imagens da Máquina Virtual no Azure][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Antes de começar
Essas etapas pressupõem que você já criou uma VM do Azure usando o modelo de implantação clássico hello e sistema de operacional de saudação configurado, incluindo anexar discos de dados. Se você precisar toocreate uma VM, leia [como tooCreate uma máquina Virtual Linux][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Capturar a máquina virtual de saudação
1. [Conecte-se a VM do toohello](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) usando um cliente SSH de sua escolha.
2. Na janela SSH hello, digite Olá comando a seguir. saudação de saída de `waagent` podem variar um pouco dependendo da versão de saudação do utilitário:

    ```bash
    sudo waagent -deprovision+user
    ```

    Olá comando anterior tentativas tooclean sistema de saudação e torná-lo adequado para reprovisionamento. Essa operação fará Olá tarefas a seguir:

   * Remove as chaves de host do SSH (se Provisioning.RegenerateSshHostKeyPair for 'y' no arquivo de configuração de saudação)
   * Limpa a configuração de servidor de nomes em /etc/resolv.conf
   * Olá remove `root` senha de usuário de/etc/sombra (se Provisioning.DeleteRootPassword for 'y' no arquivo de configuração de saudação)
   * Remove concessões de cliente DHCP em cache
   * Redefine toolocalhost.localdomain de nome de host
   * Exclui a conta de usuário provisionado última hello (obtida /var/lib/waagent) **e dados associados**.

     > [!NOTE]
     > Desprovisionamento exclui arquivos e dados muito "generalizar" hello imagem. Somente execute esse comando em uma máquina virtual que você pretende toocapture como um novo modelo de imagem. Eles não garantem imagem Olá seja limpo de todas as informações confidenciais ou é adequada para partes de toothird de redistribuição.

3. Tipo **y** toocontinue. Você pode adicionar Olá `-force` parâmetro tooavoid essa etapa de confirmação.
4. Tipo **Exit** cliente SSH tooclose hello.

   > [!NOTE]
   > Olá etapas restantes supõem que você já tiver [instalado Olá CLI do Azure](../../../cli-install-nodejs.md) no computador cliente. Olá todas as etapas a seguir também pode ser feito no hello [portal do Azure](http://portal.azure.com).

5. No computador cliente, abra CLI do Azure e logon tooyour assinatura do Azure. Para obter detalhes, leia [conectar tooan assinatura do Azure do hello CLI do Azure](../../../xplat-cli-connect.md).

   > [!NOTE]
   > No portal do Azure de Olá, faça logon no portal de toohello.

6. Verifique se você está no modo de Gerenciamento de Serviços:

    ```azurecli
    azure config mode asm
    ```

7. Desligar Olá VM já desprovisionada. Olá exemplo a seguir é desligado Olá VM denominada `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Se necessário, você pode exibir uma lista Olá todas as máquinas virtuais criadas na sua assinatura usando`azure vm list`

   > [!NOTE]
   > Se você estiver usando Olá portal do Azure, selecione Olá VM e clique em **parar** desligar Olá VM.

8. Quando Olá VM é interrompido, capture a imagem de saudação. Olá capturas de exemplo a seguir Olá VM denominada `myVM` e cria uma imagem generalizada chamada `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Olá `-t` subcomando exclusões Olá máquina virtual original.

    > [!NOTE]
    > Em Olá portal do Azure, você pode capturar uma imagem selecionando **imagem** no menu de hub hello. Você precisa Olá toosupply informações Olá imagem a seguir: nome do grupo de recursos, local, tipo de sistema operacional e caminho de blob de armazenamento.

9. Olá nova imagem está agora disponível na lista de saudação de imagens que podem ser tooconfigure de usados qualquer nova VM. Você pode exibi-lo com o comando hello:

   ```azurecli
   azure vm image list
   ```

   Em Olá [portal do Azure](http://portal.azure.com), Olá nova imagem aparecerá em Olá **imagens da VM (clássico)** que pertence a toohello **de computação** serviços. Você pode acessar **imagens da VM (clássico)** clicando _mais serviços_ na parte inferior de saudação do hello Azure lista de serviço e, em seguida, verificando Olá **de computação** serviços.   

   ![Captura de imagem bem-sucedida](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Próximas etapas
imagem de saudação está pronto toobe usado toocreate VMs. Você pode usar o comando CLI do Azure de saudação `azure vm create` e o nome de imagem Olá fonte criado por você. Para obter mais informações, consulte [usando Olá CLI do Azure com o modelo de implantação clássico](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Como alternativa, use Olá [portal do Azure](http://portal.azure.com) toocreate uma VM personalizada usando Olá **imagem** método hello a seleção de imagem e você criou. Para obter mais informações, consulte [como tooCreate uma VM personalizada][How tooCreate a Custom Virtual Machine].

**Consulte também:** [Guia do usuário do agente Linux para o Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
