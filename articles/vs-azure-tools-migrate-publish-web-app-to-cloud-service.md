---
title: "aaaHow tooMigrate e publicar um aplicativo Web tooan do serviço em nuvem do Azure do Visual Studio | Microsoft Docs"
description: "Saiba como toomigrate e publicar seu aplicativo de web tooan serviço de nuvem do Azure usando o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Como: migrar e publicar um aplicativo Web de tooan serviço de nuvem do Azure do Visual Studio
aproveitar tootake Olá serviços de hospedagem e a escalabilidade do Azure, você pode desejar toomigrate e publicar seu serviço de nuvem do Azure de tooan do aplicativo web. Você pode executar um aplicativo web no Azure com o aplicativo de tooyour alterações mínimas.

> [!NOTE]
> Este tópico é sobre como implantar serviços toocloud, não tooweb sites. Para obter informações sobre como implantar sites tooweb, consulte [implantar um aplicativo web no serviço de aplicativo do Azure](app-service-web/web-sites-deploy.md).
>
>

Para obter uma lista de modelos específicos com suporte para o Visual c# e Visual Basic, consulte a seção de saudação **suporte para modelos de projeto** mais adiante neste tópico.

Primeiro, você precisa habilitar o aplicativo Web para o Azure por meio do Visual Studio. Olá ilustração a seguir mostra Olá principais etapas toopublish o aplicativo web existente adicionando um toouse de projeto do Azure para a implantação. Esse processo adiciona um projeto do Azure com a solução de tooyour de função hello necessário da web. Com base no tipo de saudação do projeto da web que você tem, propriedades do projeto Olá para assemblies também são atualizadas quando o pacote de serviço Olá exigir assemblies adicionais para a implantação.

