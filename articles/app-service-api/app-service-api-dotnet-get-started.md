---
title: "aaaGet iniciado com aplicativos de API e o ASP.NET no serviço de aplicativo | Microsoft Docs"
description: "Saiba como toocreate, implantar e consumir um aplicativo de API do ASP.NET no serviço de aplicativo do Azure, usando o Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Introdução aos aplicativos de API, ASP.NET e Swagger no Serviço de Aplicativo do Azure
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Isso é hello primeiro em uma série de tutoriais que mostram como serviço toouse recursos do aplicativo do Azure que são úteis para desenvolver e hospedar APIs RESTful.  Este tutorial aborda o suporte para metadados de API no formato Swagger.

Você aprenderá a:

* Como toocreate e implantar [aplicativos de API](app-service-api-apps-why-best-platform.md) no serviço de aplicativo do Azure usando ferramentas integradas ao Visual Studio 2015.
* Como o pacote de Swashbuckle NuGet descoberta tooautomate API usando Olá toodynamically gerar metadados do Swagger API.
* Como tooautomatically de metadados do Swagger API toouse gerar o código do cliente para um aplicativo de API.

## <a name="sample-application-overview"></a>Visão geral do aplicativo de exemplo
Neste tutorial, você trabalha com um aplicativo de exemplo de lista de tarefas simples. aplicativo Hello tem um front-end do aplicativo de página única (SPA), uma camada intermediária da API Web do ASP.NET e uma camada de dados de API da Web ASP.NET.

