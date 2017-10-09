---
title: "aaaManage recursos de armazenamento de BLOBs do Azure com o Gerenciador de armazenamento (visualização) | Microsoft Docs"
description: "Gerenciar os contêineres de blob e blobs do Azure com o Gerenciador de Armazenamento (Preview)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Gerenciar os recursos de Armazenamento de Blobs do Azure com o Gerenciador de Armazenamento (Preview)
## <a name="overview"></a>Visão geral
[Armazenamento de BLOBs do Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.
Você pode usar dados de tooexpose de armazenamento de Blob publicamente toohello mundo ou toostore dados de aplicativo em particular. Neste artigo, você aprenderá como toouse toowork de Gerenciador de armazenamento (visualização) com os contêineres de blob e blobs.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete Olá etapas neste artigo, você precisará seguir hello:

* [Baixe e instale o Gerenciador de Armazenamento (preview)](http://www.storageexplorer.com)
* [Conecte-se a conta de armazenamento do Azure tooa ou serviço](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Criar um contêiner de blob
Todos os blobs devem residir em um contêiner de blob, que é simplesmente um agrupamento lógico de blobs. Uma conta pode conter um número ilimitado de contêineres, e cada contêiner pode armazenar um número ilimitado de blobs.

Olá etapas a seguir ilustram como toocreate um contêiner de blob no Gerenciador de armazenamento (visualização).

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda conta de armazenamento hello dentro da qual você deseja que o contêiner de blob toocreate hello.
3. Clique com botão direito **contêineres de Blob**e - no menu de contexto Olá - selecione **criar contêiner de Blob**.

   ![Menu de contexto Criar contêineres de blob][0]
4. Será exibida uma caixa de texto abaixo Olá **contêineres de Blob** pasta. Insira o nome de saudação para seu contêiner de blob. Consulte Olá [as regras de nomenclatura do contêiner](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) seção para obter uma lista de regras e restrições de nomenclatura de contêineres de blob.

   ![Caixa de texto Criar Contêineres de Blob][1]
5. Pressione **Enter** quando terminar de contêiner de blob do toocreate hello, ou **Esc** toocancel. Depois que o contêiner de blob Olá foi criado com êxito, ele será exibido em Olá **contêineres de Blob** pasta para Olá selecionada a conta de armazenamento.

   ![Contêiner de blob criado][2]

## <a name="view-a-blob-containers-contents"></a>Exibir o conteúdo de um contêiner de blobs
Os contêineres de blob contêm blobs e pastas (que também podem conter blobs).

Olá etapas a seguir ilustram como conteúdo de saudação do tooview de um contêiner de blob no Gerenciador de armazenamento (visualização):

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar tooview.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Contêiner de blob de saudação do botão direito do mouse seu gosto tooview e - no menu de contexto Olá - selecione **abrir Editor de contêiner de Blob**.
   Você também pode clicar duas vezes desejar tooview de contêiner de blob hello.

   ![Menu de contexto Abrir editor do contêiner de blobs][19]
5. painel principal Olá exibirá o conteúdo do contêiner de blob hello.

   ![Editor do Contêiner de blobs][3]

## <a name="delete-a-blob-container"></a>Excluir um contêiner de blob
Os contêineres de blob podem ser facilmente criados e excluídos conforme o necessário. (toosee como blobs toodelete individuais, consulte a seção toohello, [Gerenciando blobs em um contêiner de blob](#managing-blobs-in-a-blob-container).)

Olá etapas a seguir ilustram como toodelete um contêiner de blob no Gerenciador de armazenamento (visualização):

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar tooview.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Contêiner de blob de saudação do botão direito do mouse seu gosto toodelete e - no menu de contexto Olá - selecione **excluir**.
   Você também pode pressionar **excluir** contêiner de blob atualmente selecionado Olá toodelete.

   ![Menu de contexto Excluir contêiner de blobs][4]
5. Selecione **Sim** toohello caixa de diálogo de confirmação.

   ![Confirmação de exclusão do contêiner de blobs][5]

## <a name="copy-a-blob-container"></a>Copiar um contêiner de blobs
O Gerenciador de armazenamento (visualização) permite que você toocopy uma área de transferência de toohello de contêiner de blob e cole que o contêiner de blob em outra conta de armazenamento. (toosee como blobs toocopy individuais, consulte a seção toohello, [Gerenciando blobs em um contêiner de blob](#managing-blobs-in-a-blob-container).)

Olá, as etapas a seguir ilustra como toocopy um contêiner de blob do armazenamento de uma conta tooanother.

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar toocopy.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Contêiner de blob de saudação do botão direito do mouse seu gosto toocopy e - no menu de contexto Olá - selecione **contêiner de Blob de cópia**.

   ![Menu de contexto Copiar contêiner de blobs][6]
5. Clique em destino"hello desejado" conta de armazenamento no qual você deseja contêiner de blob toopaste Olá e - no menu de contexto Olá - selecione **contêiner de Blob de colar**.

   ![Menu de contexto Colar contêiner de blobs][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Obter Olá SAS para um contêiner de blob
Um [assinatura de acesso compartilhado (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornece acesso delegado tooresources na sua conta de armazenamento.
Isso significa que você pode conceder a que um cliente limitada tooobjects permissões na conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem a necessidade de compartilhar as chaves de acesso da conta.

Olá etapas a seguir ilustram como toocreate um SAS para um contêiner de blob:

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda a conta de armazenamento Olá que contém o contêiner de blob Olá para o qual você deseja tooget uma SAS.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Contêiner de BLOBs desejado hello e - no menu de contexto Olá - selecione **obter assinatura de acesso compartilhado**.

   ![Menu de contexto Obter SAS][8]
5. Em Olá **assinatura de acesso compartilhado** caixa de diálogo, especifique política hello, datas de início e vencimento, fuso horário e você deseja para o recurso de saudação de níveis de acesso.

   ![Opções de Obter SAS][9]
6. Quando tiver terminado de especificar opções de SAS hello, selecione **criar**.
7. Um segundo **assinatura de acesso compartilhado** caixa de diálogo, em seguida, exibirá que listas Olá contêiner de blob juntamente com a URL de saudação e QueryStrings que você pode usar tooaccess Olá recurso de armazenamento.
   Selecione **cópia** próximo URL toohello desejar toocopy toohello da área de transferência.

   ![Copiar URLs de SAS][10]
8. Ao terminar, escolha **Fechar**.

## <a name="manage-access-policies-for-a-blob-container"></a>Gerenciar políticas de acesso para um contêiner de blobs
Olá etapas a seguir ilustram como toomanage (Adicionar e remover) políticas de acesso para um contêiner de blob:

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda que contém o contêiner de blob Olá cujas desejar toomanage as políticas de acesso de conta de armazenamento hello.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Selecione o contêiner de BLOBs desejado hello e - no menu de contexto Olá - selecione **gerenciar políticas de acesso**.

   ![Menu de contexto Gerenciar políticas de acesso][11]
5. Olá **políticas de acesso** diálogo listará todas as políticas de acesso já foi criadas para o contêiner de BLOBs selecionados hello.

   ![Opções de Política de Acesso][12]        
6. Siga estas etapas, dependendo da tarefa de gerenciamento de política de acesso de saudação:

   * **Adicionar uma nova política de acesso** — escolha **Adicionar**. Uma vez gerado, Olá **políticas de acesso** caixa de diálogo exibirá Olá recém-adicionado acessar política (com configurações padrão).
   * **Editar uma política de acesso** — faça as edições desejadas e escolha **Salvar**.
   * **Remover uma política de acesso** - selecione **remover** próximo toohello de política de acesso você deseja tooremove.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Saudação de conjunto de nível de acesso público para um contêiner de blob
Por padrão, cada contêiner de blob está definido muito "Nenhum acesso público".

Olá etapas a seguir ilustram como toospecify um público acesso nível para um contêiner de blob.

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda que contém o contêiner de blob Olá cujas desejar toomanage as políticas de acesso de conta de armazenamento hello.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Selecione o contêiner de BLOBs desejado hello e - no menu de contexto Olá - selecione **definir o nível de acesso público**.

   ![Menu de contexto Definir nível de acesso público][13]
5. Em Olá **definir o nível de acesso público de contêiner** caixa de diálogo, especifique o nível de acesso de saudação desejada.

   ![Opções de Definir nível de acesso público][14]
6. Escolha **Aplicar**.

## <a name="managing-blobs-in-a-blob-container"></a>Gerenciamento de blobs em um contêiner de blobs
Depois de criar um contêiner de blob, você pode carregar um contêiner de blob do blob toothat, fazer o download de um computador local do blob tooyour, abrir um blob em seu computador local e muito mais.

Olá, as etapas a seguir ilustra como toomanage Olá blobs (e pastas) em um contêiner de blob.

1. Abra o Gerenciador de Armazenamento (Preview).
2. No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar toomanage.
3. Expanda a conta de armazenamento Olá **contêineres de Blob**.
4. Clique duas vezes no contêiner de blob Olá desejar tooview.
5. painel principal Olá exibirá o conteúdo do contêiner de blob hello.

   ![Exibir contêiner de blobs][3]
6. painel principal Olá exibirá o conteúdo do contêiner de blob hello.
7. Siga estas que etapas, dependendo da tarefa Olá desejar tooperform:

   * **Carregar o contêiner de blob tooa arquivos**

     1. Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar arquivos** do menu suspenso de saudação.

        ![Menu Carregar arquivos][15]
     2. Em Olá **carregar arquivos** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **arquivos** tooselect Olá arquivos desejar tooupload da caixa de texto.

        ![Opções de Carregar arquivos][16]
     3. Especificar o tipo de saudação do **Blob tipo**. artigo Olá [Introdução ao armazenamento de BLOBs do Azure usando o .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica as diferenças de saudação entre hello vários tipos de blob.
     4. Opcionalmente, especifique uma pasta de destino na qual arquivos selecionados hello serão carregados. Se a pasta de destino de saudação não existir, ele será criado.
     5. Escolha **Carregar**.
   * **Carregar um contêiner de blob de tooa de pasta**

     1. Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** do menu suspenso de saudação.

        ![Menu Carregar pasta][17]
     2. Em Olá **pasta carregamento** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **pasta** pasta de saudação de tooselect de caixa de texto cujo conteúdo você deseja tooupload.

        ![Opções de Carregar pasta][18]
     3. Especificar o tipo de saudação do **Blob tipo**. artigo Olá [Introdução ao armazenamento de BLOBs do Azure usando o .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica as diferenças de saudação entre hello vários tipos de blob.
     4. Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionada será carregado. Se a pasta de destino de saudação não existir, ele será criado.
     5. Escolha **Carregar**.
   * **Fazer o download de um computador local do blob tooyour**

     1. Selecione blob Olá desejar toodownload.
     2. Na barra de ferramentas do painel Olá principal, selecione **baixar**.
     3. Em Olá **especifique onde toosave Olá baixou blob** caixa de diálogo, especifique Olá local onde você deseja que o blob Olá baixado e Olá nome você deseja toogive-lo.  
     4. Selecione **Salvar**.
   * **Abrir um blob em seu computador local**

     1. Selecione blob Olá desejar tooopen.
     2. Na barra de ferramentas do painel Olá principal, selecione **abrir**.
     3. blob Olá será baixado e aberto usando o aplicativo hello associado com o tipo subjacente de arquivo do blob hello.
   * **Copiar uma área de transferência do blob toohello**

     1. Selecione blob Olá desejar toocopy.
     2. Na barra de ferramentas do painel Olá principal, selecione **cópia**.
     3. No painel esquerdo do hello, navegar tooanother contêiner de blob e clique duas vezes nele tooview-lo no painel principal hello.
     4. Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia de blob de saudação.
   * **Excluir um blob**

     1. Selecione blob Olá desejar toodelete.
     2. Na barra de ferramentas do painel Olá principal, selecione **excluir**.
     3. Selecione **Sim** toohello caixa de diálogo de confirmação.

## <a name="next-steps"></a>Próximas etapas
* Saudação de exibição [notas de versão do Gerenciador de armazenamento (visualização) e vídeos mais recentes](http://www.storageexplorer.com).
* Saiba como muito[criar aplicativos usando blobs do Azure, tabelas, filas e arquivos](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
