---
title: "aaaMove aplicativos de Serviços BizTalk tooAzure aplicativos lógicos | Microsoft Docs"
description: Mover ou migrar do Azure BizTalk Services MABS tooLogic aplicativos
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>Mover de Serviços BizTalk tooLogic aplicativos

O MABS (Serviços BizTalk do Microsoft Azure) está sendo desativado. Use este tópico toomove seu tooAzure de soluções de integração de MABS aplicativos lógicos. 

## <a name="overview"></a>Visão geral

Os Serviços BizTalk consistem em dois subserviços:

1.  Conexões Híbridas dos Serviços BizTalk da Microsoft
2.  Integração com base em ponte EAI e EDI

Se você estiver procurando as conexões híbridas toomove, em seguida, [conexões híbridas dos serviços de aplicativo do Azure](../app-service/app-service-hybrid-connections.md) descreve alterações de saudação e recursos do serviço. As Conexões Híbridas do Azure substituem as Conexões Híbridas dos Serviços BizTalk. As conexões híbridas do Azure está disponível com o serviço de aplicativo do Azure e são oferecidas em Olá portal do Azure. As conexões híbridas do Azure também fornece um novo toomanage do Gerenciador de Conexão híbrida existente conexões híbridas dos serviços do BizTalk e Olá de novas conexões híbrida, que você cria no portal. As Conexões Híbridas do Serviço de Aplicativo do Azure estão com disponibilidade geral (GA).

Para a integração com base em ponte EAI e EDI, aplicativos lógicos é substituição de saudação. Lógica de aplicativos fornece que todos os Olá os mesmos recursos de Serviços BizTalk e muito mais. Lógica de aplicativos fornece a escala de nuvem consumo recursos baseados em fluxo de trabalho e a coordenação que permitem que você tooquickly e criar facilmente soluções complexas de integração usando um navegador ou usando as ferramentas do Visual Studio.

Olá, a tabela a seguir fornece um mapeamento de recursos de Serviços BizTalk tooLogic aplicativos.

| Serviços do BizTalk   | Aplicativos Lógicos            | Finalidade                  |
| ------------------ | --------------------- | ---------------------------- |
| Conector          | Conector             | Envio e recebimento de dados   |
| Ponte             | Aplicativo Lógico             | Processador de pipeline           |
| Estágio de validação     | Ação de Validação de XML      | Validar um documento XML em relação a um esquema             |
| Estágio de enriquecimento       | Tokens de Dados      | Promover propriedades em mensagens ou para decisões de encaminhamento             |
| Estágio de transformação    | Ação Transformar      | Converter mensagens XML de um formato tooanother             |
| Estágio de decodificação       | Ação de decodificação de arquivo simples      | Converter de tooXML de arquivo simples             |
| Estágio de codificação       |  Ação de codificação de arquivo simples      | Converter o arquivo XML de tooflat             |
| Inspetor de Mensagens       |  Azure Functions ou Aplicativos de API      | Executar código personalizado em suas integrações             |
| Ação de encaminhamento      |  Condição ou Comutador      | Rota tooone de mensagens de saudação especificado conectores             |

Há vários tipos diferentes de artefato nos Serviços BizTalk.

## <a name="connectors"></a>Conectores
Conectores nos Serviços BizTalk permitem toosend pontes e recebem dados, incluindo pontes bidirecionais que habilitado interações de solicitação/resposta com base em HTTP. Aplicativos lógicos, hello mesma terminologia é usada. Conectores de aplicativos lógicos servem Olá a mesma finalidade e também incluir mais 140 que podem se conectar tooa amplo conjunto de tecnologias e serviços, no local usando Olá Gateway de dados local (substituindo Olá serviço de adaptador do BizTalk usada pelo BizTalk Services), e de nuvem SaaS e PaaS serviços como o OneDrive, Office 365, Dynamics CRM e muito mais.

Fontes nos Serviços BizTalk são tooFTP limitado, SFTP e fila do barramento de serviço ou assinatura de tópico.

![](media/logic-apps-move-from-mabs/sources.png)

Cada ponte tem um ponto de extremidade HTTP por padrão, que é configurado com hello endereço de tempo de execução e propriedades do hello endereço relativo da ponte de saudação. tooachieve Olá mesmo com lógica de aplicativos, use Olá [solicitação e resposta](../connectors/connectors-native-reqres.md) ações.

