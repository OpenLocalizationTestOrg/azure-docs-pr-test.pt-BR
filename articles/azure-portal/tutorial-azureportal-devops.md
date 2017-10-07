---
title: 'Tutorial: DevOps com hello Portal do Azure | Microsoft Docs'
description: "Saiba Olá vários fluxos de trabalho DevOps Olá Portal do Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Tutorial: DevOps com hello Portal do Azure
Olá plataforma Windows Azure está cheio de fluxos de trabalho flexíveis DevOps. Neste tutorial, você aprenderá como recursos de saudação tooleverage de saudação toodevelop do Portal do Azure, testar, implantar, solucionar problemas, monitorar e gerenciar aplicativos em execução. Este tutorial se concentra nos seguintes hello:

1. Criar um aplicativo Web e habilitar a implantação contínua
2. Desenvolver e testar aplicativos
3. Monitorar e solucionar problemas de um aplicativo
4. Tarefas de gerenciamento de aplicativo móvel

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Criar um aplicativo Web e habilitar a implantação contínua
Criar um aplicativo Web com [do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/), que você usará no restante deste tutorial hello. Inicialmente, você habilitará a implantação contínua de seu repositório de código fonte em nosso ambiente do Azure em execução.

1. Olá de logon no Portal do Azure
2. Escolha **serviços de aplicativos** &gt; **ícone Adicionar** e insira um nome, escolha sua assinatura e criar um novo tooserve de grupo de recursos como contêiner Olá para o serviço de saudação.
   
   Grupos de recursos permitem que você toomanage vários aspectos da solução hello como cobrança, implantações e monitoramento como um único grupo por meio de [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![image1][image1]
3. Após alguns instantes, o serviço de aplicativo será criado. Levar Olá de tooexplore alguns minutos várias opções de menu para serviço Olá no portal de saudação.
   
   ![image2][image2]    
4. Clique em URL hello. Observe a variedade de saudação de opções disponíveis para ferramentas e repositórios. Você também pode usar idiomas de saudação e estruturas de sua escolha, incluindo .NET, Java e Ruby.
   
   ![image3][image3]    
5. Olá portal do Azure facilita a implantação contínua um processo simples que envolve apenas algumas etapas simples. No Olá portal do Azure, escolha as configurações de ícone Olá para serviço de aplicativo hello que você acabou de criar.
   
   ![image4][image4]
   
   Na folha de saudação que é aberto no saudação à direita, role toohello seção de publicação.
   
   ![image5][image5]
6. Em seguida, configure alguns implantação contínua de tooenable configurações para o aplicativo hello. Clique em Origem da Implantação e depois em Escolher Origem. Observe a variedade de saudação de opções que disponíveis para fontes de repositório.
   
   ![image6][image6]
7. Para este exemplo, escolha GitHub. Opcionalmente escolher Olá repositório de sua escolha e credenciais de autorização de saudação de instalação.
   
   ![image7][image7]
8. Depois de repositório de tooyour de autorização, você pode escolher um projeto e desejar toodeploy de ramificação. Confira vários exemplos fictícios abaixo.
   
   ![image8][image8]
9. Depois de escolher o projeto e a ramificação, clique em ok. Você deve iniciar toosee notificações de uma implantação.
   
   ![image9][image9]
10. Navegue tooGitHub back toosee Olá webhook que foi criado o repositório de controle de origem toointegrate Olá com o Azure. Olá Portal do Azure permite a integração com GitHub com apenas algumas etapas simples.
    
    ![image10][image10]
11. implantação contínua de toodemonstrate, adicionar rapidamente alguns repositório toohello conteúdo. Para obter um exemplo simple, adicione um repositório GitHub do exemplo texto arquivo tooa. Você está livre toouse .NET, Ruby, Python ou algum outro tipo de aplicativo com o serviço de aplicativo. Sinta-se livre tooadd um arquivo de texto, repositório de toohello aplicativo ASP.NET MVC, Java e Ruby de sua escolha.
    
    ![image11][image11]
12. Após a confirmação de repositório de tooyour alterações, você verá um novo iniciar a implantação na área de notificações do portal de saudação. Se você não ver rapidamente as alterações após a confirmação tooyour repositório, clique em sincronizar.
    
    ![image12][image12]
13. Neste ponto, se você tentar e carrega a página Olá para o serviço de aplicativo hello, você receberá um erro 403. Neste exemplo, é porque não há nenhuma configuração de documento padrão típica para página hello como um arquivo como index. htm ou default. Você pode corrigir isso rapidamente com hello ferramentas no hello Portal do Azure.  No hello Portal do Azure, escolha configurações &gt; as configurações do aplicativo.
    
     ![image13][image13]
14. Uma folha será aberta para as configurações do aplicativo. Insira nome de saudação da página hello "SamplePage.html" e clique em Salvar. Levar outras configurações de saudação de tooexplore alguns minutos.
    
    ![Imagem14][image14]
15. Opcionalmente, atualize seu tooensure de URL do navegador você verá as alterações de saudação esperada. Nesse caso, há algum texto simple agora preencher a página de saudação. Cada repositório de toohello alteração adicional resulta em uma nova implantação automática.
    
    ![Imagem15][image15]
    
    Habilitar implantação contínua com hello Portal do Azure é uma experiência de fácil. Você também pode criar pipelines de lançamento mais complexas e usar muitas outras técnicas com controle de origem existente e tooAzure de toodeploy de sistemas de integração contínua, como aproveitar compilação automatizada e sistemas de gerenciamento de versão.

## <a name="develop-and-test-an-app"></a>Desenvolver e testar aplicativos
Em seguida, fazer algumas alterações toohello código base e implantar rapidamente essas alterações. Você também irá configurar alguns testes para o aplicativo Web de saudação de desempenho.

1. No hello Portal do Azure escolher os serviços de aplicativo hello no painel de navegação e localize seu serviço de aplicativo.
   
   ![Imagem16][image16]
2. Clique em Ferramentas
   
   ![Imagem17][image17]
3. Observe o hello categoria em ferramentas de desenvolvimento. Há várias ferramentas úteis aqui que nos permitem toowork com aplicativos sem deixar Olá Portal do Azure. Clique em Console.
   
   ![Imagem18][image18]
4. Na janela de console hello, você pode emitir comandos ao vivo para seu aplicativo. Digite o comando do hello dir e pressione enter. Observe que os comandos que exigem privilégios elevados não funcionam.
   
   ![Imagem19][image19]
5. Voltar toohello desenvolver categoria e escolha Visual Studio Online. Observação: o Visual Studio Online agora se chama Visual Studio Team Services.
   
   ![Imagem20][image20]
6. Alternar a experiência de edição no navegador Olá para seu aplicativo.
   
   ![Imagem21][image21]
7. Uma extensão da Web é instalada para seu aplicativo. Extensões de forma rápida e fácil adicionam funcionalidade tooapps no Azure. Observe algumas Olá outros tipos de extensão disponíveis na captura de tela de saudação abaixo.
   
   ![Imagem22][image22]
8. Quando instala o hello extensão do Visual Studio Online, clique em Ir.
   
   ![Imagem23][image23]
9. Um navegador guia abre onde você pode ver um IDE de desenvolvimento diretamente no navegador de saudação. Experiência de saudação do aviso abaixo é no Chrome.
   
   ![Imagem24][image24]
10. Você pode executar várias atividades, como editar arquivos, adicionar arquivos e pastas e baixar conteúdo de site dinâmico Olá. Verifique o arquivo de SamplePage.html de toohello edição rápida.
    
    ![Imagem25][image25]
11. Em alguns instantes, Olá alterações são salvas automaticamente. Se você navegar toohello back página, você pode ver as alterações de saudação. Lembre-se de que edições ao vivo como essas provavelmente não são adequadas para ambientes de produção. No entanto, ferramentas Olá é muito fácil toomake alterações para desenvolvimento e ambientes de teste.
    
    ![Imagem26][image26]
    
    ![Imagem27][image27]
12. Voltar a folha de ferramentas toohello e na categoria de desenvolver Olá, clique no teste de desempenho.
    
    ![Imagem28][image28]
13. É necessário tooset uma conta do team services. Confira aqui mais detalhes: [Criar uma conta do Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. Clique em novo toocreate um teste de desempenho.
    
    ![Imagem29][image29]
    
    Configurar Olá vários valores e clique em Executar teste final Olá Olá caixa de diálogo tooinitiate um teste de desempenho.
    
    ![Imagem30][image30]
    
    ![Imagem31][image31]
15. Depois que o teste de saudação inicia a execução, você pode monitorar o estado de saudação.
    
    ![Imagem32][image32]
    
    Quando termina de teste hello, clicando no resultado de saudação mostra mais detalhes.
    
    ![Imagem33][image33]
16. Neste exemplo, você criou um pequeno teste executado, portanto, há tooanalyze de dados limitada, mas você pode ver várias métricas bem como executar novamente o teste da exibição. Olá Portal do Azure torna criar, executar e analisar testes de desempenho web um processo fácil. Olá capturas de tela abaixo exibem dados de desempenho de saudação.
    
    ![Imagem34][image34]
    
    ![Imagem35][image35]
    
    ![Imagem36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Monitorar e solucionar problemas de um aplicativo
O Azure oferece muitos recursos de monitoramento e solução de problemas de aplicativos em execução.

1. Escolha Ferramentas Olá Portal do Azure para o nosso aplicativo Web.
   
   ![Imagem37][image37]
2. Em categoria de solução de problemas do hello, observe Olá várias opções para o uso de possíveis problemas de ferramentas de tootroubleshoot com um aplicativo em execução. Você pode fazer coisas como monitorar o tráfego Live HTTP, habilitar a autorrecuperação, exibir view e muito mais.
   
   ![Imagem38][image38]
3. Escolha métricas do Site tooquickly obter uma exibição de alguns códigos de HTTP.
   
   ![Imagem39][image39]
4. Escolha Diagnóstico como Serviço. Escolha o tipo de aplicativo e depois Executar.
   
   ![Imagem40][image40]
   
   Começa a coleta.
   
   ![Imagem41][image41]
5. Você pode escolher problemas potenciais do toodiagnose Olá log apropriado. Você precisa de tooenable toosee de registro em log todos os dados disponíveis Olá opções como Logs de HTTP.
   
   ![Imagem42][image42]
   
   Clicando no arquivo de despejo de memória Olá você pode baixar e analisar um DebugDiag toohelp do relatório de análise encontrar problemas potenciais.
   
   ![Imagem43][image43]
6. tooview mais dados, você precisa tooenable adicionais de log. No hello Portal do Azure, navegue toohello Web app e escolha as configurações.
   
   ![Imagem44][image44]
7. Role para baixo de categoria de recursos toohello e escolha os logs de diagnóstico.
   
      ![Imagem45][image45]
8. Observe Olá várias opções para registro em log. Ative o registro em log do servidor Web e clique em Salvar.
   
   ![Imagem46][image46]
9. Voltar à área de ferramentas toohello para o aplicativo hello e escolha diagnóstico como um serviço e clique em executar toorerun Olá a coleta de dados.
   
   ![Imagem47][image47]
10. Com a configuração de registro em log Olá HTTP ativada, você verá os dados coletados para Logs de HTTP.
    
    ![Imagem48][image48]
11. Ao clicar em log do arquivo hello HTML, você produzir um relatório de baseado em navegador avançado para obter mais informações.
    
    ![Imagem49][image49]
12. Volta toohello seção ferramentas Olá Portal do Azure para o aplicativo hello. Rolar toohello seção de ferramentas e escolha o Explorador de processos.
    
    ![Imagem50][image50]
13. Ao escolher Gerenciador de Processos, é possível exibir detalhes sobre os processos em execução. Aviso abaixo, você pode detalhar processos e até mesmo interromper processos todos do hello Portal do Azure.
    
    ![Imagem51][image51]
    
    ![Imagem52][image52]
14. Mova folha de configurações toohello Olá esquerda. Clique em Nova solicitação de suporte.
    
    ![Imagem53][image53]
15. Na folha de saudação em saudação à direita, preencha os detalhes sobre problemas de hello, insira informações de contato e até mesmo, carregar dados de diagnóstico. Olá Portal do Azure permite trabalhar com o suporte da Microsoft uma experiência perfeita.
    
    ![Imagem54][image54]
    
    ![Imagem55][image55]
    
    Olá Portal do Azure ajuda a fornecer poderoso e familiar ferramentas experiências toohelp monitor e solucionar problemas de nossos aplicativos em execução. Também é possível tootake ação rapidamente, executando tarefas como a reciclagem de processos, habilitar e desabilitar vários conjuntos de dados e até mesmo integrar com o suporte da Microsoft professional.

## <a name="general-application-management"></a>Gerenciamento geral de aplicativos
Quando o gerenciamento de aplicativos, muitas vezes é preciso tooperform uma ampla variedade de atividades, como configurar estratégias de backup, implementar e gerenciar provedores de identidade e configurando o controle de acesso baseado em função. Como com hello outras experiências DevOps, Olá plataforma Windows Azure integra essas tarefas diretamente no portal de saudação.

1. tooensure esteja mantendo Olá aplicativo Web protegido contra perda de dados é necessário tooconfigure backups. Navegue toohello área de configurações para seu aplicativo Web.
   
   ![Imagem56][image56]
2. Na folha de saudação em saudação à direita, role para baixo toohello categoria de recursos.
   
    ![Imagem57][image57]
3. Escolha os Backups; uma folha é aberta no saudação à direita.
   
   ![Imagem58][image58]
4. Clique em configurar, escolha uma conta de armazenamento na folha de saudação no saudação à direita.
   
   ![Imagem59][image59]
5. Agora crie e escolha um toohold de contêiner de armazenamento dos backups. Clique em criar na parte inferior da saudação da folha de saudação. Em seguida, selecione o contêiner de saudação.
   
   ![Imagem60][image60]
6. Depois de ter escolhido o contêiner hello, você pode configurar agendamentos, bem como os backups de configuração para bancos de dados. Para este cenário, clique em Olá salvar ícone.
   
    ![Imagem61][image61]
7. Depois de salvar, role folha toohello back Olá esquerda para Backups. Clique em aplicativo de hello tooback Backup agora.
   
    ![Imagem62][image62]
8. Em poucos instantes, verá um backup criado. Saudação de aviso Restaurar agora a opção de saudação captura de tela abaixo.
   
    ![Imagem63][image63]
9. Clique em Restaurar agora e examine a folha de toohello Olá opções em saudação à direita. Você pode escolher que um backup apropriado e fácil restauração tooan anteriormente estado conforme necessário. Olá portal do Azure nos ajudou a habilitar facilmente uma estratégia de recuperação de desastres simples para o aplicativo hello.
   
    ![Imagem64][image64]
10. Mover de folha de configurações toohello Olá esquerda e, em recursos e escolher a autenticação/autorização.
    
     ![Imagem65][image65]
11. Na folha de saudação em Olá direita escolha autenticação do serviço de aplicativo. Observe a variedade de saudação das opções que você pode configurar com provedores populares.
    
     ![Imagem66][image66]
12. Escolha provedor Olá de sua escolha e observe Olá opções para escopo de saudação. Você pode fornecer uma ID do aplicativo e o segredo do aplicativo e habilitar a autenticação do Facebook para o aplicativo hello rapidamente. Olá Portal do Azure permite a autenticação como uma solução completa para aplicativos.
    
     ![Imagem67][image67]
13. Voltar toohello folha de configurações e escolha os usuários na categoria de gerenciamento de recursos de saudação.
    
     ![Imagem68][image68]
14. Na folha de saudação em Olá direita examinar Olá várias opções para adicionar funções e usuários. Olá Portal do Azure lhe permite controlar facilmente RBAC (controle de acesso baseado em função) para o aplicativo hello.
    
     ![Imagem69][image69]

## <a name="summary"></a>Resumo
Este tutorial demonstrado alguns energia Olá com hello plataforma Windows Azure rapidamente a implantação contínua para um aplicativo web, realizam o desenvolvimento de vários e as atividades de teste, monitorando e Solucionando problemas de um aplicativo em tempo real e finalmente gerenciar chave estratégias, como recuperação de desastres, identidade e controle de acesso baseado em função. Olá plataforma Windows Azure permite uma experiência integrada para esses fluxos de trabalho de DevOps e você pode trabalhar com eficiência permanecendo no contexto para a tarefa de saudação em questão.

## <a name="next-steps"></a>Próximas etapas
* Gerenciador de recursos do Azure é importante para habilitar DevOps Olá plataforma Windows Azure.  toolearn mais visitar [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).
* toolearn mais sobre a implantação do serviço de aplicativo do Azure, visite [implantar tooAzure seu aplicativo do serviço de aplicativo](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
