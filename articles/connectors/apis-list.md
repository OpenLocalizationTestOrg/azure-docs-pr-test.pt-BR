---
title: "Conectores para Aplicativo Lógico do Azure | Microsoft Docs"
description: "Escolha dentre os conectores disponíveis pela Microsoft para compilar e criar aplicativos lógicos"
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
ms.openlocfilehash: 948b91a9fabc3ab3c4d6708968a88cb9d203b171
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="connectors-list"></a>Lista de conectores
Para localizar os gatilhos e as ações definidos por descrição do Swagger de cada conector além de todos os limites de conector, veja [Detalhes do conector](/connectors/).

Os conectores são parte integrante na criação de aplicativos lógicos. Usando esses conectores, é possível expandir seus aplicativos locais e de nuvem para fazer coisas diversas com dados criados e os dados que você já tem. Os conectores estão disponíveis como ações internas ou conectores gerenciados.

**Ações internas**: o mecanismo de Aplicativos Lógicos fornece as ações internas para a comunicação com pontos de extremidade e a execução de tarefas. Por exemplo, você pode usar essas ações para chamar pontos de extremidade HTTP, Azure Functions e operações de Gerenciamento de API do Azure, bem como para manipular mensagens com operações de dados e variáveis.

**Conectores gerenciados**: fornecem acesso às APIs de vários serviços, criando conexões de API que o serviço Aplicativos Lógicos hospeda e gerencia. Estas são as categorias de conectores gerenciados:

* **Conectores-padrão**: disponíveis e incluídos automaticamente quando você usa aplicativos lógicos. Alguns exemplos incluem o Barramento de Serviço, o Power BI, o OneDrive e muito mais.

* **Conectores local**: conecte-se a aplicativos de servidor locais usando o [gateway de dados local][gatewaydoc]. Os conectores locais incluem conectividade aos aplicativos de servidor, como o SharePoint Server, SQL Server, Oracle DB, compartilhamentos de arquivos e outros.

