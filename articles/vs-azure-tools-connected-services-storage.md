---
title: "aaaAdd de armazenamento do Azure usando os serviços conectados no Visual Studio | Microsoft Docs"
description: "Adicionar o aplicativo de tooyour de armazenamento do Azure usando a caixa de diálogo do Visual Studio adicionar conectado serviços Olá"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Adicionando armazenamento do Azure usando os serviços conectados do Visual Studio
Com o Visual Studio, você pode conectar qualquer Olá tooAzure armazenamento a seguir usando Olá **adicionar serviços conectados** caixa de diálogo:

- Serviço de nuvem do C#
- Serviço móvel de back-end .NET
- Site ou serviço ASP.NET
- Principais serviços ASP.NET
- Serviço do Trabalho Web do Azure 

Olá serviço conectado funcionalidade adiciona todas as referências de saudação necessário e projeto de tooyour de código de conexão e modifica os arquivos de configuração adequadamente. 

Após a conclusão, Olá **adicionar serviços conectados** caixa de diálogo exibe automaticamente documentação detalhando Olá etapas necessárias toostart, trabalhando com o armazenamento de BLOBs, filas e tabelas.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>Conecte-se tooAzure armazenamento usando os serviços conectados Olá caixa de diálogo
1. Abra o projeto no Visual Studio

1. Em **Gerenciador de soluções**, Olá atalho **serviços conectados** nó e, no menu de contexto hello e selecione **Adicionar serviço conectado**.
   
    ![Adicionar serviço conectado do Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. Em Olá **serviços conectados** página, selecione **armazenamento em nuvem com o armazenamento do Azure**.
   
    ![Adicionar Armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. Em Olá **armazenamento do Azure** caixa de diálogo, selecione uma conta de armazenamento existente e selecione **adicionar**.
   
    Se você precisar toocreate uma conta de armazenamento, vá toohello próxima etapa. Caso contrário, pule toostep 6.
    
    ![Adicionar tooproject de conta de armazenamento existente](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate uma conta de armazenamento: 
   
   1. Selecione **criar uma nova conta de armazenamento** na parte inferior da saudação da caixa de diálogo de saudação.

   1. Preencha Olá **criar conta de armazenamento** caixa de diálogo e selecione **criar**.
      
       ![Nova conta de armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Olá quando **armazenamento do Azure** caixa de diálogo é exibida, a nova conta de armazenamento Olá aparece na lista de saudação. Selecione a nova conta de armazenamento Olá na lista de saudação e selecione **adicionar**.

1. Olá armazenamento serviço conectado aparece sob Olá **referências de serviço** nó do projeto.
   
## <a name="how-your-project-is-modified"></a>Como o projeto é modificado
Quando você terminar de caixa de diálogo Olá, o Visual Studio adiciona referências e modifica alguns arquivos de configuração. alterações específicas Olá dependem do tipo de projeto hello: 

- Projeto ASP.NET — [O que aconteceu — projetos ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Projeto de Núcleo ASP.NET — [O que aconteceu — projetos ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Projeto de serviço de nuvem (funções Web e funções de trabalho) — [O que aconteceu — projetos Serviço de Nuvem](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Projetos de Trabalho Web — [O que aconteceu — projetos de Trabalho Web](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Próximas etapas
- [Fórum do MSDN: Armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog da equipe do Armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentação do Armazenamento do Azure](https://docs.microsoft.com/azure/storage/)