## <a name="xml-processing-and-bridges"></a>Pontes e processamento de XML
Uma ponte nos Serviços BizTalk é análogo tooa o pipeline do processamento. Uma ponte pode levar os dados recebidos de um conector, e alguns trabalhar com dados Olá e, em seguida, enviá-lo tooanother sistema. Lógica de aplicativos Olá mesmo com o suporte à saudação interação mesmo pipeline padrões como serviços do BizTalk e também fornece um número de outros padrões de integração. Olá [ponte de solicitação-resposta XML](https://msdn.microsoft.com/library/azure/hh689781.aspx) nos Serviços BizTalk é conhecido como pipeline VETER consiste em fases, que podem:

* (V) Validar
* (E) Enriquecer
* (T) Transformar
* (E) Enriquecer
* (R) Encaminhar

Conforme visto no Olá a imagem a seguir, o processamento de saudação é dividido entre solicitação e resposta e permite o controle sobre a solicitação hello e hello caminhos de resposta separadamente (por exemplo, usando mapas diferentes para cada):

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

Além disso, uma ponte unidirecional XML adiciona estágios decodificação e codificação no início de saudação e no final do processamento e Olá ponte de passagem contém um estágio de enriquecimento único.

### <a name="message-processing-and-decodingencoding"></a>Processamento de mensagens e codificação/decodificação
Nos serviços do BizTalk, você recebe mensagens XML de tipos diferentes e determinar o esquema correspondente Olá Olá mensagem recebida. Isso é executado em Olá **tipos de mensagem** estágio da saudação pipeline de processamento de recebimento. Em seguida, Olá estágio de decodificação usa toodecode de tipo de mensagem de saudação detectada usando esquema Olá fornecido. Se o esquema de saudação é um esquema de flatfile, ele converte Olá entrada flatfile tooXML. 

Os Aplicativos Lógicos fornecem recursos semelhantes. Você receber um flatfile por uma variedade de protocolos diferentes usando gatilhos de conector diferente da saudação (sistema de arquivos, FTP, HTTP e assim por diante) e usar o hello [decodificação de arquivo simples](../logic-apps/logic-apps-enterprise-integration-flatfile.md) ação tooconvert Olá entrada dados tooXML. Você pode mover os esquemas de arquivo simples existente diretamente toologic aplicativos sem a necessidade de qualquer alterações e, em seguida, carregar esquemas tooyour conta Integration.

### <a name="validation"></a>Validação
Olá os dados de entrada tooXML convertido (ou se o XML foi recebido de formato de mensagem de saudação), a validação será executado toodetermine se a mensagem de saudação cumpre o esquema XSD de tooyour. toodo isso na lógica de aplicativos, use Olá [validação de XML](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) ação. Novamente, você pode usar Olá mesmo esquemas dos Serviços BizTalk sem quaisquer alterações.

### <a name="transform-messages"></a>Transformar mensagens
Nos serviços do BizTalk, o estágio de transformação de saudação converte um tooanother de formato de mensagens baseada em XML. Isso é feito aplicando um mapa, usando o mapeador de saudação com base em TRFM. Em aplicativos lógicos, o processo de saudação é semelhante. Olá transformação ação executa um mapa de sua conta de integração. Olá principal diferença é que os mapas de aplicativos lógicos estão no formato XSLT. XSLT inclui Olá capacidade tooreuse existente já, inclusive mapas criados para o BizTalk Server que contêm functoids XSLT. 

### <a name="routing-rules"></a>Regras de roteamento
Os serviços do BizTalk toma uma decisão de roteamento no qual ponto de extremidade/conector toosend mensagens/dados de entrada. Olá capacidade tooselect um de um número de pontos de extremidade pré-configurados é possível usar a opção de filtro de roteamento de saudação:

![](media/logic-apps-move-from-mabs/route-filter.png)

Os Aplicativos Lógicos fornecem recursos de lógica mais sofisticada com [Condição](../logic-apps/logic-apps-use-logic-app-features.md) e [Opção](../logic-apps/logic-apps-switch-case.md), habilitando o fluxo de controle e o encaminhamento avançados. A conversão de filtros de encaminhamento nos Serviços BizTalk é obtida da melhor forma usando uma **condição** *se* existem apenas duas opções. Se houver mais de duas, use uma **opção**.

### <a name="enrich"></a>Enriquecer
Olá estágio enriquecimento no processamento do BizTalk Services adiciona o contexto da mensagem associado aos dados Olá recebidos toohello propriedades. Por exemplo, promovendo um toouse de propriedade para roteamento (abordado abaixo) de uma pesquisa de banco de dados, ou extraindo um valor usando uma expressão XPath. Lógica de aplicativos fornece acesso tooall dados contextuais saídas de precedentes ações, tornando fácil tooreplicate Olá mesmo comportamento. Por exemplo, usando Olá `Get Row` ação de conexão do SQL, você retornar dados de um banco de dados do SQL Server e usar Olá dados em uma ação de decisão de roteamento. Da mesma forma, propriedades de entrada do barramento do serviço de mensagens em fila por um gatilho são endereçável, bem como XPath usando a expressão de linguagem de definição de fluxo de trabalho do hello xpath.

### <a name="use-custom-code"></a>Usar código personalizado
Os serviços do BizTalk fornece a capacidade de saudação muito[executar código personalizado](https://msdn.microsoft.com/library/azure/dn232389.aspx) carregado em seus próprios conjuntos. Isso é implementado por Olá [Imessegeinspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) interface. Cada estágio na ponte de saudação inclui duas propriedades (Inspetor na entrada e na saída do Inspetor) que fornecem o tipo de .net de saudação criado que implementa essa interface. Código personalizado permite que você tooperform mais complexos, processamento de dados hello, bem como a reutilização de código existente em assemblies que executam a lógica de negócios comuns. 

Lógica de aplicativos fornece duas maneiras principais de código personalizado tooexecute: funções do Azure e aplicativos de API. Azure Functions podem ser criadas e chamadas de aplicativos lógicos. Confira [Adicionar e executar código personalizado para aplicativos lógicos por meio de Azure Functions](../logic-apps/logic-apps-azure-functions.md). Use aplicativos de API, parte do serviço de aplicativo do Azure, toocreate seus próprios gatilhos e ações. Saiba mais sobre [criando um toouse API personalizada com aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md). 

Se você tiver código personalizado em assmeblies que você chama a partir dos Serviços BizTalk, poderá mover esse código tooAzure funções ou criar APIs personalizadas com aplicativos de API. Dependendo de como você está implementando. Por exemplo, se você tiver código que encapsula a outro serviço que a lógica de aplicativos não tem um conector, em seguida, criar uma API App e usar ações de saudação que seu aplicativo de API fornece dentro de seu aplicativo de lógica. Se você tiver funções auxiliares ou bibliotecas, funções do Azure é provavelmente Olá melhor ajuste.

### <a name="edi-processing-and-trading-partner-management"></a>Gerenciamento de parceiros comerciais e processamento de EDI
Os Serviços BizTalk incluem processamento de EDI e B2B com suporte para AS2 (Applicability Statement 2), X12 e EDIFACT. Os Aplicativos Lógicos também. Nos serviços do BizTalk, a criar pontes EDI e criar/gerenciar parceiros comerciais e acordos no portal de gerenciamento e controle da dedicado hello.

Em aplicativos lógicos, essa funcionalidade é incluída com hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md). Isso consiste em ações de conta de integração e B2B Olá para processamento de EDI e B2B. Olá [conta Integration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) é toocreate usado e gerenciar [parceiros comerciais](../logic-apps/logic-apps-enterprise-integration-partners.md) e [contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md). Depois de criar uma conta de integração, você pode associar uma ou mais contas de toohello aplicativos de lógica. Quando associado, você pode usar o hello B2B ações tooaccess comerciais dentro de seu aplicativo de lógica de informações do parceiro. Olá ações a seguir é fornecido:

* Codificar AS2
* Decodificar AS2
* Codificar X12
* Decodificar X12
* Codificação de EDIFACT
* Decodificação de EDIFACT

Diferentemente de serviços do BizTalk, essas ações são separadas de protocolos de transporte de saudação. Então quando você cria seus aplicativos lógicos, você tem mais flexibilidade em conectores de que você usa toosend e recebe dados. Por exemplo, é possível tooreceive X12 arquivos como anexos de email e, em seguida, processar esses arquivos em um aplicativo lógico. 

## <a name="manage-and-monitor"></a>Gerenciar e monitorar
Bem como o gerenciamento de parceiro de negociação, Olá dedicados ao portal de Serviços BizTalk fornecido toomonitor recursos de rastreamento e solução de problemas. 

Lógica de aplicativos fornece controle mais avançados e monitoramento de recursos no hello [portal do Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md)e com hello [solução B2B Operations Management Suite](../logic-apps/logic-apps-monitor-b2b-message.md), inclusive um aplicativo móvel para manter o olho em coisas Quando você estiver no hello mova.

## <a name="high-availability"></a>Alta disponibilidade
tooachieve alta disponibilidade (HA) nos Serviços BizTalk, você usar mais de uma instância em uma saudação de tooshare região determinada carga de processamento. Com os Aplicativos Lógicos, a HA na região é interna e é fornecida sem custo adicional. Para recuperação de desastre fora de região para o processamento B2B nos Serviços BizTalk, é necessário um processo de backup e restauração. Em aplicativos de lógica, um ativo/passivo entre regiões [capacidade de recuperação de desastres](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) é fornecido; que permite a sincronização de saudação de dados de B2B entre contas de integração em regiões diferentes para continuidade de negócios.

## <a name="next"></a>Avançar
* [O que são Aplicativos Lógicos](logic-apps-what-are-logic-apps.md)
* [Crie seu primeiro aplicativo lógico](logic-apps-create-a-logic-app.md) ou comece rapidamente usando um [modelo predefinido](logic-apps-use-logic-app-templates.md)  
* [Exibir todos os conectores disponíveis de Olá](../connectors/apis-list.md) você pode usar em um aplicativo de lógica
