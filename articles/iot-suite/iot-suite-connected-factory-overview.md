---
title: "Visão geral da fábrica de conectado aaaAzure IoT Suite | Microsoft Docs"
description: "Uma descrição do hello Azure IoT Suite conectado solução pré-configurada de fábrica."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Introdução à solução de fábrica pré-configurado Olá conectado

Azure IoT Suite [soluções pré-configuradas] [ lnk-preconfigured-solutions] combinar várias IoT do Azure services toodeliver ponta a ponta soluções que implementam cenários comuns de negócios de IoT. Olá *fábrica conectada* solução pré-configurada conecta tooand monitora seus dispositivos industriais. Você pode usar o fluxo de saudação do hello solução tooanalyze de dados de seus dispositivos e produtividade operacional toodrive e lucratividade.

Este tutorial mostra como tooprovision Olá conectadas fábrica pré-configurado de solução. Ele também orienta você por meio de recursos básicos de saudação da solução Olá pré-configurado. Você pode acessar muitos desses recursos de solução de saudação *painel* que implanta como parte da solução Olá pré-configurados:

![Painel de solução pré-configurada de fábrica conectada][img-cf-home]

toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.

> [!NOTE]
> Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].
> 
> 

## <a name="provision-hello-solution"></a>Provisionar Olá solução

1. Faça logon no tooazureiotsuite.com usando suas credenciais de conta do Azure e, em seguida, clique em "**+**" toocreate uma solução.
2. Clique em **selecione** em Olá **fábrica conectada** lado a lado.
3. Digite um **Nome de solução** para a solução pré-configurada de fábrica conectada.
4. Selecione Olá **assinatura** e **região** deseja toouse tooprovision Olá solução.
5. Clique em **criar solução** Olá toobegin processo de provisionamento. Normalmente, esse processo leva vários toorun de minutos.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>Enquanto aguarda Olá toocomplete do processo de provisionamento

1. Clique em bloco de saudação para sua solução com **provisionamento** status.
2. Saudação de aviso **provisionamento estados** como serviços do Azure são implantados na sua assinatura do Azure.
3. Após a conclusão do provisionamento, Olá alterações de status muito**pronto**.
4. Clique em Olá bloco toosee Olá detalhes de sua solução no painel direito da saudação.

> [!NOTE]
> Se você encontrar problemas de implantação de solução Olá pré-configurado, examine [permissões no site do hello azureiotsuite.com] [ lnk-permissions] e hello [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md). Se os problemas de saudação persistirem, criar um tíquete de serviço em Olá [portal][lnk-portal].

