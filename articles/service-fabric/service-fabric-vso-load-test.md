---
title: aaaLoad testar seu aplicativo usando o Visual Studio Team Services | Microsoft Docs
description: Saiba como toostress testar seus aplicativos do Azure Service Fabric usando o Visual Studio Team Services.
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Executar teste de carga em seu aplicativo usando o Visual Studio Team Services
Este artigo mostra como toouse Microsoft Visual Studio load test recursos toostress testar um aplicativo. Ele usa um back-end de serviço com estado e um front-end da Web de serviço sem estado do Service Fabric do Azure. Olá, o aplicativo de exemplo usado aqui é um simulador de local de avião. Você fornece uma ID de avião, um horário de partida e um destino. back-end do aplicativo Hello processa solicitações de saudação e front-end Olá exibe em um avião de saudação do mapa que corresponde aos critérios de saudação.

Olá diagrama a seguir ilustra aplicativo do Service Fabric hello que será testado.

![Diagrama de aplicativo de local de avião de exemplo hello][0]

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, você precisa seguinte de saudação do toodo:

* Obtenha uma conta do Visual Studio Team Services. É possível obter uma gratuitamente no site do [Visual Studio Team Services](https://www.visualstudio.com).
* Obtenha e instale o Visual Studio 2013 ou o Visual Studio 2015. Este artigo usa o Visual Studio 2015 Enterprise, mas o Visual Studio 2013 e outras edições devem funcionar da mesma forma.
* Implante seu tooa aplicativo ambiente de preparo. Consulte [como toodeploy aplicativos tooa remoto de cluster usando o Visual Studio](service-fabric-publish-app-remote-cluster.md) para obter informações sobre isso.
* Entenda o padrão de uso do aplicativo. Essa informação é o padrão de carga Olá toosimulate usado.
* Entenda a meta de saudação para testes de carga. Isso ajuda você a interpretar e analisar os resultados de teste de carga hello.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Criar e executar o projeto de teste de carga e desempenho na Web Olá
### <a name="create-a-web-performance-and-load-test-project"></a>Criar um projeto de Teste de Carga e de Desempenho na Web
1. Abra o Visual Studio 2015. Escolha **arquivo** > **novo** > **projeto** no menu de saudação barra Olá tooopen **novo projeto** caixa de diálogo.
2. Expanda Olá **Visual C#** nó e escolha **teste** > **projeto de teste de carga e desempenho na Web**. Dê um nome de projeto hello e escolha Olá **Okey** botão.

    ![Captura de tela da caixa de diálogo Novo projeto Olá][1]

    Você deverá ver, no Gerenciador de Soluções, um novo projeto de Teste de Carga e de Desempenho na Web.

    ![Captura de tela do Gerenciador de soluções mostrando novo projeto de saudação][2]

### <a name="record-a-web-performance-test"></a>Registrar um teste de desempenho Web
1. Projeto de WebTest Olá aberto.
2. Escolha Olá **Adicionar gravação** ícone toostart uma sessão de gravação no seu navegador.

    ![Captura de tela de ícone de adicionar gravação da saudação em um navegador][3]

    ![Captura de tela do botão de registro de saudação em um navegador][4]
3. Navegar no aplicativo de malha do serviço toohello. Painel de gravação da saudação deve mostrar Olá web solicitações.

    ![Captura de tela de solicitações da web em Olá gravação de painel][5]
4. Execute uma sequência de ações que você espera Olá tooperform de usuários. Essas ações são usadas como uma carga de saudação toogenerate padrão.
5. Quando terminar, escolha Olá **parar** gravação de toostop do botão.

    ![Captura de tela do botão Parar de saudação][6]

    projeto de WebTest Olá no Visual Studio deve ter capturado uma série de solicitações. Os parâmetros dinâmicos são substituídos automaticamente. Neste ponto, você pode excluir qualquer solicitação de dependência extra e repetida que não faça parte do seu cenário de teste.
6. Salvar o projeto de saudação e, em seguida, escolha Olá **executar teste** desempenho da web do comando toorun Olá testar localmente e verifique se tudo está funcionando corretamente.

    ![Captura de tela de saudação comando Executar teste][7]

### <a name="parameterize-hello-web-performance-test"></a>Parâmetros de teste de desempenho web Olá
Você pode parametrizar teste de desempenho web hello, convertendo-o teste de desempenho web codificado de tooa e editando código hello. Como alternativa, você pode associar a lista de dados tooa do teste de desempenho de web hello para que hello teste itera dados saudação. Consulte [gerar e executar um teste de desempenho web codificado](https://msdn.microsoft.com/library/ms182552.aspx) para obter detalhes sobre como tooa de teste de desempenho do tooconvert Olá web codificados teste. Consulte [adicionar um teste de desempenho da web dados fonte tooa](https://msdn.microsoft.com/library/ms243142.aspx) para obter informações sobre como desempenho na web de toobind tooa de dados de teste.

Neste exemplo, converteremos teste tooa com código de teste de desempenho do Olá web para que você pode substituir Olá avião ID com um GUID gerado e adicionar mais solicitações toosend voos toodifferent locais.

### <a name="create-a-load-test-project"></a>Criar um projeto de teste de carga
Um projeto de teste de carga é composto de um ou mais cenários descritos pelo teste de desempenho web hello e teste de unidade, juntamente com as configurações do teste de carga adicional. Olá etapas a seguir mostra como toocreate uma carga de projeto de teste:

1. No menu de atalho de saudação do seu projeto de teste de carga e desempenho na Web, escolha **adicionar** > **teste de carga**. Em Olá **teste de carga** assistente, escolha Olá **próximo** botão Configurações do teste Olá tooconfigure.
2. Em Olá **padrão de carga** , escolha se deseja uma carga de usuário constante ou uma carga de etapa, que inicia com alguns usuários e aumenta Olá usuários ao longo do tempo.

    Se você tiver uma boa estimativa da quantidade de saudação de carga de usuário e deseja toosee o desempenho do sistema atual hello, escolha **de carga constante**. Se seu objetivo é toolearn se o sistema Olá consistentemente executa sob várias cargas, escolha **carga por etapa**.
3. Em Olá **Test Mix** , escolha Olá **adicionar** botão e, em seguida, selecione Olá de teste que você deseja tooinclude no teste de carga hello. Você pode usar o hello **distribuição** percentual de saudação toospecify coluna de total testes executados para cada teste.
4. Em Olá **configurações de execução** seção, especifique a duração do teste de carga hello.

   > [!NOTE]
   > Olá **iterações de teste** opção está disponível somente quando você executa um teste de carga localmente usando o Visual Studio.
   >
   >
5. Em Olá **local** seção **configurações de execução**, especifique Olá local em que as solicitações de teste de carga são geradas. Assistente de saudação pode solicitar toolog em tooyour conta do Team Services. Faça logon e, em seguida, escolha um local geográfico. Quando terminar, escolha Olá **concluir** botão.
6. Após a criação de teste de carga hello, abra Olá LoadTest projeto e escolha atual Olá executar configuração, tais como **configurações de execução** > **Settings1 executar [Active]**. Isso abre configurações Olá executar no hello **propriedades** janela.
7. Em Olá **resultados** seção Olá **configurações de execução** janela Propriedades, Olá **Timing Details Storage** configuração deve ter **nenhum** como o valor padrão. Alterar esse valor também**todos os detalhes individuais** tooget obter mais informações sobre os resultados de teste de carga hello. Consulte [teste de carga](https://www.visualstudio.com/load-testing.aspx) para obter mais informações sobre como tooconnect tooVisual Studio Team Services e execute uma carga de teste.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Saudação de execução de teste de carga usando o Visual Studio Team Services
Escolha Olá **executar teste de carga** execução de teste do comando toostart hello.

![Captura de tela de saudação comando Executar teste de carga][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Exibir e analisar os resultados de teste de carga Olá
Como Olá andamento do teste de carga, as informações de desempenho de saudação gráfico. Você verá algo semelhante toohello gráfico a seguir.

![Captura de tela do gráfico de desempenho para resultados de testes de carga][9]

1. Escolha Olá **baixar relatório** link superior Olá da página de saudação. Depois de baixar o relatório hello, escolha Olá **Exibir relatório** botão.

    Em Olá **gráfico** guia você pode ver gráficos para vários contadores de desempenho. Em Olá **resumo** guia hello geral resultados do teste aparecem. Olá **tabelas** guia mostra o número total de saudação de testes de carga passado e com falha.
2. Escolha os links de número Olá Olá **teste** > **falha** e hello **erros** > **contagem** colunas detalhes do erro toosee.

    Olá **detalhes** guia exibe informações virtuais de cenário de teste e de usuário para solicitações com falha. Esses dados podem ser úteis se o teste de carga de saudação inclui vários cenários.

Consulte [analisando carregar resultados de teste no hello exibição de gráficos do analisador de teste de carga de saudação](https://www.visualstudio.com/load-testing.aspx) resultados de teste para obter mais informações sobre a exibição de carga.

## <a name="automate-your-load-test"></a>Automatizar o teste de carga
Visual Studio Team Services teste de carga fornece APIs toohelp gerenciar testes de carga e analisar os resultados em uma conta do Team Services. Confira [APIs Rest do teste de carga de nuvem](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) para saber mais.

## <a name="next-steps"></a>Próximas etapas
* [Monitorando e diagnosticando serviços em uma configuração de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
