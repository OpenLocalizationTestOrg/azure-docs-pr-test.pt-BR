---
title: contas de armazenamento aaaManage usando hello Azure Explorer para IntelliJ | Microsoft Docs
description: Saiba como toomanage o armazenamento do Azure contas usando hello Azure Explorer para IntelliJ.
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
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>Gerenciar contas de armazenamento usando hello Azure Explorer para IntelliJ

Olá Explorer do Azure, que faz parte do hello Azure Toolkit for IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar contas de armazenamento em sua conta do Azure de dentro do ambiente de desenvolvimento integrado Olá IntelliJ (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Criar uma conta de armazenamento no IntelliJ

toocreate uma conta de armazenamento usando hello Azure Explorer Olá a seguir:

1. Entrar tooyour conta do Azure usando Olá [instruções entrar para Olá Kit de ferramentas do Azure para Eclipse]. 

2. Em hello **Azure Explorer** exibir, expanda Olá **Azure** nó, clique com botão direito **contas de armazenamento**e, em seguida, clique em **criar conta de armazenamento**.

   ![Comando para Criar Conta de Armazenamento][CS01]

3. Em Olá **criar conta de armazenamento** caixa de diálogo, especifique Olá as opções a seguir:

   ![Caixa de diálogo Criar Nova Conta de Armazenamento][CS02]

   * **Nome**: Especifica o nome Olá Olá nova conta de armazenamento.

   * **Tipo de conta**: Especifica o tipo de saudação do toocreate de conta de armazenamento (por exemplo, "armazenamento de Blob"). Para saber mais, confira [Sobre as contas de armazenamento do Azure]. 

   * **Desempenho**: Especifica a conta de armazenamento toouse da oferta do publicador de saudação selecionado (por exemplo, "Premium"). Para saber mais, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure]. 

   * **Replicação**: Especifica a replicação Olá Olá conta de armazenamento (por exemplo, "com redundância de zona"). Para saber mais, veja [Replicação do Armazenamento do Azure]. 

   * **Assinatura**: especifica Olá assinatura do Azure que você deseja toouse Olá nova conta de armazenamento.

   * **Local**: Especifica o local Olá onde sua conta de armazenamento será criada (por exemplo, "Oeste US").

   * **Grupo de recursos**: Especifica o grupo de recursos de saudação para sua máquina virtual. Selecione uma saudação as opções a seguir:
      * **Criar um novo**: Especifica que você deseja toocreate um novo grupo de recursos.
      * **Usar existente**: especifica que você selecionará em uma lista de grupos de recursos associados à sua conta do Azure.

4. Quando você tiver especificado todos Olá anterior opções, clique em **Okey**.

## <a name="create-a-storage-container-in-intellij"></a>Criar um contêiner de armazenamento no IntelliJ

toocreate um contêiner de armazenamento usando hello Azure Explorer Olá a seguir:

1. No hello exibição do Explorer do Azure, clique conta de armazenamento Olá onde toocreate um contêiner e, em seguida, clique em **criar contêiner de blob**.

   ![Comando Criar contêiner de blob][CC01]

2. Em Olá **criar contêiner de blob** caixa de diálogo Especificar nome de saudação para seu contêiner e, em seguida, clique em **Okey**. Para saber mais sobre como nomear contêineres de armazenamento, veja [Nomenclatura e referência de contêineres, blobs e metadados].

   ![Caixa de Diálogo Criar Contêiner de Armazenamento][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Excluir um contêiner de armazenamento no IntelliJ

toodelete um contêiner de armazenamento usando hello Azure Explorer Olá a seguir:

1. No hello exibição do Explorer do Azure, clique o contêiner de armazenamento hello e, em seguida, clique em **excluir**.

   ![Comando Excluir contêiner de armazenamento][DC01]

2. Na janela de confirmação de saudação, clique em **Sim**.

   ![Janela de confirmação de Excluir contêiner de armazenamento][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Excluir uma conta de armazenamento no IntelliJ

toodelete uma conta de armazenamento usando hello Azure Explorer Olá a seguir:

1. Em Olá **Azure Explorer** exibir, conta de armazenamento hello e, em seguida, selecione **excluir**.

   ![Menu Excluir Conta de Armazenamento][DS01]

2. Na janela de confirmação de saudação, clique em **Sim**.

   ![Janela de confirmação de Excluir conta de armazenamento][DS02]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre contas de armazenamento do Azure, tamanhos e preços, consulte Olá recursos a seguir:

* [Introdução tooMicrosoft armazenamento do Azure]
* [Sobre as contas de armazenamento do Azure]
* Tamanhos de conta de armazenamento do Azure
  * [Tamanhos das contas de armazenamento do Windows no Azure]
  * [Tamanhos das contas de armazenamento do Linux no Azure]
* Preços da conta de armazenamento do Azure
  * [Preços da conta de armazenamento do Windows]
  * [Preços da conta de armazenamento do Linux]

Para obter mais informações sobre kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [O que há de novo no hello Kit de ferramentas do Azure para Eclipse]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * [instruções entrar para Olá Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [O que há de novo no hello Azure Toolkit for IntelliJ]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [Instruções entrar para hello Azure Toolkit for IntelliJ]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]

Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instruções entrar para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções entrar para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Introdução tooMicrosoft armazenamento do Azure]: /azure/storage/storage-introduction
[Sobre as contas de armazenamento do Azure]: /azure/storage/storage-create-storage-account
[Replicação do Armazenamento do Azure]: /azure/storage/storage-redundancy
[Metas de desempenho e escalabilidade do Armazenamento do Azure]: /azure/storage/storage-scalability-targets
[Nomenclatura e referência de contêineres, blobs e metadados]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tamanhos das contas de armazenamento do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das contas de armazenamento do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços da conta de armazenamento do Windows]: /pricing/details/virtual-machines/windows/
[Preços da conta de armazenamento do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