* **Conectores de conta de integração**: disponíveis quando você adquire uma conta de integração. Usando esses conectores, você pode transformar e validar XML, processar mensagens entre empresas com AS2 / X12 / EDIFACT, além de codificar e decodificar arquivos simples. Se você trabalha com o BizTalk Server, então esses conectores são uma boa opção para expandir seus fluxos de trabalho do BizTalk no Azure.  

    O BizTalk Server também tem um [adaptador de aplicativos lógicos](https://msdn.microsoft.com/library/mt787163.aspx) que inclui o recebimento de um aplicativo lógico e envio para um aplicativo lógico.

* **Conectores empresariais**: incluem MQ e SAP. Disponível a um custo adicional. 

Para saber mais sobre os custos, veja [detalhes de preços](https://azure.microsoft.com/pricing/details/logic-apps/) e [modelo de preços](../logic-apps/logic-apps-pricing.md) para Aplicativos Lógicos. 

## <a name="popular-connectors"></a>Conectores populares
Milhares de aplicativos e milhões de execuções processam com êxito dados e informações usando esses conectores. 

### <a name="built-in-actions"></a>Ações internas
O mecanismo de Aplicativos Lógicos fornece ações que podem manipular os dados, se comunicar por HTTP e controlar o fluxo da definição de aplicativos lógicos. Algumas dessas ações incluem:

| |  |  |  |
| --- | --- | --- | --- |
| [![Ícone da API][HTTPicon]<br/>**HTTP**][httpdoc] | Usa aplicativos lógicos para se comunicar com qualquer ponto de extremidade via HTTP.| [![Ícone da API][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | Cria funções que executam trechos de código personalizados do C# ou node.js e, em seguida, usa essas funções em seus aplicativos lógicos.  |
| [![Ícone da API][HTTP-Requesticon]<br/>**Solicitação**][HTTP-Requestdoc] | Fornece uma URL HTTPS que pode ser chamada, normalmente usada como um webhook em outros aplicativos. Ao receber uma solicitação para essa URL, o aplicativo lógico é iniciado. | [![Ícone da API][Recurrenceicon]<br/>**Agenda**][recurrencedoc] | Inicie aplicativos lógicos com base em agendas de recorrência simples ou complexa. Por exemplo, crie agendas desde a recorrência simples de todos os dias até a recorrência por hora na última sexta-feira de cada mês entre 9:00:00 e 17:00. |
| [![Ícone da API][CallLogicApp-icon]<br/>**Chamada<br/>Aplicativo Lógico**][nested-logic-appdoc] | Chame um aplicativo lógico aninhado. Qualquer aplicativo lógico com um gatilho de solicitação pode ser chamado como um aplicativo lógico aninhado.| [![Ícone da API][API/Web-Appicon]<br/>**Aplicativo de API**][api/web-appdoc] | Chame um Aplicativo de API do Serviço de Aplicativo. Os Aplicativos de API com swagger são renderizados da mesma forma que outras ações de primeira classe.|

### <a name="standard-connectors"></a>Conectores padrão
A tabela a seguir lista alguns dos preferidos e famosos entre os nossos usuários:

| |  |  |  |
| --- | --- | --- | --- |
| [![Ícone da API][AzureBlobStorageicon]<br/>**Armazenamento<br/>de Blobs do Azure**][AzureBlobStoragedoc] | Se deseja automatizar as tarefas com sua conta de armazenamento, você deve examinar esse conector. Suporta operações CRUD (criar, ler, atualizar, excluir). | [![Ícone da API][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Um dos mais requisitados para conectores. Ela tem gatilhos e ações para ajudar a automatizar fluxos de trabalho com clientes potenciais e muito mais. |
| [![Ícone da API][Event-Hubs-icon]<br/>**Hubs de Eventos**][event-hubs-doc] | Como consumir e publicar eventos em um Hub de eventos. Por exemplo, você pode obter uma saída do seu aplicativo lógico usando os Hubs de eventos e, em seguida, enviar a saída para um provedor de análise em tempo real. | [![Ícone da API][FTPicon]<br/>**FTP**][FTPdoc] | Se o servidor FTP estiver acessível pela Internet, então, você pode automatizar fluxos de trabalho para trabalhar com arquivos e pastas. <br/><br/>O SFTP também está disponível com o conector de SFTP. |
| [![Ícone da API][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Vários gatilhos e muito mais ações para usar email do Office 365 e eventos dentro de seus fluxos de trabalho. <br/><br/>Esse conector inclui uma ação de *email de aprovação* para aprovar solicitações de férias, relatórios de despesas e assim por diante. <br/><br/>Os usuários do Office 365 também estão disponíveis com o conector de usuários do Office 365.| [![Ícone da API][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Entra facilmente com sua conta do Salesforce para obter acesso a objetos, como clientes potenciais e muito mais. | 
| [![Ícone da API][Service-Busicon]<br/>**Barramento de Serviço**][Service-Busdoc] | O conector mais popular nos aplicativos lógicos, ele inclui gatilhos e ações para produzir mensagens assíncronas e publicação/assinatura com filas, assinaturas e tópicos. |  [![Ícone da API][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Se você não fizer nada com o SharePoint e puder se beneficiar com a automação, recomendamos que examine esse conector. Pode ser usado com um SharePoint local e o SharePoint Online. |
| [![Ícone da API][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Um dos conectores mais usados, ele pode se conectar a um SQL Server local e a um banco de dados SQL do Azure. | [![Ícone da API][Twittericon]<br/>**Twitter**][Twitterdoc] | Entra facilmente com uma conta do Twitter e, em seguida, inicia um fluxo de trabalho quando um novo tweet é lançado. Depois, salva esses tweets em um banco de dados SQL ou em uma lista do SharePoint. | 

### <a name="on-premises-connectors"></a>Conectores locais 

Os conectores locais fornecem acesso a dados em servidores locais.  A criação de uma conexão co um servidor local exige um [gateway de dados local][gatewaydoc] que forneça um canal de comunicação seguro sem a necessidade de configurar a infraestrutura de rede.  Alguns dos conectores incluem:

|  |  |  |  |
| --- | --- | --- | --- |
| [![Ícone da API][db2icon]<br/>**DB2**][db2doc] | [![Ícone da API][oracle-DB-icon]<br/>**Oracle DB**][oracle-db-doc] | [![Ícone da API][sharepointicon]<br/>**SharePoint</br> Server**][sharepointserver] | [![Ícone da API][filesystem-icon]<br/>**Sistema</br> de Arquivos**][filesystemdoc] |
[![Ícone da API][sql-servericon]<br/>**SQL</br> Server**][sql-serverdoc] | ![Ícone de API][Biztalk-Servericon]<br/>**BizTalk</br> Server**| |

### <a name="integration-account-connectors"></a>Conectores da conta de integração 

O Enterprise Integration Pack (EIP) inclui conectores conhecidos na comunidade do BizTalk Server. Ao adquirir uma [conta de integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), você também pode obter os seguintes conectores: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![Ícone da API][as2icon]<br/>**Decodificação</br> de AS2**][as2decode] | [![Ícone da API][as2icon]<br/>**Codificação</br> de AS2**][as2encode] | [![Ícone da API][x12icon]<br/>**Decodificação</br> de EDIFACT**][EDIFACTdecode] | [![Ícone da API][x12icon]<br/>**Codificação</br> de EDIFACT**][EDIFACTencode] |
[![Ícone da API][flatfileicon]<br/>**Codificação</br> de arquivo simples**][flatfiledoc] | [![Ícone da API][flatfiledecodeicon]<br/>**Decodificação</br> de arquivo simples**][flatfiledecodedoc] | [![Ícone da API][integrationaccounticon]<br/>**Conta<br/>de integração**][integrationaccountdoc] | [![Ícone da API][xmltransformicon]<br/>**Transformação<br/>XML**][xmltransformdoc] |
| [![Ícone da API][x12icon]<br/>**Decodificação</br> de X12**][x12decode] | [![Ícone da API][x12icon]<br/>**Codificação</br> de X12**][x12encode] | [![Ícone da API][xmlvalidateicon]<br/>**Validação de <br/>XML**][xmlvalidatedoc] | |

### <a name="enterprise-connectors"></a>Conectores empresariais

Conecte-se com os seus aplicativos corporativos dentro de seus aplicativos lógicos.

|  |  |
| --- | --- |
|[![Ícone da API][MQicon]<br/>**MQ**][mqdoc]|[![Ícone da API][SAPicon]<br/>**SAP**][sapconnector]|

> [!TIP]
> Para começar a usar os aplicativos lógicos do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar os Aplicativos Lógicos](https://tryappservice.azure.com/?appservice=logic). Você pode criar imediatamente um aplicativo lógico de início e de curta duração. Nenhum cartão de crédito é exigido, sem compromissos.

## <a name="connectors-as-triggers-and-actions"></a>Conectores como gatilhos e ações

Um **gatilho** inicia ou executa uma instância de seu aplicativo lógico. Alguns conectores fornecem gatilhos que podem notificar seu aplicativo quando ocorrem eventos específicos. Por exemplo, o conector de FTP tem o `OnUpdatedFile` gatilho que inicia seu aplicativo lógico quando um arquivo é atualizado. 

Os aplicativos lógicos incluem os seguintes tipos de gatilhos:  

* *Gatilhos de pesquisa*: esses gatilhos pesquisam seu serviço de interesse a uma frequência especificada para verificar se há novos dados. 

    Quando novos dados são disponibilizados, uma nova instância do aplicativo lógico é executada com os dados como entrada. 

* *Gatilhos de push*: esses gatilhos escutam dados em um ponto de extremidade ou a ocorrência de eventos e disparam uma nova instância de seu aplicativo lógico.

* *Gatilho de recorrência*: esse gatilho cria uma instância do aplicativo lógico em um agendamento prescrito.

Os conectores também fornecem **ações** que podem ser usadas no fluxo de trabalho. Por exemplo, seu aplicativo lógico pode procurar dados e usá-los posteriormente em seu aplicativo lógico. Mais especificamente, você pode pesquisar os dados do cliente de um banco de dados SQL e, em seguida, usar esses dados para compilar seu fluxo de trabalho. 

> [!TIP]
> [Visão geral de conectores](connectors-overview.md) fornece mais detalhes sobre gatilhos e ações. 


## <a name="message-manipulation-actions"></a>Ações de manipulação de mensagem

Aplicativos lógicos incluem ações internas que podem alterar ou manipular os dados de conteúdo. O conector de **operações de dados** interno inclui as seguintes ações: 

| | |
|---|---|
| **Compor** | Cria ou gera valores ou objetos para usar mais tarde ou como você prepara seu fluxo de trabalho. Por exemplo, você pode criar um objeto JSON com valores de várias etapas ou calcular uma constante para referência posterior em uma execução do aplicativo lógico. |
| **Criar tabela CSV**<br/>**Criar tabela HTML** | Transforme um conjunto de resultados de matriz em uma tabela HTML ou CSV. Por exemplo, adicione a ação de "Registros da lista" de CRM e adicione um filtro para os registros adicionados hoje. Em seguida, envie os resultados como uma tabela HTML em um email. |
| **Matriz de filtro** (consulta) | Filtre um conjunto de resultados para as entradas que lhe interessam. Por exemplo, pesquise todos os tweets com `#Azure` e, em seguida, "filtre" os tweets retornados para retornar somente os resultados que são `Tweeted_by_followers > 50`. |
| **Join** | Una uma matriz de acordo com um delimitador. Por exemplo, a operação Detectar frases-chave retorna uma matriz de frases-chave. Você pode "unir" com uma `,` ou algo parecido. Portanto, em vez de `["Some", "Phrase"]`, você tem `"Some, Phrase"`. |
| **Analisar o JSON** | Analise e acesse valores de um objeto JSON no designer. Por exemplo, se sua função do Azure retorna um conteúdo JSON, você pode analisá-lo para acessar as propriedades JSON posteriormente em outra etapa. A ação também valida que o JSON corresponde ao esquema especificado no tempo de execução. | 
| **Selecionar** | Selecione determinadas propriedades de uma matriz para processamento adicional. Se você "Listar os registros" do SQL e ele retorna 15 colunas, selecione apenas algumas dessas colunas para processamento adicional. A saída é uma matriz que contém apenas as propriedades selecionadas por você. |

## <a name="custom-connectors-and-azure-certification"></a>Conectores personalizados e certificação do Azure 

Para chamar as APIs que executam o código personalizado ou não estão disponíveis como conectores, você pode estender a plataforma dos aplicativos lógicos [ criando Aplicativos de API baseados no REST](../logic-apps/logic-apps-create-api-app.md). Você também pode criar seus próprios [conectores personalizados](../logic-apps/custom-connector-overview.md) que podem ser disponibilizados para qualquer aplicativo lógico em sua assinatura.

Se você quiser tornar seus Aplicativos de API personalizada públicos e disponíveis para uso no Azure, poderá [enviar seus conectores para a certificação da Microsoft](../logic-apps/custom-connector-submit-certification.md).

## <a name="get-help"></a>Obter ajuda

Para fazer perguntas, responder às perguntas e saber o que os outros usuários dos aplicativos lógicos do Azure estão fazendo, visite o [Fórum de Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

Para ajudar a melhorar os Aplicativos Lógicos do Azure e conectores, vote ou envie ideias no [site de comentários do usuário dos Aplicativos Lógicos](http://aka.ms/logicapps-wish).

Falta um tópico do conector ou algum detalhe que você acha importante? Se sim, ajude-nos adicionando ao nosso tópicos existentes, ou escreva o seu. Nossa documentação é de software livre e hospedada no GitHub. Comece a usá-a no nosso [repositório GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Próximas etapas
* [Criar seu primeiro aplicativo lógico](../logic-apps/quickstart-create-first-logic-app-workflow.md)
* [Criar APIs personalizadas para aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md)
* [Monitorar seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[gatewaydoc]: ../logic-apps/logic-apps-gateway-connection.md "Conectar-se a fontes de dados locais de aplicativos lógicos com o gateway de dados local"
[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Integrar aplicativos lógicos a Aplicativos de API do Serviço de Aplicativo"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Gerenciar arquivos em seu contêiner de blob com o conector de Armazenamento de Blobs do Azure"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Integre aplicativos lógicos com Azure Functions"
[db2doc]: ./connectors-create-api-db2.md "Conectar-se ao IBM DB2 na nuvem ou no local. Atualizar uma linha, obter uma tabela e muito mais"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Conectar-se ao Dynamics CRM Online para que você possa trabalhar com os dados do CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Conectar-se aos Hubs de Eventos do Azure. Receber e enviar eventos entre aplicativos lógicos e Hubs de Eventos"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Conectar-se a um sistema de arquivos local"
[ftpdoc]: ./connectors-create-api-ftp.md "Conectar-se a um servidor FTP / FTPS e para tarefas FTP, incluindo carregar, obter, excluir arquivos e muito mais"
[httpdoc]: ./connectors-native-http.md "Fazer chamadas HTTP com o conector HTTP"
[http-requestdoc]: ./connectors-native-reqres.md "Adicionar ações para solicitações e respostas HTTP aos seus aplicativos lógicos"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Fazer chamadas HTTP com o conector HTTP + Swagger"
[informixdoc]: ./connectors-create-api-informix.md "Conectar-se ao Informix na nuvem ou no local. Ler uma linha, listar as tabelas e muito mais"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Integrar aplicativos lógicos a fluxos de trabalho aninhados"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Conectar-se à sua conta do Office 365. Enviar e receber emails, gerenciar seu calendário e contatos e muito mais"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Conectar-se ao banco de dados Oracle para adicionar, inserir e excluir linhas e muito mais"
[mqdoc]: ./connectors-create-api-mq.md "Conectar ao MQ local ou do Azure e enviar e receber mensagens"
[recurrencedoc]:  ./connectors-native-recurrence.md "Disparar ações recorrentes para aplicativos lógicos"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Conectar-se à sua conta do Salesforce. Gerenciar contas, clientes potenciais, oportunidades e muito mais"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Conectar-se a um sistema SAP local"
[service-busdoc]: ./connectors-create-api-servicebus.md "Envia mensagens de tópicos e filas do barramento de serviço e recebe mensagens de assinaturas e filas do barramento de serviço"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Conectar-se ao SharePoint Online. Gerenciar documentos, listar itens e muito mais"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Conecte-se com o servidor local do SharePoint. Gerenciar documentos, listar itens e muito mais"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Conectar-se ao Banco de Dados SQL do Azure ou SQL Server. Criar, atualizar, obter e excluir entradas em uma tabela do Banco de Dados SQL."
[twitterdoc]: ./connectors-create-api-twitter.md "Conectar-se ao Twitter. Obter cronogramas, postar tweets e muito mais"
[webhookdoc]: ./connectors-native-webhook.md "Adicionar ações e gatilhos de Webhook para seus aplicativos lógicos"

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


[boxDoc]: ./connectors-create-api-box.md "Conectar-se ao Box. Carregar, obter, excluir, listar arquivos e muito mais"
[delaydoc]: ./connectors-native-delay.md "Executar ações atrasadas"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Conectar-se ao Dropbox. Carregar, obter, excluir, listar arquivos e muito mais"
[facebookdoc]: ./connectors-create-api-facebook.md "Conectar-se ao Facebook. Postar em uma linha do tempo, receber um feed de página e muito mais"
[githubdoc]: ./connectors-create-api-github.md "Conectar-se ao GitHub e acompanhar os problemas"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Conectar-se ao GoogleDrive para interagir com os dados."
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Conectar-se ao Google Planilhas para poder pode modificar suas planilhas"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Conectar-se ao Google Tasks para gerenciar suas tarefas."
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Conecta-se ao Google Agenda e pode gerenciar o calendário."
[http-responsedoc]: ./connectors-native-reqres.md "Adicionar ações para solicitações e respostas HTTP aos seus aplicativos lógicos"
[instagramdoc]: ./connectors-create-api-instagram.md "Conectar-se ao Instagram. Disparar ou agir nos eventos"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Conectar-se à sua conta do MailChimp. Gerenciar e automatizar emails"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Conectar-se ao Mandrill para comunicação"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Conectar-se ao Microsoft Translator. Traduzir textos, detectar idiomas e muito mais" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Obtenha informações de vídeo, listas e canais de vídeo e URLs de reprodução de vídeos do Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Conectar-se ao seu Microsoft OneDrive pessoal. Carregar, excluir, listar arquivos e muito mais"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Conectar-se ao seu Microsoft OneDrive corporativo. Carregar, excluir, listar arquivos e muito mais"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Conectar-se à sua caixa de correio do Outlook. Gerenciar seu email, calendários, contatos e muito mais"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Conectar-se ao Microsoft Project Online. Gerenciar seus projetos, tarefas, recursos e muito mais"
[querydoc]: ./connectors-native-query.md "Selecionar e filtrar matrizes com a ação Consultar"
[rssdoc]: ./connectors-create-api-rss.md "Publicar e recuperar itens de feed, disparar operações quando um novo item for publicado em um feed RSS."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Conectar-se ao SendGrid. Enviar email e gerenciar listas de destinatários"
[sftpdoc]: ./connectors-create-api-sftp.md "Conectar-se à sua conta SFTP. Carregar, obter, excluir arquivos e muito mais"
[slackdoc]: ./connectors-create-api-slack.md "Conectar-se ao Slack e postar mensagens em canais do Slack."
[smtpdoc]: ./connectors-create-api-smtp.md "Conectar-se a um servidor SMTP e enviar emails com anexos."
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Conectar-se ao SparkPost para comunicação."
[trellodoc]: ./connectors-create-api-trello.md "Conectar-se ao Trello. Gerenciar seus projetos e organizar o que quiser com qualquer pessoa"
[twiliodoc]: ./connectors-create-api-twilio.md "Conectar-se ao Twilio. Enviar e receber mensagens, obter os números disponíveis, gerenciar números de telefone de entrada e muito mais"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Conectar-se ao Wunderlist. Gerenciar suas tarefas e listas de tarefas, manter sua vida sincronizada e muito mais"
[yammerdoc]: ./connectors-create-api-yammer.md "Conectar-se ao Yammer. Postar mensagens, receber novas mensagens e muito mais"
[youtubedoc]: ./connectors-create-api-youtube.md "Conectar-se ao YouTube. Gerenciar seus vídeos e canais"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[AppServices-icon]: ./media/apis-list/AppServices.png
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
[FileSystem-icon]: ./media/apis-list/filesystem.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
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
[API/Web-Appicon]: ./media/apis-list/appservices.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[CallLogicApp-icon]: ./media/apis-list/calllogicapp.png
[Delayicon]: ./media/apis-list/delay.png
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
