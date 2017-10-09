---
title: "aaaUsing Gerenciador de armazenamento (visualização) com o armazenamento de arquivo do Azure | Microsoft Docs"
description: "Saiba como aprender como toouse toowork de Gerenciador de armazenamento (visualização) com o arquivo de compartilhamentos e arquivos."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Usando o Gerenciador de Armazenamento (Visualização) com o Armazenamento de Arquivos do Azure

Arquivo do Azure, o armazenamento é um serviço que oferece arquivo compartilha Olá nuvem usando Olá protocolo padrão do bloco de mensagens de servidor (SMB). Há suporte ao SMB 2.1 e ao 3.0 SMB. Com o armazenamento de arquivo do Azure, você pode migrar aplicativos herdados que dependem de tooAzure de compartilhamentos de arquivo rapidamente e sem regravações caras. Você pode usar dados do arquivo armazenamento tooexpose publicamente toohello mundo ou toostore dados de aplicativo em particular. Neste artigo, você aprenderá como toouse toowork de Gerenciador de armazenamento (visualização) com o arquivo de compartilhamentos e arquivos.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete Olá etapas neste artigo, você precisará seguir hello:

- [Baixe e instale o Gerenciador de Armazenamento (preview)](http://www.storageexplorer.com/)

- [Conecte-se a conta de armazenamento do Azure tooa ou serviço](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Criar um compartilhamento de arquivos

Todos os arquivos devem residir em um compartilhamento de arquivos, que é simplesmente um agrupamento lógico de arquivos. Uma conta pode conter um número ilimitado de compartilhamentos de arquivo, e cada compartilhamento pode armazenar um número ilimitado de arquivos.

Olá, as etapas a seguir ilustra como toocreate um compartilhamento de arquivo no Gerenciador de armazenamento (visualização).

1. Abra o Gerenciador de Armazenamento (Preview).

2. No painel esquerdo do hello, expanda a conta de armazenamento hello dentro da qual você deseja toocreate Olá compartilhamento de arquivos

3. Clique com botão direito **compartilhamentos de arquivos**e - no menu de contexto Olá - selecione **criar compartilhamento de arquivos**.

    ![Criar o compartilhamento de arquivos](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Será exibida uma caixa de texto abaixo Olá **compartilhamentos de arquivos** pasta. Insira o nome de saudação para o compartilhamento de arquivos. Consulte Olá [compartilhar as regras de nomenclatura](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) seção para obter uma lista de regras e restrições de nomenclatura de compartilhamentos de arquivos.

    ![Compartilhamento de saudação de nomenclatura](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Pressione **Enter** quando concluído toocreate Olá compartilhamento de arquivos, ou **Esc** toocancel. Depois que o compartilhamento de arquivo hello foi criado com êxito, ele será exibido em Olá **compartilhamentos de arquivos** pasta para Olá selecionada a conta de armazenamento.

    ![novo compartilhamento de saudação](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Exibir o conteúdo de um compartilhamento de arquivos

Compartilhamentos de arquivos contêm arquivos e pastas (que também podem conter arquivos).

Olá etapas a seguir ilustram como tooview Olá conteúdo de um arquivo de compartilhamento de dentro do Gerenciador de armazenamento (visualização): +

1. Abra o Gerenciador de Armazenamento (Preview).

2. No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar tooview.

3. Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.

4. Compartilhamento de arquivos com o botão direito Olá seu gosto tooview e - no menu de contexto Olá - selecione **abrir**. Você também pode clicar duas vezes desejar tooview de compartilhamento de arquivo hello.

    ![Abrir compartilhamento](media/vs-azure-tools-storage-explorer-files/image4.png)

5. painel principal Olá exibirá o conteúdo do compartilhamento de arquivo hello.
    
    ![Olá conteúdo do compartilhamento](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Excluir um compartilhamento de arquivos

Os compartilhamentos de arquivos podem ser criados e excluídos facilmente conforme a necessidade. (toosee como toodelete de arquivos individuais, consulte a seção toohello, [gerenciar arquivos em um compartilhamento de arquivo](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Olá, as etapas a seguir ilustra como toodelete um compartilhamento de arquivo no Gerenciador de armazenamento (visualização):

1. Abra o Gerenciador de Armazenamento (Preview).

2. No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar tooview.

3. Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.

4. Compartilhamento de arquivos com o botão direito Olá seu gosto toodelete e - no menu de contexto Olá - selecione **excluir**. Você também pode pressionar **excluir** compartilhamento de arquivo atualmente selecionado Olá toodelete.

    ![Exclusão](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Selecione **Sim** toohello caixa de diálogo de confirmação.
    
    ![Diálogo de confirmação](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Copiar um compartilhamento de arquivos

O Gerenciador de armazenamento (visualização) permite que você toocopy uma área de transferência de toohello de compartilhamento de arquivo e, em seguida, cole o compartilhamento de arquivos em outra conta de armazenamento. (toosee como toocopy de arquivos individuais, consulte a seção toohello, [gerenciar arquivos em um compartilhamento de arquivo](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Olá, as etapas a seguir ilustra como toocopy um arquivo de compartilhamento de um tooanother de conta de armazenamento.

1. Abra o Gerenciador de Armazenamento (Preview).

2. No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar toocopy.

3. Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.

4. Compartilhamento de arquivos com o botão direito Olá seu gosto toocopy e - no menu de contexto Olá - selecione **compartilhamento de arquivo de cópia**.

    ![Copiar o compartilhamento de arquivos](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Clique em destino"hello desejado" conta de armazenamento no qual você deseja compartilhamento de arquivo hello toopaste e - no menu de contexto Olá - selecione **de compartilhamento de arquivo colar**.

    ![Colar o compartilhamento de arquivos](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Obter Olá SAS para um compartilhamento de arquivos

Um [assinatura de acesso compartilhado (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornece acesso delegado tooresources na sua conta de armazenamento. Isso significa que você pode conceder a que um cliente limitado tooobjects permissões na conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter que tooshare suas chaves de acesso da conta.

Olá etapas a seguir ilustram como toocreate um SAS para um arquivo de compartilhar: +

1. Abra o Gerenciador de Armazenamento (Preview).

2. No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivos Olá para o qual você deseja tooget um SAS.

3. Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.

4. Compartilhamento de arquivo desejado hello e - no menu de contexto Olá - selecione **obter assinatura de acesso compartilhado**.

    ![Obter Assinatura de Acesso Compartilhado](media/vs-azure-tools-storage-explorer-files/image10.png)

5. Em Olá **assinatura de acesso compartilhado** caixa de diálogo, especifique política hello, datas de início e vencimento, fuso horário e você deseja para o recurso de saudação de níveis de acesso.

    ![Diálogo Obter SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Quando tiver terminado de especificar opções de SAS hello, selecione **criar**.

7. Um segundo **assinatura de acesso compartilhado** caixa de diálogo, em seguida, exibirá que listas Olá compartilhamento de arquivos juntamente com a URL de saudação e QueryStrings que você pode usar tooaccess Olá recurso de armazenamento. Selecione **cópia** próximo URL toohello desejar toocopy toohello da área de transferência.
    
    ![Segundo diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Ao terminar, escolha **Fechar**.

## <a name="manage-access-policies-for-a-file-share"></a>Gerenciar políticas de acesso para um compartilhamento de arquivos

Olá etapas a seguir ilustram como toomanage (Adicionar e remover) políticas de acesso para um compartilhamento de arquivos: +. Olá políticas de acesso é usada para criar URLs da SAS por meio do qual as pessoas podem usar Olá tooaccess recursos de arquivo de armazenamento durante um período de tempo definido.

1. Abra o Gerenciador de Armazenamento (Preview).

2. No painel esquerdo do hello, expanda conta de armazenamento de saudação contendo o compartilhamento de arquivo hello cujas desejar toomanage as políticas de acesso.

3. Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.

4. Selecione Compartilhamento de arquivo desejado hello e - no menu de contexto Olá - **gerenciar políticas de acesso**.

    ![Menu de contexto Gerenciar políticas de acesso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Olá **políticas de acesso** diálogo listará todas as políticas de acesso já criadas para o compartilhamento de arquivo selecionado hello.
    
    ![Políticas de acesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Siga estas etapas, dependendo da tarefa de gerenciamento de política de acesso de saudação:
    
    - **Adicionar uma nova política de acesso** — escolha **Adicionar**. Uma vez gerado, Olá **políticas de acesso** caixa de diálogo exibirá Olá recém-adicionado acessar política (com configurações padrão).

    - **Editar uma política de acesso** — faça as edições desejadas e escolha **Salvar**.

    - **Remover uma política de acesso** - selecione **remover** próximo toohello de política de acesso você deseja tooremove.

7. Crie uma nova URL de SAS usando Olá política de acesso que você criou anteriormente:
    
    ![Obter SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e propriedades SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Gerenciando arquivos em um compartilhamento de arquivos

Depois de criar um compartilhamento de arquivos, você pode carregar um compartilhamento de arquivos do arquivo toothat, faça o download de um computador local do arquivo tooyour, abrir um arquivo em seu computador local e muito mais.

Olá etapas a seguir ilustram como compartilham a toomanage Olá arquivos (e pastas) dentro de um arquivo.

1.  Abra o Gerenciador de Armazenamento (Preview).

2.  No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar toomanage.

3.  Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.

4.  Clique duas vezes desejar tooview de compartilhamento de arquivo hello.

5.  painel principal Olá exibirá o conteúdo do compartilhamento de arquivo hello.

    ![Olá conteúdo do compartilhamento](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  painel principal Olá exibirá o conteúdo do compartilhamento de arquivo hello.

7.  Siga estas que etapas, dependendo da tarefa Olá desejar tooperform:

    - **Carregar o compartilhamento de arquivos de tooa de arquivos**

        a.  Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar arquivos** do menu suspenso de saudação.

        ![Carregar arquivos](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. Em Olá **carregar arquivos** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **arquivos** tooselect Olá arquivos desejar tooupload da caixa de texto.

        ![Adicionando arquivos](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Escolha **Carregar**.

    - **Carregar uma pasta de compartilhamento de arquivo de tooa**
        
        a. Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** do menu suspenso de saudação.

        ![Menu Carregar pasta](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. Em Olá **pasta carregamento** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **pasta** pasta de saudação de tooselect de caixa de texto cujo conteúdo você deseja tooupload.

        c. Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionada será carregado. Se a pasta de destino de saudação não existir, ele será criado.

        d. Escolha **Carregar**.

    - **Fazer o download de um computador local do arquivo tooyour**
        
        a. Selecione arquivo hello desejar toodownload.
        
        b. Na barra de ferramentas do painel Olá principal, selecione **baixar**.
        
        c. Em Olá **especifique onde toosave Olá baixou o arquivo** caixa de diálogo, especifique Olá local onde você deseja que o arquivo hello baixado e Olá nome você deseja toogive-lo.

        d. Selecione **Salvar**.

    - **Abrir um arquivo em seu computador local**
        
        a.  Selecione arquivo hello desejar tooopen.
        
        b.  Na barra de ferramentas do painel Olá principal, selecione **abrir**.
        
        c.  arquivo Hello será baixado e abertos usando o aplicativo hello associado com o tipo subjacente de arquivo do arquivo hello.

    - **Copiar uma área de transferência do arquivo toohello**

        a. Selecione arquivo hello desejar toocopy.

        b. Na barra de ferramentas do painel Olá principal, selecione **cópia**.

        c. No painel esquerdo do hello, navegar tooanother compartilhamento de arquivo e clique duas vezes nele tooview-lo no painel principal hello.

        d. Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia do arquivo hello.

    - **Excluir um arquivo**

        a. Selecione arquivo hello desejar toodelete.

        b. Na barra de ferramentas do painel Olá principal, selecione **excluir**.

        c. Selecione **Sim** toohello caixa de diálogo de confirmação.

## <a name="next-steps"></a>Próximas etapas

- Saudação de exibição [notas de versão do Gerenciador de armazenamento (visualização) e vídeos mais recentes](http://www.storageexplorer.com/).

- Saiba como muito[criar aplicativos usando blobs do Azure, tabelas, filas e arquivos](https://azure.microsoft.com/documentation/services/storage/).
