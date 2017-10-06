---
title: entrega de aaaContinuous com o Visual Studio Team Services no Azure | Microsoft Docs
description: "Saiba como tooconfigure o Visual Studio Team Services projetos da equipe tooautomatically compilar e implantar o recurso de aplicativo Web toohello nos serviços de nuvem ou do serviço de aplicativo do Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>Fornecimento contínuo tooAzure usando o Visual Studio Team Services
Você pode configurar sua compilação de tooautomatically de projetos de equipe do Visual Studio Team Services e implantar aplicativos da web de tooAzure ou serviços de nuvem.  (Para obter informações sobre como tooset até uma compilação contínua e implantar o sistema usando uma *local* Team Foundation Server, consulte [entrega contínua para serviços de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).)

Este tutorial presume que você tenha o Visual Studio 2013 e hello SDK do Azure instalado. Se você ainda não tiver o Visual Studio 2013, baixá-lo escolhendo Olá **comece gratuitamente** link [www.visualstudio.com](http://www.visualstudio.com). Instalar Olá SDK do Azure na [aqui](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> É necessário um toocomplete de conta do Visual Studio Team Services este tutorial: você pode [abrir uma conta do Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset a um tooautomatically de serviço de nuvem compilar e implantar tooAzure usando o Visual Studio Team Services, siga estas etapas.

## <a name="1-create-a-team-project"></a>1: Criar um projeto de equipe
Siga as instruções de saudação [aqui](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate sua equipe de projeto e vinculá-lo tooVisual Studio. Este passo a passo pressupõe que você está usando oo Controle de Versão do Team Foundation (TFVC). Se você quiser toouse Git para controle de versão, consulte [versão de Git Olá deste passo a passo](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: check-in de controle de toosource um projeto
1. No Visual Studio, abra a solução de saudação desejado toodeploy ou criar um novo.
   Você pode implantar um aplicativo web ou um serviço de nuvem (aplicativo do Azure) pelo Olá seguir as etapas neste passo a passo.
   Se você quiser toocreate uma nova solução, crie um novo projeto de serviço de nuvem do Azure ou um novo projeto ASP.NET MVC. Certifique-se de que Olá destinos do projeto do .NET Framework 4 ou 4.5 e se você estiver criando um projeto de serviço de nuvem, adicionar uma função web do ASP.NET MVC e uma função de trabalho e escolha o aplicativo de Internet para a função da web de saudação. Quando solicitado, escolha **Aplicativo da Internet**.
   Se você quiser toocreate um aplicativo web, escolha o modelo de projeto de aplicativo Web ASP.NET hello e escolha MVC. Consulte [Criar um aplicativo web ASP.NET no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > O Visual Studio Team Services só suporta implantações de CI de aplicativos Web do Visual Studio no momento. Projetos de Site estão fora do escopo.
   > 
   > 
2. Abra o menu de contexto de saudação para solução de saudação e escolha **tooSource adicionar solução controle**.
   
    ![][5]
3. Aceitar ou alterar os padrões de saudação e escolha Olá **Okey** botão. Após a conclusão do processo de hello, ícones do controle de origem aparecem na **Gerenciador de soluções**.
   
    ![][6]
4. Abra Olá menu de atalho Olá solução e escolha **Check-In**.
   
    ![][7]
5. Em Olá **alterações pendentes** área de **Team Explorer**, digite um comentário para check-in hello e escolha Olá **Check-In** botão.
   
    ![][8]
   
    Observação: Olá opções tooinclude ou excluir alterações específicas ao fazer check-in. Se desejar que as alterações são excluídas, escolha Olá **incluir tudo** link.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: conectar Olá projeto tooAzure
1. Agora que você tiver um projeto de equipe do VS Team Services com algum código-fonte nela, você está pronto tooconnect tooAzure de projeto de equipe.  Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), selecione o aplicativo web ou serviço de nuvem ou crie um novo escolhendo Olá  **+**  ícone na esquerda inferior hello e escolhendo **doserviçodenuvem** ou **aplicativo da Web** e **criação rápida**. Escolha Olá **configurar a publicação com o Visual Studio Team Services** link.
   
    ![][10]
2. No Assistente de Olá, digite o nome de saudação da sua conta do Visual Studio Team Services na caixa de texto de saudação e clique em Olá **autorizar agora** link. Você pode ser solicitado toosign no.
   
    ![][11]
3. Em Olá **solicitação de Conexão** caixa de diálogo pop-up, escolha Olá **aceitar** botão tooauthorize tooconfigure do Azure que sua equipe de projeto no VS Team Services.
   
    ![][12]
4. Quando a autorização for bem-sucedida, você verá uma lista suspensa que contém uma lista de seus projetos de equipe do Visual Studio Team Services. Escolher nome de saudação do projeto de equipe que você criou nas etapas anteriores hello e, em seguida, escolha o botão de marca de seleção do Assistente de saudação.
   
    ![][13]
5. Depois que o projeto está vinculado, você verá algumas instruções para fazer check-in do projeto de equipe do Visual Studio Team Services de tooyour de alterações.  No próximo check-in, o Visual Studio Team Services criará e implantará tooAzure seu projeto.  Tente agora clicando Olá **Check-In do Visual Studio** link e, em seguida, Olá **iniciar o Visual Studio** link (ou hello equivalente **Visual Studio** botão na parte inferior de saudação do portal tela Hello).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: Disparar uma recompilação e reimplantar seu projeto
1. No Visual Studio **Team Explorer**, escolha Olá **Gerenciador de controle do código-fonte** link.
   
    ![][15]
2. Navegue tooyour o arquivo de solução e abri-lo.
   
    ![][16]
3. No **Gerenciador de Soluções**, abra um arquivo e altere-o. Por exemplo, altere o arquivo hello `_Layout.cshtml` em modos de exibição de saudação\\pasta compartilhada em uma função da web MVC.
   
    ![][17]
4. Editar saudação logotipo para o site de saudação e escolha **Ctrl + S** toosave arquivo de saudação.
   
    ![][18]
5. Em **Team Explorer**, escolha Olá **alterações pendentes** link.
   
    ![][19]
6. Insira um comentário e, em seguida, escolha Olá **Check-In** botão.
   
    ![][20]
7. Escolha Olá **inicial** botão tooreturn toohello **Team Explorer** página inicial.
   
    ![][21]
8. Escolha Olá **cria** saudação do link tooview compilações em andamento.
   
    ![][22]
   
    **Team Explorer** mostra que uma compilação foi disparada para seu check-in.
   
    ![][23]
9. À medida que avança de compilação Olá, clique duas vezes em nome de saudação do hello compilação em andamento tooview um log detalhado.
   
    ![][24]
10. Enquanto a compilação de saudação está em andamento, dê uma olhada na definição de compilação de saudação que foi criada quando você vinculou tooAzure TFS usando o Assistente de saudação.  Abra o menu de atalho Olá Olá para definição de compilação e escolha **editar definição de compilação**.
    
     ![][25]
    
     Em Olá **gatilho** guia, você verá que definição de compilação de saudação é definida toobuild em cada check-in por padrão.
    
     ![][26]
    
     Em Olá **processo** guia, você pode ver o ambiente de implantação Olá é definido toohello nome do seu aplicativo web ou serviço de nuvem. Se você estiver trabalhando com aplicativos web, propriedades de saudação que verá serão diferentes daqueles mostrados aqui.
    
     ![][27]
11. Especifica valores para propriedades de saudação se você quiser que os valores diferentes de padrões de saudação. Olá propriedades de publicação do Azure estão em Olá **implantação** seção.
    
     Olá tabela a seguir mostra propriedades disponíveis Olá em Olá **implantação** seção:
    
    | Propriedade | Valor Padrão |
    | --- | --- |
    | Permitir certificados não confiáveis |Se falso, os certificados SSL deve ser assinados por uma autoridade raiz. |
    | Permitir Atualização |Olá implantação tooupdate permite que uma implantação existente em vez de criar um novo. Preserva o endereço IP hello. |
    | Não exclua |Se verdadeiro, não substitua uma implantação não relacionada existente (a atualização é permitida). |
    | Caminho tooDeployment configurações |Olá caminho tooyour. pubxml arquivo para um aplicativo web, a pasta raiz de toohello relativo do repositório de saudação. Ignorado para serviços de nuvem. |
    | Ambiente de implantação do Sharepoint |Olá mesmo como o nome do serviço hello. |
    | Ambiente de implantação do Azure |Olá aplicativo ou nuvem nome do serviço web. |
12. Se você estiver usando várias configurações de serviço (arquivos. cscfg), você pode especificar a configuração de serviço desejado de saudação em Olá **compilar, Avançado, argumentos de MSBuild** configuração. Por exemplo, toouse ServiceConfiguration.Test.cscfg, defina os argumentos de MSBuild opção de linha de `/p:TargetProfile=Test`.
    
     ![][38]
    
     A essa altura, sua compilação deve estar concluída com êxito.
    
     ![][28]
13. Se você clicar duas vezes nome de compilação hello, o Visual Studio mostra uma **Resumo da compilação**, incluindo os resultados dos testes de associadas a projetos de teste de unidade.
    
     ![][29]
14. Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você pode exibir a implantação de saudação associada em Olá **implantações** guia quando Olá ambiente de preparo é selecionado.
    
     ![][30]
15. Procure tooyour URL do seu site. Para um aplicativo web, basta clicar Olá **procurar** botão na barra de comandos de saudação. De um serviço de nuvem, escolha URL Olá Olá **rápidos** seção Olá **painel** página que mostra o ambiente de preparo de saudação para um serviço de nuvem. As implantações de integração contínua para serviços de nuvem são publicados toohello ambiente de preparo por padrão. Você pode alterar essa configuração Olá **ambiente de serviço de nuvem alternativo** propriedade muito**produção**. Esta captura de tela mostra onde hello URL do site na página do painel do serviço de nuvem hello.
    
    ![][31]
    
    Uma nova guia do navegador será aberto tooreveal seu site em execução.
    
    ![][32]
    
    Para serviços de nuvem, se você fizer a outro projeto de tooyour alterações, você gatilho mais cria e acumularão várias implantações. Hello mais recente marcado como ativo.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: Reimplantar um build anterior
Essa etapa se aplica a serviços toocloud e é opcional. Em Olá portal clássico do Azure, escolha uma implantação anterior e Olá **reimplantar** botão toorewind tooan seu site anteriormente check-in.  Observe que isso vai disparar uma nova compilação no TFS e criará uma nova entrada em seu histórico de implantação.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: alterar a implantação de produção de hello
Essa etapa se aplica apenas o toocloud serviços, não os aplicativos web. Quando estiver pronto, você pode promover Olá preparo toohello ambiente de produção, escolhendo Olá **trocar** botão Olá portal clássico do Azure. ambiente de preparo Olá implantado recentemente é promovida tooProduction e ambiente de produção anterior hello, se houver, torna-se um ambiente de preparo. Olá implantação ativa pode ser diferente para ambientes de preparo e produção de hello, mas o histórico de implantação de saudação de builds recentes é Olá mesmo independentemente do ambiente.

![][35]

## <a name="7-run-unit-tests"></a>7: Executar testes de unidade
Essa etapa se aplica a aplicativos de tooweb apenas, não os serviços de nuvem. tooput um portão de qualidade na sua implantação, você pode executar testes de unidade e se elas falharem, você pode interromper a implantação hello.

1. No Visual Studio, adicione um projeto de teste de unidade.
   
   ![][39]
2. Adicione projeto de toohello de referências de projeto você deseja tootest.
   
   ![][40]
3. Adicione alguns testes de unidade. tooget iniciado, tente um teste fictício que sempre seja aprovado.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Editar definição de compilação hello, escolha Olá **processo** guia e, em seguida, expanda Olá **teste** nó.
5. Saudação de conjunto **falhar compilação em caso de falha do teste** tooTrue. Isso significa que a implantação de Olá não ocorreu, a menos que Olá testes foram bem-sucedidos.
   
   ![][41]
6. Fila de uma nova compilação.
   
   ![][42]
   
   ![][43]
7. Enquanto está procedendo compilação hello, verifica seu andamento.
   
    ![][44]
   
    ![][45]
8. Quando terminar de compilação hello, verifique os resultados de teste de saudação.
   
    ![][46]
   
    ![][47]
9. Tente criar um teste que falhará. Adicione um novo teste copiando Olá primeiro, renomeá-lo e comentar a linha hello de código que afirma que NotImplementedException é uma exceção não esperada.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Check-in Olá alterar tooqueue uma nova compilação.
    
     ![][48]
11. Exibir detalhes toosee dos resultados do teste Olá sobre falha de saudação.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o teste de unidade no Visual Studio Team Services, consulte [Executar testes de unidade em sua compilação](http://go.microsoft.com/fwlink/p/?LinkId=510474). Se você estiver usando o Git, consulte [compartilhar seu código no Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) e [tooAzure implantação contínua do serviço de aplicativo](../app-service-web/app-service-continuous-deployment.md).  Para obter mais informações sobre o Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
