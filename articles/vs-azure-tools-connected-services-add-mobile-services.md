---
title: "aaaAdding serviços móveis usando os serviços conectados no Visual Studio | Microsoft Docs"
description: "Adicionar serviços móveis usando a caixa de diálogo do Visual Studio adicionar conectado serviços Olá"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Adicionando Serviços Móveis usando os serviços conectados do Visual Studio
Com o Visual Studio 2015, você pode se conectar a serviços móveis de tooAzure usando Olá **Adicionar serviço conectado** caixa de diálogo. É possível se conectar de qualquer aplicativo cliente C#, qualquer aplicativo JavaScript ou aplicativo Cordova entre plataformas. Uma vez conectado, você criar e acessar dados, criar APIs personalizadas e trabalhos agendados, ou adicionar suporte para notificações por push.  Olá serviços conectados operação adiciona todas as referências apropriadas e código de conexão. Você também pode aproveitar o suporte interno para autenticação com uma variedade de esquemas conhecidos de identidade, como o AD do Azure, Facebook, Twitter e Contas da Microsoft.

## <a name="supported-project-types"></a>Tipos de projeto com suporte
> [!NOTE]
> No Visual Studio 2015, a adição de projetos universais do Windows (Windows 10) de tooa de serviços móveis do Azure usando a caixa de diálogo de adicionar serviços conectados Olá não é suportada. Você pode adicionar serviços móveis do Azure instalando Olá pacotes apropriado usando Olá NuGet Package Manager do seu projeto.
> 
> 

Você pode usar o hello serviços conectados diálogo tooconnect tooAzure serviços móveis em Olá seguintes tipos de projeto.

* Projetos de aplicativo Windows 8.1 Store, Phone e Universal para .NET
* Projetos de aplicativo Windows 8.1 Store, Phone e Universal para JavaScript
* Projetos criados usando o Visual Studio Tools para Apache Cordova

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Conectar tooAzure Mobile Services usando a caixa de diálogo Olá adicionar serviços conectados
1. Verifique se você tem uma conta do Azure. Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Olá abrir **adicionar serviços conectados** caixa de diálogo.
   
   * Para aplicativos .NET, abra seu projeto no Visual Studio, o menu de contexto de saudação aberto para Olá **referências** nó no Gerenciador de soluções e, em seguida, escolha **Adicionar serviço conectado**
     
        ![Conectando tooAzure serviço móvel](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Para projetos de aplicativo do Apache Cordova, abra seu projeto no Visual Studio, o menu de contexto Olá aberta para o nó do projeto Olá no Gerenciador de soluções e, em seguida, escolha **Adicionar serviço conectado**.
3. Em Olá **Adicionar serviço conectado** caixa de diálogo caixa, escolha **serviços móveis do Azure**e, em seguida, escolha Olá **configurar** botão. Se você ainda não fez isso, é possível toolog solicitada no Azure.
   
    ![Adicionando um Serviço Móvel do Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Em Olá **serviços móveis do Azure** caixa de diálogo caixa, escolha um serviço móvel existente, se você tiver um. Se você precisar toocreate um novo serviço móvel do Azure, siga o procedimento de saudação abaixo toodo assim. Caso contrário, pule toohello próxima etapa.
   
    toocreate uma nova conta de serviço móvel:
   
   1. Escolha hello * * criar serviço * * o link na parte inferior de Olá Olá da caixa de diálogo.
       ![Adicionar novo serviço conectado móvel](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Em Olá **criar serviço móvel** caixa de diálogo, você pode escolher um serviço móvel de back-end JavaScript, ou um serviço móvel de back-end do .NET do hello **tempo de execução** lista suspensa. 
      
       ![Criando um serviço móvel](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Um serviço de back-end JavaScript é simples e eficiente. Se você criar um serviço móvel de back-end JavaScript, código de JavaScript do lado do servidor de saudação é armazenado na nuvem hello, mas você pode editar scripts de servidor usando o Gerenciador de servidores ou o portal de gerenciamento do Azure hello. 
      
       Um serviço móvel de back-end .NET fornece Olá total poder e flexibilidade de API da Web e o Entity Framework. Se você criar um serviço móvel de back-end .NET, um projeto é criado e adicionado tooyour solução. 
   3. Escolha Olá **região** onde serviço móvel hello e, em seguida, insira um nome de usuário e senha para o servidor de saudação.
   4. Depois de inserir todas as informações necessárias de saudação, escolha Olá **criar** botão serviço móvel de saudação toocreate.
   5. novo serviço móvel de saudação deve aparecer na lista de serviço Olá em Olá **serviços móveis do Azure** caixa de diálogo. Escolha o novo serviço móvel de saudação na lista de saudação e Olá **adicionar** projeto tooyour do botão tooadd Olá service.
5. Revisão Olá Introdução página que aparece e descubra como seu projeto foi modificado. Uma página de introdução aparece no navegador sempre que você adiciona um serviço conectado. Você pode examinar Olá próximas etapas sugeridas e exemplos de código ou alternar toohello toosee de página o que aconteceu quais referências foram adicionadas tooyour projeto e como os arquivos de código e configuração foram modificados.
6. Usando os exemplos de código hello como guia, comece a escrever código tooaccess seu serviço móvel!

## <a name="how-your-project-is-modified"></a>Como o projeto é modificado
Como o Visual Studio modifica seu projeto depende do tipo de projeto de saudação. Para aplicativos cliente C#, consulte [O que aconteceu — projetos C#](http://go.microsoft.com/fwlink/p/?LinkId=513119). Para aplicativos cliente JavaScript, consulte [O que aconteceu — projetos JavaScript](http://go.microsoft.com/fwlink/p/?LinkId=513120). Para aplicativos Cordova, consulte [O que aconteceu — projetos Cordova](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Próximas etapas
Faça perguntas e obtenha ajuda: 

* [Fórum do MSDN: Serviços Móveis do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Serviços móveis do Azure no Blog da equipe do Microsoft Azure da saudação](https://azure.microsoft.com/blog/topics/mobile/)
* [Serviços Móveis do Azure em azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentação dos Serviços Móveis do Azure em azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

