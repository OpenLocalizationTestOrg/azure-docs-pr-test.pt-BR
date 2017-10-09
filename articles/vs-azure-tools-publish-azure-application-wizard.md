---
title: "Olá aaaUsing Visual Studio Azure Assistente para publicar aplicativo | Microsoft Docs"
description: "Saiba como tooconfigure Olá várias configurações no Visual Studio Azure Assistente para publicar aplicativo do hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Usando o Visual Studio Azure Assistente para publicar aplicativo do hello
Depois de desenvolver um aplicativo web no Visual Studio, você pode publicar esse tooan aplicativo serviço de nuvem do Azure usando Olá **publicar aplicativo do Azure** assistente. 

> [!NOTE]
> Este tópico é sobre como implantar serviços toocloud, não tooweb sites. Para obter informações sobre como implantar sites tooweb, consulte [como tooDeploy um Site do Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Acessar o Assistente para publicar aplicativo do Azure de saudação

Você pode acessar o Assistente de publicar aplicativo do Azure de saudação de duas maneiras, dependendo do tipo de saudação do projeto do Visual Studio que você tem.

**Se você tiver um projeto de serviço de nuvem do Azure:**

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **publicar**.

**Se você tiver um projeto de aplicativo Web que não está habilitado para o Azure:**

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **converter** > **converter o projeto de serviço de nuvem do tooAzure**. 

1. Em **Solution Explorer**, projeto do Azure Olá recém-criado e, no menu de contexto hello, selecione **publicar**.

## <a name="sign-in-page"></a>Página de entrada

![Página de entrada](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Conta** - selecione uma conta ou selecione **adicionar uma conta** na lista de suspensa Olá conta.

**Escolha sua assinatura** -escolha Olá toouse de assinatura para sua implantação.
   
## <a name="settings-page---common-settings-tab"></a>Página Configurações - guia Configurações Comuns   

![Configurações Comuns](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Serviço de nuvem** -usando Olá suspensa, selecione uma nuvem existente de serviço ou selecione  **&lt;criar novo >**e criar um serviço de nuvem. Centro de dados de saudação é exibido entre parênteses para cada serviço de nuvem. É recomendável que Olá local do data center para hello serviço de nuvem ser Olá mesmo como o local do data center Olá Olá conta de armazenamento (configurações avançadas).  

**Ambiente** - selecione **Produção** ou **Preparo**. Escolha Olá ambiente de preparo, se você quiser toodeploy seu aplicativo em um ambiente de teste. 

**Configuração da compilação** - selecione **Depurar** ou **Liberar**.

**Configuração de serviço** - selecione **Nuvem** ou **Local**.
   
**Habilitar área de trabalho remota para todas as funções** -Verifique essa opção se quiser tooremotely de toobe capaz de conectar-se toohello serviço. Essa opção é usada principalmente para solução de problemas. Quando você selecionar essa caixa de seleção, Olá **configuração da área de trabalho remota** caixa de diálogo é exibida. Escolha Olá **configurações** configuração de saudação do link toochange.
   
**Habilitar a implantação da Web para todas as funções web** -Marque esta opção, a implantação de web tooenable para serviço de saudação. Você deve selecionar Olá **habilitar a área de trabalho remota para todas as funções** opção toouse esse recurso. Para saber mais, confira [[Publicação de um serviço de nuvem do Azure usando o Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Página Configurações — guia Configurações Avançadas

![Configurações avançadas](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Rótulo de implantação** -aceite o nome da saudação padrão ou insira um nome de sua escolha. tooappend Olá data toohello rótulo de implantação, deixe Olá caixa de seleção. 
   
**Conta de armazenamento** - selecione Olá toouse de conta de armazenamento para essa implantação, * *&lt;criar novo > toocreate uma conta de armazenamento. Centro de dados de saudação é exibido entre parênteses para cada conta de armazenamento. É recomendável que Olá local do data center para hello conta de armazenamento ser Olá mesmo como o local do data center Olá Olá serviço de nuvem (configurações comuns).  
   
Olá conta de armazenamento do Azure armazena pacote Olá Olá para implantação de aplicativo. Após a implantação do aplicativo hello, pacote de saudação é removido da conta de armazenamento de saudação.

**Excluir implantação em caso de falha** -Selecione esta opção toohave Olá implantação que excluído se houver erros durante a publicação. Isso deve ser desmarcado se você quiser toomaintain um endereço IP virtual constante para seu serviço de nuvem.

**Atualização de implantação** -Selecione esta opção se você quiser toodeploy somente os componentes atualizados. Esse tipo de implantação pode ser mais rápido do que uma implantação completa. Isso deve ser verificado se você quiser toomaintain um endereço IP virtual constante para seu serviço de nuvem. 

**Atualização - configurações de implantação** -esta caixa de diálogo é usada toofurther especificar como você deseja Olá funções toobe atualizado. Se você escolher **atualização Incremental**, cada instância do aplicativo é atualizada após o outro, para que esse aplicativo hello sempre esteja disponível. Se você escolher **atualização simultânea**, todas as instâncias do aplicativo são atualizadas no hello simultaneamente. Atualização simultânea é mais rápido, mas o serviço pode não estar disponível durante o processo de atualização de saudação. 

![Configurações de implantação](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Habilitar o IntelliTrace** -Especifique se deseja tooenable IntelliTrace. Com o IntelliTrace, você pode registrar em log informações extensas de depuração sobre uma instância de função quando ela é executada no Azure. Se você precisar toofind causa de saudação de um problema, você pode usar toostep de logs do IntelliTrace Olá pelo código do Visual Studio como se ele estivesse sendo executado no Azure. Para saber mais sobre como usar o IntelliTrace, confira [Depuração de um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Habilitar a criação de perfil** -Especifique se deseja que o perfil de desempenho de tooenable. o criador de perfil do Hello Visual Studio permite tooget uma análise detalhada dos aspectos computacionais de saudação do funcionamento do seu serviço de nuvem. Para obter mais informações sobre como usar o criador de perfil do hello Visual Studio, consulte [testar o desempenho de saudação de um serviço de nuvem do Azure](./vs-azure-tools-performance-profiling-cloud-services.md).

**Habilitar o depurador remoto para todas as funções** -Especifique se deseja tooenable a depuração remota. Para saber mais sobre como depurar os serviços de nuvem usando o Visual Studio, confira [Depuração de um serviço de nuvem ou máquina virtual do Azure no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Página Configurações de Diagnóstico

![Configurações de diagnóstico](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

O diagnóstico permite tootroubleshoot um serviço de nuvem do Azure (ou máquina virtual do Azure). Para saber mais sobre diagnósticos, confira [Configuração do Diagnóstico para os Serviço de Nuvem e as Máquinas Virtuais do Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Para saber mais sobre o Application Insights, confira [O que é o Application Insights?](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Página Resumo

![Resumo](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Perfil de destino** -você pode escolher um perfil de publicação de toocreate Olá das configurações de que você escolheu. Por exemplo, você pode criar um perfil para um ambiente de teste e outro para produção. toosave este perfil, escolha Olá **salvar** ícone. Assistente de saudação cria o perfil de saudação e salva-o no projeto do Visual Studio hello. nome do perfil toomodify hello, abra Olá **perfil de destino** lista e, em seguida, escolha **< Gerenciar … >**.
   
   > [!NOTE]
   > perfil de publicação Olá aparece no Gerenciador de soluções do Visual Studio, e as configurações de perfil de saudação são gravadas tooa arquivo com uma extensão. azurePubxml. As configurações são salvas como atributos de marcas XML.
   > 
   > 

## <a name="publishing-your-application"></a>Publicação do aplicativo

Depois de definir todas as configurações de saudação para implantação do projeto, selecione **publicar** na parte inferior da saudação da caixa de diálogo de saudação. Você pode monitorar o status do processo de saudação em Olá **saída** janela no Visual Studio.

## <a name="next-steps"></a>Próximas etapas
- [Migrar e publicar um aplicativo Web de tooan serviço de nuvem do Azure do Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Saiba como o serviço de nuvem toouse Visual Studio toopublish do Azure](./vs-azure-tools-publishing-a-cloud-service.md)
- [Depuração de um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Testar o desempenho de saudação de um serviço de nuvem do Azure](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Configuração do Diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). 
- [O que é o Application Insights?](./application-insights/app-insights-overview.md)