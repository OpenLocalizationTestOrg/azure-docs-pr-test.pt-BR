---
title: aaaAzure lista de contas de armazenamento
description: "Gerenciar as configurações de conta de armazenamento usando Olá Kit de ferramentas do Azure para Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Lista de contas do Armazenamento do Azure
Habilitar contas de armazenamento do Azure baixar toobe locais usado para o seu JDK, servidor de aplicativos e componentes arbitrários, bem como para armazenar o estado ao usar o cache. O Eclipse mantém uma lista de contas de armazenamento conhecidas que são projetos tooyour disponíveis no seu espaço de trabalho do Eclipse. Olá tooopen **contas de armazenamento** caixa de diálogo, que é usado toomanage que listam no Eclipse, clique em **janela**, clique em **preferências**, expanda **Azure** e, em seguida, clique em **contas de armazenamento**.

Veja a seguir de Olá Olá **contas de armazenamento** caixa de diálogo.

![][ic719496]

Essa caixa de diálogo também pode ser aberta em uma **contas** em caixas de diálogo que usam contas de armazenamento, como a seguir Olá link:

* Olá **JDK** guia da saudação **configuração do servidor** caixa de diálogo.
* Olá **servidor** guia da saudação **configuração do servidor** caixa de diálogo.
* Olá **adicionar componente** caixa de diálogo.
* Olá **cache** caixa de diálogo Propriedades.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>tooimport contas de armazenamento usando um arquivo de configurações de publicação
1. Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em **importar do arquivo de configurações de publicação**.

2. (Ignore esta etapa se você já tiver salvo uma máquina local tooyour de arquivo publicar configurações). Em Olá **importar informações de assinatura** caixa de diálogo, clique em **baixar o arquivo de configurações de publicação**. Se você ainda não está conectados à sua conta do Azure, será solicitado toolog no. Em seguida, será solicitado que você toosave do Azure publica o arquivo de configurações. (Você pode ignorar Olá resultante instruções nas páginas de logon Olá - eles são fornecidos pelo Olá portal do Azure e são destinados a usuários do Visual Studio.) Salve-o computador local tooyour.

3. Ainda no hello **importar informações de assinatura** caixa de diálogo, clique em Olá **procurar** botão, selecione Olá Publicar arquivo de configurações que você salvou anteriormente e, em seguida, clique em **abrir**.

4. Clique em **Okey** tooclose Olá **importar informações de assinatura** caixa de diálogo.

## <a name="toocreate-a-new-storage-account"></a>toocreate uma nova conta de armazenamento
1. Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em **adicionar**.

2. Dentro de saudação **adicionar conta de armazenamento** caixa de diálogo, clique em **novo**.

3. Dentro de saudação **nova conta de armazenamento** caixa de diálogo, especifique valores para seguir hello:

   * Nome da conta de armazenamento.

   * Local da conta de armazenamento de saudação.

   * Descrição da conta de armazenamento de saudação.

   * conta de armazenamento Olá assinatura toowhich Olá pertence.

4. Clique em **Okey** tooclose Olá **nova conta de armazenamento** caixa de diálogo.

Ele pode levar vários minutos para que seu toobe de conta de armazenamento criada. Depois de criado, clique em **Okey** tooclose Olá **adicionar conta de armazenamento** caixa de diálogo e sua nova conta de armazenamento serão adicionado toohello lista de contas de armazenamento disponível.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd uma lista de toohello de conta de armazenamento existente
1. Se você ainda não tiver um armazenamento do Azure da conta, crie uma saudação etapas listadas na Olá **toocreate uma nova seção de conta de armazenamento** acima. (Como alternativa, você pode criar uma nova conta de armazenamento no hello [Portal de gerenciamento][Azure Management Portal].)

2. Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em **adicionar**.

3. Dentro de saudação **adicionar conta de armazenamento** caixa de diálogo, insira valores para **nome** e **chave de acesso**. chave de acesso e nome da conta de saudação deve ser uma conta de armazenamento do Azure existente. Saudação de uso **armazenamento** seção Olá [Portal de gerenciamento] [ Azure Management Portal] tooview nomes e as chaves de sua conta de armazenamento. O **adicionar conta de armazenamento** caixa de diálogo será a aparência a seguir toohello semelhante.
   
   ![][ic719497]

4. Clique em **Okey** tooclose Olá **adicionar conta de armazenamento** caixa de diálogo.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify uma conta de armazenamento toouse uma nova chave de acesso
1. Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em Olá conta de armazenamento que você deseja tooedit e, em seguida, clique em **editar**.

2. Dentro de saudação **Editar chave de acesso de conta de armazenamento** caixa de diálogo, modificar Olá **chave de acesso** valor.

3. Clique em **Okey** tooclose Olá **Editar chave de acesso de conta de armazenamento** caixa de diálogo.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove uma conta de armazenamento da saudação lista mantida no Eclipse
1. Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em Olá conta de armazenamento que você deseja tooedit e, em seguida, clique em **remover**.

2. Clique em **Okey** quando tooremove solicitada Olá conta de armazenamento.

> [!NOTE]
> Removendo Olá conta de armazenamento por meio de saudação **contas de armazenamento** diálogo apenas a remove da lista de saudação de contas de armazenamento podem ser visualizadas no Eclipse. Ele não remove o conta de armazenamento Olá sua assinatura do Azure. Além disso, o conta de armazenamento Olá pode aparecer novamente na sua lista, após o Eclipse recarregar os detalhes de saudação da sua assinatura.
> 
> 

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
