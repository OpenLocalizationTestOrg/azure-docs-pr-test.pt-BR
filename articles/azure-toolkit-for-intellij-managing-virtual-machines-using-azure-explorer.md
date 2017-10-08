---
title: "máquinas virtuais de aaaManage usando hello Azure Explorer para IntelliJ | Microsoft Docs"
description: "Saiba como toomanage as máquinas virtuais do Azure usando hello Azure Explorer para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Gerenciar máquinas virtuais usando hello Azure Explorer para IntelliJ

Hello Azure Explorer, que faz parte do hello Azure Toolkit for IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar as máquinas virtuais em sua conta do Azure de dentro do ambiente de desenvolvimento integrado Olá IntelliJ (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Criar uma máquina virtual no IntelliJ

toocreate uma máquina virtual usando hello Azure Explorer Olá a seguir: 

1. Entrar tooyour conta do Azure usando as etapas de Olá Olá [instruções entrar para hello Azure Toolkit for IntelliJ] artigo.

2. Em hello **Azure Explorer** exibir, expanda Olá **Azure** nó, clique com botão direito **máquinas virtuais**e, em seguida, clique em **criar VM**. 

   ![Olá comando Criar VM][CR01]  
    Olá **criar nova máquina Virtual** assistente é aberto.

3. Em Olá **escolher uma assinatura** janela, selecione sua assinatura e, em seguida, clique em **próximo**. 

   ![Olá janela Escolha uma assinatura][CR02]

4. Em Olá **selecionar uma imagem de máquina Virtual** janela, digite Olá informações a seguir:

   * **Localização**: especifica o local no qual sua máquina virtual será criada (por exemplo, *Oeste dos EUA*). 

   * **Imagem recomendada**: especifica que você escolherá uma imagem de uma lista abreviada de imagens usadas com frequência.

   * **Imagem personalizada**: Especifica que você escolherá uma imagem personalizada, fornecendo Olá informações a seguir:

      * **Publicador**: Especifica o publicador de saudação que criou a imagem de saudação que você usará para sua máquina virtual (por exemplo, *Microsoft*).

      * **Oferecer**: Especifica a máquina virtual de saudação toouse da oferta do publicador selecionado hello (por exemplo, *JDK*).

      * **SKU**: especifica Olá toouse SKU (unidade) de manutenção de estoque de oferta de saudação selecionado (por exemplo, *JDK_8*).

      * **Versão #**: especifica qual versão de saudação selecionada toouse SKU.

   ![Olá selecione uma janela de imagem de máquina Virtual][CR03]

5. Clique em **Avançar**. 

6. Em Olá **configurações básicas de máquina Virtual** janela, digite Olá informações a seguir:

   * **Nome da máquina virtual**: Especifica o nome Olá para sua nova máquina virtual, que deve começar com uma letra e conter apenas letras, números e hifens.

   * **Tamanho**: Especifica o número de saudação de núcleos e memória tooallocate para sua máquina virtual.

   * **Nome de usuário**: especifica Olá toocreate de conta de administrador para gerenciar sua máquina virtual.

   * **Senha** e **confirmar**: Especifica a senha Olá para sua conta de administrador.

   ![janela de configurações básicas de máquina Virtual Olá][CR04]

7. Clique em **Avançar**. 

8. Em Olá **recursos associados** janela, digite Olá informações a seguir:

   * **Grupo de recursos**: Especifica o grupo de recursos de saudação para sua máquina virtual. Selecione uma saudação as opções a seguir:
      * **Criar um novo**: Especifica que você deseja toocreate um novo grupo de recursos.
      * **Usar existente**: Especifica que você deseja tooselect em uma lista de grupos de recursos que estão associados com sua conta do Azure.

       ![janela de recursos associado Olá][CR07]

   * **Conta de armazenamento**: especifica Olá toouse de conta de armazenamento para armazenar a máquina virtual. Escolha uma conta de armazenamento existente ou crie uma nova. Se você escolher **criar novo**, Olá caixa de diálogo a seguir será exibida:

      ![caixa de diálogo Criar conta de armazenamento Olá][CR05]

   * **Rede virtual** e **sub-rede**: Especifica a rede virtual hello e a sub-rede que sua máquina virtual será conectado ao. Use uma rede e sub-rede existentes ou crie uma nova rede e sub-rede. Se você selecionar **criar novo**, Olá caixa de diálogo a seguir será exibida:

      ![caixa de diálogo Criar rede Virtual Olá][CR06]

   * **Endereço IP público**: especifica um endereço IP externo para sua máquina virtual. Você pode escolher um novo endereço IP toocreate ou, se sua máquina virtual não terá um endereço IP público, você pode selecionar **(nenhum)**. 

   * **Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual. Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**. 

   * **Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer. Você pode selecionar um conjunto de disponibilidade existente, crie um novo conjunto de disponibilidade ou, se sua máquina virtual não pertencerá tooan conjunto de disponibilidade, selecione **(nenhum)**.

9. Clique em **Concluir**.  
    Sua nova máquina virtual é exibida na janela de ferramenta do Gerenciador do Azure hello. 

   ![Nova máquina virtual no hello exibição do Explorer do Azure][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Reiniciar uma máquina virtual no IntelliJ

toorestart uma máquina virtual usando hello Azure Explorer no IntelliJ, Olá a seguir:

1. Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **reiniciar**.

   ![Olá comando de reinicialização de máquina virtual][RE01]

2. Na janela de confirmação de saudação, clique em **Sim**. 

   ![Olá reiniciar a janela de confirmação da máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Desligar uma máquina virtual no IntelliJ

tooshut para baixo de uma máquina virtual em execução usando hello Azure Explorer no IntelliJ, Olá a seguir:

1. Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **desligamento**.

   ![comando de desligamento de máquina virtual Olá][SH01]

2. Na janela de confirmação de saudação, clique em **Sim**. 

   ![Olá desligar a janela de confirmação da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Excluir uma máquina virtual no IntelliJ

toodelete uma máquina virtual usando hello Azure Explorer no IntelliJ, Olá a seguir:

1. Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **excluir**.

   ![Olá comando de exclusão de máquina virtual][DE01]

2. Na janela de confirmação de saudação, clique em **Sim**. 

   ![Olá excluir a janela de confirmação da máquina virtual][DE02]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre preços e tamanhos de máquina virtual do Azure, consulte Olá recursos a seguir:

* Tamanhos de máquinas virtuais do Azure
  * [Tamanhos das máquinas virtuais do Windows no Azure]
  * [Tamanhos das máquinas virtuais do Linux no Azure]
* Preços de máquinas virtuais do Azure
  * [Preços de máquinas virtuais do Windows]
  * [Preços de máquinas virtuais do Linux]

Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [O que há de novo no hello Kit de ferramentas do Azure para Eclipse]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * [Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [O que há de novo no hello Azure Toolkit for IntelliJ]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [instruções entrar para hello Azure Toolkit for IntelliJ]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]

Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[instruções entrar para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquinas virtuais do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquinas virtuais do Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
