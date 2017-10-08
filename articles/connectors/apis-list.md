---
title: "aaaConnectors para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Escolha todas as toobuild de conectores disponíveis gerenciada pela Microsoft hello e criar aplicativos lógicos"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Lista de conectores
> [!TIP]
> Olá [lista completa de A-Z](#az) (neste tópico) lista todos os conectores disponíveis Olá você pode usar em seus aplicativos lógicos. [Detalhes do conector](/connectors/) lista os disparadores e as ações definidas em swagger hello e também lista os limites para cada conector.

Os conectores são parte integrante na criação de aplicativos lógicos. Usando esses conectores, você pode realmente expandir seu local e nuvem coisas diferentes de toodo de aplicativos com dados que você criar e que você já tiver. conectores de saudação estão disponíveis no hello categorias a seguir: 

* **Conectores-padrão**: disponíveis e incluídos automaticamente quando você usa aplicativos lógicos. Alguns exemplos incluem o Barramento de Serviço, o Power BI, o Oracle Database, o OneDrive e muito mais.

* **Conectores de conta de integração**: disponíveis quando você adquire uma conta de integração. Usando esses conectores, você pode transformar e validar XML, processar mensagens entre empresas com AS2 / X12 / EDIFACT, além de codificar e decodificar arquivos simples. Se você trabalha com o BizTalk Server, esses conectores são que uma boa opção tooexpand seus fluxos de trabalho do BizTalk no Azure.  

    BizTalk Server também tem um [adaptador aplicativos lógicos](https://msdn.microsoft.com/library/mt787163.aspx) que inclui o recebimento de um aplicativo de lógica e enviando o aplicativo lógico de tooa.

* **Conectores empresariais**: incluem MQ e SAP. Disponível a um custo adicional. 

[Preços de aplicativos com a lógica](https://azure.microsoft.com/pricing/details/logic-apps/) e [modelo de preços](../logic-apps/logic-apps-pricing.md) fornecem mais detalhes sobre os custos de saudação. 

## <a name="popular-connectors"></a>Conectores populares
Milhares de aplicativos e milhões de execuções processam com êxito dados e informações usando esses conectores. Olá, a tabela a seguir lista hello mais popular e alguns favoritos com nossos usuários:

| |  |  |  |
| --- | --- | --- | --- |
| [![Ícone de API][AzureBlobStorageicon]<br/>**Armazenamento de Blobs<br/>do Azure**][AzureBlobStoragedoc] | Se você quiser tooautomate todas as tarefas com sua conta de armazenamento, você deve examinar este conector. Suporta operações CRUD (criar, ler, atualizar, excluir). | [![API Icon][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | Cria funções que executam trechos de código personalizados do C# ou node.js e, em seguida, usa essas funções em seus aplicativos lógicos.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Uma saudação mais frequentes para os conectores. Ele tem gatilhos e ações toohelp automatize fluxos de trabalho com clientes potenciais e muito mais. | [![API Icon][Event-hubs-icon]<br/>**Hubs de eventos**][event-hubs-doc] | Como consumir e publicar eventos em um Hub de eventos. Por exemplo, você pode obter saída do seu aplicativo lógico usando Hubs de eventos e, em seguida, enviar o provedor do hello saída tooa análise em tempo real. |
| [![Ícone de API][FTPicon]<br/>**FTP**][FTPdoc] | Se seu servidor FTP estiver acessível dos Olá internet, em seguida, você pode automatizar toowork fluxos de trabalho com arquivos e pastas. <br/><br/>SFTP também está disponível com o conector SFTP hello. | [![Ícone de API][HTTPicon]<br/>**HTTP**][httpdoc] | Use lógica aplicativos toocommunicate com qualquer ponto de extremidade HTTP. |
| [![Ícone de API][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Muitos dos gatilhos e muito mais emails de toouse Office 365 de ações e eventos em seus fluxos de trabalho. <br/><br/>Esse conector inclui um *email de aprovação* tooapprove solicitações de ação de férias, relatórios de despesas e assim por diante. <br/><br/>Usuários do Office 365 também estão disponíveis com o conector de usuários do Office 365 hello.| [![API Icon][HTTP-Requesticon]<br/>**Solicitação / Resposta**][HTTP-Requestdoc] | Esse conector fornece uma URL HTTPS. Quando Olá lógica aplicativo recebe uma solicitação de URL toothis, o aplicativo de lógica de saudação é iniciado. |
| [![Ícone de API][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Facilmente entrar com sua equipe de vendas conta tooget acesso tooobjects, como clientes potenciais e muito mais. |  [![Ícone de API][Service-Busicon]<br/>**Barramento de Serviço**][Service-Busdoc] | conector mais popular do Hello dentro de aplicativos lógicos, ele inclui gatilhos e ações toodo mensagens assíncronas e publicação/assinatura com tópicos, assinaturas e filas. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Se você não fizer nada com o SharePoint e puder se beneficiar com a automação, recomendamos que examine esse conector. Pode ser usado com um SharePoint local e o SharePoint Online. | [![Ícone de API][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Uma saudação usado mais conectores, ele pode se conectar tooan local do SQL Server e um banco de dados do SQL Azure. | 
| [![Ícone de API][Twittericon]<br/>**Twitter**][Twitterdoc] | Entra facilmente com uma conta do Twitter e, em seguida, inicia um fluxo de trabalho quando um novo tweet é lançado. Em seguida, salve essas banco de dados do SQL tweets tooa ou lista do SharePoint. | | | 

## <a name="integration-account-connectors"></a>Conectores da conta de integração 

Olá Enterprise Integration Pack (EIP) inclui os conectores que são conhecido toohello comunidade do BizTalk Server. Quando você adquire uma [conta integration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), você também pode obter Olá conectores a seguir: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![Ícone de API][as2icon]<br/>**Decodificação</br> de AS2**][as2decode] | [![Ícone de API][as2icon]<br/>**Codificação</br> de AS2**][as2encode] | [![Ícone de API][x12icon]<br/>**Decodificação</br> EDIFACT**][EDIFACTdecode] | [![Ícone de API][x12icon]<br/>**Codificação</br> EDIFACT**][EDIFACTencode] |
[![Ícone de API][flatfileicon]<br/>**Codificação de</br> arquivo simples**][flatfiledoc] | [![Ícone de API][flatfiledecodeicon]<br/>**Decodificação de</br> arquivo simples**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Conta de<br/> integração**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**Transformação<br/> XML**][xmltransformdoc] |
| [![Ícone de API][x12icon]<br/>**Decodificação</br> de X12**][x12decode] | [![Ícone de API][x12icon]<br/>**Codificação</br> de X12**][x12encode] | [![Ícone de API][xmlvalidateicon]<br/>**Validação de <br/>XML**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Conectores empresariais

Conecte-se a aplicativos corporativos de tooyour dentro de seus aplicativos lógicos.

|  |  |
| --- | --- |
|[![Ícone de API][MQicon]<br/>**MQ**][mqdoc]|[![Ícone de API][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Lista completa de A-Z

[Detalhes do conector](/connectors/) lista quaisquer gatilhos e ações definidas em swagger Olá e também lista os limites para cada conector.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>Agendamento de compromisso 10to8<br/><br/><a name="a"></a>AGIR!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Gerenciamento de API do Azure<br/>Serviços de Aplicativo do Azure<br/>Aplicativo do Azure<br/>Automação do Azure<br/>[Armazenamento de Blobs do Azure][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Azure Functions][azure-functionsdoc]<br/>[Aplicativos Lógicos do Azure][nested-logic-appdoc]<br/>AzureML<br/>Filas do Azure<br/>Gerenciador de Recursos do Azure<br/>[Banco de dados SQL do Azure][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Email de parâmetro de comparação<br/>Pesquisa do Bing<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Cápsula CRM<br/>Chatter<br/>Formulários do Cognito<br/>API da Pesquisa Visual Computacional dos Serviços Cognitivos<br/>API de detecção facial de serviços cognitivos<br/>Serviços Cognitivos LUIS<br/>Análise de texto de serviços cognitivos<br/>Common Data Service<br/>Conversão de conteúdo<br/>Control-Terminate<br/>[APIs personalizadas/aplicativos Web][api/web-appdoc]<br/><br/><a name="d"></a>Operações de dados<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Hubs de Eventos][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[Sistema de Arquivos][filesystemdoc]<br/>[Arquivo simples][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>FreshService<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google Calendar<br/>Contatos do Google<br/>Google Drive<br/>Google Sheets<br/>Google Tasks<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[Webhook HTTP][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Conta de integração<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Média<br/>Microsoft Forms<br/>Equipes da Microsoft<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Clima<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Outlook do Office 365][office365-outlookdoc]<br/>Usuários do Office 365<br/>Vídeo do Office 365<br/>OneDrive<br/>OneDrive for Business<br/>OneNote (comercial)<br/>[Oracle Database][oracle-db-doc]<br/>Gerenciador de clientes do Outlook<br/>Tarefas do Outlook<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Analisador<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planejador<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Solicitação / Resposta][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[Servidor de aplicativos SAP][sapconnector]<br/>[Servidor de mensagens SAP][sapconnector]<br/>[Agenda][recurrencedoc]<br/>Escopo<br/>SendGrid<br/>Enviar mensagens toobatch<br/>[Barramento de Serviço][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Margem de atraso<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Projetos Teamwork<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[Transformar XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Variables<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[Validação de XML][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget de Introdução aos aplicativos do Azure lógica antes de se inscrever para uma conta do Azure, vá muito[tente lógica aplicativos](https://tryappservice.azure.com/?appservice=logic). Você pode criar imediatamente um aplicativo lógico de início e de curta duração. Nenhum cartão de crédito é exigido, sem compromissos.

## <a name="connectors-as-triggers-and-actions"></a>Conectores como gatilhos e ações

Um **gatilho** inicia ou executa uma instância de seu aplicativo lógico. Alguns conectores fornecem gatilhos que podem notificar seu aplicativo quando ocorrem eventos específicos. Por exemplo, o conector Olá FTP tem Olá `OnUpdatedFile` gatilho que inicia o aplicativo de lógica quando um arquivo é atualizado. 

Aplicativos lógicos incluem hello tipos de gatilhos a seguir:  

* *Sondar gatilhos*: estes gatilhos sondagem o serviço em um toocheck frequência especificada para novos dados. 

    Quando novos dados estiverem disponíveis, uma nova instância da sua lógica de aplicativo é executado com dados saudação como entrada. 

* *Enviar por push gatilhos*: estes gatilhos escutam para dados em um ponto de extremidade, ou para um evento toohappen, em seguida, dispara uma nova instância da sua lógica de aplicativo.

* *Gatilho de recorrência*: esse gatilho cria uma instância do aplicativo lógico em um agendamento prescrito.

Os conectores também fornecem **ações** que podem ser usadas no fluxo de trabalho. Por exemplo, seu aplicativo lógico pode procurar dados e usá-los posteriormente em seu aplicativo lógico. Mais especificamente, você pode pesquisar os dados do cliente de um banco de dados SQL e, em seguida, usar esse toobuild de dados do cliente seu fluxo de trabalho. 

> [!TIP]
> [Visão geral de conectores](connectors-overview.md) fornece mais detalhes sobre gatilhos e ações. 


## <a name="message-manipulation-actions"></a>Ações de manipulação de mensagem

Aplicativos lógicos incluem ações internas que podem alterar ou manipular os dados de conteúdo. Olá interna **operações de dados** connector inclui Olá ações a seguir: 

| | |
|---|---|
| **Compor** | Criar ou gerar toouse valores ou objetos mais tarde ou que você criar o fluxo de trabalho. Por exemplo, você pode criar um objeto JSON com valores de várias etapas ou calcular uma constante tooreference mais tarde em um aplicativo de lógica executar. |
| **Criar tabela CSV**<br/>**Criar tabela HTML** | Transforme um conjunto de resultados de matriz em uma tabela HTML ou CSV. Por exemplo, adicionar ação de "Registros de lista" hello CRM e adicionar um filtro de registros adicionados hoje. Em seguida, envie os resultados de saudação como uma tabela HTML em um email. |
| **Matriz de filtro** (consulta) | Filtre um toohello entradas do conjunto de resultados que lhe interessam. Por exemplo, pesquisar todos os tweets com `#Azure`, e, em seguida, Olá "filtro" retornado tweets tooonly retornam resultados que são `Tweeted_by_followers > 50`. |
| **Join** | Una uma matriz a um delimitador. Por exemplo, Olá operação detectar frases-chave retorna uma matriz de frases-chave. Você pode "unir" com uma `,` ou algo parecido. Portanto, em vez de `["Some", "Phrase"]`, você tem `"Some, Phrase"`. |
| **Analisar o JSON** | Analisar e acessar valores de um objeto JSON no designer de saudação. Por exemplo, se a função do Azure retorna uma carga JSON, em seguida, você pode analisá-lo tooaccess propriedades JSON Olá posteriormente em outra etapa. ação de saudação também valida que Olá JSON correspondências Olá esquema especificado em tempo de execução. | 
| **Seleção** | Selecione determinadas propriedades de uma matriz para processamento adicional. Se você "Listar os registros" do SQL e ele retorna 15 colunas, selecione apenas algumas dessas colunas para processamento adicional. saída de Hello é uma matriz que contém somente propriedades Olá selecionadas. |

## <a name="custom-connectors-and-azure-certification"></a>Conectores personalizados e certificação do Azure 

toocall em APIs que execute o código personalizado ou não estão disponíveis como conectores, você pode estender a plataforma de aplicativos lógicos Olá por [criando aplicativos de API baseada em REST que os conectores personalizados](../logic-apps/logic-apps-create-api-app.md). 

Se você quiser toomake seu personalizado aplicativos de API pública e disponível toouse no Azure, em seguida, envie sua toohello indicações [do programa Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder a perguntas e veja que outros usuários de aplicativos do Azure lógicos estão fazendo, vá toohello [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos lógicos](http://aka.ms/logicapps-wish).

Falta um tópico do conector ou algum detalhe que você acha importante? Se Sim, ajude-na adicionando tópicos existentes tooour ou escrever suas próprias. Nossa documentação é de software livre e hospedada no GitHub. Comece a usá-a no nosso [repositório GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Próximas etapas
* [Criar seu primeiro aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)
* [Criar APIs personalizadas para aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md)
* [Monitorar seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Integrar aplicativos lógicos a Aplicativos de API do Serviço de Aplicativo"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Gerenciar arquivos em seu contêiner de blob com o conector de Armazenamento de Blobs do Azure"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Integre aplicativos lógicos com Azure Functions"
[db2doc]: ./connectors-create-api-db2.md "Conecte-se tooIBM DB2 em nuvem hello ou local. Atualizar uma linha, obter uma tabela e muito mais"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Conecte-se tooDynamics CRM Online para que possa trabalhar com dados do CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Conecte-se tooAzure Hubs de eventos. Receber e enviar eventos entre aplicativos lógicos e Hubs de Eventos"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Conecte-se o sistema de arquivos local tooan"
[ftpdoc]: ./connectors-create-api-ftp.md "Conecte-se tooan FTP / servidor FTPS para tarefas FTP, como carregar, obtendo, excluindo arquivos e muito mais"
[httpdoc]: ./connectors-native-http.md "Fazer chamadas HTTP com o conector HTTP Olá"
[http-requestdoc]: ./connectors-native-reqres.md "Adicionar ações para aplicativos de lógica de tooyour de solicitações e respostas HTTP"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Fazer chamadas HTTP com o conector HTTP + Swagger"
[informixdoc]: ./connectors-create-api-informix.md "Conecte-se tooInformix em nuvem hello ou local. Ler uma linha, tabelas de saudação da lista e muito mais"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Integrar aplicativos lógicos a fluxos de trabalho aninhados"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Conecte-se a conta tooyour Office 365. Enviar e receber emails, gerenciar seu calendário e contatos e muito mais"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Conecte-se tooadd de banco de dados Oracle tooan, inserir, excluir linhas e muito mais"
[mqdoc]: ./connectors-create-api-mq.md "Conecte-se tooMQ no local ou no Azure e enviar e receber mensagens"
[recurrencedoc]:  ./connectors-native-recurrence.md "Disparar ações recorrentes para aplicativos lógicos"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Conecte-se a conta do Salesforce tooyour. Gerenciar contas, clientes potenciais, oportunidades e muito mais"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Conecte-se tooan no sistema local da SAP"
[service-busdoc]: ./connectors-create-api-servicebus.md "Envia mensagens de tópicos e filas do barramento de serviço e recebe mensagens de assinaturas e filas do barramento de serviço"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Conecte-se tooSharePoint on-line. Gerenciar documentos, listar itens e muito mais"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Conecte-se tooSharePoint no servidor local. Gerenciar documentos, listar itens e muito mais"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Conecte-se tooAzure banco de dados SQL ou SQL server. Criar, atualizar, obter e excluir entradas em uma tabela do Banco de Dados SQL."
[twitterdoc]: ./connectors-create-api-twitter.md "Conecte-se tooTwitter. Obter cronogramas, postar tweets e muito mais"
[webhookdoc]: ./connectors-native-webhook.md "Adicionar aplicativos de lógica de tooyour de gatilhos e ações de Webhook"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Saiba mais sobre a integração corporativa do AS2."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Saiba mais sobre a integração corporativa do X12"
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre o arquivo simples de integração corporativa."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre o arquivo simples de integração corporativa."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Saiba mais sobre a validação de XML de integração corporativa."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Saiba mais sobre as transformações de integração corporativa."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Saiba mais sobre a decodificação AS2 de integração corporativa"
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Saiba mais sobre a codificação AS2 de integração corporativa"
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Saiba mais sobre a decodificação X12 de integração corporativa"
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Saiba mais sobre a codificação X12 de integração corporativa"
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Saiba mais sobre a decodificação EDIFACT de integração corporativa"
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Saiba mais sobre a codificação EDIFACT de integração corporativa"
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Pesquisa esquemas, mapas, parceiros e muito mais em sua conta de integração"


[boxDoc]: ./connectors-create-api-box.md "Conecte-se tooBox. Carregar, obter, excluir, listar arquivos e muito mais"
[delaydoc]: ./connectors-native-delay.md "Executar ações atrasadas"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Conecte-se tooDropbox. Carregar, obter, excluir, listar arquivos e muito mais"
[facebookdoc]: ./connectors-create-api-facebook.md "Conecte-se tooFacebook. Após a tooa da linha do tempo, obtenha uma página de feed e muito mais"
[githubdoc]: ./connectors-create-api-github.md "Conecte-se tooGitHub e rastrear problemas"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Conecte-se tooGoogleDrive para que possa trabalhar com seus dados"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Conecte-se tooGoogle folhas para que você pode pode modificar as folhas"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Conecta-se tooGoogle tarefas para que você pode gerenciar suas tarefas"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Conecta-se tooGoogle calendário e pode gerenciar o calendário."
[http-responsedoc]: ./connectors-native-reqres.md "Adicionar ações para aplicativos de lógica de tooyour de solicitações e respostas HTTP"
[instagramdoc]: ./connectors-create-api-instagram.md "Conecte-se tooInstagram. Disparar ou agir nos eventos"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Conecte-se a conta do MailChimp tooyour. Gerenciar e automatizar emails"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Conecte-se tooMandrill para comunicação"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Conecte-se tooMicrosoft conversor. Traduzir textos, detectar idiomas e muito mais" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Obtenha informações de vídeo, listas e canais de vídeo e URLs de reprodução de vídeos do Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Conecte-se tooyour Microsoft OneDrive pessoal. Carregar, excluir, listar arquivos e muito mais"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Conecte-se tooyour negócios Microsoft OneDrive. Carregar, excluir, listar arquivos e muito mais"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Conecte-se a caixa de correio do Outlook tooyour. Gerenciar seu email, calendários, contatos e muito mais"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Conecte-se tooMicrosoft Project Online. Gerenciar seus projetos, tarefas, recursos e muito mais"
[querydoc]: ./connectors-native-query.md "Selecionar e filtrar matrizes com a ação de consulta Olá"
[rssdoc]: ./connectors-create-api-rss.md "Publicar e recuperar itens do feed, disparar operações quando um novo item é publicado tooan RSS feed."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Conecte-se tooSendGrid. Enviar email e gerenciar listas de destinatários"
[sftpdoc]: ./connectors-create-api-sftp.md "Conecte-se a conta SFTP tooyour. Carregar, obter, excluir arquivos e muito mais"
[slackdoc]: ./connectors-create-api-slack.md "Conecte-se tooSlack e postar mensagens tooSlack canais"
[smtpdoc]: ./connectors-create-api-smtp.md "Conecte-se o servidor de SMTP tooa e envie um e-mail com anexos"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Conecta-se tooSparkPost para comunicação"
[trellodoc]: ./connectors-create-api-trello.md "Conecte-se tooTrello. Gerenciar seus projetos e organizar o que quiser com qualquer pessoa"
[twiliodoc]: ./connectors-create-api-twilio.md "Conecte-se tooTwilio. Enviar e receber mensagens, obter os números disponíveis, gerenciar números de telefone de entrada e muito mais"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Conecte-se tooWunderlist. Gerenciar suas tarefas e listas de tarefas, manter sua vida sincronizada e muito mais"
[yammerdoc]: ./connectors-create-api-yammer.md "Conecte-se tooYammer. Postar mensagens, receber novas mensagens e muito mais"
[youtubedoc]: ./connectors-create-api-youtube.md "Conecte-se tooYouTube. Gerenciar seus vídeos e canais"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
