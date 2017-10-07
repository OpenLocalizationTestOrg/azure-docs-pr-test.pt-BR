---
title: "serviço com o Visual Studio e o IntelliTrace em nuvem aaaDebugging publicado um Azure | Microsoft Docs"
description: "Saiba como toodebug uma nuvem de serviço com o Visual Studio e o IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Depurando um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace
Com o IntelliTrace, você pode registrar em log informações extensas de depuração sobre uma instância de função quando ela é executada no Azure. Se você precisar toofind causa de saudação de um problema, você pode usar toostep de logs do IntelliTrace Olá pelo código do Visual Studio como se ele estivesse sendo executado no Azure. Em vigor, IntelliTrace registra código ambiente e da execução os dados quando o aplicativo do Azure está sendo executado como um serviço de nuvem no Azure e permite que você reproduza os dados de saudação registrado do Visual Studio. 

Você poderá usar o IntelliTrace se tiver o Visual Studio Enterprise instalado e seu aplicativo Azure se destinar ao .NET Framework 4 ou uma versão posterior. O IntelliTrace coleta informações sobre suas funções no Azure. máquinas virtuais de saudação para essas funções sempre executadas sistemas operacionais de 64 bits.

Como alternativa, você pode usar [depuração remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach diretamente tooa serviço de nuvem está em execução no Azure.

> [!IMPORTANT]
> O IntelliTrace destina-se apenas aos cenários de depuração e não deve ser usado para uma implantação de produção.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Configurar o IntelliTrace em um aplicativo do Azure
tooenable IntelliTrace para um aplicativo do Azure, você deve criar e publicar o aplicativo hello de um projeto do Azure do Visual Studio. Você deve configurar o IntelliTrace para seu aplicativo do Azure antes de publicá-lo tooAzure. Se você publicar seu aplicativo sem configurar o IntelliTrace, é necessário o projeto de saudação toorepublish. Para obter mais informações, consulte [Publicando projetos de serviços de nuvem do Azure usando o Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Quando estiver pronto toodeploy seu aplicativo do Azure, verifique se seus destinos de compilação do projeto são definidos muito**depurar**.

1. Em **Solution Explorer**, clique com botão direito e, no menu de contexto hello, selecione **publicar**.
   
1. Em Olá **publicar aplicativo do Azure** caixa de diálogo, selecione Olá assinatura do Azure e selecione **próximo**.

1. Em Olá **configurações** página, selecione Olá **configurações avançadas** guia.

1. Ativar Olá **habilitar IntelliTrace** opção toocollect os logs do IntelliTrace para seu aplicativo quando ele é publicado na nuvem de saudação.
   
1. toocustomize Olá IntelliTrace configuração básica, selecione **configurações** Avançar muito**habilitar IntelliTrace**.

    ![Link de configurações do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. Em Olá **configurações do IntelliTrace** caixa de diálogo, você pode especificar quais eventos toolog, se toocollect chamar informações, toocollect quais módulos e processos de logs para e gravação de toohello de tooallocate quanto espaço. Para saber mais sobre o IntelliTrace, consulte [Depurando com o IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Configurações do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

o log do IntelliTrace Olá é um arquivo de log circular de tamanho máximo de saudação especificado nas configurações do IntelliTrace hello (tamanho da saudação padrão é 250 MB). Os logs do IntelliTrace são coletados tooa arquivo no sistema de arquivos de saudação da máquina virtual de saudação. Quando você solicitar logs Olá, um instantâneo é obtido no momento e baixado o computador local tooyour.

Olá serviço de nuvem do Azure foi tooAzure publicado, você pode determinar se o IntelliTrace foi habilitado de saudação do Azure nó **Server Explorer**, conforme mostrado no Olá a imagem a seguir:

![Gerenciador de Servidores – IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Baixar logs do IntelliTrace de uma instância de função
Com o Visual Studio, é possível baixar os logs do IntelliTrace de uma instância de função seguindo estas etapas:

1. Em **Server Explorer**, expanda Olá **serviços de nuvem** nó e localize a instância de função cujos logs que você deseja toodownload. 

1. Instância de função hello e Olá s no menu de contexto, selecione **Exibir Logs do IntelliTrace**. 

    ![Opção de menu Exibir logs do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. os logs do IntelliTrace Olá são arquivo tooa baixado em um diretório no computador local. Cada vez que você solicitar os logs do IntelliTrace hello, um novo instantâneo é criado. Enquanto Olá logs estão sendo baixadas, Visual Studio exibe o andamento de saudação da operação de saudação em hello **o Log de atividades do Azure** janela. Conforme mostrado na figura a seguir de saudação, você pode expandir item de linha de saudação de saudação operação toosee mais detalhes.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Você pode continuar toowork no Visual Studio enquanto os logs do IntelliTrace Olá são baixadas. Quando o log de saudação download for concluído, ele é aberto no Visual Studio.

> [!NOTE]
> Olá logs do IntelliTrace podem conter as exceções framework hello gera e gerencia posteriormente. O código interno da estrutura gera essas exceções como uma parte normal de iniciar uma função, de modo que você pode ignorá-las com segurança.
> 
> 

## <a name="next-steps"></a>Próximas etapas
- [Opções de depuração dos serviços de nuvem do Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publicando um serviço de nuvem do Azure usando o Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)