---
title: aaaBrowsing e gerenciamento de recursos de armazenamento com o Server Explorer | Microsoft Docs
description: Navegando e gerenciando recursos de armazenamento com o Gerenciador de Servidores
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Navegando e gerenciando recursos de armazenamento com o Gerenciador de Servidores
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Visão geral
Se você tiver instalado as ferramentas do Azure Olá para Microsoft Visual Studio, você pode exibir dados da tabela, blob e fila de suas contas de armazenamento do Azure. nó de armazenamento do Azure Olá no Gerenciador de servidores mostra os dados que estão em sua conta do emulador de armazenamento local e suas outras contas de armazenamento do Azure.

Escolha tooview Gerenciador de servidores no Visual Studio, na barra de menus do hello, **exibição**, **Server Explorer**. nó de armazenamento Olá mostra todas as contas de armazenamento Olá que existem em cada assinatura do Azure/certificado que estiver conectado à. Se sua conta de armazenamento não aparecer, você pode adicioná-lo seguindo as instruções de saudação [mais adiante neste tópico](#add-storage-accounts-by-using-server-explorer).

A partir do Azure SDK 2.7, também pode usar Olá novo Cloud Explorer tooview e gerenciar seus recursos do Azure. Consulte [Gerenciando recursos do Azure com o Gerenciador de nuvem](vs-azure-tools-resources-managing-with-cloud-explorer.md) para obter mais informações.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Exibir e gerenciar recursos de armazenamento no Visual Studio
O Gerenciador de Servidores automaticamente mostra uma lista de blobs, filas e tabelas na conta do emulador de armazenamento. conta do emulador de armazenamento Hello está listada no Gerenciador de servidores no nó de armazenamento de saudação como Olá **desenvolvimento** nó.

recursos da conta do emulador de armazenamento Olá toosee, expanda Olá **desenvolvimento** nó. Se o emulador de armazenamento Olá não foi iniciada quando você expande Olá **desenvolvimento** nó, ele será iniciado automaticamente. Isso pode levar vários minutos. Você pode continuar toowork em outras áreas do Visual Studio ao inicia o emulador de armazenamento hello.

recursos de tooview em uma conta de armazenamento, expanda o nó de saudação conta de armazenamento no Gerenciador de servidores. Olá seguintes subnós são exibidos:

* Blobs
* Filas
* Tabelas

## <a name="work-with-blob-resources"></a>Trabalhar com recursos de blob
nó de Blobs Olá exibe uma lista de contêineres para a conta de armazenamento de saudação selecionada. Contêineres de blob contêm arquivos de blob e você pode organizar esses blobs em pastas e subpastas. Consulte [como toouse armazenamento de BLOBs no .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) para obter mais informações.

### <a name="toocreate-a-blob-container"></a>toocreate um contêiner de blob
1. Menu de atalho Olá aberto para Olá **Blobs** nó e, em seguida, escolha **criar contêiner de Blob**.
2. Em Olá **criar contêiner de Blob** caixa de diálogo, digite o nome de saudação do novo contêiner de saudação.  
3. Pressione **ENTER** do teclado, ou você pode clique ou toque em fora do contêiner de blob de Olá Olá nome campo toosave.
   
   > [!NOTE]
   > nome do contêiner de blob Olá deve começar com uma letra minúscula (a-z) ou um número (0-9).
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete um contêiner de blob
* Menu de atalho Olá aberta para o contêiner de blob Olá você deseja tooremove e, em seguida, escolha **excluir**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay uma lista de itens de saudação contidos em um contêiner de blob
* Abra o menu de atalho de saudação para um nome de contêiner de blob na lista de saudação e, em seguida, escolha **abrir**.
  
    Quando você exibe o conteúdo de saudação de um contêiner de blob, ele aparece em uma guia conhecida como exibição de contêiner de blob hello.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Você pode executar Olá seguintes operações em blobs usando botões de saudação no canto superior direito de saudação do modo de exibição de contêiner de blob hello:
  
  * Inserir um valor de filtro e aplicá-lo
  * Atualize a lista de saudação de blobs no contêiner de saudação
  * Carregar um arquivo
  * Excluir um blob
    
    > [!NOTE]
    > Excluir um arquivo de um contêiner de blob não exclui o arquivo de base de saudação; Ele apenas a remove do contêiner de blob hello.
    > 
    > 
  * Abrir um blob
  * Salvar um computador local do blob toohello

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate uma pasta ou subpasta em um contêiner de blob
1. Escolha o contêiner de blob Olá no Gerenciador de nuvem. Na janela de contêiner de saudação, escolha Olá **carregar Blob** botão.
   
    ![Carregar um arquivo em uma pasta de blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. Em Olá **carregue o novo arquivo** caixa de diálogo caixa, escolha Olá **procurar** arquivo de saudação do botão toospecify você deseja tooupload e, em seguida, digite um nome de pasta no hello **pasta (opcional)** caixa .
   
    Você pode adicionar subpastas em pastas de contêiner seguindo Olá mesmo procedimento. Se você não especificar um nome de pasta, arquivo hello será carregado de nível superior toohello saudação do contêiner de blob. arquivo Hello aparece na pasta de especificado de saudação no contêiner de saudação.
   
    ![Pasta adicionada tooa contêiner de blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Clique duas vezes em pasta hello ou pressione ENTER toosee Olá conteúdo Olá pasta. Quando você estiver na pasta do contêiner hello, você pode navegar toohello back raiz do contêiner Olá escolhendo Olá **diretório pai aberto** (seta para cima) botão.

### <a name="toodelete-a-container-folder"></a>toodelete uma pasta do contêiner
* Excluir todos os arquivos de saudação na pasta Olá
  
  > [!NOTE]
  > Como pastas em contêineres de blob são pastas virtuais, não é possível criar uma pasta vazia nem excluir uma pasta toodelete seu conteúdo do arquivo. Você tem toodelete Olá todo o conteúdo de uma pasta de saudação toodelete.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>toofilter blobs em um contêiner
Você pode filtrar os blobs de saudação que são exibidos especificando um prefixo comum.

Por exemplo, se você inserir o prefixo Olá `hello` em Olá caixa de texto de filtro e escolha Olá **Execute** (**!**) botão, somente os blobs que começam com "hello" é exibido.

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> campo de filtro de saudação diferencia maiusculas de minúsculas e não oferece suporte a filtragem com caracteres curinga. Os blobs só podem ser filtrados pelo prefixo. prefixo de saudação pode incluir um delimitador se você estiver usando blobs de tooorganize um delimitador em uma hierarquia virtual. Por exemplo, a filtragem em Olá prefixo HelloFabric / retorna todos os blobs que começam com essa cadeia de caracteres.
> 
> 

### <a name="toodownload-blob-data"></a>dados de blob toodownload
* Em **Cloud Explorer**, abra o menu de atalho Olá para um ou mais blobs e, em seguida, escolha **abrir**, ou escolha o nome do blob Olá e escolha Olá **abrir** botão, ou clique duas vezes em nome do blob Hello.
  
    progresso de saudação de um download de blob aparece no hello **o Log de atividades do Azure** janela.
  
    blob de saudação é aberto no editor de padrão de saudação para esse tipo de arquivo. Se o sistema operacional de saudação reconhecer o tipo de arquivo hello, arquivo de saudação é aberto em um aplicativo instalado localmente; Caso contrário, será solicitado que você toochoose um aplicativo que é apropriado para o tipo de arquivo de saudação do blob hello. arquivo de local de saudação que é criado quando você baixa um blob está marcado como somente leitura.
  
    Dados BLOB é armazenado em cache localmente e comparados saudação hora da última modificação do blob no hello serviço Blob. Se o blob Olá tiver sido atualizada desde que foi baixado, ele será baixado novamente; Caso contrário, Olá blob será carregado do disco local hello. Por padrão, um blob é o diretório temporário tooa baixado. diretório de específico de tooa de blobs do toodownload, menu de atalho Olá aberto para Olá selecionado nomes de blob e escolha **Salvar como**. Quando você salva um blob dessa maneira, Olá blob arquivo não está aberto e arquivo local Olá é criado com os atributos de leitura / gravação.

### <a name="tooupload-blobs"></a>blobs tooupload
* Escolha Olá **carregar Blob** botão quando o contêiner hello está aberta para exibição no modo de exibição de contêiner de blob hello.
  
    Você pode escolher uma ou mais tooupload de arquivos e você pode carregar arquivos de qualquer tipo. Olá **o Log de atividades do Azure** mostra Olá progresso de carregamento de saudação. Para obter mais informações sobre como toowork com dados de blob, consulte [como toouse Olá serviço de armazenamento de Blob do Azure no .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>os logs de tooview transferidos tooblobs
* Se você estiver usando dados do diagnóstico do Azure toolog do seu aplicativo do Azure e tiver transferido logs conta de armazenamento de tooyour, você verá os contêineres que foram criados pelo Azure para esses logs. Exibindo esses logs no Gerenciador do servidor é um problemas tooidentify de maneira fácil com o seu aplicativo, especialmente se ele tiver sido implantado tooAzure. Para saber mais sobre o Diagnóstico do Azure, consulte [Coletar dados do log usando o Diagnóstico do Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>tooget Olá URL para um blob
* Abra o menu de atalho do blob hello e, em seguida, escolha **Copiar URL**.

### <a name="tooedit-a-blob"></a>tooedit um blob
* Selecione blob hello e escolha Olá **abrir Blob** botão.
  
    Olá é o local temporário tooa baixado e aberto no computador local hello. Você deve carregar o blob Olá novamente depois de fazer alterações.

## <a name="work-with-queue-resources"></a>Trabalhar com recursos de fila
Filas de serviços de armazenamento são hospedadas em uma conta de armazenamento do Azure e usá-los tooallow seu toocommunicate de funções de serviço de nuvem entre si e com outros serviços por um mecanismo de passagem de mensagem. Você pode acessar a fila de saudação programaticamente por meio de um serviço de nuvem e sobre um serviço web para clientes externos. Você também pode acessar a fila de saudação diretamente, usando o Gerenciador de servidores no Visual Studio.

Ao desenvolver um serviço de nuvem que usa filas, você pode desejar filas de toocreate toouse Visual Studio e trabalhar interativamente com elas enquanto você desenvolver e testar seu código.

No Gerenciador de servidores, você pode exibir filas Olá em uma conta de armazenamento, criar e excluir filas, abrir uma fila tooview suas mensagens de e adicionar mensagens tooa fila. Quando você abrir uma fila para exibição, você pode exibir mensagens de saudação individuais, e você pode executar ações a seguir na fila de saudação usando botões de saudação no canto superior esquerdo de saudação do hello:

* Atualizar exibição da saudação da fila de saudação
* Adicionar uma fila de mensagens toohello
* Mensagem de saudação do mais alto de remoção da fila
* Fila inteira Olá limpar

Olá a imagem a seguir mostra uma fila que contém duas mensagens.

![Exibindo uma fila](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Para obter mais informações sobre o armazenamento de filas de serviço, consulte [como: Olá usar serviço de armazenamento de fila](http://go.microsoft.com/fwlink/?LinkID=264702). Para obter informações sobre o serviço web de saudação para filas de serviço de armazenamento, consulte [conceitos do serviço de fila](http://go.microsoft.com/fwlink/?LinkId=264788). Para obter informações sobre como toosend mensagens tooa dos serviços de armazenamento fila usando o Visual Studio, consulte [tooa de envio de mensagens fila de serviços de armazenamento](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Filas de serviços de armazenamento são diferentes de filas do barramento de serviço. Para obter mais informações sobre filas do barramento de serviço, consulte Filas do barramento de serviço, tópicos e assinaturas.
> 
> 

## <a name="work-with-table-resources"></a>Trabalhar com recursos de tabela
saudação de serviço de armazenamento de tabela do Azure armazena grandes quantidades de dados estruturados. serviço de saudação é um repositório de dados NoSQL que aceita autenticado chamadas dentro e fora de saudação nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

### <a name="toocreate-a-table"></a>toocreate uma tabela
1. No Pesquisador de objetos de nuvem, selecione Olá **tabelas** nó de armazenamento de saudação de conta e, em seguida, escolha **Create Table**.
2. Em Olá **Create Table** caixa de diálogo caixa, digite um nome para a tabela de saudação.

### <a name="tooview-table-data"></a>dados da tabela tooview
1. No Pesquisador de objetos de nuvem, abra Olá **Azure** nó e então abra hello **armazenamento** nó.
2. Nó de conta de armazenamento Olá abertos que você está interessado em e, em seguida, abra Olá **tabelas** nó toosee uma lista de tabelas Olá conta de armazenamento.
3. Abra o menu de atalho Olá para uma tabela e escolha **Exibir tabela**.
   
    ![Uma tabela do Azure no Gerenciador de Soluções](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

Olá tabela é organizada por entidades (mostradas nas linhas) e propriedades (mostradas nas colunas). Por exemplo, Olá ilustração a seguir mostra as entidades listadas no hello **Designer de tabela**:

### <a name="tooedit-table-data"></a>dados da tabela tooedit
1. Em Olá **Designer de tabela**, abra o menu de atalho Olá para uma entidade (uma única linha) ou uma propriedade (uma única célula) e, em seguida, escolha **editar**.
   
    ![Adicionar ou editar uma entidade de tabela](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Entidades em uma única tabela não são Olá toohave necessário mesmo conjunto de propriedades (colunas). Lembre-Olá mente restrições a seguir ao exibir e editar dados da tabela.
   
   * Você não pode exibir ou editar dados binários (tipo byte[]), mas pode armazená-los em uma tabela.
   * Não é possível editar Olá **PartitionKey** ou **RowKey** valores, como o armazenamento de tabela no Azure não oferece suporte a essa operação.
   * Você não pode criar uma propriedade chamada Timestamp, os serviços de armazenamento do Azure usam uma propriedade com esse nome.
   * Se você inserir um valor DateTime, você deve seguir um formato apropriado toohello configurações de região e idioma do computador (por exemplo, DD/MM/AAAA HH [AM | PM] para os EUA ).

### <a name="tooadd-entities"></a>entidades de tooadd
1. Em Olá **Designer de tabela**, escolha Olá **Adicionar entidade** botão.
   
    ![Adicionar entidade](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. Em Olá **Adicionar entidade** caixa de diálogo caixa, digite os valores de saudação do hello **PartitionKey** e **RowKey** propriedades.
   
    ![Adicionar caixa de diálogo de entidade](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Insira valores hello com cuidado porque você não pode alterá-los depois de fechar a caixa de diálogo hello, a menos que você excluir a entidade hello e adicioná-lo novamente.

### <a name="toofilter-entities"></a>entidades de toofilter
Você pode personalizar o conjunto de saudação de entidades que aparecem em uma tabela, se você usar o construtor de consultas de saudação.

1. Construtor de consultas do tooopen hello, abra uma tabela para exibição.
2. Escolha o botão do construtor de consultas de Olá na barra de ferramentas da exibição da tabela de saudação.
   
    Olá **construtor de consultas** caixa de diálogo é exibida. Olá ilustração a seguir mostra uma consulta que está sendo criada no construtor de consultas de saudação.
   
    ![Construtor de Consultas](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Quando você terminar criar consulta hello, feche a caixa de diálogo de saudação. Olá resultante formulário de texto Olá consulta aparece em uma caixa de texto como um filtro do WCF Data Services.
4. Olá toorun de consulta, escolha o ícone de triângulo verde hello.
   
    Você também pode filtrar dados de entidade que aparecem no hello **Designer de tabela** se você inserir uma cadeia de caracteres de filtro do WCF Data Services diretamente no campo de filtro de saudação. Esse tipo de cadeia de caracteres é semelhante tooa cláusula SQL WHERE, mas é enviado toohello server como uma solicitação HTTP. Para obter informações sobre como tooconstruct filtrar cadeias de caracteres, consulte [construindo cadeias de caracteres de filtro para Olá Designer de tabela](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Olá ilustração a seguir mostra um exemplo de uma cadeia de caracteres de filtro válida:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Atualizar dados de armazenamento
Quando o Gerenciador de servidores se conecta a tooor obtém dados de uma conta de armazenamento, pode levar até um minuto tooa Olá operação toocomplete. Se ele não pode se conectar, a operação de saudação pode atingir o tempo limite. Enquanto os dados são recuperados, você pode continuar toowork em outras partes do Visual Studio. operação de saudação toocancel se ele estiver demorando muito, escolha Olá **Parar atualização** botão na barra de ferramentas do Gerenciador de servidores hello.

#### <a name="toorefresh-blob-container-data"></a>dados de contêiner de blob toorefresh
* Selecione Olá **Blobs** nó **armazenamento** e escolha Olá **atualizar** botão na barra de ferramentas do Gerenciador de servidores hello.
* lista Olá toorefresh de blobs que é exibida, escolha Olá **Execute** botão.

#### <a name="toorefresh-table-data"></a>dados da tabela toorefresh
* Selecione Olá **tabelas** nó **armazenamento** e escolha Olá **atualização** botão.
* lista Olá toorefresh de entidades que é exibida no hello **Designer de tabela**, escolha Olá **Execute** botão Olá **Designer de tabela**.

#### <a name="toorefresh-queue-data"></a>dados da fila toorefresh
* Selecione Olá **filas** nó e, em seguida, escolha Olá **atualização** botão.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>toorefresh todos os itens em uma conta de armazenamento
* Escolha o nome da conta hello e escolha Olá **atualização** botão na barra de ferramentas de saudação do Gerenciador de servidores.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Adicionar contas de armazenamento usando o Gerenciador de Servidores
Há duas maneiras tooadd contas de armazenamento usando o Gerenciador de servidores. Você pode criar uma nova conta de armazenamento na sua assinatura do Azure ou pode anexar uma conta de armazenamento existente.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate uma nova conta de armazenamento usando o Gerenciador de servidores
1. No Gerenciador de servidores, abra Olá menu de atalho para o nó de armazenamento hello e, em seguida, escolha Criar conta de armazenamento.
   
    ![Criar uma nova conta de armazenamento do Azure](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Selecione ou digite Olá seguintes informações Olá nova conta de armazenamento no hello **criar conta de armazenamento** caixa de diálogo.
   
   * Olá toowhich de assinatura do Azure que você deseja tooadd conta de armazenamento de saudação.
   * Olá nome toouse para a nova conta de armazenamento hello.
   * região de saudação ou grupo de afinidade (como Oeste dos EUA ou Ásia Oriental).
   * Olá tipo de replicação você deseja toouse Olá conta de armazenamento, como com redundância geográfica.
3. Escolha **Criar**.
   
    Olá nova conta de armazenamento aparece no hello **armazenamento** lista no Gerenciador de soluções.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach uma conta de armazenamento existente usando o Gerenciador de servidores
1. No Gerenciador de servidores, abra Olá menu de atalho para o nó de armazenamento do Azure hello e, em seguida, escolha **anexar armazenamento externo**.
   
    ![Adicionar uma conta de armazenamento existente](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Selecione ou digite Olá seguintes informações Olá nova conta de armazenamento no hello **criar conta de armazenamento** caixa de diálogo.
   
   * nome de Olá Olá existente da conta de armazenamento que você deseja tooattach. Você pode digitar um nome ou selecioná-lo na lista de saudação.
   * chave Olá Olá selecionado conta de armazenamento. Esse valor geralmente é fornecido para você quando seleciona uma conta de armazenamento. Se desejar que a chave de conta de armazenamento do Visual Studio tooremember hello, selecione caixa chave da conta Olá lembrar.
   * Olá protocolo toouse tooconnect toohello conta de armazenamento, como HTTP, HTTPS ou um ponto de extremidade personalizado. Consulte [como cadeias de caracteres de Conexão tooConfigure](https://msdn.microsoft.com/library/azure/ee758697.aspx) para obter mais informações sobre pontos de extremidade personalizados.

### <a name="tooview-hello-secondary-endpoints"></a>pontos de extremidade secundários tooview Olá
* Se você tiver criado uma conta de armazenamento usando Olá **acesso de leitura com redundância geográfica com** opção de replicação, você pode exibir os pontos de extremidade secundários. Abrir menu de atalho Olá para o nome da conta hello e, em seguida, escolha **propriedades**.
  
    ![Pontos de extremidade de armazenamento secundários](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove uma conta de armazenamento do Gerenciador de servidores
* No Gerenciador de servidores, abra Olá menu de atalho para o nome da conta hello e, em seguida, escolha **excluir**. Se você excluir uma conta de armazenamento, qualquer informação de chave salva para essa conta também é removida.
  
  > [!NOTE]
  > Se você excluir uma conta de armazenamento do Gerenciador de servidores, ele não afeta a sua conta de armazenamento ou todos os dados que ele contém; simplesmente remova a referência de saudação do Gerenciador de servidores. toopermanently excluir uma conta de armazenamento, use Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como usar os serviços de armazenamento do Azure, consulte [acessar serviços de armazenamento do Azure Olá](https://msdn.microsoft.com/library/azure/ee405490.aspx).

