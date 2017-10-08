---
title: "aaaSign em instruções de saudação Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toosign no Microsoft Azure usando Olá Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Entrada do Azure em instruções para Olá Kit de ferramentas do Azure para Eclipse

Olá Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:

  * **Interativo** – quando você estiver usando esse método, você inserirá suas credenciais do Azure sempre que entrar na conta do Azure.
  * **Automatizada** - quando você estiver usando esse método, você criará um arquivo de credenciais que contém seus dados de entidade de serviço, após o qual você pode usar o hello credenciais arquivo tooautomatically logon em sua conta do Azure.

Olá etapas Olá seções a seguir descrevem como toouse cada método.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Entrar em sua conta do Azure interativamente

Olá etapas a seguir ilustrará como toosign no Azure inserindo manualmente suas credenciais do Azure.

1. Abra seu projeto com o Eclipse.

1. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.

   ![Menu do Eclipse para Entrar no Azure][I01]

1. Olá quando **Azure entrar** caixa de diálogo é exibida, selecione **interativo**e, em seguida, clique em **entrar**.

   ![Caixa de diálogo Entrar][I02]

1. Olá quando **Log no Azure** caixa de diálogo for exibida, insira suas credenciais do Azure e, em seguida, clique em **entrar**.

   ![Caixa de Diálogo de Logon do Azure][I03]

1. Olá quando **selecione assinaturas** caixa de diálogo for exibida, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.

   ![Caixa de diálogo Selecionar Assinaturas][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Sair de sua conta do Azure quando você entrou no modo interativo

Depois que você configurou etapas Olá na seção anterior Olá, você será conectado automaticamente sua conta do Azure cada vez que você reinicie o Eclipse. No entanto, se você quiser toosign fora da sua conta do Azure sem reiniciar o Eclipse, use Olá etapas a seguir.

1. No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.

   ![Menu do Eclipse para saída do Azure][L01]

1. Olá quando **Azure sair** caixa de diálogo for exibida, clique em **Sim**.

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Entrar em sua conta do Azure automaticamente e criar credenciais de um arquivo toouse no hello futuras

Olá seguinte irá orientá-lo na criação de um arquivo de credenciais que contém seus dados de entidade de serviço. Depois de concluir essas etapas, será Eclipse automaticamente o logon use Olá credenciais arquivo tooautomatically que você no Azure cada vez que você abra seu projeto.

1. Abra seu projeto com o Eclipse.

1. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.

   ![Menu do Eclipse para Entrar no Azure][A01]

1. Olá quando **Azure entrar** caixa de diálogo é exibida, selecione **automatizada**e, em seguida, clique em **novo**.

   ![Caixa de diálogo Entrar][A02]

1. Olá quando **Log no Azure** caixa de diálogo for exibida, insira suas credenciais do Azure e, em seguida, clique em **entrar**.

   ![Caixa de Diálogo de Logon do Azure][A03]

1. Olá quando **criar arquivos de autenticação** caixa de diálogo for exibida, assinaturas de saudação selecione deseja toouse, escolha o diretório de destino e, em seguida, clique em **iniciar**.

   ![Caixa de Diálogo de Logon do Azure][A04]

1. Olá **Status de criação da entidade de serviço** caixa de diálogo será exibida e depois que os arquivos foram criados com êxito, clique em **Okey**.

   ![Caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. Olá quando **Azure entrar** caixa de diálogo for exibida, clique em **entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

1. Olá quando **selecione assinaturas** caixa de diálogo for exibida, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Sair de sua conta do Azure quando você entrou automaticamente

Depois que você configurou etapas Olá na seção anterior Olá, Olá Kit de ferramentas do Azure você entrará automaticamente em sua conta do Azure cada vez que você reinicie o Eclipse. No entanto, toosign fora da sua conta do Azure e impedir que o hello Kit de ferramentas do Azure você entrar automaticamente, Olá use as etapas a seguir.

1. No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.

   ![Menu do Eclipse para saída do Azure][L01]

1. Olá quando **Azure sair** caixa de diálogo for exibida, clique em **Sim**.

   ![Caixa de diálogo Saída do Azure][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Entre automaticamente em sua conta do Azure usando um arquivo de credenciais que você já criou

Se você sair do Azure quando você estiver usando o Eclipse, você precisará Olá tooreconfigure Kit de ferramentas do Azure para Eclipse toouse um arquivo de credenciais que tiver criado antes que você pode entrar automaticamente em sua conta do Azure. Olá etapas a seguir orientará você pela configuração Olá Kit de ferramentas do Azure toouse um arquivo existente de credenciais.

1. Abra seu projeto com o Eclipse.

1. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.

   ![Menu do Eclipse para Entrar no Azure][A01]

1. Olá quando **Azure entrar** caixa de diálogo é exibida, selecione **automatizada**e, em seguida, clique em **procurar**.

   ![Caixa de diálogo Entrar][A02]

1. Olá quando **Selecionar arquivo autenticado** caixa de diálogo for exibida, selecione um arquivo de credenciais que você criou anteriormente e, em seguida, clique em **selecione**.

   ![Caixa de diálogo Entrar][A08]

1. Olá quando **Azure entrar** caixa de diálogo for exibida, clique em **entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

1. Olá quando **selecione assinaturas** caixa de diálogo for exibida, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Novidades no Kit de ferramentas do Azure para Eclipse de saudação]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * *Entrada em instruções Olá Kit de ferramentas do Azure para Eclipse (Este artigo)*
  * [Criar um aplicativo Web Hello World para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [Entrada em instruções hello Azure Toolkit for IntelliJ]
  * [Criar um aplicativo Web Hello World para o Azure no IntelliJ]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Entrada em instruções hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
