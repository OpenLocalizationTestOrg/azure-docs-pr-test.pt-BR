---
title: "recursos de documentação do aaaAzure WebJobs"
description: "Recursos de aprendizagem de recomendado como toouse WebJobs do Azure e Olá SDK do Azure WebJobs."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Recursos de documentação do Azure Webjobs
## <a name="overview"></a>Visão geral
Este tópico vincula toodocumentation recursos sobre como toouse WebJobs do Azure e Olá SDK do Azure WebJobs. WebJobs do Azure fornecem um scripts toorun de maneira fácil ou processos no contexto de saudação de plano de fundo de programas como um [aplicativo do serviço de aplicativo web, aplicativo de API ou aplicativo móvel](../app-service/app-service-value-prop-what-is.md). Você pode carregar e executar um arquivo executável, como cmd, bat, exe (.NET), ps1, sh, php, py, js, e jar. Esses programas são executados como WebJobs em uma agenda (cron) ou continuamente.

Olá finalidade Olá [SDK do WebJobs](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) toosimplify Olá código gravar para tarefas comuns que pode executar um trabalho Web, como processamento de imagem, processamento de fila, agregação de RSS, manutenção de arquivo e enviar emails. Olá SDK do WebJobs possui recursos internos para trabalhar com o armazenamento do Azure e o barramento de serviço, para o agendamento de tarefas e tratamento de erros e muitos outros cenários comuns. Além disso, ele tem projetado toobe extensível e há um [repositório do código-fonte aberto para extensões](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [As funções do Azure](../azure-functions/functions-overview.md) (atualmente em visualização) baseia-se em uma versão do SDK do WebJobs que funciona com o c# script, Node. js e outras linguagens de saudação. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Criar, implantar e gerenciar WebJobs é fácil com ferramentas integradas no Visual Studio. Você pode criar WebJobs a partir de modelos, publicar e gerenciar (executar, interromper, monitorar e depurar). 

painel do WebJobs Olá no hello portal do Azure fornece recursos de gerenciamento avançado que lhe dá controle total sobre a execução de saudação do WebJobs, incluindo Olá capacidade tooinvoke funções individuais em trabalhos Web. painel Olá também exibe a saída de log e tempos de execução de função. 

## <a name="getstarted"></a>Guia de Introdução com os trabalhos Web e Olá SDK do WebJobs
* [Introdução tooAzure WebJobs](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [O Azure Webjobs é impressionante e você deve começar a usá-lo agora mesmo!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Postagem no blog por Troy Hunt).
* [Recursos de Trabalhos Web do Azure](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [O que é Olá SDK do WebJobs](websites-dotnet-webjobs-sdk.md)
* [Diretrizes de trabalhos em segundo plano pelos Padrões e Práticas da Microsoft](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Anunciando Olá 1.1.0 RTM do Microsoft Azure SDK do WebJobs](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Introdução ao SDK do Azure WebJobs de saudação](websites-dotnet-webjobs-sdk-get-started.md)
* [Como o armazenamento com hello SDK do WebJobs de fila toouse do Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Como toouse Azure blob storage com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Como o armazenamento com hello SDK do WebJobs de tabela toouse do Azure](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Como toouse de barramento de serviço do Azure com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-service-bus.md)
* [Guia de referência rápida do SDK de Trabalhos Web do Azure (download do PDF)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Documentação de configurações de Trabalhos Web no GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Vídeos
  * [Os trabalhos Web e Olá SDK do WebJobs](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Série de vídeos de Trabalhos Web do Azure no Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Apresentando as ferramentas de Trabalhos Web do Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Depuração remota e ferramentas de Trabalhos Web](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Atualização do Azure WebJobs com Pranav Rastogi - extensibilidade na versão 1.1](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Consulte também Olá seções a seguir [implantar WebJobs](#deploy) e [teste e depuração WebJobs](#debug).

## <a name="deploy"></a>Implantando Trabalhos Web
* [Como tooDeploy WebJobs do Azure usando o Visual Studio](websites-dotnet-deploy-webjobs.md)
* [Como toodeploy WebJobs usando Olá Portal do Azure](web-sites-create-web-jobs.md)
* [Habilitando entrega de linha de comando ou contínua dos Trabalhos Web do Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Git Implantando um tooAzure de aplicativo de console .NET usando WebJobs](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Implantando um tooAzure WebJob F #](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Implantando serviços personalizados como Azure WebJobs](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Vídeos
  * [Apresentando as ferramentas de Trabalhos Web do Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Depuração remota e ferramentas de Trabalhos Web](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Agendando Trabalhos Web
* [Hello Azure WebJob caixa de diálogo Adicionar](websites-dotnet-deploy-webjobs.md#configure)
* [Criar um trabalho Web agendado no hello Portal do Azure](web-sites-create-web-jobs.md#CreateScheduled)
* [Um trabalho de Agendador tooa WebJob de gancho](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Agendando Azure WebJobs com expressões cron](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Agendamento de funções de trabalho Web individuais usando Olá TimerTrigger de SDK do WebJobs](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Testando e depurando Trabalhos Web
* [Novos recursos de desenvolvedor e de depuração para Trabalhos Web do Azure no Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Exibir hello painel do WebJobs](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Como toowrite logs usando Olá SDK do WebJobs e exibi-los no hello painel](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Depuração remota de Trabalhos Web](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Quem criou esse blob?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Código interativo no hello nuvem de hospedagem](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Adicionando rastreamento tooAzure WebJobs](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Monitoramento, diagnóstico e solução de problemas de Armazenamento do Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Vídeos
  * [Depuração remota e ferramentas de Trabalhos Web](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Dimensionando de WebJobs
* [Dimensionando seu aplicativo Web com sites do Azure](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Serviço de aplicativo do Azure: Arquitetura de aplicativos Web prontos para empresa de grande escala](https://channel9.msdn.com/Events/Build/2014/3-626). Abrange a expansão de aplicativos web com o WebJobs, incluindo Olá SDK do WebJobs.
* Vídeos
  * [Expandindo Trabalhos Web](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Recursos adicionais de Trabalhos Web
* [Postagem no blog WebJobs GA do Azure de Magnus Mårtensson](http://magnusmartensson.com/azure-webjobs-ga)
* [Executando Trabalhos Web do Powershell no Serviço de Aplicativo do Azure](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Seja notificado quando os Trabalhos Web disparados pelo Azure forem concluídos](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Política de retenção de backup de site simples com Trabalhos Web](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Sites do Azure e Serviços de Nuvem lentos na primeira solicitação](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Mostra como toouse WebJobs toosimulate Olá recurso AlwaysOn que só está disponível para a camada de preços padrão hello.
* [Desligamento normal dos Trabalhos Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Para o desligamento normal do SDK de Trabalhos Web, consulte [Desligamento normal](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).)
* [Automatizando Backups com WebJobs do Azure e AzCopy](http://markjbrown.com/azure-webjobs-azcopy/)
* Vídeos
  * [Vídeos de Trabalhos Web do Azure, de Magnus Mårtensson](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Série de vídeos de Trabalhos Web do Azure no Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Recursos adicionais do SDK de Trabalhos Web
* [Notas de lançamento do SDK do WebJobs](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [Código-fonte do SDK de Trabalhos Web](https://github.com/Azure/azure-webjobs-sdk)
* [Extensões do SDK do WebJobs do código-fonte](https://github.com/Azure/azure-webjobs-sdk-extensions), com [modelo de extensibilidade do guia detalhadas toohello](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [Código-fonte do script do SDK de WebJobs](https://github.com/Azure/azure-webjobs-sdk-script/) (usado para o [Azure Functions](../azure-functions/functions-overview.md))
* [Arquivos de FREB WebJob tooupload tooAzure armazenamento usando Olá SDK do WebJobs](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Hospedagem do Azure webjobs fora do Azure, com hello log benefícios de um Azure webjob hospedado](http://bypassion.dk/?p=510)
* [Criando uma ferramenta de importação de dados com Trabalhos Web do Azure](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Visão geral das Funções do Azure](../azure-functions/functions-overview.md)
* Vídeos
  * [Série de vídeos de Trabalhos Web do Azure no Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Aplicativos de Trabalhos Web de exemplo
* [Aplicativos de exemplo fornecidos pela equipe do hello WebJobs no GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Aplicativo Web do Azure simples com WebJobs Backend usando Olá SDK do WebJobs](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Demonstra o uso de WebJobs agendados e controlados por evento. Consulte a postagem de blog Olá [Olá de reconstrução SiteMonitR usando o SDK do Azure WebJobs](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogs
* [Blog do Azure](/blog)
* [Blog de Amit Apple](http://blog.amitapple.com/). Se concentra em trabalhos Web (não Olá SDK).
* [Blog de Magnus Mårtensson](http://magnusmartensson.com/)

## <a name="gethelp"></a>Obtendo ajuda com Trabalhos Web
* [StackOverflow para Trabalhos Web](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow para Olá SDK do WebJobs](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow para Azure Functions](http://stackoverflow.com/questions/tagged/azure-functions)
* [Fórum do Azure e ASP.NET](http://forums.asp.net/1247.aspx)
* [Fórum de aplicativos Web do Serviço de Aplicativo do Azure](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Site de voz do usuário de Aplicativos Web do Azure](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Use Olá hashtag #AzureWebJobs.
* [Relatar um problema ou bug do WebJobs](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

