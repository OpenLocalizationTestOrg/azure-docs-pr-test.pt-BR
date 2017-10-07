---
title: "aaaSync conteúdo de uma pasta de nuvem tooAzure do serviço de aplicativo"
description: "Saiba como toodeploy seu tooAzure de aplicativo do serviço de aplicativo por meio do conteúdo de sincronização de uma pasta de nuvem."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Sincronizar o conteúdo de uma pasta de nuvem tooAzure do serviço de aplicativo
Este tutorial mostra como toodeploy muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) por sincronizando o conteúdo dos serviços de armazenamento de nuvem populares como o Dropbox e OneDrive. 

## <a name="overview"></a>Visão geral da implantação de sincronização de conteúdo
implantação de sincronização de conteúdo sob demanda de saudação é alimentada por Olá [mecanismo de implantação Kudu](https://github.com/projectkudu/kudu/wiki) integrado com o serviço de aplicativo. Em Olá [Portal do Azure](https://portal.azure.com), você pode designar uma pasta no seu armazenamento em nuvem, com o código do aplicativo e o conteúdo na pasta de trabalho e sincronização tooApp serviço com hello clique de um botão. Sincronização de conteúdo utiliza o processo de Kudu Olá para compilação e implantação. 

## <a name="contentsync"></a>Como o conteúdo de tooenable sincronizar implantação
sincronização de conteúdo de tooenable de saudação [Portal do Azure](https://portal.azure.com), siga estas etapas:

1. Na folha do seu aplicativo em Olá Portal do Azure, clique em **configurações** > **origem de implantação**. Clique em **Escolher fonte**, em seguida, selecione **OneDrive** ou **Dropbox** como origem Olá para implantação. 
   
    ![Sincronização de conteúdo](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Devido a diferenças subjacentes no hello APIs, **OneDrive para empresas** não tem suporte no momento. 
   > 
   > 
2. Tooenable de fluxo de trabalho de autorização Olá completa tooaccess do serviço de aplicativo um determinado pré-definidas caminho designado para OneDrive ou Dropbox onde todo o conteúdo do serviço de aplicativo serão armazenados.  
    Após a saudação de autorização plataforma do serviço de aplicativo dará a você Olá opção toocreate uma pasta de conteúdo em hello designada caminho de conteúdo ou toochoose uma pasta de conteúdo existente nesse caminho de conteúdo designado. caminhos de conteúdo Olá designado em suas contas de armazenamento de nuvem usados para sincronização do serviço de aplicativo são seguinte hello:  
   
   * **OneDrive**: `Apps\Azure Web Apps` 
   * **Dropbox**: `Dropbox\Apps\Azure`
3. Depois de saudação sincronização de conteúdo de saudação inicial de sincronização de conteúdo pode ser iniciada sob demanda de saudação portal do Azure. Histórico de implantação está disponível com hello **implantações** folha.
   
    ![Histórico de implantação](./media/app-service-deploy-content-sync/onedrive_sync.png)

Mais informações para a implantação do Dropbox estão disponíveis em [Implantar por meio do Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