![Publicar um aplicativo de Web tooMicrosoft do Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Olá **converter**, **converter tooAzure projeto de serviço de nuvem** comando é exibido somente para o projeto da web de saudação em sua solução. Por exemplo, o comando Olá não está disponível para um projeto do Silverlight em sua solução.
> Quando você cria um pacote de serviço ou publica seu aplicativo tooAzure, avisos ou erros podem ocorrer. Esses avisos e erros podem ajudá-lo a corrigir problemas antes de implantar tooAzure. Por exemplo, você pode receber um aviso sobre um assembly ausente. Para obter mais informações sobre como tootreat todos os avisos como erros, consulte [configurar um projeto de serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Se você cria seu aplicativo, executá-lo localmente usando o emulador de computação hello ou publicá-lo tooAzure, talvez você veja Olá após erro em Olá **lista de erros** janela: **Olá especificado caminho, nome de arquivo, ou ambos são muito longos** . Esse erro ocorre porque o comprimento de saudação do nome totalmente qualificado do projeto do Azure da saudação é muito longo. comprimento de saudação do nome do projeto hello, incluindo o caminho completo do hello, não pode ser mais de 146 caracteres. Por exemplo, este é o nome completo do projeto de saudação inclui o caminho para um projeto do Azure que é criado para um aplicativo do Silverlight: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Você pode ter toomove solução tooa diferentes diretório que tem um comprimento menor caminho tooreduce saudação do nome totalmente qualificado do projeto de saudação.
>
>

toomigrate e publicar um tooAzure de aplicativo web do Visual Studio, siga estas etapas.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Habilitar um aplicativo Web para implantação tooAzure
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable um aplicativo web para implantação tooAzure
1. tooenable o aplicativo web para implantação tooAzure, menu de atalho Olá aberto para um web do projeto em sua solução e escolha Adicionar projeto de implantação do Azure.

    Olá ações a seguir ocorre:

   * Um projeto do Azure chamado `<name of hello web project>.Azure` é adicionado toohello solução para seu aplicativo.
   * Uma função web para o projeto da web de saudação é adicionada toothis projeto do Azure.
   * Olá **Copy Local** propriedade está definida tootrue para todos os assemblies que são necessários para MVC 2, MVC 3, MVC 4 e aplicativos de negócios Silverlight. Isso adiciona o pacote de serviço de toohello esses assemblies que é usado para a implantação.

   > [!IMPORTANT]
   > Se você tiver outros assemblies ou arquivos que são necessários para este aplicativo web, você deve definir propriedades Olá para esses arquivos manualmente. Para obter informações sobre como tooset essas propriedades, consulte Olá seção **incluir arquivos no hello pacote de serviço** posteriormente neste artigo.
   >
   > [!NOTE]
   > Se já existe uma função web para um projeto da web específicos em um projeto do Azure na solução de saudação **converter**, **converter o projeto de serviço de nuvem do tooAzure** não é exibido no menu de atalho Olá para este projeto da web .
   >
   >

   Se você tiver vários projetos da web em seu aplicativo web e você deseja ter funções web toocreate para cada projeto da web, você deve executar etapas de saudação neste procedimento para cada projeto da web. Isso cria projetos do Azure separados para cada função web. Cada projeto Web pode ser publicado separadamente. Como alternativa, você pode adicionar manualmente outra função tooan existente do Azure projeto web em seu aplicativo web. toodo, menu de atalho Olá aberto para Olá **funções** pasta em seu projeto do Azure, escolha **adicionar**, em seguida, **projeto de função Web na solução**, escolha Olá tooadd de projeto como uma web função e, em seguida, escolha Olá **Okey** botão.

## <a name="use-an-azure-sql-database-for-your-application"></a>Usar um Banco de Dados SQL do Azure para seu aplicativo
Se você tiver uma cadeia de caracteres de conexão para o aplicativo web que usa um banco de dados do SQL Server local hello, você deve alterar essa cadeia de caracteres de conexão toouse uma instância do banco de dados SQL que hospeda do Azure em vez disso.

> [!IMPORTANT]
> Sua assinatura deve habilitá-lo toouse banco de dados SQL. Se você acessar sua assinatura do hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você pode determinar quais serviços sua assinatura fornece. Olá instruções a seguir se aplicam toohello liberado [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Se você estiver usando Olá [portal do Azure](http://portal.microsoft.com), ignore toohello próximo procedimento.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse uma instância de banco de dados SQL em sua função web para sua cadeia de conexão
1. toocreate uma instância do banco de dados SQL em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), siga as etapas de Olá Olá artigo a seguir: [criar um servidor de banco de dados do SQL](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Quando você configura as regras de firewall Olá para sua instância do banco de dados SQL, você deve selecionar Olá **permitir que outros serviços do Azure tooaccess este servidor** caixa de seleção.
   >
   >
2. toocreate uma instância do banco de dados SQL toouse para sua cadeia de conexão, execute as etapas de saudação na próxima seção Olá Olá artigo a seguir: [criar um banco de dados do SQL](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toouse de cadeia de caracteres de conexão toocopy Olá ADO.NET para sua cadeia de conexão, execute Olá etapas Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Escolha Olá **banco de dados** botão e nó hello, em seguida, abra para assinatura Olá usado toocreate sua instância do banco de dados SQL.
   2. instâncias disponíveis do hello toodisplay de banco de dados SQL, escolha Olá **bancos de dados SQL** nó.
   3. Propriedades de saudação toodisplay para banco de dados Olá, escolha o banco de dados de hello. Olá **propriedades** exibição aparece.

      > [!NOTE]
      > Se hello **propriedades** exibição não for exibido, talvez seja necessário tooopen usando Olá divisor.
      >
      >
   4. cadeias de conexão do toodisplay hello, escolha tooView próximo do botão Olá reticências (...).

      Olá **cadeias de caracteres de Conexão** caixa de diálogo é exibida.
   5. Olá toocopy cadeia de caracteres de conexão ADO.NET, realce o texto de saudação e escolha as teclas Ctrl + C de saudação.
   6. caixa de diálogo tooclose Olá caixa, escolha Olá **fechar** botão.
4. conexão de saudação tooreplace cadeia de caracteres de Olá Web. config arquivo toouse esta instância do banco de dados SQL, abra o arquivo Web. config de saudação, realce a entrada de cadeia de caracteres de conexão existente hello e escolha teclas Ctrl + V de saudação. Olá cadeia de conexão ADO.NET para instância de saudação do banco de dados SQL substitui a cadeia de conexão existente hello.
5. Você também deve adicionar o parâmetro hello `MultipleActiveResultSets=True` toohello cadeia de caracteres de conexão. cadeia de caracteres de conexão Olá deve ter Olá formato a seguir:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Opcional) Uma cadeia de caracteres de conexão do método alternativo toochanging Olá diretamente no arquivo Web. config de saudação é tooadd uma seção em um dos arquivos de transformação do Web. config hello, dependendo da configuração de compilação de saudação que você use toocreate seu pacote de serviço. Abra um Olá Web.Debug.Config arquivo ou Olá Web.Release.Config. Adicione Olá seção a seguir no arquivo:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Salvar arquivo hello modificado e republique o seu aplicativo.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>uma instância do banco de dados SQL por meio de toouse Olá portal clássico do Azure
1. Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), escolha o nó de bancos de dados SQL hello.

   * Se a instância de saudação do banco de dados SQL que você deseja toouse for exibida, escolha tooopen-lo.
   * Se você não criou nenhuma instância, escolha o link apropriado hello e, em seguida, crie uma instância.
2. Depois que você abrir ou cria uma instância de banco de dados, escolha Olá **cadeias de caracteres de Conexão** link.
3. Final Olá Olá página, escolha Olá link tooconfigure configurações do firewall e aceite os valores padrão de saudação ou configurar Olá valores que você precisa.
4. Copie a cadeia de conexão ADO.NET Olá, cole-o em seu arquivo Web. config em cadeia de conexão antiga Olá para banco de dados de local de saudação e ser tooadd se `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Publicar um aplicativo Web tooAzure
### <a name="toopublish-a-web-application-tooazure"></a>toopublish um tooAzure de aplicativo Web
1. aplicativo de hello tootest no ambiente de desenvolvimento local hello usando o emulador de computação do Azure Olá, menu de atalho de Olá aberto de saudação do Azure de projeto para a função de web hello e escolha **definir como projeto de inicialização**. Em seguida, escolha **Depurar**, **Iniciar depuração** (teclado: **F5**).

    Olá **Olá iniciar o ambiente de depuração do Azure** caixa de diálogo é aberta e o aplicativo hello inicia no navegador Olá. Para obter detalhes específicos sobre como toostart cada tipo de aplicativo web no hello emulador de computação, consulte a tabela Olá nesta seção.
2. tooset os serviços de saudação para tooAzure de toopublish seu aplicativo, você deve ter uma conta da Microsoft e uma assinatura do Azure. Olá Use as etapas em Olá tópico tooset os seus serviços a seguir: [preparar toopublish ou implantar um aplicativo do Azure do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish Olá web aplicativo tooAzure, abra Olá menu de atalho Olá web projeto e escolha **publicar tooAzure**.

    Olá **publicar aplicativo do Azure** caixa de diálogo é aberta e o Visual Studio inicia o processo de implantação hello. Para obter mais informações sobre como toopublish Olá aplicativo, consulte a seção de saudação **publicar um aplicativo do Azure do Visual Studio** na [publicando um serviço de nuvem usando ferramentas do Azure Olá](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > Você também pode publicar o aplicativo da web de saudação do hello projeto do Azure. toodo isso, abra o menu de atalho de saudação de saudação projeto do Azure e escolha **publicar**.
   >
   >
4. progresso de saudação do toosee de implantação de saudação, você pode exibir hello **o Log de atividades do Azure** janela. Esse log é exibido automaticamente quando o processo de implantação Olá inicia. Você pode expandir o item de linha de saudação no log de atividades de saudação tooshow informações detalhadas, como mostrado na ilustração a seguir de saudação:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Processo de implantação de saudação toocancel (opcional), abra o menu de atalho de saudação de item de linha de saudação no log de atividades de saudação e escolha **Cancelar e remover**. Isso interrompe o processo de implantação de saudação e exclui o ambiente de implantação de saudação do Azure.

   > [!NOTE]
   > tooremove esse ambiente de implantação depois que ele tiver sido implantado, você deve usar Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Opcional) Depois que suas instâncias de função forem iniciadas, o Visual Studio mostra automaticamente o ambiente de implantação Olá no hello **de computação do Azure** nó **Cloud Explorer** ou **Server Explorer**. Aqui você pode exibir o status de Olá Olá individuais de instâncias de função.

    Olá, ilustração a seguir mostra instâncias de função hello em **Server Explorer** enquanto eles ainda estão no estado Inicializando da saudação:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess seu aplicativo após a implantação, escolha Olá seta próxima tooyour implantação quando o status de **concluído** aparece no hello **log de atividades do Azure**. Isso exibe a URL de saudação do seu aplicativo web no Azure. Consulte Olá para obter detalhes de saudação sobre como toostart um determinado tipo de aplicativo web do Azure a tabela a seguir.

    Olá, a tabela a seguir lista os detalhes de Olá sobre como toostart aplicativos web do Azure ou toorun ou depurar um aplicativo web localmente usando Olá emulador de computação do Azure:

   | Tipo de aplicativo Web | Olá executar/depurar localmente usando o emulador de computação | em execução no Azure |
   | --- | --- | --- |
   | Aplicativo Web do ASP.NET |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Escolha Olá hiperlink da URL exibida em Olá **implantação** guia Olá **log de atividades do Azure** página de início de saudação tooload no navegador de saudação. |
   | Aplicativo Web ASP.NET MVC 2 |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Escolha Olá hiperlink da URL exibida em Olá **implantação** guia Olá **log de atividades do Azure** página de início de saudação tooload no navegador de saudação. |
   | Aplicativo Web ASP.NET MVC 3 |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Escolha Olá hiperlink da URL exibida em Olá **implantação** guia Olá **log de atividades do Azure** página de início de saudação tooload no navegador de saudação. |
   | Aplicativo Web ASP.NET MVC 4 |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Escolha Olá hiperlink da URL exibida em Olá **implantação** guia Olá **log de atividades do Azure** página de início de saudação tooload no navegador de saudação. |
   | Aplicativo Web ASP.NET vazio |Você deve adicionar uma página. aspx no seu aplicativo que você definir como página inicial de saudação do projeto web. Em seguida, na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Se você tiver uma página. aspx padrão em seu aplicativo, escolha o hiperlink da URL de saudação exibido no hello **implantação** guia Olá **log de atividades do Azure** e essa página for carregada no navegador de saudação. Se você tiver uma página. aspx diferente, você precisa toonavigate toothis página específica usando Olá formato a seguir para sua url:`<url for deployment>/<name of page>.aspx` |
   | Aplicativo Silverlight |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Você precisará toonavigate toohello uma página específica para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of page>.aspx` |
   | Aplicativo de negócios Silverlight |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Você precisará toonavigate toohello uma página específica para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of page>.aspx` |
   | Aplicativo de navegação Silverlight |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Você precisará toonavigate toohello uma página específica para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of page>.aspx` |
   | Aplicativo de serviço WCF |Você deve definir o arquivo. svc de saudação saudação inicial página para seu projeto de serviço do WCF. Em seguida, na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |É necessário um arquivo do toonavigate toohello svc para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of service file>.svc` |
   | Aplicativo de serviço de fluxo de trabalho WCF |Você deve definir o arquivo. svc de saudação saudação inicial página para seu projeto de serviço do WCF. Em seguida, na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |É necessário um arquivo do toonavigate toohello svc para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of service file>.svc` |
   | Entidades dinâmicas do ASP.NET |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Você deve atualizar a cadeia de caracteres de conexão de saudação (consulte a próxima seção). Você também precisa toonavigate toohello uma página específica para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of page>.aspx` |
   | TooSQL de Linq de dados dinâmicos do ASP.NET |Na barra de menus do hello, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Você deve seguir etapas neste procedimento Olá: usar um banco de dados do SQL Azure para seu aplicativo (consulte a seção anterior neste tópico). Você também precisa toonavigate toohello uma página específica para seu aplicativo usando Olá formato a seguir para sua url:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Atualizar uma cadeia de conexão para Entidades dinâmicas do ASP.NET
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate uma cadeia de caracteres de Conexão para entidades dinâmicas do ASP.NET
1. toocreate um banco de dados do SQL Azure que pode ser usado para um aplicativo da web de entidades dinâmicas do ASP.NET, siga as etapas de saudação do procedimento de saudação **usar um banco de dados do SQL Azure para seu aplicativo** anteriormente neste tópico.
2. Adicionar tabelas hello e campos que você precisa para esse banco de dados Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
3. cadeia de caracteres de conexão de saudação para esse tipo de aplicativo tem Olá formato no arquivo Web. config de saudação a seguir:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Saudação de atualização *connectionString* valor com hello cadeia de conexão ADO.NET para seu banco de dados do SQL Azure da seguinte maneira:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. toosave Olá Web. config com alterações Olá feitas toohello cadeia de conexão, na barra de menus Olá escolha **arquivo**, **salvar o Web. config**.

## <a name="supported-project-templates"></a>Modelos de projeto com suporte
toopublish um tooAzure de aplicativo web, aplicativo hello deve usar um dos modelos de projeto Olá para c# ou Visual Basic que está listado na tabela de saudação abaixo.

| Grupo de modelos de projeto | Modelo do projeto |
| --- | --- |
| Web |Aplicativo Web do ASP.NET |
| Web |Aplicativo Web ASP.NET MVC 2 |
| Web |Aplicativo Web ASP.NET MVC 3 |
| Web |Aplicativo Web ASP.NET MVC 4 |
| Web |Aplicativo Web ASP.NET vazio |
| Web |Aplicativo Web ASP.NET MVC 2 vazio |
| Web |Aplicativo Web de entidades de dados dinâmicos ASP.NET |
| Web |TooSQL de Linq de dados dinâmicos do ASP.NET aplicativo Web |
| Silverlight |Aplicativo Silverlight |
| Silverlight |Aplicativo de negócios Silverlight |
| Silverlight |Aplicativo de navegação Silverlight |
| WCF |Aplicativo de serviço WCF |
| WCF |Aplicativo de serviço de fluxo de trabalho WCF |
| Fluxo de trabalho |Aplicativo de serviço de fluxo de trabalho WCF |

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a publicação, consulte [preparar tooPublish ou implantar um aplicativo do Azure do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Confira também [Configuração de credenciais de autenticação nomeadas](vs-azure-tools-setting-up-named-authentication-credentials.md).
