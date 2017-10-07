---
title: "aaaGet iniciado com o Gerenciador de armazenamento (visualização) | Microsoft Docs"
description: "Gerenciar os recursos de armazenamento do Azure com o Gerenciador de Armazenamento (Visualização)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Introdução ao Gerenciador de armazenamento (visualização)
## <a name="overview"></a>Visão geral
Gerenciador de armazenamento do Azure (visualização) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e macOS. Neste artigo, você aprenderá Olá várias maneiras de se conectar tooand gerenciar suas contas de armazenamento do Azure.

![Gerenciador de Armazenamento do Microsoft Azure (Preview)][15]

## <a name="prerequisites"></a>Pré-requisitos
* [Baixe e instale o Gerenciador de armazenamento (visualização)](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Conecte-se a conta de armazenamento tooa ou serviço
O Gerenciador de armazenamento (visualização) fornece várias maneiras tooconnect toostorage contas. Por exemplo, você pode:
* Conecte-se toostorage contas associadas às suas assinaturas do Azure.
* Conecte-se toostorage contas e serviços compartilhados de outras assinaturas do Azure.
* Conecte-se tooand gerenciar armazenamento local usando Olá emulador de armazenamento do Azure. 

Além disso, você pode trabalhar com contas nacionais e internacionais de armazenamento no Azure:

* [Conectar-se a assinatura do Azure do tooan](#connect-to-an-azure-subscription): gerenciar recursos de armazenamento que pertencem a tooyour assinatura do Azure.
* [Trabalhar com o armazenamento de desenvolvimento local](#work-with-local-development-storage): gerenciar o armazenamento local usando Olá emulador de armazenamento do Azure.
* [Anexar armazenamento tooexternal](#attach-or-detach-an-external-storage-account): gerenciar recursos de armazenamento que pertencem a tooanother assinatura do Azure ou que estão sob national nuvens do Azure usando o nome da conta de armazenamento hello, chave e pontos de extremidade.
* [Anexar uma conta de armazenamento usando uma SAS](#attach-storage-account-using-sas): gerenciar recursos de armazenamento que pertencem tooanother assinatura do Azure usando uma assinatura de acesso compartilhado (SAS).
* [Anexe um serviço usando uma SAS](#attach-service-using-sas): gerenciar um serviço de armazenamento específico (contêiner de blob, fila ou tabela) que pertence a tooanother assinatura do Azure usando uma SAS.

## <a name="connect-tooan-azure-subscription"></a>Conecte-se tooan assinatura do Azure
> [!NOTE]
> Se não tiver uma conta do Azure, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. No Gerenciador de Armazenamento (Visualização), selecione **Configurações de conta do Azure**.

    ![Configurações de conta do Azure][0]

2. painel esquerdo Olá exibe todas as contas da Microsoft hello em que você entrou. conta de tooanother tooconnect, selecione **adicionar uma conta**e, em seguida, siga Olá instruções toosign com uma conta da Microsoft que está associada a pelo menos uma assinatura ativa do Azure.

    >[!NOTE]
    >Conectar toonational Azure (como o Azure Alemanha, governo do Azure e do Azure na China por meio de entrada) não é suportado atualmente. Consulte hello "anexar ou desanexar uma conta de armazenamento externo" seção para saber como contas de armazenamento do Azure toonational tooconnect.

3. Depois que você entrar com êxito com uma conta da Microsoft, Olá esquerda painel é populado com hello assinaturas do Azure associadas a essa conta. Selecione Olá assinaturas do Azure que você deseja toowork com e, em seguida, selecione **aplicar**. (Selecionar **todas as assinaturas** alterna selecionando todos ou nenhum Olá listados assinaturas do Azure.)

    ![Selecionar assinaturas do Azure][3]  
    painel esquerdo Olá exibe as contas de armazenamento Olá associadas a assinaturas do Azure Olá selecionado.

    ![Assinaturas do Azure selecionadas][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Conecte-se a assinatura do Azure pilha tooan

Para obter informações sobre assinatura de pilha do Azure tooan conexão, consulte [conectar o Gerenciador de armazenamento tooan assinatura do Azure pilha](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Trabalhar com o armazenamento de desenvolvimento local
Com o Gerenciador de armazenamento (visualização), você pode trabalhar no armazenamento local usando Olá emulador de armazenamento do Azure. Essa abordagem permite que você escreva o código e teste de armazenamento sem necessariamente ter uma conta de armazenamento implantada no Azure, porque a conta de armazenamento hello está sendo emulada pelo Olá emulador de armazenamento do Azure.

> [!NOTE]
> Olá emulador de armazenamento do Azure é suportada atualmente apenas para Windows.
>
>

1. No painel esquerdo de saudação do Gerenciador de armazenamento (visualização), expanda Olá **(Local e conectado)** > **contas de armazenamento** > **(desenvolvimento)** nó.

    ![Nó de desenvolvimento local][21]

2. Se você ainda não tiver instalado Olá emulador de armazenamento do Azure, é solicitada toodo caso por meio de uma barra de informações. Se a barra de informações Olá for exibida, selecione **Baixe a versão mais recente Olá**e, em seguida, instale o emulador de saudação.

    ![Baixar o prompt do Emulador de Armazenamento do Azure][22]

3. Depois de instalar o emulador hello, você pode criar e trabalhar com locais blobs, filas e tabelas. toolearn como tipo toowork com cada conta de armazenamento, consulte um dos seguintes hello:

    * [Gerenciar recursos de Armazenamento de Blobs do Azure](vs-azure-tools-storage-explorer-blobs.md)
    * Gerenciar recursos de armazenamento de compartilhamento de arquivos do Azure: *em breve*
    * Gerenciar recursos de armazenamento de filas do Azure: *em breve*
    * Gerenciar recursos de armazenamento de tabelas do Azure: *em breve*

## <a name="attach-or-detach-an-external-storage-account"></a>Conexão ou desconexão de uma conta de armazenamento externo
Com o Gerenciador de armazenamento (visualização), você pode anexar tooexternal contas de armazenamento para que as contas de armazenamento podem ser facilmente compartilhadas. Esta seção explica como tooattach too(and detach from) contas de armazenamento externo.

### <a name="get-hello-storage-account-credentials"></a>Obter credenciais de conta de armazenamento Olá
tooshare uma conta de armazenamento externo, o proprietário de saudação dessa conta deve primeiro obter credenciais de saudação (nome da conta e chave) para a conta de saudação e, em seguida, compartilhar essas informações com hello quem quer tooattach toothat (externos) conta. Você pode obter credenciais de conta de armazenamento Olá via Olá portal do Azure fazendo Olá seguinte:

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Selecione **Procurar**.

3. Selecione **Contas de Armazenamento**.

4. Em Olá **contas de armazenamento** folha, selecione Olá desejado conta de armazenamento.

5. Em Olá **configurações** folha para Olá selecionada a conta de armazenamento, selecione **chaves de acesso**.

    ![Opção Chaves de Acesso][5]

6. Em Olá **chaves de acesso** folha, Olá cópia **nome da conta de armazenamento** e **key1** valores para uso ao anexar toohello conta de armazenamento.

    ![Chaves de acesso][6]

### <a name="attach-tooan-external-storage-account"></a>Anexar a conta de armazenamento externo de tooan
conta de armazenamento externo de tooan tooattach, é necessário nome e a chave da conta hello. Olá "Credenciais de conta de armazenamento do Get hello" seção explica como tooobtain esses valores de Olá portal do Azure. No entanto, no portal de Olá Olá conta chave é chamada de **key1**. Portanto em que o Gerenciador de armazenamento (visualização) solicita uma chave de conta, digite Olá **key1** valor.

1. No Gerenciador de armazenamento (visualização), selecione **conectar o armazenamento de tooAzure**.

    ![Conecte-se a opção de armazenamento tooAzure][23]

2. Em Olá **conectar tooAzure armazenamento** caixa de diálogo, especifique a chave de conta hello (Olá **key1** valor da saudação portal do Azure) e, em seguida, selecione **próximo**.

    > [!NOTE]
    > Você pode inserir a cadeia de caracteres de conexão de armazenamento Olá de uma conta de armazenamento no Azure nacional. Por exemplo, contas de armazenamento do tooconnect tooAzure Alemanha, insira o seguinte de toohello conexão cadeias de caracteres semelhante: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >Você pode obter a cadeia de caracteres de conexão de saudação do hello Azure portal em Olá mesmo maneira conforme descrito em Olá seção "Obter credenciais de conta de armazenamento Olá".

    ![Conecte-se a caixa de diálogo de armazenamento tooAzure][24]

3. Em Olá **anexar armazenamento externo** caixa de diálogo Olá **nome da conta** caixa, digite o nome de conta de armazenamento hello, especifique outras configurações desejadas e, em seguida, selecione **próximo**.

    ![Caixa de diálogo Anexar Armazenamento Externo][8]

4. Em Olá **Conexão resumo** caixa de diálogo caixa, verifique as informações de saudação. Se você desejar toochange qualquer coisa, selecione **novamente** e redigitar as definições de saudação desejada. 

5. Selecione **Conectar**.

6. Depois que ele está conectado com êxito, a conta de armazenamento externo de saudação é exibida com **(externo)** acrescentado toohello nome da conta de armazenamento.

    ![Resultado de conectar-se a conta de armazenamento externo de tooan][9]

### <a name="detach-from-an-external-storage-account"></a>Desconexão de uma conta de armazenamento externo
1. Clique em Olá conta de armazenamento externo que você deseja toodetach e, em seguida, selecione **desanexar**.

    ![Opção Desanexar do armazenamento][10]

2. Na mensagem de confirmação de saudação, selecione **Sim** tooconfirm desconexão de saudação da conta de armazenamento externo de saudação.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Como anexar uma conta de armazenamento usando uma SAS
Um [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) permite Olá administrador de uma assinatura do Azure conceder a conta de armazenamento temporário acesso tooa sem ter que tooprovide credenciais de assinatura do Azure.

tooillustrate neste cenário, vamos dizer que UserA é um administrador de uma assinatura do Azure e UserA quer tooallow UserB tooaccess conta de armazenamento por um período limitado com determinadas permissões:

1. UserA gera uma SAS (consistindo de cadeia de caracteres de conexão de Olá Olá conta de armazenamento) para um momento específico período e com permissões de saudação desejada.

2. Compartilhamentos de UserA Olá SAS com pessoa de saudação (UserB, em nosso exemplo) que deseja conta de armazenamento toohello de acesso.  

3. UserB usa a conta de toohello de tooattach do Gerenciador de armazenamento (visualização) que pertence a tooUserA usando Olá fornecido SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Obter um SAS para a conta de saudação desejado tooshare
1. No Gerenciador de armazenamento (visualização), clique na conta de armazenamento Olá você deseja compartilhar e, em seguida, selecione **obter assinatura de acesso compartilhado**.

    ![Opção do menu de contexto Obter SAS][13]

2. Em Olá **assinatura de acesso compartilhado** caixa de diálogo, especifique o período de tempo de saudação e as permissões que você deseja para a conta de saudação e, em seguida, selecione **criar**.

    ![Caixa de diálogo Obter SAS][14]  
    Olá **assinatura de acesso compartilhado** caixa de diálogo é aberta e exibe o saudação SAS.

3. Próxima toohello **cadeia de caracteres de Conexão**, selecione **cópia** toocopy-toohello área de transferência e, em seguida, selecione **fechar**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Anexar conta toohello compartilhado usando Olá SAS
1. No Gerenciador de armazenamento (visualização), selecione **conectar o armazenamento de tooAzure**.

    ![Conecte-se a opção de armazenamento tooAzure][23]

2. Em Olá **conectar tooAzure armazenamento** caixa de diálogo, especifique a cadeia de caracteres de conexão hello e, em seguida, selecione **próximo**.

    ![Conecte-se a caixa de diálogo de armazenamento tooAzure][24]

3. Em Olá **Conexão resumo** caixa de diálogo caixa, verifique as informações de saudação. alterações de toomake, selecione **novamente**e então insira configurações de saudação desejado. 

4. Selecione **Conectar**.

5. Depois que ele é anexado, conta de armazenamento Olá é exibida com **(SAS)** acrescentado toohello nome da conta que você forneceu.

    ![Resultado da conta tooan anexados usando SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a>Como anexar um serviço usando uma SAS
seção de "Anexar a uma conta de armazenamento usando uma SAS" Hello explica como um administrador de assinatura do Azure pode conceder a conta de armazenamento temporário acesso tooa gerando e compartilhando um SAS para a conta de armazenamento hello. Da mesma forma, uma SAS pode ser gerada para um serviço específico (contêiner de blobs, fila ou tabela) em uma conta de armazenamento.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Gerar um SAS para o serviço de saudação que você deseja tooshare
Nesse contexto, um serviço pode ser um contêiner de blob, fila ou tabela. Olá toogenerate SAS para um serviço listado, consulte:

* [Obter Olá SAS para um contêiner de blob](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Obter Olá SAS para um compartilhamento de arquivos: *em breve*
* Obter Olá SAS para uma fila: *em breve*
* Obter Olá SAS para uma tabela: *em breve*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Anexar toohello compartilhado conta serviço usando Olá SAS
1. No Gerenciador de armazenamento (visualização), selecione **conectar o armazenamento de tooAzure**.

    ![Conecte-se a opção de armazenamento tooAzure][23]

2. Em Olá **conectar tooAzure armazenamento** caixa de diálogo, especifique Olá URI SAS e, em seguida, selecione **próximo**.

    ![Conecte-se a caixa de diálogo de armazenamento tooAzure][24]

3. Em Olá **Conexão resumo** caixa de diálogo caixa, verifique as informações de saudação. alterações de toomake, selecione **novamente**e então insira configurações de saudação desejado. 

4. Selecione **Conectar**.

5. Depois que ele é anexado, hello serviço recentemente anexado é exibido em Olá **(serviço SAS)** nó.

    ![Resultado da anexação de serviço tooa compartilhado usando uma SAS][20]

## <a name="search-for-storage-accounts"></a>Pesquisar nas contas de armazenamento
Se você tiver uma longa lista de contas de armazenamento, uma maneira rápida de toolocate uma determinada conta de armazenamento é toouse caixa de pesquisa de saudação na parte superior de saudação do painel esquerdo do hello.

Conforme você digita na caixa de pesquisa hello, Olá painel esquerdo exibe contas de armazenamento de saudação que correspondam ao valor de pesquisa de saudação que você inseriu toothat ponto. Por exemplo, uma pesquisa para armazenamento de todas as contas cujo nome contém **tarcher** é mostrado no hello captura de tela a seguir:

![Pesquisa na conta de armazenamento][11]

## <a name="next-steps"></a>Próximas etapas
* [Como gerenciar os recursos de armazenamento de Blobs do Azure com o Gerenciador de armazenamento (visualização)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