![Diagrama do aplicativo de exemplo de Aplicativos de API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Aqui está uma captura de tela de saudação [AngularJS](https://angularjs.org/) front-end.

![Lista de toodo de aplicativo de exemplo de aplicativos de API](./media/app-service-api-dotnet-get-started/todospa.png)

Olá solução do Visual Studio inclui três projetos:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -front-end Olá: um SPA AngularJS que chama a camada intermediária hello.
* **ToDoListAPI** -camada intermediária Olá: um projeto de API da Web ASP.NET que chama a camada de dados Olá tooperform as operações CRUD em itens de tarefas pendentes.
* **ToDoListDataAPI** -camada de dados Olá: um projeto de API da Web ASP.NET que executa operações CRUD de itens pendentes.

arquitetura de três camadas de saudação é uma das muitas arquiteturas que você pode implementar usando aplicativos de API e é usado aqui apenas para fins de demonstração. código de saudação em cada camada é tão simple quanto possível toodemonstrate recursos de aplicativos de API; Por exemplo, a camada de dados Olá usa memória do servidor, em vez de um banco de dados como seu mecanismo de persistência.

Ao concluir este tutorial, você terá dois projetos de API da Web Olá para cima e em execução na nuvem de saudação em aplicativos de API do serviço de aplicativo.

tutorial Avançar Olá série de saudação implanta a nuvem de toohello Olá SPA front-end.

## <a name="prerequisites"></a>Pré-requisitos
* ASP.NET Web API - Olá instruções de tutorial presumem que você tenha um conhecimento básico de como toowork com o ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) no Visual Studio.
* Conta do Azure ‒ você pode [Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) ou [Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/). Lá, você poderá criar imediatamente um aplicativo de curta duração inicial no Serviço de Aplicativo — **sem exigência de cartão de crédito**e sem compromisso.
* Visual Studio 2015 com hello [SDK do Azure para .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -Olá SDK instala o Visual Studio 2015 automaticamente se você ainda não o fez.
  
  * No Visual Studio, clique em Ajuda -> Sobre o Microsoft Visual Studio e verifique se você tem "Ferramentas do Serviço de Aplicativo do Azure v2.9.1" ou superior instalado.
    
    ![Versão das Ferramentas de Aplicativo do Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > Dependendo de quantos das dependências do SDK Olá você já tiver em seu computador, Olá instalar SDK pode levar muito tempo, de alguns minutos tooa meia hora ou mais.
    > 
    > 

## <a name="download-hello-sample-application"></a>Baixe o aplicativo de exemplo hello
1. Baixar Olá [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repositório.
   
    Você pode clicar em Olá **baixar ZIP** botão ou clone do repositório de saudação em seu computador local.
2. Abra a solução de lista de tarefas pendentes de Olá no Visual Studio 2015 ou 2013.
   
   1. Você precisará tootrust cada solução.
         ![Aviso de Segurança](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Crie pacotes do NuGet Olá solução (CTRL + SHIFT + B) toorestore hello.
   
    Se você quiser toosee aplicativo hello operação antes de implantá-lo, você pode executá-lo localmente. Certifique-se de que ToDoListDataAPI é o projeto de inicialização e a solução de saudação de execução. Você deve esperar o erro toosee um HTTP 403 em seu navegador.

## <a name="use-swagger-api-metadata-and-ui"></a>Usar a interface do usuário e metadados de API do Swagger
O suporte a metadados da API 2.0 do [Swagger](http://swagger.io/) é integrado ao Serviço de Aplicativo do Azure. Cada aplicativo de API pode especificar um ponto de extremidade de URL que retorna metadados para Olá API no formato JSON Swagger. Olá retornado do ponto de extremidade de metadados podem ser usado toogenerate o código do cliente.

Um projeto de API da Web ASP.NET pode gerar dinamicamente os metadados do Swagger usando Olá [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pacote NuGet. Olá pacote Swashbuckle NuGet já está instalado em projetos Olá ToDoListDataAPI e ToDoListAPI que você baixou.

Nesta seção do tutorial hello, examinar metadados do Swagger 2.0 Olá gerado e, em seguida, experimente um teste de interface do usuário com base nos metadados do Swagger hello.

1. Definir Olá ToDoListDataAPI projeto (**não** projeto de ToDoListAPI Olá) como o projeto de inicialização hello.
   
    ![Definir ToDoDataAPI como Projeto de Inicialização](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Pressione F5 ou clique **Depurar > Iniciar depuração** projeto de saudação toorun no modo de depuração.
   
    navegador de saudação é aberto e mostra a página de erro de HTTP 403 hello.
3. Na barra de endereços do navegador, adicione `swagger/docs/v1` toohello final da linha de saudação e depois pressione Return. (Olá URL é `http://localhost:45914/swagger/docs/v1`.)
   
    Este é o saudação padrão URL usado pelo Swashbuckle tooreturn Swagger 2.0 JSON metadados para Olá API.
   
    Se você estiver usando o Internet Explorer, o navegador Olá solicita toodownload um *v1.json* arquivo.
   
    ![Baixar metadados JSON no IE](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Se você estiver usando o Chrome, Firefox ou borda, o navegador de saudação exibe Olá JSON na janela do navegador hello. Navegadores diferentes lidar com JSON diferente, e a janela do navegador pode não ser exatamente igual exemplo hello.
   
    ![Metadados JSON no Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Olá, exemplo a seguir mostra a primeira seção Olá de metadados Swagger Olá Olá API, com definição Olá Olá método Get. Esses metadados são Olá quais unidades Swagger da interface do usuário que você usar Olá etapas a seguir e usá-lo em uma seção posterior tooautomatically tutorial Olá gerar código de cliente.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Feche o navegador hello e parar a depuração do Visual Studio.
5. Em Olá ToDoListDataAPI project no **Solution Explorer**, abra Olá *App_Start\SwaggerConfig.cs* arquivo e, em seguida, role a tela para baixo tooline 174 e remova os comentários Olá código a seguir.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Olá *SwaggerConfig.cs* arquivo é criado quando você instala o pacote de Swashbuckle Olá em um projeto. arquivo Hello fornece um número de maneiras tooconfigure Swashbuckle.
   
    código de saudação que tiver removidos Olá habilita Swagger interface do usuário que você usa em Olá seguindo as etapas. Quando você cria um projeto de API da Web usando o modelo de projeto de aplicativo hello API, esse código é comentado por padrão como uma medida de segurança.
6. Execute o projeto Olá novamente.
7. Na barra de endereços do navegador, adicione `swagger` toohello final da linha de saudação e depois pressione Return. (Olá URL é `http://localhost:45914/swagger`.)
8. Na página de interface do usuário Swagger hello, clique em **ToDoList** toosee métodos de saudação disponíveis.
   
    ![Métodos disponíveis na interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. Clique em Olá primeiro **obter** botão na lista de saudação.
10. Em Olá **parâmetros** seção, digite um asterisco como valor de saudação do hello `owner` parâmetro e clique **Experimente**.
    
    Quando você adicionar autenticação em tutoriais subsequentes, camada intermediária Olá fornecerá a camada de dados toohello do ID de usuário real hello. Agora, todas as tarefas terá asterisco sua ID do proprietário enquanto executa o aplicativo hello sem autenticação habilitada.
    
    ![Teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Olá Swagger da interface do usuário chama Olá método Get da lista de tarefas e exibe o código de resposta hello e resultados JSON.
    
    ![Resultados do teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Clique em **Post**e, em seguida, clique em caixa Olá em **esquema de modelo**.
    
    Clicando em Olá modelo esquema prefills Olá caixa de entrada onde você pode especificar o valor do parâmetro hello para Olá método Post. (Se isso não funcionar no Internet Explorer, use um navegador diferente ou insira o valor do parâmetro hello manualmente na próxima etapa do hello.)  
    
    ![Postagem do teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. Saudação de alteração JSON em Olá `todo` caixa para que ele se parece com hello exemplo a seguir, ou substituir seu próprio texto de descrição de entrada de parâmetro:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Clique em **Experimentar**.
    
    Olá ToDoList API retorna um código de resposta HTTP 204 que indica êxito.
14. Clique Olá primeiro **obter** botão e clique em Olá nessa seção da página de saudação **Experimente** botão.
    
    Olá resposta de obtenção de método agora inclui o novo item de toodo hello.
15. Opcional: Tente também Olá Put, Delete e obter pelos métodos de ID.
16. Feche o navegador hello e parar a depuração do Visual Studio.

O Swashbuckle funciona com qualquer projeto de API Web ASP.NET. Se você desejar tooadd Swagger metadados geração tooan projeto existente, apenas instale o pacote de Swashbuckle de saudação.

> [!NOTE]
> Os metadados do Swagger incluem uma ID exclusiva para cada operação da API. Por padrão, o Swashbuckle pode gerar IDs de operação do Swagger duplicadas para os métodos do controlador da API Web. Isso acontecerá se o controlador tiver métodos HTTP sobrecarregados, como `Get()` e `Get(id)`. Para obter informações sobre como toohandle sobrecargas, consulte [definições de API gerado personalizar Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md). Se você criar um projeto de API da Web no Visual Studio usando o modelo de aplicativo de API do Azure hello, o código que gera IDs exclusivo da operação será automaticamente adicionado toohello *SwaggerConfig.cs* arquivo.  
> 
> 

## <a id="createapiapp"></a>Criar um aplicativo de API no Azure e implantar código tooit
Nesta seção, você usar as ferramentas do Azure que são integradas a saudação Visual Studio **Publicar Web** Assistente toocreate uma nova API de aplicativo no Azure. Em seguida, implante Olá ToDoListDataAPI projeto toohello novo aplicativo de API e chamar a API de saudação executando Olá Swagger da interface do usuário.

1. Em **Solution Explorer**, clique com botão direito Olá ToDoListDataAPI e, em seguida, clique em **publicar**.
   
    ![Clicar em Publicar no Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. Em Olá **perfil** etapa Olá **Publicar Web** assistente, clique em **serviço de aplicativo do Microsoft Azure**.
   
   ![Clicar no Serviço de Aplicativo do Azure em Publicar Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Entrar tooyour conta do Azure, se você ainda não tiver feito isso, ou atualizar suas credenciais se elas estiverem expirado.
4. Nas Olá a caixa de diálogo do serviço de aplicativo, escolha hello Azure **assinatura** você deseja toouse e, em seguida, clique em **novo**.
   
    ![Clicar em Novo no diálogo Serviço de Aplicativo](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Olá **hospedagem** guia da saudação **criar serviço de aplicativo** caixa de diálogo é exibida.
   
    Porque você estiver implantando um projeto de API da Web que tem Swashbuckle instalado, o Visual Studio pressupõe que você deseja toocreate App uma API. Isso é indicado por Olá **API App Name** title e por Olá fatos que Olá **alterar tipo** lista suspensa está definida muito**API App**.
   
    ![Tipo de aplicativo no diálogo Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/apptype.png)
5. Insira um **API App Name** que é exclusivo no hello *azurewebsites.net* domínio. Você pode aceitar o nome padrão de saudação que propõe do Visual Studio.
   
    Se você inserir um nome que outra pessoa já usado, você verá um direito de toohello de ponto de exclamação vermelho.
   
    Olá URL do aplicativo hello API será `{API app name}.azurewebsites.net`.
6. Em Olá **grupo de recursos** lista suspensa, clique **novo**e, em seguida, digite "ToDoListGroup" ou outro nome se você preferir.
   
    Um grupo de recursos é uma coleção de recursos do Azure, como aplicativos de API, bancos de dados, VMs e assim por diante.    Para este tutorial, é melhor toocreate um novo grupo de recursos porque o que torna mais fácil toodelete em uma única etapa que todos Olá recursos do Azure que você cria para o tutorial hello.
   
    Essa caixa permite que você selecione um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) existente ou crie um novo digitando um nome diferente de qualquer grupo de recursos existente na assinatura.
7. Clique em Olá **novo** toohello próximo botão **plano do serviço de aplicativo** lista suspensa.
   
    captura de tela Hello mostra valores de exemplo para **API App Name**, **assinatura**, e **grupo de recursos** – seus valores serão diferentes.
   
    ![Criar caixa de diálogo do Serviço de Aplicativo](./media/app-service-api-dotnet-get-started/createas.png)
   
    Olá etapas a seguir, você criará um plano de serviço de aplicativo hello novo grupo de recursos. Um plano de serviço de aplicativo especifica os recursos de computação Olá que executa o seu aplicativo de API. Por exemplo, se você escolher a camada gratuita hello, seu aplicativo de API executa em máquinas virtuais compartilhados, enquanto para algumas camadas pagas, ele é executado em máquinas virtuais dedicadas. Para saber mais sobre os planos do Serviço de Aplicativo, consulte a [Visão geral dos planos do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, digite "ToDoListPlan" ou outro nome, se você preferir.
9. Em Olá **local** lista suspensa, escolha o local de saudação tooyou mais próximo.
   
    Essa configuração especifica em qual datacenter do Azure o aplicativo será executado. Escolha um local fechar tooyou toominimize [latência](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. Em Olá **tamanho** lista suspensa, clique **livre**.
    
    Para este tutorial, Olá livre preço fornecem desempenho suficiente.
11. Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, clique em **Okey**.
    
    ![Clicar em OK em Configurar Plano do Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/configasp.png)
12. Em Olá **criar serviço de aplicativo** caixa de diálogo, clique em **criar**.
    
    ![Clicar em Criar no diálogo Criar Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio cria o aplicativo de API hello e um perfil de publicação que tem todas as configurações de saudação necessária para o aplicativo hello API. Em seguida, ele abre Olá **Publicar Web** assistente, que você usará toodeploy projeto de saudação.
    
    Olá **Publicar Web** assistente é aberto no hello **Conexão** guia (mostrado abaixo).
    
    Em Olá **Conexão** guia hello **servidor** e **nome do Site** configurações do aplicativo de API tooyour ponto. Olá **nome de usuário** e **senha** são credenciais de implantação que o Azure cria para você. Após a implantação, o Visual Studio abrirá um navegador toohello **URL de destino** (que é a única finalidade Olá de **URL de destino**).  
13. Clique em **Avançar**.
    
    ![Clique em Avançar na guia Conexão de Publicar Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    próxima guia do Hello é hello **configurações** guia (mostrado abaixo). Aqui você pode alterar toodeploy de guia de configuração de compilação Olá uma compilação de depuração para [depuração remota](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Olá guia também oferece várias **opções de publicação do arquivo**:
    
    * Remover os arquivos adicionais no destino
    * Pré-compilar durante a publicação
    * Excluir arquivos da pasta App_Data de saudação
    
    Para este tutorial, você não precisará de qualquer uma delas. Para obter explicações detalhadas sobre o que fazem, confira [Como implantar um projeto Web usando a publicação de um clique no Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).
14. Clique em **Avançar**.
    
    ![Clique em Avançar na guia Configurações de Publicar Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    Next é Olá **visualização** guia (mostrado abaixo), que dá a você uma toosee oportunidade quais arquivos serão toobe copiado do seu aplicativo de API de toohello do projeto. Quando você estiver implantando um aplicativo de tooan API do projeto que você já implantou tooearlier, somente os arquivos alterados são copiados. Se você quiser toosee uma lista da qual serão copiados, você pode clicar em Olá **iniciar visualização** botão.
15. Clique em **Publicar**.
    
    ![Clicar em Publicar na guia Visualização de Publicar Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    O Visual Studio implanta Olá ToDoListDataAPI projeto toohello novo aplicativo de API. Olá **saída** janela registra o êxito da implantação e a página "criada com êxito" será exibida em uma URL do navegador janela aberta toohello do aplicativo hello API.
    
    ![Implantação bem-sucedida da janela de saída](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Página Novo aplicativo de API criado com êxito](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Adicionar URL de toohello "swagger" na barra de endereços do navegador hello e pressione Enter. (Olá URL é `http://{apiappname}.azurewebsites.net/swagger`.)
    
    navegador de saudação exibe Olá mesmo Swagger interface de usuário que você viu anteriormente, mas agora ele está em execução na nuvem hello. Experimente Olá método Get, e você vê que você está itens de tarefas 2 toohello back padrão. Olá alterações feitas anteriormente salvas na memória no computador local hello.
17. Olá abrir [portal do Azure](https://portal.azure.com/).
    
    Olá portal do Azure é uma interface da web para gerenciar os recursos do Azure, como aplicativos de API.
18. Clique em **Mais Serviços > Serviços de Aplicativos**.
    
    ![Procurar Serviços de Aplicativos](./media/app-service-api-dotnet-get-started/browseas.png)
19. Em Olá **serviços de aplicativos** folha, localize e clique em seu novo aplicativo de API. (No hello portal do Azure, são chamadas de janelas que são abertas direita toohello *folhas*.)
    
    ![Folha Serviços de Aplicativos](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Duas folhas são abertas. Um blade tem uma visão geral do aplicativo de API hello e um tem uma longa lista de configurações que você pode exibir e alterar.
20. Em Olá **configurações** folha, localizar Olá **API** seção e clique em **de definição de API**.
    
    ![Definição de API na folha Configurações](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Olá **de definição de API** folha permite que você especifique o URL de saudação que retorna metadados do Swagger 2.0 no formato JSON. Quando o Visual Studio cria um aplicativo hello API, ele define o valor de padrão do hello API definição URL toohello para Swashbuckle metadados gerados pelo que você viu anteriormente, que é o aplicativo hello API base URL mais `/swagger/docs/v1`.
    
    ![URL de definição da API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Quando você seleciona um código de cliente de toogenerate de aplicativo de API para ele, o Visual Studio recupera metadados de saudação dessa URL.

## <a id="codegen"></a>Gerar código de cliente para a camada de dados Olá
Uma das vantagens de saudação da integração do Swagger em aplicativos de API do Azure é a geração de código automática. Classes de cliente gerada tornam mais fácil toowrite o código que chama um aplicativo de API.

projeto de ToDoListAPI Olá já tiver um código de cliente de saudação gerado, mas no hello etapas você excluí-la e recriá-lo toosee como toodo Olá a geração de código.

1. No Visual Studio **Solution Explorer**, em Olá ToDoListAPI projeto, excluir Olá *ToDoListDataAPI* pasta. **Cuidado: Exclua apenas o hello pasta, projeto de ToDoListDataAPI Olá não.**
   
    ![Excluir código de cliente gerado](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Esta pasta foi criada usando o processo de geração de código Olá que você está prestes a toogo por meio de.
2. Clique com botão direito Olá ToDoListAPI e, em seguida, clique em **Adicionar > REST API cliente**.
   
    ![Adicionar o cliente da API REST ao Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. Em Olá **Adicionar cliente de API REST** caixa de diálogo, clique em **URL Swagger**e, em seguida, clique em **selecione Azure ativo**.
   
    ![Selecionar Ativo do Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. Em Olá **do serviço de aplicativo** caixa de diálogo, expanda o grupo de recursos de saudação você está usando para este tutorial e selecione seu aplicativo de API e, em seguida, clique em **Okey**.
   
    ![Selecionar aplicativo de API para geração de código](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Observe que, quando você retornar toohello **Adicionar cliente de API REST** caixa de diálogo, caixa de texto de saudação tenha sido preenchida com definição Olá API valor da URL que você viu anteriormente no portal de saudação.
   
    ![URL de definição da API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Metadados de tooget uma maneira alternativa para geração de código são tooenter Olá URL diretamente em vez de passar pela caixa de diálogo de procura de saudação. Se desejar que o código de cliente toogenerate antes de implantar tooAzure, é possível executar o projeto de API da Web hello localmente, vá toohello URL que fornece o arquivo de Swagger JSON hello, salve-Olá, e usar Olá **selecionar um arquivo de metadados do Swagger existente**opção.
   > 
   > 
5. Em Olá **Adicionar cliente de API REST** caixa de diálogo, clique em **Okey**.
   
    Visual Studio cria uma pasta chamada após o aplicativo hello API e gera classes de cliente.
   
    ![Arquivos de código para cliente gerado](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. No projeto de ToDoListAPI hello, abra *Controllers\ToDoListController.cs* toosee código de saudação na linha 40 que chama a API hello usando gerada de saudação do cliente.
   
    saudação de trecho de código a seguir mostra como o código Olá instancia o objeto de saudação do cliente e chama Olá método Get.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    o parâmetro de construtor Olá obtém URL de ponto de extremidade de saudação do hello `toDoListDataAPIURL` configuração do aplicativo. No arquivo Web. config de hello, esse valor é o conjunto toohello local IIS Express URL da API de saudação do projeto para que você possa executar o aplicativo hello localmente. Se você omitir o parâmetro de construtor Olá, o ponto de extremidade saudação padrão é a URL de Olá que gerou o código de saudação do.
7. A classe de cliente será gerado com um nome diferente com base no nome do aplicativo de API; alterar o código de saudação em *Controllers\ToDoListController.cs* para que hello tipo nome coincide com o que foi gerado em seu projeto. Por exemplo, se chamar o aplicativo de API de ToDoListDataAPI071316, você alterará este código:
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Criar uma camada intermediária do API aplicativo toohost Olá
Anteriormente você [criado o aplicativo de API de camada de dados hello e implantado código tooit](#createapiapp).  Agora que você siga Olá mesmo procedimento para o aplicativo de camada intermediária API hello.

1. Em **Solution Explorer**, com o botão direito Olá intermediária ToDoListAPI (não camada de dados de saudação ToDoListDataAPI) do projeto e, em seguida, clique em **publicar**.
   
    ![Clicar em Publicar no Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. Em Olá **perfil** guia da saudação **Publicar Web** assistente, clique em **serviço de aplicativo do Microsoft Azure**.
3. Em Olá **do serviço de aplicativo** caixa de diálogo, clique em **novo**.
4. Em Olá **hospedagem** guia da saudação **criar serviço de aplicativo** caixa de diálogo caixa, aceite o padrão de saudação **API App Name** ou digite um nome que seja exclusivo no hello  *azurewebsites.NET* domínio.
5. Escolha hello Azure **assinatura** que foi usado.
6. Em Olá **grupo de recursos** lista suspensa, escolha Olá mesmo grupo de recursos que você criou anteriormente.
7. Em Olá **plano do serviço de aplicativo** lista suspensa, escolha Olá mesmo plano que você criou anteriormente. O padrão será o valor de toothat.
8. Clique em **Criar**.
   
    Visual Studio cria o aplicativo hello API, cria um perfil de publicação para ele e exibe o saudação **Conexão** etapa Olá **Publicar Web** assistente.
9. Em Olá **Conexão** etapa Olá **Publicar Web** assistente, clique em **publicar**.
   
   Visual Studio implanta Olá ToDoListAPI projeto toohello novo aplicativo de API e abre uma URL de toohello do navegador de saudação do aplicativo de API. página Hello "criado com êxito" será exibida.

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Configurar a camada de dados Olá camada intermediária toocall Olá
Se você chamou o aplicativo de API de camada intermediária Olá agora, ele seria tente toocall da camada de dados de saudação usando Olá localhost URL que ainda está no arquivo Web. config de saudação. Nesta seção você inserir a URL do aplicativo de API do hello dados da camada em uma configuração de ambiente no aplicativo de API de camada intermediária hello. Quando hello código no aplicativo de API de camada intermediária Olá recupera configuração de URL de camada de dados hello, configuração do ambiente de saudação substituirá o que está no arquivo Web. config de saudação.

1. Vá toohello [portal do Azure](https://portal.azure.com/)e, em seguida, navegue toohello **API App** folha para o aplicativo hello API que você criou o projeto do toohost Olá TodoListAPI (camada intermediária).
2. Em Olá da API App **configurações** folha, clique em **configurações de aplicativo**.
3. Em Olá da API App **configurações do aplicativo** folha, role para baixo toohello **configurações do aplicativo** seção e adicione o seguinte Olá chave e valor. valor de saudação será Olá URL da API de saudação primeiro aplicativo publicado neste tutorial.
   
   | **Chave** | toDoListDataAPIURL |
   | --- | --- |
   | **Valor** |https://{nome do aplicativo de API da sua camada de dados}.azurewebsites.net |
   | **Exemplo** |https://todolistdataapi.azurewebsites.net |
4. Clique em **Salvar**.
   
    ![Clicar em Salvar para Configurações de Aplicativo](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Quando o código de saudação é executado no Azure, esse valor substituirá agora Olá localhost URL que está no arquivo Web. config de saudação.

## <a name="test"></a>Teste
1. Em uma janela de navegador, procure toohello URL de camada intermediária novo aplicativo de API que você acabou de criar para ToDoListAPI hello. Você pode chegar lá clicando em URL Olá na folha de principal do aplicativo hello API no portal de saudação.
2. Adicionar URL de toohello "swagger" na barra de endereços do navegador hello e pressione Enter. (Olá URL é `http://{apiappname}.azurewebsites.net/swagger`.)
   
    navegador exibe Olá Olá mesmo Swagger da interface do usuário que você viu anteriormente para ToDoListDataAPI, mas agora `owner` não é um campo obrigatório para a operação de obtenção de hello, porque o aplicativo de camada intermediária API hello está enviando esse aplicativo de API do valor toohello dados da camada para você. (Hello tutoriais de autenticação, camada intermediária Olá enviará as IDs de usuário real para Olá `owner` parâmetro; para agora ela é codificar um asterisco.)
3. Experimente Olá método Get e hello toovalidate outros métodos que Olá aplicativo de API de camada intermediária é com êxito chamando Olá da camada de dados do aplicativo de API.
   
    ![Método Get da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Solucionar problemas
Caso você encontre um problema ao percorrer este tutorial, aqui estão algumas ideias para solução de problemas:

* Certifique-se de que você está usando a versão mais recente de saudação do hello [SDK do Azure para .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Dois nomes de saudação do projeto são semelhante (ToDoListAPI, ToDoListDataAPI). Se não estiver tudo conforme descrito nas instruções de hello quando você estiver trabalhando com um projeto, certifique-se de que abrir projeto correto hello.
* Se você estiver em uma rede corporativa e está tentando toodeploy tooAzure do serviço de aplicativo por meio de um firewall, certifique-se de que as portas 443 e 8172 estão abertas para implantação da Web. Se não puder abrir essas portas, você poderá usar outros métodos de implantação.  Consulte [implantar tooAzure seu aplicativo do serviço de aplicativo](../app-service-web/web-sites-deploy.md).
* Erros de "nomes de rota devem ser exclusivos" – você pode obter essas se você acidentalmente implantar Olá projeto errado tooan API do aplicativo e, posteriormente, implante Olá tooit correta de um. toocorrect, reimplantação Olá projeto correto toohello API aplic e em Olá **configurações** guia da saudação **Publicar Web** assistente, selecione **remover arquivos adicionais no destino**.

Depois de ter seu aplicativo de API do ASP.NET em execução no serviço de aplicativo do Azure, talvez você queira toolearn mais sobre os recursos do Visual Studio que simplificam a solução de problemas. Para saber mais sobre o registro em log, a depuração remota e muito mais, confira [Solução de problemas dos aplicativos do Serviço de Aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Próximas etapas
Você viu como toodeploy API da Web projetos tooAPI aplicativos existentes, gerar o código do cliente para aplicativos de API e consumir aplicativos de API de clientes .NET. tutorial Avançar Olá nesta série mostra como muito[usar CORS tooconsume API aplicativos clientes do JavaScript](app-service-api-cors-consume-javascript.md).

Para obter mais informações sobre geração de código de cliente, consulte Olá [Azure/AutoRest](https://github.com/azure/autorest) repositório em GitHub.com. Para obter ajuda com problemas para usar o cliente Olá gerado, abra um [problema no repositório de AutoRest Olá](https://github.com/azure/autorest/issues).

Se você quiser toocreate novos projetos de API aplicativo do zero, use Olá **aplicativo de API do Azure** modelo.

![Modelo de Aplicativo de API no Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Olá **aplicativo de API do Azure** modelo de projeto é o equivalente toochoosing Olá **vazio** ASP.NET 4.5.2 modelo, clicando no suporte da API da Web tooadd Olá caixa de seleção e, em seguida, instalar Olá pacote Swashbuckle NuGet. Além disso, o modelo de saudação adiciona alguns Swashbuckle configuração código desenvolvido tooprevent Olá criação da operação de Swagger duplicada IDs. Depois de criar um projeto de API App, você pode implantá-lo tooan API Olá de aplicativo mesmo modo que você viu neste tutorial.

