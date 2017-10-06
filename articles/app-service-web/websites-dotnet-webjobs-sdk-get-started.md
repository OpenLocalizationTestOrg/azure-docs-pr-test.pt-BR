---
title: "aaaCreate um WebJob de .NET no serviço de aplicativo do Azure | Microsoft Docs"
description: "Criar um aplicativo de várias camadas usando o MVC ASP.NET e o Azure. Olá front-end executa em um aplicativo web no serviço de aplicativo do Azure e Olá back end executa como um trabalho Web. Olá aplicativo usa o Entity Framework, o banco de dados SQL e filas de armazenamento do Azure e blobs."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Criar um Trabalho Web do .NET no Serviço de Aplicativo do Azure
Este tutorial mostra como toowrite código de um aplicativo ASP.NET MVC 5 multicamado simples que usa Olá [SDK do WebJobs](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Olá finalidade Olá [SDK do WebJobs](websites-webjobs-resources.md) toosimplify Olá código gravar para tarefas comuns que pode executar um trabalho Web, como processamento de imagem, processamento de fila, agregação de RSS, manutenção de arquivo e enviar emails. Olá SDK do WebJobs possui recursos internos para trabalhar com o armazenamento do Azure e o barramento de serviço, para o agendamento de tarefas e tratamento de erros e muitos outros cenários comuns. Além disso, ele tem projetado toobe extensível e há um [repositório do código-fonte aberto para extensões](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

aplicativo de exemplo Hello é um quadro de avisos de publicidade. Os usuários podem carregar imagens para anúncios e um processo de back-end converte Olá imagens toothumbnails. página de lista de ad Olá mostra miniaturas de saudação e página de detalhes do ad Olá mostra a imagem em tamanho normal Olá. Esta é uma captura de tela:

![Lista de anúncios](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Este aplicativo de exemplo funciona com [filas do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) e [blobs do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Olá tutorial mostra como toodeploy Olá aplicativo muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) e [banco de dados do SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Pré-requisitos
Olá tutorial presume que você sabe como toowork com [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projetos no Visual Studio.

tutorial de saudação foi gravado originalmente para Visual Studio 2013, mas pode ser usado com versões posteriores do Visual Studio. Se você estiver usando o Visual Studio 2015 ou 2017, tome nota que, antes de executar o aplicativo hello localmente, você deve alterar Olá `Data Source` parte da cadeia de caracteres de conexão de LocalDB do SQL Server a saudação em arquivos Web. config e App. config de saudação de `Data Source=(localdb)\v11.0` muito`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Você deve ter uma conta do Azure toocomplete este tutorial:
>
> * Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): você obtém créditos que você pode usar tootry out paga serviços do Azure e até mesmo depois que eles são usados para cima, você pode manter Olá conta e usar serviços do Azure gratuitos, como sites. Seu cartão de crédito nunca será cobrado a menos que você explicitamente alterar suas configurações e pergunte toobe cobrado.
> * É possível [ativar os benefícios do Azure mensais para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): sua assinatura concede créditos todos os meses que podem ser usados para experimentar serviços pagos do Azure.
>
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
>
>

## <a id="learn"></a>O que você vai aprender
tutorial de saudação mostra como as tarefas de saudação toodo a seguir:

* Habilite o computador para o desenvolvimento do Azure instalando Olá SDK do Azure (apenas para o Visual Studio 2013 e 2015 usuários).
* Crie um projeto de aplicativo de Console que implanta automaticamente como um trabalho de Web do Azure, quando você implanta o projeto da web associados de saudação.
* Teste um back-end do SDK do WebJobs localmente no computador de desenvolvimento de saudação.
* Publica um aplicativo com um back-end tooa da web no aplicativo WebJobs no serviço de aplicativo.
* Carregar arquivos e armazená-las em Olá serviço Blob do Azure.
* Use Olá SDK do Azure WebJobs toowork com blobs e filas de armazenamento do Azure.

## <a id="contosoads"></a>Arquitetura do aplicativo
usa o aplicativo de exemplo Hello Olá [centrado em fila de trabalho padrão](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga trabalho de saudação com uso intensivo de CPU de criação de processo de back-end tooa miniaturas.

aplicativo Hello armazena anúncios em um banco de dados SQL, usando tabelas de saudação do Entity Framework Code First toocreate e acessar dados de saudação. Para cada anúncio, o banco de dados de saudação armazena duas URLs: uma para imagem em tamanho normal hello e uma miniatura hello.

![Tabela de anúncios](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Quando um usuário carrega uma imagem, Olá web app armazena a imagem de saudação em uma [BLOBs do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e armazena informações de ad Olá no banco de dados de saudação com uma URL que aponta toohello blob. AT Olá mesmo tempo, ele grava um tooan de mensagem da fila do Azure. Em um processo de back-end em execução como um trabalho de Web do Azure, Olá SDK do WebJobs sonda fila Olá novas mensagens. Quando uma nova mensagem for exibida, Olá WebJob cria uma miniatura para essa imagem e atualizações Olá campo de banco de dados em miniatura do URL para que o ad. Aqui está um diagrama que mostra como partes de saudação do aplicativo hello interagem:

![Arquitetura do Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
instruções de tutorial Olá aplicam tooAzure SDK para .NET 2.7.1 ou posterior.

## <a id="storage"></a>Criar uma conta do Armazenamento do Azure
Uma conta de armazenamento do Azure fornece recursos para armazenar dados blob e fila na nuvem hello. Ele também é usado por Olá dados de log de toostore do SDK do WebJobs para o painel de saudação.

Em um aplicativo real, você normalmente cria contas à parte para dados de aplicativo em comparação com dados de registro em log e separa contas para dados de teste em comparação com dados de produção. Neste tutorial você usará apenas uma conta.

1. Olá abrir **Server Explorer** janela no Visual Studio.
2. Saudação de atalho **Azure** nó e, em seguida, clique **conectar tooMicrosoft assinatura do Azure...** .
   
   ![Conecte-se tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Entre utilizando suas credenciais do Azure.
4. Clique com botão direito **armazenamento** em Olá nó do Azure e, em seguida, clique em **criar conta de armazenamento**.
   
   ![Criar conta de armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. Em Olá **criar conta de armazenamento** caixa de diálogo, digite um nome para a conta de armazenamento hello.

    nome da saudação deve ser exclusivo (nenhuma outra conta de armazenamento do Azure pode ter Olá mesmo nome). Se nome hello inserido já está em uso, você obterá uma chance toochange-lo.

    Olá URL tooaccess sua conta de armazenamento será *{name}*. t.
6. Saudação de conjunto **região ou grupo de afinidade** tooyou mais próximo da lista suspensa toohello região.

    Essa configuração especifica qual datacenter do Azure hospedará a conta de armazenamento. Para este tutorial, sua escolha não fará uma diferença notável. No entanto, para um aplicativo da web de produção, você deseja o servidor web e o toobe de conta de armazenamento no hello encargos de saída de dados e latência de toominimize mesma região. aplicativo web de saudação (que você criará mais tarde) datacenter deve estar o mais próximo possíveis navegadores toohello acessando Olá web app na latência de toominimize de ordem.
7. Saudação de conjunto **replicação** suspensa lista muito**localmente redundante**.

    Quando a replicação geográfica é habilitada para uma conta de armazenamento, o conteúdo de Olá armazenado é replicado tooa datacenter secundário tooenable failover toothat local em caso de um grande desastre no local principal hello. A replicação geográfica pode incorrer em custos adicionais. Para contas de teste e desenvolvimento, geralmente você não quiser toopay para replicação geográfica. Para saber mais, confira [Criar, gerenciar ou excluir uma conta de armazenamento](../storage/common/storage-create-storage-account.md).
8. Clique em **Criar**.

    ![Nova conta de armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Baixar o aplicativo hello
1. Baixe e descompacte Olá [concluído solução](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Inicie o Visual Studio.
3. De saudação **arquivo** menu escolha **abrir > projeto/solução**, navegue toowhere baixado solução hello e, em seguida, abra o arquivo de solução de saudação.
4. Pressione a solução de saudação toobuild CTRL + SHIFT + B.

    Por padrão, o Visual Studio automaticamente restaura Olá NuGet conteúdo do pacote, que não foi incluído no hello *. zip* arquivo. Se não restaurar os pacotes de saudação, instalá-los manualmente por vai toohello **gerenciar pacotes NuGet para solução** caixa de diálogo e clicar em Olá **restaurar** botão na parte superior de saudação à direita.
5. Em **Solution Explorer**, certifique-se de que **ContosoAdsWeb** é selecionado como projeto de inicialização de saudação.

## <a id="configurestorage"></a>Configurar Olá aplicativo toouse sua conta de armazenamento
1. Abra o aplicativo hello *Web. config* arquivo hello ContosoAdsWeb projeto.

    arquivo Hello contém uma cadeia de caracteres de conexão SQL e uma cadeia de caracteres de conexão de armazenamento do Azure para trabalhar com blobs e filas.

    saudação de cadeia de caracteres de conexão SQL pontos tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) banco de dados.

    cadeia de caracteres de conexão de armazenamento Olá é um exemplo que tem espaços reservados para a chave de acesso e do nome de conta de armazenamento do hello. Isso será substituído com uma cadeia de caracteres de conexão que tem o nome de saudação e a chave da sua conta de armazenamento.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    cadeia de caracteres de conexão de armazenamento Olá é chamada AzureWebJobsStorage porque é Olá Olá de nome que SDK do WebJobs usa por padrão. saudação de mesmo nome é usado aqui para que você tenha tooset valor de cadeia de caracteres de apenas uma conexão em Olá ambiente do Azure.
2. Em **Server Explorer**, com o botão direito sua conta de armazenamento em Olá **armazenamento** nó e, em seguida, clique **propriedades**.

    ![Clique em Propriedades da Conta de Armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. Em Olá **propriedades** janela, clique em **chaves da conta de armazenamento**e em seguida, clique nas reticências de saudação.

    ![Chaves da conta de armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Saudação de cópia **cadeia de caracteres de Conexão**.

    ![Caixa de diálogo Chaves da Conta de Armazenamento](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Substitua a cadeia de caracteres de conexão de armazenamento a saudação em Olá *Web. config* arquivo com a cadeia de caracteres de conexão de saudação copiado. Certifique-se de que selecionar todos os itens dentro de aspas hello, mas não incluindo Olá aspas antes de colá-lo.
6. Olá abrir *App. config* arquivo hello ContosoAdsWebJob projeto.

    Esse arquivo tem duas cadeias de conexão de armazenamento: uma para dados do aplicativo e outra para registro em log. Você pode usar contas de armazenamento separadas para dados de aplicativo e registro em log, além de usar [várias contas de armazenamento para dados](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Neste tutorial, você usará uma única conta de armazenamento. cadeias de caracteres de conexão Olá tem espaços reservados para chaves de conta de armazenamento hello.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    Por padrão, a saudação SDK do WebJobs procura cadeias de caracteres de conexão chamadas AzureWebJobsStorage e AzureWebJobsDashboard. Como alternativa, você pode [armazenar a cadeia de caracteres de conexão de saudação no entanto, você deseja e passá-lo no explicitamente toohello `JobHost` objeto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Substitua ambas as cadeias de caracteres de conexão de armazenamento com a cadeia de caracteres de conexão de saudação copiados anteriormente.
8. Salve suas alterações.

## <a id="run"></a>Executar o aplicativo hello localmente
1. web toostart Olá front-end do aplicativo hello, pressione CTRL + F5.

    navegador padrão de saudação abre toohello home page. (projeto da web de saudação é executado porque você fez o projeto de inicialização hello.)

    ![Home page dos Anúncios da Contoso](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart Olá WebJob back-end do aplicativo hello, clique com botão direito Olá ContosoAdsWebJob em **Solution Explorer**e, em seguida, clique em **depurar** > **iniciar nova instância** .

    Uma janela do aplicativo de console é aberto e exibe mensagens de log que indica o objeto de trabalhos Web SDK JobHost Olá iniciou toorun.

    ![Janela de aplicativo de console mostrando que back-end hello está em execução](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. No navegador, clique em **Criar um anúncio**.
4. Insira alguns dados de teste, selecione um tooupload de imagem e, em seguida, clique em **criar**.

    ![Criar página](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    aplicativo Hello vai toohello página de índice, mas ela não mostra uma miniatura para ad novo Olá porque não foi feito ainda que o processamento.

    Enquanto isso, após uma curta espera uma mensagem de log na janela de aplicativo de console Olá mostra que uma mensagem da fila foi recebida e foi processada.

    ![Janela do aplicativo de console mostrando que uma mensagem da fila foi processada](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Depois de ver Olá Registrando as mensagens na janela de aplicativo de console hello, atualize Olá índice toosee Olá miniatura.

    ![Página de índice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Clique em **detalhes** para a imagem em tamanho normal do ad toosee hello.

    ![Página de detalhes](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Executa aplicativo hello no computador local e está usando um SQL Server banco de dados localizado em seu computador, mas está trabalhando com filas e blobs no hello nuvem. Em Olá seção a seguir você executará aplicativo hello na nuvem hello, usando um banco de dados de nuvem, bem como filas e blobs de nuvem.  

## <a id="runincloud"></a>Executar o aplicativo hello na nuvem Olá
Isso será feito Olá aplicativo de hello toorun etapas na nuvem Olá a seguir:

* Implante aplicativos tooWeb. O Visual Studio cria automaticamente um novo aplicativo Web no Serviço de Aplicativo e uma instância do Banco de Dados SQL.
* Configure Olá web aplicativo toouse sua conta de armazenamento e de banco de dados do SQL Azure.

Depois de criar alguns anúncios durante a execução na nuvem Olá, você verá Olá Olá toosee de painel de SDK do WebJobs avançado de recursos ele tem toooffer monitoramento.

### <a name="deploy-tooweb-apps"></a>Implantar aplicativos tooWeb

1. Feche o navegador hello e janela de aplicativo de console hello.
2. Siga as etapas de Olá Olá [publicar tooAzure com o banco de dados SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) seção.
3. Depois de concluir as etapas de saudação para implantar, continue com as tarefas restantes Olá neste artigo.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Configurar Olá web aplicativo toouse sua conta de armazenamento e de banco de dados do SQL Azure
É uma prática recomendada de segurança muito[evitar que informações confidenciais, como cadeias de caracteres de conexão nos arquivos que são armazenados em repositórios de código fonte](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). O Azure fornece uma maneira toodo: você pode definir a cadeia de caracteres de conexão e outros valores de configuração no hello ambiente do Azure e APIs de configuração do ASP.NET selecionar automaticamente esses valores quando o aplicativo hello é executado no Azure. Você pode definir esses valores no Azure usando **Server Explorer**, Olá Portal do Azure, o Windows PowerShell, ou Olá interface de linha de comando de plataforma cruzada. Para saber mais, veja [Como funcionam as cadeias de caracteres de aplicativos e de conexão](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

Nesta seção, você deve usar **Server Explorer** tooset valores de cadeia de caracteres de conexão no Azure.

1. No **Gerenciador de Servidores**, clique com o botão direito do mouse no aplicativo Web em **Azure > Serviço de Aplicativo > {seu grupo de recursos}** e clique em **Exibir Configurações**.

    Olá **aplicativo Web do Azure** janela será aberta no hello **configuração** guia.
2. Alterar o nome de saudação do nome de toohello de cadeia de caracteres de conexão do hello DefaultConnection escolhido quando você configurou o banco de dados SQL Olá no Olá [publicar tooAzure com o banco de dados SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artigo.

    Azure criada automaticamente essa cadeia de caracteres de conexão quando você criou Olá web aplicativo com um banco de dados associado, portanto, já tem o valor de cadeia de caracteres de conexão à direita de saudação. Você está alterando apenas o hello nome toowhat que seu código está procurando.
3. Adicione duas novas cadeias de conexão, chamadas AzureWebJobsStorage e AzureWebJobsDashboard. Definir o tipo de banco de dados de saudação muito**personalizado**e o conjunto Olá conexão cadeia valor toohello mesmo valor que você usou anteriormente para Olá *Web. config* e *App. config* arquivos. (Certifique-se incluir a cadeia de caracteres de conexão inteira de hello, não apenas chave de acesso do hello e não inclua aspas hello.)

    Essas cadeias de caracteres de conexão são usadas pelo Olá SDK do WebJobs, um para dados de aplicativos e um para o log. Como você viu anteriormente, Olá para dados de aplicativos também é usado pelo código do Olá web front-end.
4. Clique em **Salvar**.

    ![Cadeias de conexão no Portal do Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. Em **Server Explorer**, clique com botão direito Olá web app e, em seguida, clique em **parar**.
6. Depois de parar aplicativo web de saudação, clique novamente o aplicativo web de saudação e, em seguida, clique em **iniciar**.

   Olá trabalho Web é iniciado automaticamente quando você publicar, mas é interrompido quando você faz uma alteração de configuração. toorestart-lo, você pode reiniciar o aplicativo web de saudação ou reiniciar Olá Olá WebJob [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715). É geralmente recomendado toorestart Olá web aplicativo após uma alteração de configuração.
7. Atualize a janela do navegador de saudação que tem a URL do aplicativo web hello na sua barra de endereços.

    Olá home page aparece.
8. Criar um anúncio, como fez quando você [executado localmente o aplicativo hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   página de índice Olá mostra sem uma miniatura primeiro.
9. Atualize a página de saudação após alguns segundos e hello miniatura é exibida.

   Se a miniatura Olá não aparecer, você poderá ter toowait aproximadamente um minuto para Olá WebJob toorestart. Se após alguns instantes, você ainda não vir miniatura hello quando você atualiza a página hello, Olá trabalho Web pode não ter sido iniciado automaticamente. Nesse caso, vá toohello **serviços de aplicativos** folha em Olá [portal do Azure](https://portal.azure.com/), localize seu aplicativo web e, em seguida, clique em **iniciar**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Saudação de exibição dashboard do SDK do WebJobs
1. Em Olá [portal do Azure](https://portal.azure.com/), selecione Olá **folha de serviços de aplicativo**, localize seu aplicativo web e selecione **WebJobs**.
3. Selecione Olá **Logs** guia.

    ![Guia logs](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Uma nova guia do navegador é aberto toohello painel do SDK do WebJobs. Painel de saudação mostra que Olá trabalho Web está em execução e mostra uma lista de funções em seu código que Olá disparado do SDK do WebJobs.
4. Clique em um dos detalhes de toosee funções hello sobre sua execução.

    ![Painel do SDK de Trabalhos Web](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Painel do SDK de Trabalhos Web](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Olá **função reprodução** botão nesta página faz com que Olá SDK do WebJobs função do framework toocall hello novamente, e ele fornece uma oportunidade toochange Olá dados passados toohello função primeiro.

> [!NOTE]
> Quando tiver terminado de teste, considere a exclusão Olá web app, conta de armazenamento e sua instância de banco de dados SQL. Olá web aplicativo é gratuito, mas hello conta de armazenamento do SQL e a instância de banco de dados acumulam cobranças (embora mínima devido tamanho pequeno toohello). Além disso, se você deixar Olá web aplicativo em execução, qualquer pessoa que localiza a URL pode criar e exibir anúncios. 
>
>

### <a name="delete-your-web-app"></a>Excluir seu aplicativo Web
No portal de hello, vá toohello **serviços de aplicativos** folha, localize e selecione o aplicativo web e, em seguida, clique em **excluir**. Se você quiser apenas tootemporarily impedir que outros usuários de acessar o aplicativo da web de saudação, clique em **parar** em vez disso. Nesse caso, os encargos continuarão tooaccrue para Olá conta de armazenamento e de banco de dados SQL.

### <a name="delete-your-storage-account"></a>Excluir conta de armazenamento
toodelete sua conta de armazenamento, consulte [excluir uma conta de armazenamento](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Excluir banco de dados
toodelete SQL de banco de dados, consulte Olá [API de REST de banco de dados SQL do Azure](https://docs.microsoft.com/rest/api/sql/) documentação.

## <a id="create"></a>Criar aplicativo hello a partir do zero
Nesta seção, você fará Olá seguintes tarefas:

* Criar uma solução do Visual Studio com um projeto Web.
* Adicionar um projeto de biblioteca de classe para dados saudação camada de acesso que é compartilhada entre Olá front-end e back-end.
* Adicione um projeto de aplicativo de Console para o back-end hello, com a implantação de trabalhos Web habilitada.
* Adicionar pacotes NuGet.
* Definir referências de projeto.
* Copie arquivos de código e configuração do aplicativo de aplicativo hello baixado que trabalhou na seção anterior de saudação do tutorial de saudação.
* Examine as partes de saudação do código de saudação que funcionam com filas e blobs do Azure e Olá SDK do WebJobs.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Criar uma solução do Visual Studio com um projeto Web e um projeto de biblioteca de classes
1. No Visual Studio, escolha **Arquivo** > **Novo** > **Projeto**.
2. Em Olá **novo projeto** caixa de diálogo, escolha **Visual C#** > **Web** > **o aplicativo Web do ASP.NET (.NET Framework)**.
3. Nomeie o projeto de saudação ContosoAdsWeb, nomeie a solução Olá ContosoAdsWebJobsSDK (alterar o nome de solução de saudação se estiver colocando ele em Olá mesma pasta Olá baixado solução) e, em seguida, clique em **Okey**.

    ![Novo Projeto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. Em Olá **novo aplicativo Web ASP.NET** caixa de diálogo, escolha o modelo MVC hello e selecione **alterar autenticação**.

    ![Alterar Autenticação](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. Em Olá **alterar autenticação** caixa de diálogo, escolha **sem autenticação**e, em seguida, clique em **Okey**.

    ![Sem Autenticação](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. Em Olá **novo aplicativo Web ASP.NET** caixa de diálogo, clique em **Okey**.

    Visual Studio cria solução hello e o projeto da web de saudação.
7. Em **Solution Explorer**, com o botão direito solução hello (não o projeto de saudação) e escolha **adicionar** > **novo projeto**.
8. Em Olá **adicionar novo projeto** caixa de diálogo, escolha **Visual C#** > **área de trabalho clássica do Windows** > **(.NET da biblioteca de classe Framework)** modelo.  
9. Projeto de saudação do nome *ContosoAdsCommon*e, em seguida, clique em **Okey**.

    Este projeto contém contexto do Entity Framework hello e modelo de dados de saudação que Olá front-end e back-end usará. Como alternativa, você poderia definir classes de relacionada ao EF Olá no projeto da web de saudação e referência de projeto do projeto do WebJob hello. Mas, em seguida, seu projeto WebJob teria um assemblies de tooweb de referência, que não precisa.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Adicionar um projeto de Aplicativo do Console com a implantação de Trabalhos Web habilitada
1. Clique com botão direito Olá web (não de saudação solução ou projeto de biblioteca de classe Olá) e, em seguida, clique em **adicionar** > **novo projeto do Azure WebJob**.

    ![Seleção de menu de Novo Projeto de Trabalho Web do Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. Em hello **adicionar Azure WebJob** caixa de diálogo, digite ContosoAdsWebJob como ambos os Olá **nome do projeto** e hello **o nome do WebJob**. Deixe **modo de execução do WebJob** definido muito**executar continuamente**.
3. Clique em **OK**.

   Visual Studio cria um aplicativo de Console é toodeploy configurado como um trabalho Web sempre que você implantar o projeto da web de saudação. toodo que, ela executada Olá tarefas a seguir depois de criar o projeto de saudação:

   * Adicionado um *settings.json publicar webjob* arquivo na pasta de propriedades de projeto Olá WebJob.
   * Adicionado um *webjobs list.json* arquivo na pasta de propriedades de projeto Olá web.
   * Instalado Olá pacote Microsoft.Web.WebJobs.Publish NuGet no projeto do WebJob hello.

   Para obter mais informações sobre essas alterações, consulte [como toodeploy trabalhos Web usando o Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Adicionar pacotes NuGet
modelo de novo projeto de saudação para um projeto do WebJob instala automaticamente o pacote do NuGet do WebJobs SDK Olá [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) e suas dependências.

Uma saudação dependências SDK do WebJobs que é instalado automaticamente no projeto do WebJob Olá é Olá biblioteca de cliente de armazenamento do Azure (SCL). No entanto, você precisa tooadd-toohello toowork de projeto da web com blobs e filas.

1. Olá abrir **gerenciar pacotes NuGet** caixa de diálogo de solução de saudação.
2. No painel esquerdo do hello, selecione **pacotes instalados**.
3. Localize Olá *armazenamento do Azure* do pacote e, em seguida, clique em **gerenciar**.
4. Em Olá **selecione projetos** caixa, selecione Olá **ContosoAdsWeb** caixa de seleção e, em seguida, clique em **Okey**.

    Todos os três projetos usam saudação do Entity Framework toowork com dados no banco de dados SQL.
5. No painel esquerdo do hello, selecione **Online**.
6. Localize Olá *EntityFramework* NuGet do pacote e instalá-lo em todos os três projetos.

### <a name="set-project-references"></a>Definir referências de projeto
Web e projetos de trabalho Web trabalham com hello banco de dados SQL para que ambos precisam de uma referência de projeto do ContosoAdsCommon toohello.

1. No projeto de ContosoAdsWeb de saudação, defina uma referência de projeto do ContosoAdsCommon toohello. (Clique com botão direito Olá ContosoAdsWeb e, em seguida, clique em **adicionar** > **referência**. 
2. Em Olá **Gerenciador de referências** caixa de diálogo, selecione **projetos** > **solução** > **ContosoAdsCommon**e, em seguida, clique em **Okey**.)
   
    projeto do WebJob Olá precisa referências para trabalhar com imagens e para acessar as cadeias de caracteres de conexão.

4. No projeto de ContosoAdsWebJob hello, defina uma referência muito`System.Drawing` e `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Adicionar código e arquivos de configuração
Este tutorial não mostra como muito[criar controladores MVC e modos de exibição usando o scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), como muito[escrever código do Entity Framework que funciona com bancos de dados do SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), ou [Olá Noções básicas de programação no ASP.NET 4.5 assíncrona](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Portanto, tudo o que permanece toodo é copiar os arquivos de código e configuração de solução Olá baixado na solução novo hello. Depois de fazer isso, hello seções a seguir mostram e explicam as principais partes do código de saudação.

tooadd arquivos tooa projeto ou uma pasta, projeto de saudação do botão direito do mouse ou pasta e clique em **adicionar** > **Item existente**. Selecione Olá arquivos que você deseja e clique em **adicionar**. Se for perguntado se deseja tooreplace os arquivos existentes, clique em **Sim**.

1. No projeto de ContosoAdsCommon hello, exclua Olá *Class1.cs* de arquivo e adicione seu Olá local seguintes arquivos de projeto Olá baixado.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. No projeto de ContosoAdsWeb Olá, adicione Olá seguintes arquivos de projeto Olá baixado.

   * *Web.config*
   * *Global.asax.cs*  
   * Em Olá *controladores* pasta: *AdController.cs*
   * Em Olá *exibições \ compartilhadas* pasta: *cshtml* arquivo
   * Em Olá *Views\Home* pasta: *cshtml*
   * Em Olá *Views\Ad* pasta (criar pasta Olá primeiro): cinco *. cshtml* arquivos
3. No projeto de ContosoAdsWebJob Olá, adicione Olá seguintes arquivos de projeto Olá baixado.

   * *App. config* (alterar o filtro de tipo de arquivo hello muito**todos os arquivos**)
   * *Program.cs*
   * *Functions.cs*

Você agora pode criar, executar e implantar o aplicativo hello conforme instruído anteriormente no tutorial de saudação. Antes de fazer isso, no entanto, pare Olá WebJob ainda está em execução no aplicativo da web primeiro Olá implantada. Caso contrário, esse trabalho Web serão processar mensagens da fila criadas localmente ou por aplicativo hello em execução em um novo aplicativo web, desde que todos estão usando Olá mesmo conta de armazenamento.

## <a id="code"></a>Examine o código do aplicativo hello
Olá, seções a seguir explicam o código de saudação relacionadas tooworking com hello SDK do WebJobs e blobs de armazenamento do Azure e filas.

> [!NOTE]
> Para Olá código específico toohello SDK do WebJobs, vá toohello [Program.cs e Functions.cs](#programcs) seções.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
arquivo de Ad.cs de saudação define um enum de categorias do ad e uma classe de entidade POCO para obter informações do ad.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Olá classe ContosoAdsContext Especifica que a classe de Ad de saudação é usada em uma coleção DbSet, que armazena o Entity Framework em um banco de dados SQL.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

classe de saudação tem dois construtores. Olá primeiro é usado pelo projeto da web de saudação e especifica Olá nome de uma cadeia de conexão que é armazenada no arquivo Web. config de saudação ou ambiente de tempo de execução do Azure hello. construtor segundo Olá permite que você toopass na cadeia de caracteres de conexão real hello. Necessário ao projeto do WebJob Olá porque ele não tem um arquivo Web. config. Você viu anteriormente em que essa cadeia de caracteres de conexão foi armazenada, e você verá posteriormente como código Olá recupera a cadeia de caracteres de conexão de saudação quando ele cria a classe DbContext de saudação.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
Olá `BlobInformation` classe é usada toostore informações sobre um blob de imagem em uma mensagem da fila.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Código que é chamado de hello `Application_Start` método cria um *imagens* contêiner de blob e uma *imagens* fila se ainda não existirem. Isso garante que, sempre que você começar a usar uma nova conta de armazenamento, Olá necessários fila e o contêiner de blob são criadas automaticamente.

Olá conta de armazenamento do código obtém acesso toohello usando a cadeia de conexão de armazenamento de saudação do hello *Web. config* arquivo ou ambiente de tempo de execução do Azure.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Em seguida, ele obtém uma referência toohello *imagens* contêiner de blob, cria o contêiner de saudação se ele ainda não existir, conjuntos de permissões e acesso no novo contêiner de saudação. Por padrão, novos contêineres permitem somente a clientes com blobs de tooaccess de credenciais de conta de armazenamento. aplicativo web de saudação precisa Olá blobs toobe público para que ele possa exibir imagens usando URLs que blobs de imagem toohello ponto.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Um código semelhante obtém uma referência toohello *thumbnailrequest* de fila e cria uma nova fila. Nesse caso, nenhuma alteração de permissão é necessária.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Olá *cshtml* arquivo define o nome do aplicativo Olá Olá cabeçalho e rodapé e cria uma entrada de menu "Anúncios".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Olá *Views\Home\Index.cshtml* arquivo exibe links de categoria na home page do hello. Olá links passam o valor inteiro Olá Olá `Category` enum em uma página de índice de anúncios de toohello variável de querystring.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Em Olá *AdController.cs* arquivo, chamadas de construtor Olá Olá `InitializeStorage` objetos de biblioteca de cliente de armazenamento do Azure do método toocreate que fornecem uma API para trabalhar com blobs e filas.

Em seguida, o código de Olá obtém uma referência toohello *imagens* contêiner de blob que você viu anteriormente na *Global.asax.cs*. Enquanto faz isso, ele define uma [política de repetição](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) padrão apropriada para um aplicativo Web. política de repetição de retirada exponencial saudação padrão pode travar Olá web app para mais de um minuto em várias tentativas para uma falha temporária. política de repetição de saudação especificada aqui aguarda três segundos após cada tente para backup toothree tentativas.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Um código semelhante obtém uma referência toohello *imagens* fila.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

A maioria do código do controlador Olá é comum para trabalhar com um modelo de dados do Entity Framework usando uma classe DbContext. Uma exceção é hello HttpPost `Create` método, que carrega um arquivo e o salva no armazenamento de blob. associador de modelo Olá fornece um [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método do objeto.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Se o usuário Olá selecionado tooupload um arquivo, código Olá carrega o arquivo hello, salva-o em um blob e atualiza o registro de banco de dados do Ad Olá com uma URL que aponta toohello blob.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Olá código Olá carregamento está em Olá `UploadAndSaveBlobAsync` método. Ele cria um nome GUID para o blob de hello, carrega e salva Olá arquivo e retorna um blob de referência toohello salvada.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

Depois de saudação HttpPost `Create` método carrega um blob e atualizações Olá banco de dados, ele cria um fila mensagem tooinform Olá processo back-end que uma imagem está pronta para a miniatura de tooa de conversão.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Olá código para hello HttpPost `Edit` método é semelhante, exceto que se o usuário Olá seleciona um novo arquivo de imagem, todos os blobs que já existem para este anúncio devem ser excluídos.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Aqui está o código de saudação que exclui os blobs quando você exclui um anúncio:

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml
Olá *cshtml* arquivo exibe miniaturas com hello outros dados do ad:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Olá *Details.cshtml* arquivo exibe a imagem em tamanho normal hello:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml e Edit.cshtml
Olá *Create.cshtml* e *Edit.cshtml* arquivos especificam que habilita Olá Olá do controlador tooget de codificação de formulário `HttpPostedFileBase` objeto.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Um `<input>` elemento informa Olá navegador tooprovide uma caixa de diálogo de seleção de arquivo.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Quando Olá WebJob inicia, hello `Main` chamadas de método hello SDK do WebJobs `JobHost.RunAndBlock` execução do método toobegin funções disparada no thread atual hello.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - método GenerateThumbnail
Olá SDK do WebJobs chama este método quando é recebida uma mensagem da fila. método Hello cria uma miniatura e coloca Olá miniatura URL no banco de dados de saudação.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Olá `QueueTrigger` atributo direciona Olá SDK do WebJobs toocall este método quando uma nova mensagem é recebida na fila de thumbnailrequest hello.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Olá `BlobInformation` objeto na mensagem da fila de saudação é automaticamente desserializado em Olá `blobInfo` parâmetro. Quando o método hello for concluído, mensagem de saudação do fila é excluída. Se o método hello falhar antes da conclusão, mensagem de saudação do fila não será excluída; Depois que uma concessão de 10 minutos expira, mensagem de saudação é lançada toobe pegou novamente e processado. Essa sequência não será repetida indefinidamente se uma mensagem sempre causar uma exceção. Depois de 5 malsucedida tentativas tooprocess uma mensagem, mensagem de saudação é movido tooa fila denominada {queuename}-suspeitas. Olá o número máximo de tentativas é configurável.
* Olá dois `Blob` atributos fornecem objetos que estão associadas tooblobs: um blob de imagem existente toohello e um tooa novo em miniatura blob criado pelo método hello.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Nomes de blob vêm de propriedades de saudação do `BlobInformation` objeto recebido na mensagem da fila de saudação (`BlobName` e `BlobNameWithoutExtension`). tooget Olá todas as funcionalidades de saudação biblioteca de cliente de armazenamento, você pode usar o hello `CloudBlockBlob` toowork de classe com blobs. Se você quiser tooreuse código escrito toowork com `Stream` objetos, você pode usar o hello `Stream` classe.

Para obter mais informações sobre como toowrite funções que usam atributos de SDK do WebJobs, consulte Olá recursos a seguir:

* [Como o armazenamento com hello SDK do WebJobs de fila toouse do Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Como toouse Azure blob storage com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Como o armazenamento com hello SDK do WebJobs de tabela toouse do Azure](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Como toouse de barramento de serviço do Azure com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Se seu aplicativo web é executado em várias VMs, vários trabalhos de Web serão executados simultaneamente e em alguns cenários, isso pode resultar em Olá mesmo dados obtendo processados várias vezes. Isso não é um problema se você usar fila interna hello, blob e gatilhos de barramento de serviço. Olá SDK garante que as funções serão processadas apenas uma vez para cada mensagem ou blob.
> * Para obter informações sobre como tooimplement de desligamento normal, consulte [desligamento](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Olá código Olá `ConvertImageToThumbnailJPG` método (não mostrado) usa classes Olá `System.Drawing` namespace para simplificar. No entanto, as classes nesse namespace Olá foram projetados para uso com o Windows Forms. Elas não têm suporte para uso em um serviço Windows ou ASP.NET. Para obter mais informações sobre opções de processamento de imagem, consulte [Geração dinâmica de imagem](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Visão aprofundada de redimensionamento de imagens](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você viu um aplicativo de multicamada simples que usa Olá SDK do WebJobs para o processamento de back-end. Esta seção oferece algumas sugestões para saber mais sobre os aplicativos ASP.NET com várias camadas e Trabalhos Web.

### <a name="missing-features"></a>Recursos ausentes
aplicativo Hello foi mantido simple para obter um tutorial de Introdução. Em um aplicativo do mundo real, você poderia implementar [injeção de dependência](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) e hello [repositório e unidade de trabalho padrões](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [uma interface para registro em log](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [ Migrações do Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage dados alterações do modelo e usar [resiliência de Conexão EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage erros de rede transitório.

### <a name="scaling-webjobs"></a>Dimensionamento de trabalhos
Os trabalhos Web executado no contexto de saudação de um aplicativo web e não é escalonáveis separadamente. Por exemplo, se você tiver uma instância de aplicativo da web padrão, você tem apenas uma instância do processo em segundo plano em execução e está usando alguns Olá recursos do servidor (CPU, memória, etc.) que de outro modo seria tooserve disponíveis de conteúdo web.

Se o tráfego varia por hora do dia ou dia da semana, e se Olá back-end de processamento é necessário toodo pode esperar, foi possível agendar o toorun WebJobs em momentos de pouco tráfego. Se a carga de saudação ainda é muito alta para essa solução, você pode executar Olá back-end como um trabalho Web em um aplicativo web separado dedicado para essa finalidade. Em seguida, você pode dimensionar seu aplicativo Web de back-end independentemente do seu aplicativo Web de front-end.

Para saber mais, veja [Dimensionando WebJobs](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Evitando desligamentos de tempo limite de aplicativo Web
toomake-se de que seus WebJobs sempre estão em execução e em execução em todas as instâncias de seu aplicativo web, você tem Olá tooenable [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) recurso.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>Usando Olá SDK do WebJobs fora do WebJobs
Um programa que usa o SDK do WebJobs de saudação não tem toorun no Azure em um trabalho Web. Ele pode ser executado localmente e também pode ser executado em outros ambientes, como em uma função de trabalho do serviço de nuvem ou um serviço Windows. No entanto, você pode acessar somente Olá painel do SDK do WebJobs por meio de um aplicativo web do Azure. Painel de saudação toouse ter tooconnect Olá web aplicativo toohello conta de armazenamento usada ao definir a cadeia de caracteres de conexão do hello AzureWebJobsDashboard em Olá **configurar** guia do portal clássico do hello. Em seguida, você pode obter toohello painel usando Olá URL a seguir:

https://{NomeDoAplicativoWeb}.scm.azurewebsites.net/azurejobs/#/functions

Para obter mais informações, consulte [obtendo um painel para desenvolvimento local com hello SDK do WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), mas observe que ela mostra um nome de cadeia de caracteres de conexão antigo.

### <a name="more-webjobs-documentation"></a>Mais documentação de Trabalhos Web
Para sabe r mais, consulte [Recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?LinkId=390226).