Há detalhes esperado toosee que não estejam listados para sua solução? Envie sugestões de recursos no [User Voice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="scenario-overview"></a>Visão geral do cenário

Quando você implanta Olá conectado fábrica pré-configurado solução, ele será preenchido com recursos que permitem que você toostep por meio de um cenário industrial comum. Nesse cenário, diversas fábricas conectado relatórios de solução de toohello toocompute necessária de valores de dados de saudação eficiência geral de equipamentos (OEE) e indicadores chave de desempenho (KPIs). Olá seções a seguir mostram como para:

* Monitorar fábrica, linhas de produção, OEE de estação e valores de KPI
* Analisar dados de telemetria Olá gerados a partir desses dispositivos usando o Azure Insights de série de tempo
* Agir sobre problemas de toofix de alertas

Um recurso principal deste cenário é que você pode executar todas essas ações remotamente no painel de solução de saudação. Dispositivos de toohello acesso físico não é necessário.

## <a name="view-hello-solution-dashboard"></a>Painel de solução de saudação de View

Painel de solução de saudação permite toomanage solução de saudação implantada. É uma representação hierárquica de uma configuração global de fábrica. Por exemplo, você pode exibir KPIs e OEE, publicar novos nós para alertas de telemetria e de ação.

1. Quando Olá provisionamento for concluído e lado a lado para sua solução pré-configurada Olá indica **pronto**, escolha **iniciar** tooopen seu portal de solução de fábrica conectados em uma nova guia.

    ![Iniciar a solução de saudação pré-configurado][img-launch-solution]

1. Por padrão, o portal de solução Olá mostra Olá *painel*. toonavigate tooother áreas do portal hello, use o menu de saudação no lado esquerdo de saudação da página de saudação.

    ![Painel de solução pré-configurada de fábrica conectada][cf-img-menu]

Painel de saudação exibe Olá informações a seguir:

* Um **lista fábrica** painel que mostra o status de saudação, o local e a configuração atual de produção na solução de saudação. Quando você executa solução hello, há um número de dispositivos simulados. simulação de linha de produção de Hello é composta de três OPC UA servidores reais por linha de produção que executem tarefas simuladas e compartilham dados. Para obter mais informações sobre OPC UA, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).
* Um **mapa** exibe Olá local de cada dispositivo conectado toohello solução. solução de saudação pode usar informações de tooplot de API do Bing Maps Olá mapa hello. Se sua assinatura estiver habilitada para a API do Bing Maps Enterprise, esse recurso será usado automaticamente. Se não, consulte Olá [perguntas frequentes sobre] [ lnk-faq] toolearn como toomake Olá mapa dinâmico.
* Um painel **Alertas** que exibe alertas gerados quando um valor KPI/OEE ou de telemetria excede um limite específico.
* Um **eficiência geral de equipamento** painel que mostra valores OEE Olá Olá fábrica/produção ou empresa inteira Olá linha/estação que você está exibindo. Esse valor é agregado de saudação estação exibição toohello de nível empresarial. a Figura OEE Hello e seus elementos constituintes podem ser analisados adicional.
* **Indicadores chave de desempenho** painel que exibe o número de saudação de unidades produzidas e energia usada pela empresa inteira hello ou linha de fábrica/produção de hello/estação que você está exibindo. Esses valores são agregados de um nível de empresa toohello estação exibição.

## <a name="view-factories"></a>Exibir fábricas

Olá *fábricas* painel mostra Olá localização geográfica de todas as fábricas de Olá Olá solução, seus status e configuração de produção atual. Na lista de locais de saudação, você pode navegar toohello outros níveis na hierarquia de solução de saudação. linhas de saudação na lista de saudação são hiperlinks que vinculam os detalhes das linhas de produção de hello nesse local. É possível toodrill em detalhes da linha de produção de hello e para baixo de exibição de nível de estação de toohello. Você também pode aplicar uma lista de toohello de filtro.

![Fábricas de solução pré-configurada de fábrica conectada][cf-img-factories] 

1. Olá **painel fábrica** Olá mostra a lista de fábrica para esta solução.

2. lista de fábrica Olá inicialmente mostra seis fábricas criadas pelo processo de provisionamento de saudação. Você pode adicionar a solução de toohello de dispositivos adicionais simulada e físico.

3. tooview detalhes de saudação de uma fábrica, clique em lista de fábrica de saudação da linha de saudação.

4. detalhes de saudação tooview de uma linha de produção, clique em lista de saudação da linha de saudação.

5. Olá tooview publicado nós OPC UA da estação na linha de produção de hello, clique em linha hello na lista de saudação.

6. tooview detalhes em um nó específico na estação Olá, clique em lista de saudação da linha de saudação. Essa ação inicia o painel de contexto Olá com visualizações de informações da série de tempo. Clique nessas análises adicionais de toodo gráficos em ambiente de explorer Olá Insights de série de tempo.

## <a name="view-map"></a>Exibir mapa

Se sua assinatura tiver acesso toohello API do Bing Maps, Olá *fábricas* mapa mostra localização geográfica hello e o status de todas as fábricas de saudação na solução de saudação. toodrill detalhes Olá local, clique em locais de saudação exibidos no mapa de saudação.

![Mapa de solução pré-configurada de fábrica conectada][cf-img-map]

## <a name="view-alerts"></a>Exibir alertas

