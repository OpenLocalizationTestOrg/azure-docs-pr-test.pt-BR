---
title: 'Exemplo de IoT do Azure do MyDriving: crie-o | Microsoft Docs'
description: "Criar um aplicativo que é uma abrangente demonstração de como tooarchitect um sistema IoT usando o Microsoft Azure, incluindo análise de fluxo, aprendizado de máquina e Hubs de eventos."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Criar e implantar Olá MyDriving solução tooyour ambiente
O MyDriving é uma solução de IoT (Internet das Coisas) que reúne dados do seu carro, processa-os usando o aprendizado de máquina e apresenta-os no seu celular. back-end Olá consiste em uma variedade de serviços fornecidos pelo Microsoft Azure. clientes de saudação podem ser telefones Android, iOS ou Windows 10.

Criamos Olá MyDriving solução toogive é um ponto de partida na criação de seu próprio sistema de IoT. De saudação [MyDriving repositório no GitHub](https://github.com/Azure-Samples/MyDriving), você pode obter scripts do Azure Resource Manager toodeploy arquitetura de back-end de saudação em sua própria conta do Azure. Desse ponto, você pode reconfigurar serviços diferentes Olá, modificar Olá consultas toosuit seus próprios dados e assim por diante. Você pode encontrar esses scripts – juntamente com o código de aplicativo móvel hello, projeto de API de serviço de aplicativo do Azure hello e muito mais – no repositório de MyDriving hello.

Se você ainda não tentou o aplicativo hello ainda, examinar Olá [guia de Introdução Get](iot-solution-get-started.md).

Há um relatório detalhado de arquitetura de saudação do hello [guia de referência MyDriving](http://aka.ms/mydrivingdocs). Em resumo, há várias partes que configuramos toocreate um projeto semelhante:

* Um **aplicativo cliente** é executado em telefones Android, iOS e Windows 10. Usamos Olá Xamarin plataforma tooshare do código de saudação, que é armazenado no GitHub em `src/MobileApp`. aplicativo Hello realmente executa duas funções distintas:
  * Ele retransmite telemetria de dispositivo de diagnóstico integrado (OBD) do hello e de back-end de nuvem do seu próprio toohello sistema local service.
  * Ele é uma interface do usuário em que usuários podem fazer consultas sobre suas viagens gravadas.
* Um **serviço de nuvem** recebe dados de viagem Olá em tempo real e processa-os. trabalho de saudação principal de criar esse serviço é toochoose, parametrizar e conectar uma variedade de serviços do Azure. Algumas partes do hello exigem scripts toofilter e processo Olá os dados de entrada. Usamos uma tooconfigure de modelo do Azure Resource Manager todas as partes de saudação.
* Um **aplicativo de serviço móvel** é Olá web serviço por trás da parte de interface de usuário Olá Olá do aplicativo de dispositivo. Seu trabalho principal é o banco de dados de saudação de tooquery de dados armazenados e processados. Seu código está no GitHub em `src/MobileAppService`.
* **Visual Studio com Xamarin** é nosso ambiente de desenvolvimento. Xamarin, que existe como um componente do Visual Studio e um ambiente autônomo de desenvolvimento integrado (IDE), é usado toobuild código de várias plataformas de dispositivo de saudação. código de iOS Olá toobuild, é necessário toohave uma instância do Xamarin em execução em uma máquina OS X. Se necessário, ele pode ser executado como um agente gerenciado do Visual Studio.
* **Teste de unidade** do dispositivo Olá aplicativos é executada em Xamarin Test Cloud.
* **GitHub** repositório Olá onde armazenamos todos os modelos, scripts e código hello.
* **Visual Studio Team Services** é um serviço de nuvem que usou a criação contínua de saudação toomanage e teste de aplicativos de serviço e o dispositivo de Olá web.
* **HockeyApp** é usado toodistribute versões de código de dispositivo de saudação. Ele também coleta relatórios de uso e de falhas, bem como comentários do usuário.
* **Visual Studio Application Insights** monitores Olá serviço web móvel.

Vejamos como configurar tudo isso. 

> [!NOTE] 
> Muitas das Olá etapas a seguir são opcionais.
>
>

## <a name="sign-up-for-accounts"></a>Inscrever-se em contas
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Esse programa gratuito fornece ferramentas de desenvolvedor toomany acesso fácil e serviços, incluindo o Visual Studio, o Visual Studio Team Services e o Azure. Ele concede U$25 por mês de crédito no Azure por 12 meses. Ele também inclui o treinamento de tooPluralsight de assinaturas e Xamarin University. Você pode se inscrever separadamente para camadas gratuitas do [Azure](https://azure.com) e do [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), mas eles não fornecem créditos do Azure.
* [HockeyApp](https://rink.hockeyapp.net/) (opcional), para gerenciar a distribuição de teste de aplicativos móveis e a coleta de telemetria.
* [Xamarin](https://xamarin.com/) (obrigatório), para a criação de aplicativos móveis hello e execuções de depuração e testes em execução [Xamarin Test Cloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (opcional), toocreate livre repositórios públicos para seu próprio código (repositórios privados pagas). Como alternativa, você pode usar o plano básico Olá no Visual Studio Team Services para repositórios privados.
* [Power BI](https://powerbi.microsoft.com/) (opcional), visualizações avançadas de toocreate de dados em todo o sistema hello.

> [!NOTE]
> Você não precisa tooaccess conta Olá MyDriving código no GitHub [Olá repositório GitHub MyDriving](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Instalar ferramentas de desenvolvimento
Olá configuração a seguir é para o desenvolvimento de solução completa Olá: um iOS, Android e Windows 10 Mobile back-end de aplicativo de plataforma cruzada, com um Azure.

Como alternativa, você pode usar o Xamarin Studio em um Mac ou Windows toodevelop Olá aplicativos móveis se você não está trabalhando hello Azure volta terminar.

Há uma [descrição maior dessa configuração](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Computador de desenvolvimento do Windows
ferramenta de saudação central no Windows é o Visual Studio, para trabalhar com hello MyDriving aplicativo para Android e Windows, projeto de API do serviço de aplicativo hello e extensões de microsserviço.

Xamarin, Git, emuladores e outros componentes úteis são todos integrados ao Visual Studio.

Instalar:

* [Visual Studio com Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (qualquer edição – a Community é gratuita).
* [SQLite para Plataforma Universal do Windows](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Necessário código do toobuild Olá Windows 10 Mobile.
* [SDK do Azure para o Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Fornece Olá SDK para aplicativos em execução no Azure, junto com as ferramentas de linha de comando para o gerenciamento do Azure.
* [SDK do Azure Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Olá necessário toobuild [microsserviço](../service-fabric/service-fabric-get-started.md) extensão.

Certifique-se de que você tem extensões do Visual Studio direita hello. Verifique se, em **Ferramentas**, é exibido **Android, iOS, Xamarin...**. Se não estiver, abra o Visual Studio, procure Xamarin e siga Olá prompts tooinstall-lo. Além disso, verifique se **Git para Windows** está instalado. Se não, no Visual Studio, procure-o e siga Olá prompts tooinstall-lo. 

### <a name="mac-development-machine"></a>Computador de desenvolvimento do Mac
Olá Mac (Yosemite ou posterior) é necessário se você quiser toodevelop para iOS. Embora é usar o Visual Studio com o Xamarin no Windows toodevelop e gerenciar todos os códigos de hello, Xamarin usa um agente instalado em um Mac em ordem toobuild e entrada hello código do iOS.

![Desenvolver no Windows e compilar no Mac](./media/iot-solution-build-system/image1.png)

(Como alternativa, você pode usar Xamarin Studio diretamente em aplicativos de plataforma cruzada Olá Mac toodevelop).

Olá Mac não é necessário se você não quiser iOS tooinclude como uma plataforma de destino.

Instalar:

* [Xamarin Studio para iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Você também pode configurar o Visual Studio e Xamarin em um Mac que executa uma máquina virtual do Windows. Consulte [Configuração, instalação e verificações para usuários do Mac](https://msdn.microsoft.com/library/mt488770.aspx) no MSDN.
* [Ferramentas de desenvolvimento do Azure](https://azure.microsoft.com/downloads/) (opcionais).

Habilitar logon remoto no hello Mac. Abra **Preferências do Sistema** > **Compartilhamento** e selecione **Logon Remoto**.

Quando você abre um projeto do iOS no Visual Studio no Windows, Olá Xamarin plug-in solicitará que você para a ID de saudação da saudação Mac.

## <a name="fetch-hello-github-repository"></a>Buscar o repositório do GitHub Olá
Buscar uma cópia local do [Olá repositório GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) usando Olá **baixar ZIP** botão no GitHub, Visual Studio ou outro cliente de Git.

Descompacte Olá arquivo tooa pasta com um nome de caminho curto, como c:\\código.

Como alternativa, se você desejar tookeep backup toodate com ou contribuir código tooour, clone o repositório de saudação da seguinte maneira:

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Obter uma chave de API do Bing Mapas
[Registre-se para uma chave de API do Bing Mapas](https://msdn.microsoft.com/library/ff428642.aspx).

Você precisa tooreplace isso na linha 22 em `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Criar aplicativo de demonstração de Olá
Abra essas soluções no Visual Studio:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Você receberá prompts para:

* Confiar em alguns projetos potencialmente não confiáveis. Escolha tooopen-los se você quiser toogo em frente.
* Definir o Modo de desenvolvedor se você estiver trabalhando em um novo computador do Windows 10.
* Fornecer suas credenciais do Xamarin.
* Conecte-se toohello Xamarin Mac. Se você não tiver um Mac, iOS de saudação do atalho do projeto no Visual Studio e selecione **descarregar projeto**.

Recompile a solução de saudação.

Se você tiver a construção de problemas, tente Olá soluções tooquirks que encontramos:

* *Não carrega projeto VINLookupApplication*: Certifique-se de que você instalou o hello [SDK do Azure para Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Projeto de serviço de malha não compilar*: criar projetos de interface Olá primeiro e certifique-se de que você instalou o hello SDK do Service Fabric.
* *O aplicativo do Android não cria*:
  
  * Abra **Ferramentas** > **Android** > **Gerenciador de SDK do Android** e verifique se o Android 6 (API 23)/Plataforma de SDK está instalado.
  * Exclua este diretório e recrie:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Obter o código de saudação tooknow
Solução de saudação, você encontrará:

* Extensões do Azure: Service Fabric.
* Azure HDInsight: scripts para processar dados de viagem no Azure.
* Aplicativos móveis: Olá aplicativos de dispositivos.
* MobileAppsService/MyDrivingService: Olá web volta terminar.
* Power BI: definição de relatório Olá.
* Scripts:
  
  * Gerenciador de recursos: modelos toobuild Olá recursos do Azure.
  * PowerShell: Modelos Scripts toorun Olá Gerenciador de recursos.
  * Banco de Dados SQL do Azure: depuração de bancos de dados.
* Banco de Dados SQL: CreateTables: definições de esquema.
* O Azure Stream Analytics: Consulta esse fluxo de dados de entrada do hello de transformação.

## <a name="run-hello-apps-in-development-mode"></a>Executar aplicativos de saudação no modo de desenvolvimento
Execute ação toorun Olá aplicativos, com base no dispositivo de saudação que você está usando:

* Back-end: MyDrivingService definir como projeto de inicialização hello e pressione F5 toorun Olá back-end web Services. Ela será aberta uma exibição de navegador de listagem Olá API.
* Clientes móveis: Olá [aplicativos móveis são desenvolvidos em Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: Para obter detalhes, consulte [Depuração do Android no Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: para obter detalhes, consulte [Depuração no iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: para obter detalhes, consulte [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Carregar Olá tooHockeyApp de aplicativo móvel
HockeyApp gerencia a distribuição de saudação de seu Android, iOS ou Windows aplicativo tootest usuários, notificar os usuários das novas versões. Ele também coleta relatórios de falha úteis, comentários do usuário com capturas de tela e métricas de uso.

[Comece carregando](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) seu aplicativo de build. Em seguida, entrar muito[HockeyApp](https://rink.hockeyapp.net) em seu computador de desenvolvimento. No painel do desenvolvedor hello, clique em **novo aplicativo**e arraste arquivos Olá criado para janela hello. (Posteriormente, você pode automatizar seu toodo de serviço de compilação isso.)

Agora você está no painel do aplicativo.

![Guia de visão geral no painel de controle de aplicativo hello](./media/iot-solution-build-system/image2.png)

Repetir o processo de saudação de seu aplicativo é executado em cada plataforma. Em seguida, você pode fazer a seguir hello:

* Saudação de uso [ID do aplicativo](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) de comentários do seu aplicativo e dados de falha do hello painel toosend. Em MyDriving, atualize as IDs de saudação em src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Convide os usuários de teste](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Você obtém uma URL toorecruit usuários testadores. Vai ser capaz de toosign para sua equipe, baixe o aplicativo hello e enviar comentários.
* Se você preferir uma versão beta mais aberta, defina Olá toopublic de distribuição. Clique em **Gerenciar Aplicativo** > **Distribuição** > **Download = Público**. Agora qualquer pessoa poderá baixar seu aplicativo e enviar comentários, e eles verão uma notificação quando você postar uma nova versão. E você também pode receber alguns relatórios de falha deles.
  
   ![Equipes de painel Olá](./media/iot-solution-build-system/image3.png)
* [Relatórios de falha de link tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Clique em **Gerenciar Aplicativos** > **Visual Studio Team Services**. O HockeyApp pode criar itens de trabalho automaticamente no Team Services quando há relatórios de falha ou ao receber comentários.

Ler mais em Olá [HockeyApp site](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Testar o aplicativo móvel de saudação em Xamarin Test Cloud
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatiza o teste de interface do usuário em dispositivos reais na nuvem de saudação. Usando Olá NUnit framework, você escrever testes que executam seu aplicativo por meio da interface do usuário hello.

toouse Xamarin, você incorporar Olá [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK em seu aplicativo, que é fornecida como um pacote do NuGet. Você encontrará o aplicativo de demonstração hello e tem incluído quando você criar novos projetos de teste com hello Xamarin modelos.

![Onde toofind Olá SDK de plataforma cruzada na interface de saudação](./media/iot-solution-build-system/image4.png)

Um exemplo de projeto de teste está incluído no aplicativo hello no repositório de saudação. Em [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), procure em [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Se você usar uma compilação do Visual Studio Team Services, é fácil toowrite testes de unidade de Xamarin UI e executá-los como parte de sua compilação.

## <a name="deploy-azure-services"></a>Implantar os serviços do Azure
tooperform uma implantação automática de serviços do Azure e serviços de compilação do Team Services, consulte toohello detalhadas instruções **scripts/README.md**.

Microsoft Azure fornece uma grande variedade de serviços diferentes que você pode usar toobuild aplicativos em nuvem. Embora muitas podem ser usadas individualmente (por exemplo, aplicativos de serviço/da Web do aplicativo), eles são em sua melhor quando eles são interconectados tooform um sistema integrado como usamos em MyDriving.

É possível toocreate e interconexão de serviços do Azure manualmente, mas é muito mais rápidos e mais confiáveis modelos do Azure Resource Manager toouse. [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md) automatiza a implantação de saudação de recursos de uma solução e tornando interconexões Olá entre eles.

Você encontrará o modelo de saudação para o sistema de MyDriving Olá no repositório do GitHub Olá em [scripts/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Ele fornece uma exibição abrangente e concisa da maneira como os diferentes serviços Olá em nossa arquitetura são interconectados. Explicaremos todos esses detalhadamente Olá [MyDriving guia de referência](http://aka.ms/mydrivingdocs), mas você pode aprender muito apenas através da leitura por meio do modelo de saudação em si.

> [!NOTE]
> Os serviços do Azure mais tem um custo associado, dependendo da saudação de preço. Se você for novo tooAzure, você pode [Experimente gratuitamente](https://azure.microsoft.com/free/). No entanto, se você não planeja toouse alguns componentes em Olá MyDriving system, ser tooremove-se de que eles custos gera tooavoid. Olá "Calcular os custos operacionais" seção posteriormente neste artigo fornece um resumo das despesas de serviço típico.
> 
> 

### <a name="edit-hello-template"></a>Editar modelo Olá
toocustomize sua implantação, talvez tooremove desnecessários componentes ou tooadd outras pessoas, primeiro fazer um cópias do cenário\_complete.params.json e cenário\_complete.json em quais alterações toomake.

Você pode usar o cenário de saudação\_complete.params.json arquivo toooverride vários valores padrão, como Olá serviço SKU ou hello replicação tipo de armazenamento, conforme descrito em Olá a tabela a seguir. valores padrão de saudação selecionar opções de menor custo de saudação.

| **Parâmetro** | **Descrição** | **Valor padrão** |
| --- | --- | --- |
| SKU do Hub IoT |Camada para o serviço do Hub IoT do Azure |F1 |
| Tipo de Conta de Armazenamento |Tipo de replicação de armazenamento |LRS Padrão |
| Objetivo de Serviço do SQL |Consumo de slot de simultaneidade |DW100 |
| SKU do Plano de Hospedagem |Plano de serviço para o Serviço de Aplicativo |F1 |

No cenário\_complete.json:

* Procure "nome de base" e alterá-la tooa nome desejado.
* Procure por "Criar". Cada uma dessas seções cria um recurso.
* Defina sqlServerAdminLogin e sqlServerAdminPassword toosuitable valores.
* Antes de excluir uma seção que cria um recurso, verifique se ele possui dependentes pesquisando por seu nome em outro lugar no arquivo hello. Observe que cada seção que cria um serviço inclui uma seção *dependsOn* que lista suas dependências.

Aqui o modelo Olá configura. Os detalhes estão no hello [guia de referência](http://aka.ms/mydrivingdocs).

| **Serviço** | **Descrição e detalhes** |
| --- | --- |
| Contas de armazenamento |modelo de saudação cria três contas: |
| -Um banco de dados SQL que recebe telemetria agregada de análise de fluxo e serve como armazenamento de backup Olá tabelas de serviço de aplicativo do Azure que expõem esses dados por meio de pontos de extremidade de API. | |
| -Armazenamento de blob que acumula dados históricos de outro trabalho de análise de fluxo, toobe processada pelo HDInsight. | |
| -   Um Banco de Dados SQL que recebe os resultados processados pelo HDInsight para uso com o Power BI. | |
| Hub IoT do Azure |Estabelece um dispositivo conectado que tooeach conexão bidirecional. Olá MyDriving solução, aplicativo móvel Olá age como um campo gateway toosend dados tooAzure IoT Hub. IoT Hub do Azure, em seguida, serve como uma entrada tooStream análise. |
| Hubs de eventos do Azure |Saída para um trabalho do Stream Analytics filas Olá tooextensions de saída que são criados com o Azure Service Fabric. |
| SQL Data Warehouse do Azure | |
| Trabalhos do Stream Analytics |Conectar entradas e saídas com uma consulta, que é usado tooaggregate dados históricos e em tempo real para Olá APIs do serviço de aplicativo, aprendizado de máquina do Azure, extensões e Power BI. |
| Espaço de trabalho do Machine Learning |Inclui experimentos, código R e serviço de API. |
| Fábrica de dados do Azure |Readaptação adaptada do Machine Learning. |
| Plano de hospedagem do Service Fabric |Para extensões. |
| Serviço de Aplicativo (“Aplicativo Móvel”) |Projeto de API de aplicativos móveis que fornece pontos de extremidade de aplicativo móvel Olá Olá a hosts. Olá código da API deve ser implantado tooApp serviço do Visual Studio. |
| Regras de alerta |Envia que email se as respostas de aplicativo hello indicam falhas. |
| Application Insights |Para monitorar o desempenho de saudação APIs no serviço de aplicativo. Você tem conexão de saudação tooconfigure no Visual Studio. |
| Cofre da Chave do Azure |Para salvar o certificado de cluster do serviço de web hello. |

### <a name="run-hello-template"></a>Execute Olá modelo
Em **scripts/README.md**, há instruções detalhadas para o modelo de saudação em execução.

tooprovision todos esses serviços em sua própria conta do Azure usando o script hello, siga um destes Olá a seguir:

* Use o PowerShell:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *local* é hello [local do Azure](https://azure.microsoft.com/regions/), como `North Europe` ou `West US`. Use `Get-AzureLocation` toofind uma lista de locais disponíveis.
  * *resourceGroupName* é Olá nome que você quiser que todos os recursos de saudação pertencerão ao grupo de toohello toogive. Quando tiver terminado com recursos Olá, poderá excluí-los juntos excluir esse grupo.
* Execute DeploymentScripts/Bash/deploy.sh com o Bash.
* Abrir e criar a solução do Visual Studio Olá DeploymentScripts/VS/DeployARM.sln.

Observe que cada modelo de saudação do tempo é executado, ele cria um novo conjunto de recursos com novos nomes. recursos de saudação toodelete, vá toohello portal e excluir o grupo de recursos de saudação.

Se o script hello falhar por algum motivo, você pode executá-lo novamente.

proporciona ao script Olá Olá opção de configuração da integração contínua no Visual Studio Team Services. Se você tiver configurado um projeto de Serviços para equipes, você terá uma URL: https://NomeDaSuaConta.visualstudio.com. Insira o URL completa hello quando for solicitado. Você pode atribuir um nome novo ou existente a um projeto do Team Services.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Configurar o build e testar definições no Visual Studio Team Services
Usamos o Team Services neste projeto principalmente devido aos seus recursos de build e teste. Contudo, ele também dá um suporte excelente à colaboração, como gerenciamento de tarefas com quadros Kanban, revisão de código integrada com tarefas e controle do código-fonte e builds restritos. Ele se integra bem com outras ferramentas como o GitHub, Xamarin, HockeyApp e, claro, o Visual Studio. Você pode acessá-lo por meio da interface web hello ou Visual Studio, o que for mais conveniente a qualquer momento.

Olá as etapas de compilação hello e definições de versão usam uma variedade de plug-in Serviços que estão disponíveis no hello Team Services [Marketplace](https://marketplace.visualstudio.com/VSTS). Em linhas de comando adição toobasic utilitários toorun ou copiar arquivos, há serviços que invocar compilações, Xamarin, Android e outros fornecedores, e que se conectam tooHockeyApp.

![Opções de build no Team Services](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definições de build
Temos as definições de compilação para cada um dos principais alvos de saudação. Também temos variações de recurso e testes de regressão. Isso nos fornece:

* MyDriving.Services (Olá o aplicativo web de back-end para aplicativo móvel Olá)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android-Feature
  * MyDriving.Xamarin.Android-Regression
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS-Feature
  * MyDriving.Xamarin.iOS-Regression
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP-Feature
  * MyDriving.Xamarin.UWP-Regression

Se você quiser toosee Olá detalhes de nossa configuração, consulte a seção 4.7 Olá [MyDriving guia de referência](http://aka.ms/mydrivingdocs), "Configuração de versão e compilação." Seguem Olá mesmo padrão geral. script Hello:

1. Restaura o pacote do NuGet hello. Nós não manter código compilado no repositório de saudação para que primeiras etapas saudação de cada compilação são toorestore Olá necessário pacotes do NuGet.
2. Ativa a licença de saudação. Olá compilação é executada na nuvem Olá, onde é necessário ter uma licença – em particular, para Olá Xamarin criar serviço-- tenho tooactivate nossa licença no computador de compilação atual Olá. Em seguida, podemos desativá-lo imediatamente posteriormente, tooallow-toobe usada em outro computador.
3. Cria usando o serviço apropriado hello. Usamos compilações Xamarin para aplicativos móveis Olá, e o Visual Studio compila para o serviço da web de back-end de saudação.
4. Testes de builds.
5. Executa testes. Iremos executar testes de aplicativo móvel Olá no Xamarin Test Cloud.
6. Publica o local de destino do hello compilação resultado toohello.

gatilho Olá para compilações de saudação principal é definido toocontinuous integração. Ou seja, Olá é executada sempre que o código é verificado na ramificação mestre toohello.

![Interface em que o gatilho de saudação é conjunto toocontinuous integração](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definições de versão
Definições de versão são configuradas no muito Olá mesmo modo.

Para o serviço da web de hello, configuramos implantação como um aplicativo web do Azure:

![Interface para configurar a implantação como um aplicativo Web do Azure](./media/iot-solution-build-system/image7.png)

E podemos definir a implantação de toocontinuous Olá versão disparador. Ou seja, cada check-in seguido pelos resultados compilação bem-sucedida em um aplicativo de web de toohello de atualização.

![Interface para a configuração de implantação de toocontinuous de gatilho de versão Olá](./media/iot-solution-build-system/image8.png)

Para aplicativos móveis, implantamos tooHockeyApp:

![Interface para implantar um aplicativo móvel tooHockeyApp](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Explorar telemetria usando o Application Insights
[Application Insights](../application-insights/app-insights-overview.md) coleta a telemetria sobre desempenho hello e o uso de serviços da web. Olá SDK do Application Insights envia Telemetria da saudação serviço toohello recurso do Application Insights no Azure.

Procure toohello recurso do Application Insights modelo Olá configurado. Lá, você pode explorar os gráficos de desempenho de saudação de seu [projeto de serviço de aplicativo móvel](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Eles mostram solicitações do servidor e tempos de resposta, falhas e contagens de exceção. Também são gráficos de dependência de tempos de resposta – ou seja, o banco de dados chamadas toohello e tooREST APIs, como o aprendizado de máquina. Se houver problemas de desempenho, você será capaz de toosee que parte do sistema está fazendo com que eles.

![Exemplo de gráfico de desempenho](./media/iot-solution-build-system/image11.png)

Se você tiver um serviço web que você configurou manualmente, é fácil tooget Olá mesmo gráficos. Na folha de serviço da web de saudação, clique em **ferramentas** > **extensões** > **adicionar**. Selecione **Application Insights**.

![Interface para a seleção de gráficos de saudação do Application Insights tooget](./media/iot-solution-build-system/image12.png)

o recurso de saudação funciona por instrumentar seu aplicativo com hello SDK do Application Insights.

Você pode adicionar telemetria personalizada (ou instrumentar um aplicativo que está em execução em algum lugar fora do Azure), [adicionando Olá SDK do Application Insights](../application-insights/app-insights-asp-net.md) no tempo de desenvolvimento. Isso é útil toolog métricas que dependem de aplicativo hello, como comprimento da viagem média dos usuários ou quilometragem total. No Visual Studio, clique com botão direito hello e, em seguida, selecione **adicionar Application Insights**.

![Interface para a seleção de telemetria personalizada de tooadd adicionar Application Insights](./media/iot-solution-build-system/image10.png)

O Application Insights enviará emails de alerta caso observe números incomuns de respostas de falha. Você também pode configurar seus próprios alertas em várias métricas, como tempos de resposta.

Toobe apenas se seu serviço web está sempre ativado e em execução, você pode configurar [testes de disponibilidade](../application-insights/app-insights-monitor-web-app-availability.md). Esses testes ping seu site em vários locais em todo o mundo de saudação a cada 15 minutos. Novamente, você receberá um email se parece toobe um problema.

## <a name="estimate-operational-costs"></a>Custos operacionais estimados
É extremamente baixo custo toorun um aplicativo como este em pequena escala. Muitos serviços Olá têm níveis de nível básico gratuitos, para que o custam de desenvolvimento e a operação em pequena escala muito pouco. E claro, seus próprios aplicativos não tem toouse todos os recursos de saudação demonstrados MyDriving.

Aqui está uma estimativa aproximada de nossos custos na configuração de saudação desenvolvimento para MyDriving. Indicamos também algumas alternativas que *não* usamos. Essas informações podem ser úteis ao estimar seus próprios custos.

Supomos que:

* Uma equipe de até cinco membros (mais partes interessadas observadoras).
* Execução por cerca de um mês.
* 100 usuários com quatro viagens por dia.

> [!NOTE]
> Se você for novo tooAzure, há um [conta gratuita](https://azure.microsoft.com/free/).
> 
> 

| **Serviço/componente** | **Observações** | **Custo/mês** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) com [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Ambiente de desenvolvimento de plataforma cruzada |Visual Studio Community. (Necessário [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) para [xamarin. Forms](https://xamarin.com/forms), toodesign de várias plataformas de uma base de código único.) |U$0 |
| [Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Toodevices de conexão de dados bidirecional |8 mil mensagens + 0,5 KB/mensagem gratuito. |U$0 |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Processamento de dados de fluxo de alto volume |Cobrança de U$0,031 por unidade de streaming por hora, enquanto estiver habilitado. Você escolher Olá número de unidades de streaming desejado. tooscale mais para cima. |U$23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Respostas adaptáveis |U$10/estação/mês. <br/>                                                                                                                                                                                 + 3 horas de teste \* U$1/hora de teste. <br/>                                                                                                                                                           + 3.5 hora de CPU da API \* U$2/hora de CPU de produção. <br/>                                                                                                                                                          O tempo de CPU da API supõe 5 min/dia de readaptação, embora isso possa aumentar com mais dados de entrada.                   <br/>                                                                                                                                                                     + min 2/dia pontuação tooprocess 400 viagens por dia. |U$20 |
| [Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/)  <br/> para o back-end móvel |Camada B1: aplicativos Web de produção. |U$56 |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Build, teste de unidade e gerenciamento de versão; gerenciamento de tarefas |Agentes privados, cinco usuários. |U$0 |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Monitore o desempenho e uso dos serviços Web e sites |Camada gratuita. |U$0 |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> Distribuição de aplicativos beta, além de coleta de dados de comentários, de uso e de falha |Dois aplicativos gratuitos para novos usuários.<br/> U$30/ mês posteriormente. |U$0 |
| [Xamarin](https://store.xamarin.com/)<br/> Código em uma plataforma uniforme para vários dispositivos |Avaliação gratuita. <br/>U$25/mês posteriormente. |U$0 |
| [Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/) para o Serviço de Aplicativo do Azure |Camada Básica; modelo banco de dados individual. |U$5 |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (opcional) |Execute um cluster local. |U$0 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Exibições e investigação versáteis de dados transmitidos e estáticos |Camada gratuita: 1GB, 10 mil linhas/hora, atualização diária. <br/> U$10/usuário/mês para [limites mais altos](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), mais opções de conexão e colaboração. |U$0 |
| [Armazenamento](https://azure.microsoft.com/pricing/details/storage/) |L (localmente redundante) &lt; 100 G, U$0,024/GB. |U$3 |
| [Fábrica de dados](https://azure.microsoft.com/pricing/details/data-factory/) |U$0,60 por atividade \* (8h a 17h gratuitamente). |U$2 |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  Cluster sob demanda para readaptação diária |Três nós A3 por US $0,32/hora por uma hora diariamente * 31 dias. |U$30 |
| [Hubs de Evento](https://azure.microsoft.com/pricing/details/event-hubs/) |Básico com unidade de produtividade U$11/mês + U$0,028 de entrada. |U$11 |
| Dongle OBD | |U$12 |
| **Total** | |**U$157** |

Para obter mais informações, consulte:

* Resumo dos [limites e cotas do serviço do Azure](../azure-subscription-service-limits.md#iot-hub-limits)
* [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Envie-nos seus comentários
Como criamos MyDriving toohelp iniciar seus próprios sistemas de IoT, queremos certamente toohear você sobre como ele funciona. Fale conosco se:

* Você encontra dificuldades ou desafios.
* Há um ponto de extensão para que seja mais adequada do cenário de tooyour.
* Você encontrar um tooaccomplish de maneira mais eficiente determinadas necessidades.
* Você tem outras sugestões para melhorar o MyDriving ou essa documentação.

comentários de toogive [problema no GitHub] ou deixar um comentário abaixo (en-us edition).

Aguardamos toohearing você!

## <a name="next-steps"></a>Próximas etapas
É recomendável Olá [guia de referência de MyDriving](http://aka.ms/mydrivingdocs), que é uma descrição completa do design de saudação do sistema hello e seus componentes.

