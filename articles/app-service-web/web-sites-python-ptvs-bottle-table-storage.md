---
title: aaaBottle e armazenamento de tabela do Azure no Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo de garrafa que armazena dados no armazenamento de tabela do Azure e implante Olá web aplicativo tooAzure aplicativos de Web do serviço de aplicativo."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Bottle e Armazenamento de Tabela do Azure com Ferramentas Python 2.2 para Visual Studio
Neste tutorial, vamos usar [ferramentas Python para Visual Studio] toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa. Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=GJXDGaEPy94).

Olá sondagens web aplicativo define uma abstração para seu repositório, assim você pode alternar facilmente entre tipos diferentes de repositórios (na memória, armazenamento de tabela do Azure, MongoDB).

Aprenderá como toocreate um armazenamento do Azure a conta, como tooconfigure Olá web aplicativo toouse armazenamento de tabela do Azure e toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com os serviços do MongoDB, armazenamento de tabela do Azure, MySQL e banco de dados SQL. Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2015
* [Ferramentas Python 2.2 para Visual Studio]
* [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]
* [Ferramentas do SDK do Azure para VS 2015]
* [Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="create-hello-project"></a>Criar hello projeto
Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra. Criaremos um ambiente virtual e instalaremos pacotes necessários. Em seguida, vamos executar aplicativo hello localmente usando o repositório do saudação padrão em memória.

1. No Visual Studio, selecione **Arquivo**, **Novo Projeto**.
2. Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**. Selecione **sondagens garrafa Web projeto** e clique em projeto de saudação toocreate Okey.
   
     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. Você será pacotes externos tooinstall solicitada. Selecione **Instalar em um ambiente virtual**.
   
     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. Selecione **Python 2.7** ou **Python 3.4** como interpretador base hello.
   
     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. Confirme se o aplicativo hello funciona pressionando `F5`. Por padrão, o aplicativo hello usa um repositório de memória que não exige qualquer configuração. Todos os dados são perdidos quando o servidor de web hello é interrompido.
6. Clique em **Criar Votações de Exemplo**e, em seguida, clique em uma votação e vote.
   
     ![Navegador da Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Criar uma conta de armazenamento do Azure
toouse operações de armazenamento, você precisa de uma conta de armazenamento do Azure. Você pode criar uma conta de armazenamento seguindo essas etapas.

1. Faça logon no hello [Portal do Azure](https://portal.azure.com/).
2. Clique em Olá **novo** ícone no início de saudação à esquerda da saudação Portal, clique em **dados + armazenamento** > **conta de armazenamento**.  Clique em Olá **criar** botão, em seguida, dê um nome exclusivo de conta de armazenamento hello e criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ele.
   
      ![Criação Rápida](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    Quando tiver sido criada a conta de armazenamento hello, Olá **notificações** botão pisca uma verde **êxito** e folha da conta de armazenamento hello está aberta tooshow que ele pertence toohello novo recurso de grupo criado.
3. Clique em Olá **chaves de acesso** parte na folha da conta de armazenamento hello. Anote o nome de conta hello e key1.
   
      ![simétricas](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    Precisaremos este tooconfigure informações seu projeto na próxima seção, Olá.

## <a name="configure-hello-project"></a>Configurar Olá projeto
Nesta seção, configuraremos nosso conta de armazenamento do aplicativo toouse Olá que acabamos de criar. Em seguida, vamos executar aplicativo hello localmente.

1. No Visual Studio, clique com o botão direito do mouse no nó do projeto no Gerenciador de Soluções e selecione **Propriedades**. Clique em Olá **depurar** guia.
   
     ![Configurações de depuração do projeto](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Definir valores de saudação de variáveis de ambiente exigidos pelo aplicativo hello em **depurar servidor comando**, **ambiente**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Isso definirá as variáveis de ambiente hello quando você **iniciar depuração**. Se você quiser Olá variáveis toobe definida quando você **Start Without Debugging**, Olá conjunto mesmo valores em **executar comando de servidor** também.
   
   Como alternativa, você pode definir variáveis de ambiente usando Olá painel de controle do Windows. Isso é uma opção melhor se você quiser tooavoid credenciais de armazenagem no código-fonte / arquivo de projeto. Observe que você precisará toorestart Visual Studio para o aplicativo hello novo ambiente valores toobe toohello disponíveis.
3. Olá código que implementa o repositório de armazenamento de tabela do Azure hello está em **models/azuretablestorage.py**. Consulte Olá [documentação] para obter mais informações sobre como toouse serviço de tabela do Python.
4. Executar o aplicativo hello com `F5`. Pesquisas que são criadas com **criar pesquisas de exemplo** e dados de saudação enviados ao votar serão serializados no armazenamento de tabela do Azure.
   
   > [!NOTE]
   > Olá ambiente Virtual do Python 2.7 pode causar uma interrupção de exceção no Visual Studio.  Pressione `F5` toocontinue carregar Olá web projeto.
   > 
   > 
5. Procurar toohello **sobre** tooverify de página que Olá aplicativo está usando Olá **armazenamento de tabela do Azure** repositório.
   
     ![Navegador da Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Explorar Olá armazenamento de tabela do Azure
É fácil tooview e editar tabelas de armazenamento usando o Gerenciador de nuvem no Visual Studio. Nesta seção, nós usaremos Server Explorer tooview Olá conteúdo Olá sondagens aplicativo tabelas.

> [!NOTE]
> Isso requer toobe de ferramentas do Microsoft Azure instalado, que estão disponíveis como parte da saudação [SDK do Azure para .NET].
> 
> 

1. Abra o **Cloud Explorer**. Expanda **Contas de Armazenamento**, sua conta de armazenamento e, em seguida, **Tabelas**.
   
     ![Gerenciador de Nuvem](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Clique duas vezes em Olá **sondagens** ou **opções** tooview conteúdo de saudação da tabela de saudação em uma janela de documento, bem como adicionar/remover/editar entidades de tabela.
   
     ![Resultados da consulta de tabela](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo
Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo web do serviço de aplicativo.

1. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.
   
     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Clique em **Aplicativos Web do Microsoft Azure**.
3. Clique em **novo** toocreate um novo aplicativo web.
4. Preencha Olá campos a seguir e clique em **criar**.
   
   * **Nome do aplicativo Web**
   * **Plano do Serviço de Aplicativo**
   * **Grupo de recursos**
   * **Região**
   * Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**
5. Aceite todos os outros padrões e clique em **Publicar**.
6. Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados. Se você procurar toohello sobre a página, você verá que ele usa Olá **na memória** repositório, Olá não **armazenamento de tabela do Azure** repositório.
   
   Isso ocorre porque as variáveis de ambiente Olá não são definidas na instância de aplicativos Web de Olá no serviço de aplicativo do Azure, portanto, ele usa valores padrão de saudação especificados em **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Configurar a instância de aplicativos Web Olá
Nesta seção, configuraremos variáveis de ambiente para a instância de aplicativos Web hello.

1. Em [Portal do Azure], abra a folha de seu aplicativo da web hello clicando **procurar** > **serviços de aplicativos** > nome do aplicativo web.
2. Na folha do seu aplicativo Web, clique em **Todas as configurações** depois clique em **Configurações do Aplicativo**.
3. Role para baixo toohello **configurações do aplicativo** seção e definir valores de saudação para **repositório\_nome**, **armazenamento\_nome** e  **ARMAZENAMENTO\_chave** conforme descrito em Olá **projeto de saudação configurar** seção acima.
   
     ![Configurações do aplicativo](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Clique em **Save**. Depois que você recebeu notificações de saudação que alterações Olá foram aplicadas, clique em **procurar** na folha principal do aplicativo Olá Web.
5. Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **armazenamento de tabela do Azure** repositório.
   
   Parabéns!
   
     ![Navegador da Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>Próximas etapas
Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, garrafa e armazenamento de tabela do Azure.

* [Ferramentas Python para documentação do Visual Studio]
  * [Projetos da Web]
  * [Projetos do serviço de nuvem]
  * [Depuração remota no Microsoft Azure]
* [Documentação do Bottle]
* [Armazenamento do Azure]
* [SDK do Azure para Python]
* [Como tooUse Olá serviço de armazenamento de tabela do Python]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentação]:../cosmos-db/table-storage-how-to-use-python.md
[Como tooUse Olá serviço de armazenamento de tabela do Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Portal do Azure]: https://portal.azure.com
[SDK do Azure para .NET]: http://azure.microsoft.com/downloads/
[ferramentas Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do Bottle]: http://bottlepy.org/docs/dev/index.html
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Armazenamento do Azure]: http://azure.microsoft.com/documentation/services/storage/
[SDK do Azure para Python]: https://github.com/Azure/azure-sdk-for-python