Olá **alerta** painel mostra alertas gerados devido tooa relatado valor ou um valor calculado de OEE/KPI exceder seu limite configurado. Esse painel exibe alertas em cada nível da hierarquia de hello, da exibição global do toohello Olá estação exibição de nível. alertas de saudação contêm uma descrição do alerta hello, data, hora, local e número de ocorrências. Você pode obter informações em dados toohello que causou o alerta de saudação usando Olá dados Insights de série de tempo. Olá tempo série Insights dados são visualizados no hello alertas, onde aplicável. Se você for um administrador, você pode executar ações de padrão em alertas hello, como:

* Alerta de saudação fechar.
* Reconhece o alerta de saudação.

Opcionalmente, você pode executar ações mais complexas. Por exemplo, para Olá pressão OPC UA nó de saudação Assembly, você pode:

* Exiba informações de suporte em uma página da Web em uma nova janela do navegador.
* Mitigar a causa de saudação do alerta Olá chamando um método de OPC UA no dispositivo de saudação.
* Suprima a disponibilidade de saudação de ações de padrão de saudação.

    ![Alertas de solução pré-configurada de fábrica conectada][cf-img-alerts]

> [!NOTE]
> Esses alertas são gerados por regras que são especificadas em um arquivo de configuração na solução Olá pré-configurado. Essas regras podem gerar alertas quando Olá OEE ou valores KPI ou valores de OPC UA nó estão excedendo o limite configurado.

1. Olá **painel alertas** mostra Olá alertas gerados nesta solução.

2. detalhes de saudação tooview de um alerta, clique no painel de alertas Olá Olá.

3. toofurther analisar dados de alerta de saudação, clique em gráfico de saudação no ambiente de explorer Olá painel alerta tooopen Olá Insights de série de tempo.

4. tooaddress Olá alerta, várias ações estão disponíveis no painel alerta hello. Escolha a opção apropriada Olá para você e clique em Olá executar botão de comando de ação.

## <a name="view-overall-equipment-efficiency"></a>Exibir a eficiência geral do equipamento

Taxas OEE Olá eficiência do processo de produção de hello usando uma chave parâmetros operacionais relacionados à produção. OEE é um padrão de medida calculada multiplicando a taxa de disponibilidade hello, a taxa de desempenho e a taxa de qualidade da indústria: OEE = disponibilidade x qualidade de desempenho x.

![OEE de solução pré-configurada de fábrica conectada][cf-img-oee]

1. tooview OEE para qualquer nível da hierarquia hello, navegue toohello exibição específica que você precisa. Olá OEE para essa exibição é exibido no painel de saudação junto com cada um dos elementos de saudação que compõem a saudação porcentagem OEE.

2. toofurther analisar hello OEE para qualquer nível de dados da hierarquia hello, clique Olá OEE, disponibilidade, desempenho ou porcentagem de qualidade. Um painel de contexto é exibida com informações da série de tempo alimentadas visualizações que mostra dados de saudação última hora, últimas 24 horas e últimos 7 dias.

    ![Visualização de TSI de solução pré-configurada de fábrica conectada][cf-img-tsi-visualization]

3. toofurther analisar dados de alerta de saudação, clique em gráfico de saudação no painel alerta hello. Essa ação abre o ambiente de explorer Olá Insights de série de tempo.

    ![Explorador de TSI de solução pré-configurada de fábrica conectada][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Exibir Indicadores Chave de Desempenho

solução de saudação fornece dois indicadores chave de desempenho, *unidades por hora* e *energia usada em kWh*.

![KPI de solução pré-configurada de fábrica conectada][cf-img-kpi]

1. unidades de tooview por hora ou energia usada para qualquer nível da hierarquia hello, navegue toohello exibição específica que você precisa. unidades de saudação por hora e energia usadas exibição no painel de saudação.

2. unidades tooanalyze por hora ou energia usada para qualquer nível na hierarquia de saudação adicional, clique em Olá indicador em hello **indicadores chave de desempenho** painel. Um painel de contexto é exibido com visualizações de Insights de série de tempo da plataforma, permitindo que você tooview dados Olá última hora, Olá últimas 24 horas e últimos 7 dias.

## <a name="scenario-review"></a>Análise do cenário

Nesse cenário, você monitorou os fábricas OEE KPIs valores e, no painel de saudação. Em seguida, usado tooprovide de informações da série de tempo mais informações toohelp aprofundar ainda mais em dados de telemetria Olá para KPIs e OEE toohelp com detecção de anomalias. Você também usado problemas de tooview do painel alerta Olá com seu fábricas e você usou o alerta de Olá Olá ações disponíveis tooyou tooresolve.

## <a name="other-features"></a>Outros recursos

Olá seções a seguir descreve alguns recursos adicionais de solução de fábrica Olá conectado que não são descritos no cenário anterior hello.

## <a name="apply-filters"></a>Aplicar filtros

1. Clique em Olá **divisa** toodisplay uma lista de filtros disponíveis no painel de locais de fábrica hello ou painel de alertas de saudação.

2. Painel de filtros de saudação é exibida para você. 

    ![Filtros de solução pré-configurados de fábrica conectada][cf-img-alert-filter]

3. Escolha o filtro de saudação que você precisa. Também é possível tootype o texto livre nos campos de filtro de saudação.

4. saudação de filtro é aplicada para você. estado do filtro Olá também é exibido no painel de saudação por meio de um funil que exibe em fábricas hello e tabelas de alertas.

    ![Filtros de solução pré-configurados de fábrica conectada][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Um filtro ativo não afeta valores hello exibido OEE e um KPI, ela apenas filtra o conteúdo da lista de saudação.

5. tooclear um filtro, clique em funil hello e filtro no painel de contexto de filtro de saudação. Olá texto **todos os** é exibido no fábricas hello e tabelas de alertas.

## <a name="browse-an-opc-ua-server"></a>Procurar um servidor de OPC UA

Quando você implanta a solução Olá pré-configurados, você automaticamente provisionar servidores OPC UA simulados que você pode procurar por meio do Gerenciador de soluções de saudação. Esses servidores são *servidores OPC UA simulados*. Servidores simuladas tornam mais fácil para você tooexperiment com solução Olá pré-configurado sem Olá necessidade toodeploy real servidores físicos. Se você quiser tooconnect uma solução de toohello servidor OPC UA real, consulte Olá [conectar sua solução de fábrica pré-configurado OPC UA dispositivo toohello conectado] [ lnk-connect-cf] tutorial.

1. Clique em Olá **ícone fábrica** na barra de navegação do painel de saudação.

    ![Navegador de servidor de chamada de solução pré-configurada de fábrica conectada][cf-img-server-browser]

2. Escolha um dos servidores de saudação lista pré-configurado de saudação. Esta lista mostra os servidores de saudação que são implantados na solução Olá pré-configurado.

    ![Seleção de chamada de solução pré-configurada de fábrica conectada][cf-img-server-choice]

3. Clique em **Conectar**. Uma caixa de diálogo de segurança será exibida. Simulação de Olá, é seguro tooclick **prosseguir**

4. tooexpand qualquer um de nós de saudação na árvore de saudação do servidor, clique nele. Nós que estão publicando telemetria têm uma marcação ao lado deles.

    ![Árvore de chamada de solução pré-configurada de fábrica conectada][cf-img-server-tree]

5. Clique com botão direito tooread um item, gravar, publicar ou chamar esse nó. Olá ações disponíveis tooyou dependem de suas permissões e os atributos de saudação do nó de saudação. Olá ler opção toodisplays um painel de contexto que mostram o valor de saudação do nó específico hello. Olá gravar opção exibe um painel de contexto em que você pode inserir um novo valor. opção de chamada Hello exibe um nó onde você pode inserir parâmetros Olá para chamada de saudação.

## <a name="publish-a-node"></a>Publicar um nó

Quando você procura um *server simulada de OPC UA*, você também pode escolher toopublish novos nós. Você pode analisar a telemetria de saudação desses nós na solução de saudação. Essas *simulados servidores OPC UA* torná-lo tooexperiment fácil com a solução Olá pré-configurado sem implantar dispositivos físicos reais.

1. Procure nó tooa Olá árvore do navegador OPC UA server que você deseja toopublish.

2. Nó de saudação com o botão direito.

3. Escolha **Publicar**.

    ![A fábrica conectada publica o nó][cf-img-publish-node]

4. Um painel de contexto é exibido que informa que Olá publicação foi bem-sucedida. nó de saudação aparece na exibição de nível de estação Olá com uma marca de seleção ao lado dela.

    ![Publicação com êxito de chamada de solução pré-configurada de fábrica conectada][cf-img-publish-success]

## <a name="command-and-control"></a>Comando e controle

fábrica conectado Olá permite comando e controlar os dispositivos de setor diretamente da nuvem hello. Você pode usar este tooalerts toorespond de recurso gerado pelo dispositivo hello. Por exemplo, você pode enviar um dispositivo de toohello do comando de nuvem hello. Você pode encontrar hello comandos disponíveis no hello **StationCommands** nó Olá árvore do navegador de servidores de OPC UA. Nesse cenário, você deve abrir uma válvula de versão de pressão na estação de assembly de saudação de uma linha de produção em Munique. toouse Olá comando e controle de funcionalidade, você deve estar no hello **administrador** função hello pré-configurado a implantação da solução.

1. Procurar toohello **StationCommands** nó Olá árvore do navegador de servidor OPC UA.

2. Escolha o comando Olá que você deseja usar.

3. Nó de saudação com o botão direito.

4. Escolha **Chamar**.

    ![Comando de chamada de solução pré-configurada de fábrica conectada][cf-img-call-command]

5. Um painel de contexto é exibido informando a você qual método você sobre toocall e quaisquer detalhes de parâmetro é aplicável.

6. Escolha **Chamar**.

    ![Contexto de chamada de solução pré-configurada de fábrica conectada][cf-img-call-context]

7. Painel de contexto de saudação é atualizada tooinform que Olá chamada de método foi bem-sucedida. Você pode verificar a chamada hello teve êxito ao ler o valor de saudação do nó de pressão Olá atualizados como resultado da chamada de saudação.

    ![Sucesso de chamada de solução pré-configurada de fábrica conectada][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Em segundo plano da saudação

Quando você implanta uma solução pré-configurada, o processo de implantação de saudação cria vários recursos no hello assinatura do Azure que você selecionou. Você pode exibir esses recursos no hello Azure [portal][lnk-portal]. o processo de implantação Olá cria um **grupo de recursos** com um nome baseado no nome hello escolhido para sua solução pré-configurada:

![Solução pré-configurada em Olá portal do Azure][img-cf-portal]

Você pode exibir configurações de saudação de cada recurso, selecionando-o na lista de saudação de recursos no grupo de recursos de saudação.

Você também pode exibir o código-fonte Olá para solução de saudação pré-configurado. Olá conectado fábrica pré-configurado solução código-fonte está em Olá [azure iot-conectado-fábrica] [ lnk-cfgithub] repositório GitHub:

Quando você terminar, você pode excluir solução Olá pré-configurado de sua assinatura do Azure em Olá [azureiotsuite.com] [ lnk-azureiotsuite] site. Este site permite que você exclua tooeasily que todos os recursos que foram provisionados quando você criou a solução Olá pré-configurado de hello.

> [!NOTE]
> tooensure excluir tudo relacionados à solução toohello pré-configurado, excluí-la em Olá [azureiotsuite.com] [ lnk-azureiotsuite] site. Não exclua o grupo de recursos de saudação no portal de saudação.

## <a name="next-steps"></a>Próximas etapas

Agora que você implantou uma solução de trabalho pré-configurados, você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:

* [Passo a passo de solução pré-configurada de fábrica conectada][lnk-rm-walkthrough]
* [Conectar sua solução do dispositivo toohello conectado fábrica pré-configurado][lnk-connect-cf]
* [Permissões no site de azureiotsuite.com Olá][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md