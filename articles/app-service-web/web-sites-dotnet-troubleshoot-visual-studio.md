---
title: "aaaTroubleshoot um aplicativo web no serviço de aplicativo do Azure usando o Visual Studio"
description: "Saiba como tootroubleshoot um aplicativo web do Azure usando a depuração remota, rastreamento e registro em log das ferramentas que são criados no tooVisual Studio 2013."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Solucionar problemas de um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio
## <a name="overview"></a>Visão geral
Este tutorial mostra como toouse ferramentas do Visual Studio que ajudam a depurar um aplicativo web no [do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714), executando em [modo de depuração](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotamente ou exibindo logs de aplicativos e logs do servidor web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Você aprenderá a:

* Quais funções de gerenciamento de aplicativo Web do Azure estão disponíveis no Visual Studio.
* Como remota do Visual Studio toouse exibir toomake alterações em um aplicativo web remoto.
* Como modo de depuração toorun remotamente enquanto um projeto está em execução no Azure, para um aplicativo web e um trabalho Web.
* Como o aplicativo toocreate logs de rastreamento e exibi-los ao aplicativo hello é criá-los.
* Como os logs do servidor web tooview, incluindo mensagens de erro detalhadas e rastreamento de solicitação falha.
* Como o diagnóstico toosend registra tooan conta de armazenamento do Azure e exibi-los lá.

Se você tiver o Visual Studio Ultimate, também é possível utilizar o [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) para depuração. O IntelliTrace não é abordado neste tutorial.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial funciona com o ambiente de desenvolvimento hello, projeto da web e aplicativo web do Azure que você configurou em [Introdução ao Azure e ASP.NET][GetStarted]. Seções de trabalhos Web hello, você precisará de aplicativo hello criadas no [Introdução ao SDK do Azure WebJobs de saudação][GetStartedWJ].

código de saudação exemplos mostrados neste tutorial são para um aplicativo da web MVC c#, mas Olá procedimentos de solução de problemas são Olá mesmo para aplicativos Visual Basic e formulários da Web.

tutorial de saudação pressupõe que você está usando o Visual Studio 2015 ou 2013. Se você estiver usando o Visual Studio 2013, Olá WebJobs requerem [atualização 4](http://go.microsoft.com/fwlink/?LinkID=510314) ou posterior.

os logs de streaming Olá recurso só funciona para aplicativos que o destino do .NET Framework 4 ou posterior.

## <a name="sitemanagement"></a>Gerenciamento e configuração de aplicativo Web
O Visual Studio fornece acesso tooa subconjunto de funções de gerenciamento de aplicativo de web hello e configurações disponíveis no hello [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Nesta seção, você verá o que está disponível usando o **Gerenciador de Servidores**. recursos de integração do Azure mais recentes Olá de toosee, experimente **Cloud Explorer** também. Você pode abrir o windows da saudação **exibição** menu.

1. Se você não tiver entrado no tooAzure no Visual Studio, clique em Olá **conectar tooAzure** no botão **Server Explorer**.

    Uma alternativa é tooinstall um certificado de gerenciamento que permite acessar tooyour conta. Se você escolher tooinstall um certificado, clique com botão direito Olá **Azure** nó **Server Explorer**e, em seguida, clique em **gerenciar e assinaturas de filtro** no menu de contexto de saudação. Em Olá **gerenciar assinaturas do Azure** caixa de diálogo, clique em Olá **certificados** guia e, em seguida, clique em **importação**. Execute toodownload de direções de saudação e, em seguida, importar um arquivo de assinatura (também chamado de um *. publishsettings* arquivo) para sua conta do Azure.

   > [!NOTE]
   > Se você baixar um arquivo de assinatura, salve-a pasta tooa fora dos diretórios de código de origem (por exemplo, na pasta de Downloads de saudação) e, em seguida, excluí-lo após a conclusão da importação de saudação. Um usuário mal-intencionado que obtém o arquivo de assinatura de toohello acesso pode editar, criar e excluir seus serviços do Azure.
   >
   >

    Para obter mais informações sobre como conectar tooAzure recursos do Visual Studio, consulte [gerenciar contas, assinaturas e funções administrativas](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. No **Gerenciador de Servidores**, expanda **Azure** e **Serviço de Aplicativo**.
3. Expanda Olá grupo de recursos que inclui o aplicativo web hello que você criou na [guia de Introdução ao Azure e ASP.NET][GetStarted]e, em seguida, clique o nó de aplicativo web hello e clique em **deconfiguraçõesdeexibição**.

    ![Exibir Configurações no Gerenciador de Servidores](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Olá **aplicativo Web do Azure** guia é exibida e você pode ver que há Olá web aplicativo configuração e gerenciamento de tarefas que estão disponíveis no Visual Studio.

    ![Janela Aplicativo Web do Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    Neste tutorial, você vai usar o log hello e rastreamento suspensos. Você também usará a depuração remota, mas você usará um método diferente de tooenable-lo.

    Para obter informações sobre caixas de cadeias de caracteres de Conexão e as configurações do aplicativo hello nesta janela, consulte [aplicativos Web do Azure: como cadeias de caracteres de aplicativo e o trabalho de cadeias de caracteres de Conexão](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Se você quiser tooperform uma tarefa de gerenciamento de aplicativo da web não pode ser feita nesta janela, clique em **abrir no Portal de gerenciamento** tooopen uma janela de navegador toohello portal do Azure.

## <a name="remoteview"></a>Acessar arquivos de aplicativo Web no Gerenciador de Servidores
Você normalmente implanta um projeto da web com hello `customErrors` sinalizador no conjunto de arquivos Web. config de saudação muito`On` ou `RemoteOnly`, que significa que você não receberá uma mensagem de erro úteis quando algo dá errado. Para muitos erros tudo que você obter é uma página como uma saudação seguindo os.

**Erro de servidor no aplicativo '/':**

![Página de erro inútil](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Ocorreu um erro:**

![Página de erro inútil](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**site de saudação não é possível exibir a página de saudação**

![Página de erro inútil](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Com frequência hello mais fácil maneira toofind Olá causa erro Olá é tooenable mensagens de erro detalhadas que Olá primeiro Olá anterior capturas de tela explica como toodo. Isso exige que uma alteração no hello implantado o arquivo Web. config. Você pode editar Olá *Web. config* arquivo no projeto de saudação e projeto de saudação de reimplantação, ou criar um [transformação do Web. config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) e implantar uma compilação de depuração, mas há uma maneira mais rápida: no **solução Gerenciador de** diretamente, você pode exibir e editar arquivos no hello remoto web app usando Olá *exibição remota* recurso.

1. Em **Server Explorer**, expanda **Azure**, expanda **do serviço de aplicativo**, expanda o grupo de recursos de saudação localizado em seu aplicativo web e, em seguida, expanda o nó de saudação para seu aplicativo web.

    Você verá nós que fornecem acesso toohello web app arquivos de conteúdo e arquivos de log.
2. Expanda Olá **arquivos** nó e clique duas vezes em Olá *Web. config* arquivo.

    ![Abrir Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio abre o arquivo Web. config de saudação do aplicativo de web remoto de saudação e mostra [remoto] nome do arquivo toohello Avançar na barra de título de saudação.
3. Adicionar Olá toohello linha a seguir `system.web` elemento:

    `<customErrors mode="Off"></customErrors>`

    ![Editar Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Atualizar Olá navegador que está sendo exibida a mensagem de erro inútil hello e agora você receberá uma mensagem de erro detalhada, como Olá exemplo a seguir:

    ![Mensagem de erro detalhada](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (erro Olá mostrado foi criado pela adição de linha hello mostrada em vermelho muito*Views\Home\Index.cshtml*.)

Edição Olá Web. config é apenas um exemplo de cenários que capacidade Olá tooread e editar arquivos em seu aplicativo web do Azure tornam a solução de problemas.

## <a name="remotedebug"></a>Depuração remota de aplicativos Web
Se a mensagem de erro detalhada Olá não fornece informações suficientes e você não pode recriar a erro de saudação localmente, tootroubleshoot de outra forma é toorun no modo de depuração remotamente. Você pode definir pontos de interrupção, manipular memória diretamente, percorrer o código e até mesmo alterar o caminho de código de saudação.

A depuração remota não funciona em edições Express do Visual Studio.

Esta seção mostra como toodebug remotamente usando Olá projeto que você criar no [guia de Introdução ao Azure e ASP.NET][GetStarted].

1. Projeto web hello abertos que você criou na [guia de Introdução ao Azure e ASP.NET][GetStarted].
2. Abra o *Controllers\HomeController.cs*.
3. Excluir Olá `About()` método e a seguir Olá inserir código em seu lugar.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Definir um ponto de interrupção](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) em Olá `ViewBag.Message` linha.
5. Em **Solution Explorer**, clique com botão direito hello e clique em **publicar**.
6. Em Olá **perfil** lista suspensa, selecione Olá mesmo perfil que você usou no [guia de Introdução ao Azure e ASP.NET][GetStarted].
7. Clique em Olá **configurações** guia e alterar **configuração** muito**depurar**e, em seguida, clique em **publicar**.

    ![Publicar em modo de depuração](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Após a implantação for concluída e o navegador abre toohello Azure URL de seu aplicativo web, o navegador Olá fechar.
9. No **Gerenciador de Servidores**, clique com o botão direito do mouse no seu aplicativo Web e clique em **Anexar Depurador**.

    ![Anexar Depurador](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    navegador de saudação automaticamente abre tooyour home page em execução no Azure. Você pode ter toowait 20 segundos ou então enquanto Azure configura o servidor de saudação para depuração. Esse atraso ocorre apenas Olá primeira vez que executar no modo de depuração em um aplicativo web. Na próxima vez em Olá próximas 48 horas, quando você iniciar a depuração novamente não será um atraso.

    **Observação:** se você tiver problemas para iniciar o depurador hello, tente toodo usando **Cloud Explorer** em vez de **Server Explorer**.
10. Clique em **sobre** no menu de saudação.

     O Visual Studio parar no ponto de interrupção hello e código hello está em execução no Azure, não no computador local.
11. Passe o mouse sobre Olá `currentTime` valor de tempo de saudação toosee variável.

     ![Exibir variável no modo de depuração em execução no Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     tempo de saudação que você vê é hora do servidor do Azure hello, que pode estar em um fuso horário diferente do seu computador local.
12. Insira um novo valor para Olá `currentTime` variável, como "Agora em execução no Azure".
13. Pressione F5 toocontinue em execução.

     Olá sobre a página em execução no Azure exibe Olá novo valor que você inseriu na variável do hello currentTime.

     ![A página Sobre com o novo valor](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> Trabalhos Web de depuração remota
Esta seção mostra como toodebug remotamente usando Olá projeto e o aplicativo web que você criar no [Introdução ao SDK do Azure WebJobs de saudação](websites-dotnet-webjobs-sdk.md).

recursos de saudação mostrados nesta seção estão disponíveis apenas no Visual Studio 2013 com atualização 4 ou posterior.

A depuração remota só funciona com Trabalhos Web contínuos. Trabalhos Web agendados e sob demanda não oferecem suporte a depuração.

1. Projeto web hello abertos que você criou na [Introdução ao SDK do Azure WebJobs de saudação][GetStartedWJ].
2. No projeto de ContosoAdsWebJob hello, abra *Functions.cs*.
3. [Definir um ponto de interrupção](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) na primeira instrução Olá Olá `GnerateThumbnail` método.

    ![Definir ponto de interrupção](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. Em **Solution Explorer**, clique com botão direito Olá web (não projeto WebJob Olá) e clique em **publicar**.
5. Em Olá **perfil** lista suspensa, selecione Olá mesmo perfil que você usou no [Introdução ao SDK do Azure WebJobs de saudação](websites-dotnet-webjobs-sdk.md).
6. Clique em Olá **configurações** guia e alterar **configuração** muito**depurar**e, em seguida, clique em **publicar**.

    O Visual Studio implanta Olá web e projetos de trabalho Web e seu navegador abrirá toohello Azure URL de seu aplicativo web.
7. Em **Gerenciador de Servidores**, expanda **Azure > Serviço de Aplicativo > seu grupo de recursos > seu aplicativo Web > WebJobs > Contínuo** e clique com o botão direito do mouse em **ContosoAdsWebJob**.
8. Clique em **Anexar o depurador**.

    ![Anexar Depurador](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    navegador de saudação automaticamente abre tooyour home page em execução no Azure. Você pode ter toowait 20 segundos ou então enquanto Azure configura o servidor de saudação para depuração. Esse atraso ocorre apenas Olá primeira vez que executar no modo de depuração em um aplicativo web. Olá próxima vez que você anexar o depurador de saudação existe não será um atraso, se você pode fazer isso dentro de 48 horas.
9. No navegador da web hello que é aberto toohello Contoso anúncios home page, crie um novo anúncio.

    Criando um anúncio faz com que uma fila mensagem toobe criado, que será capturada pelo Olá WebJob e processado. Quando Olá SDK do WebJobs chama a função tooprocess Olá fila mensagem de saudação do, Olá atingida pelo código seu ponto de interrupção.
10. Quando depurador Olá interrompida no ponto de interrupção, você pode examinar e alterar valores de variáveis durante saudação nuvem hello. Na Olá depurador de saudação ilustração a seguir mostra o conteúdo de saudação do objeto de blobInfo Olá passado toohello GenerateThumbnail método.

     ![Objeto blobInfo no depurador](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Pressione F5 toocontinue em execução.

     Olá GenerateThumbnail método termina de criar miniatura hello.
12. No navegador de hello, página de índice de saudação de atualização e você verá miniatura hello.
13. No Visual Studio, pressione SHIFT + F5 toostop depuração.
14. Em **Server Explorer**, clique o nó de ContosoAdsWebJob hello e clique em **painel de exibição**.
15. Entrar com suas credenciais do Azure e clique em página de toohello Olá WebJob nome toogo para seu trabalho Web.

     ![Clicar em ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Olá painel mostra que Olá função GenerateThumbnail executada recentemente.

     (Olá da próxima vez que você clicar em **painel de exibição**, você não tem toosign no e navegador Olá diretamente vai toohello página para seu trabalho Web.)
16. Clique em detalhes sobre a execução da função de saudação da saudação função nome toosee.

     ![Detalhes da função](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

Se sua função [gravou logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), você pode clicar em **ToggleOutput** toosee-los.

## <a name="notes-about-remote-debugging"></a>Observações sobre a depuração remota
* A execução em modo de depuração em produção não é recomendada. Se seu aplicativo da web de produção não é expandido toomultiple instâncias de servidor, depuração impedirá que servidor de web hello de solicitações de tooother está respondendo. Se você fizer várias instâncias do servidor web, quando você anexa o depurador toohello você terá uma instância aleatória e você não tiver tooensure nenhuma maneira navegador subsequente solicitações irá toothat instância. Além disso, você normalmente não implanta um tooproduction de compilação de depuração e otimizações de compilador para compilações de versão podem tornar impossível tooshow que está acontecendo linha por linha em seu código-fonte. Para solucionar problemas de produção, os melhores recursos são o rastreamento do aplicativo e os logs do servidor Web.
* Evite paradas longas em pontos de interrupção durante a depuração remota. O Azure trata um processo parado por mais de alguns minutos como um processo sem resposta e o desliga.
* Durante a depuração, o servidor de saudação está enviando dados tooVisual Studio, o que poderia afetar os encargos de largura de banda. Para obter informações sobre as taxas de largura de banda, consulte [Preço do Azure](https://azure.microsoft.com/pricing/calculator/).
* Certifique-se de que Olá `debug` atributo de saudação `compilation` elemento Olá *Web. config* arquivo é definido como tootrue. Ele é definido tootrue por padrão, quando você publica uma configuração de compilação de depuração.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Se você achar que o depurador Olá não entrar no código que você deseja toodebug, talvez seja necessário toochange configuração de apenas meu código de saudação.  Para obter mais informações, consulte [restringir revisão tooJust meu código](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Um temporizador é iniciado no servidor de saudação quando você habilitar o recurso de depuração remota hello e depois de 48 horas Olá recurso será automaticamente desativado. Esse limite de 48 horas é definido por razões de segurança e desempenho. Você pode facilmente ligue recurso Olá quantas vezes desejar. É recomendável deixá-lo desabilitado quando você não está depurando ativamente.
* Você pode anexar manualmente o processo de tooany depurador hello, não apenas Olá web processo do aplicativo (w3wp.exe). Para obter mais informações sobre como toouse depurar modo no Visual Studio, consulte [depuração no Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Visão geral dos logs de diagnóstico
Um aplicativo ASP.NET que é executado em um aplicativo web do Azure pode criar hello tipos de logs a seguir:

* **Logs de rastreamento de aplicativos**<br/>
  Olá aplicativo cria esses logs chamando métodos de saudação [Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) classe.
* **Logs do servidor Web**<br/>
  servidor de web Hello cria uma entrada de log para cada aplicativo web de toohello de solicitação HTTP.
* **Logs de mensagens de erro detalhadas**<br/>
  servidor de web Hello cria uma página HTML com algumas informações adicionais para solicitações HTTP com falha (aquelas que resultam no código de status 400 ou superior).
* **Logs de rastreamento de solicitações com falha**<br/>
  servidor de web Hello cria um arquivo XML com informações de rastreamento detalhadas para solicitações HTTP com falha. servidor de web Hello também fornece Olá um XSL tooformat de arquivo XML em um navegador.

Log afeta o desempenho do aplicativo web, para que o Azure oferece Olá tooenable capacidade ou desabilitar cada tipo de log, conforme necessário. Para logs de aplicativo, você pode especificar que apenas os logs acima de um determinado nível de gravidade devem ser gravados. Por padrão, quando você cria um novo aplicativo Web, todo o registro em log está desabilitado.

Os logs são gravados toofiles uma *LogFiles* pasta no sistema de arquivos de saudação do seu aplicativo web e são acessível por meio de FTP. Logs do servidor Web e logs de aplicativos também podem ser gravados tooan conta de armazenamento do Azure. Você pode manter um maior volume de logs em uma conta de armazenamento que é possível no sistema de arquivo hello. Você está limitado tooa máximo de 100 megabytes de logs ao usar o sistema de arquivo hello. (Os logs do sistema de arquivos são apenas para retenção de curto prazo. Azure exclui antigo espaço toomake de arquivos de log para novos depois Olá limite for atingido.)  

## <a name="apptracelogs"></a>Criar e exibir logs de rastreamento de aplicativos
Nesta seção, você fará Olá seguintes tarefas:

* Adicionar projeto da web de toohello de instruções de rastreamento que você criou na [Introdução ao Azure e ASP.NET][GetStarted].
* Exibir logs de hello quando você executar o projeto de saudação localmente.
* Exibir logs de saudação conforme eles são gerados pelo aplicativo hello em execução no Azure.

Para obter informações sobre como o aplicativo toocreate registra em trabalhos Web, consulte [como toowork com o uso do armazenamento de fila do Azure Olá SDK do WebJobs - como toowrite registra](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). Olá instruções a seguir para exibir os logs e controle de como eles são armazenados no Azure também aplicam os logs de tooapplication criados por trabalhos Web.

### <a name="add-tracing-statements-toohello-application"></a>Adicionar aplicativo de toohello de instruções de rastreamento
1. Abra *Controllers\HomeController.cs*e substitua Olá `Index`, `About`, e `Contact` código métodos com hello a seguir na ordem tooadd `Trace` instruções e um `using` instrução para `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Adicionar um `using System.Diagnostics;` superior de toohello de instrução de arquivo hello.

### <a name="view-hello-tracing-output-locally"></a>Rastreamento de saudação exibir saído localmente
1. Pressione F5 aplicativo de hello de toorun no modo de depuração.

    ouvinte de rastreamento padrão Olá grava todos os toohello de saída de rastreamento **saída** janela, junto com outra saída de depuração. Olá ilustração a seguir mostra saída Olá Olá instruções de rastreamento que você adicionou toohello `Index` método.

    ![Rastreamento na janela Depuração](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Olá, as etapas a seguir mostra como tooview a saída do rastreamento em uma página da web, sem compilar no modo de depuração.
2. Abra o arquivo Web. config do aplicativo hello (um localizado na pasta de projeto Olá Olá) e adicione um `<system.diagnostics>` elemento final de saudação do arquivo hello logo antes de fechamento Olá `</configuration>` elemento:

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Olá `WebPageTraceListener` permite exibir a saída de rastreamento navegando muito`/trace.axd`.
3. Adicionar um <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">elemento trace</a> em `<system.web>` no arquivo de Web. config hello, como Olá exemplo a seguir:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. Pressione CTRL + F5 aplicativo de hello de toorun.
5. Na barra de endereços Olá Olá da janela do navegador, adicione *trace.axd* toohello URL, e pressione Enter (Olá URL será toohttp://localhost:53370/trace.axd semelhante).
6. Em Olá **rastreamento de aplicativo** , clique em **exibir detalhes** na primeira linha do hello (não Olá BrowserLink linha).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Olá **detalhes da solicitação** página será exibida e em Olá **informações de rastreamento** seção Consulte saída Olá Olá das instruções de rastreamento que você adicionou toohello `Index` método.

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    Por padrão, `trace.axd` só está disponível localmente. Se você quisesse toomake-lo de um aplicativo web remoto, você pode adicionar `localOnly="false"` toohello `trace` elemento Olá *Web. config* de arquivos, conforme mostrado no exemplo a seguir de saudação:

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    No entanto, habilitar `trace.axd` em um de produção aplicativo web geralmente não é recomendado por motivos de segurança e Olá seções a seguir, você verá um tooread de maneira mais fácil rastreamento logs em um aplicativo web do Azure.

### <a name="view-hello-tracing-output-in-azure"></a>Exibir saída de rastreamento Olá no Azure
1. Em **Solution Explorer**, clique com botão direito Olá web e clique em **publicar**.
2. Em Olá **Publicar Web** caixa de diálogo, clique em **publicar**.

    Depois que o Visual Studio publica sua atualização, ele abre uma janela de navegador tooyour home page (supondo que você não desmarcar **URL de destino** em Olá **Conexão** guia).
3. No **Gerenciador de Servidores**, clique com o botão direito do mouse no aplicativo Web e selecione **Exibir Logs de Streaming**.

    ![Exibir Logs de Streaming no menu de contexto](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Olá **saída** janela mostra que você está conectado toohello log de streaming de serviço e adiciona uma linha de notificação a cada minuto que não toodisplay um log.

    ![Exibir Logs de Streaming no menu de contexto](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. Na janela de navegador Olá que mostra a home page do aplicativo, clique em **entre em contato com**.

    Em alguns Olá segundos de saída do rastreamento em nível de erro Olá adicionado toohello `Contact` método aparece no hello **saída** janela.

    ![Rastreamento de erro na janela Saída](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    O Visual Studio só mostra os rastreamentos de nível de erro porque o que é a configuração de padrão de hello quando você habilitar o serviço de monitoração de log de saudação. Quando você cria um novo aplicativo web do Azure, todos log é desabilitado por padrão, como visto quando você abriu a página de configurações de saudação anteriormente:

    ![Log do aplicativo desativado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    No entanto, se você selecionou **Exibir Logs de Streaming**, Visual Studio automaticamente alterado **aplicativo Logging(File System)** muito**erro**, que significa que os logs de nível de erro são reportadas. Em ordem toosee todos os logs de rastreamento, você pode alterar essa configuração muito**detalhado**. Quando você seleciona um nível de severidade inferior a erro, todos os logs para níveis de severidade mais altos são relatados. Portanto, quando selecionar detalhado, você também verá logs de informações, avisos e erros.  

1. Em **Server Explorer**, clique com botão direito Olá web app e, em seguida, clique em **exibir configurações** como você fez anteriormente.
2. Alterar **(sistema de arquivos) de log de aplicativo** muito**detalhado**e, em seguida, clique em **salvar**.

    ![Configuração tooVerbose de nível de rastreamento](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. Na janela do navegador Olá que agora está mostrando o **entre em contato com** , clique em **início**, em seguida, clique em **sobre**e, em seguida, clique em **entre em contato com**.

    Em alguns segundos, Olá **saída** janela mostra todos os a saída de rastreamento.

    ![Saída de rastreamento detalhado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    Nesta seção você habilitou e desabilitou o registro em log usando as configurações de aplicativo Web do Azure. Você também pode habilitar e desabilitar ouvintes de rastreamento, modificando o arquivo Web. config de saudação. No entanto, modificar o arquivo Web. config de saudação faz com que Olá toorecycle de domínio de aplicativo, ao habilitar o log por meio de configuração de aplicativo da web hello não faz isso. Se problema Olá leva um tempo longo tooreproduce ou intermitente, a reciclagem de domínio de aplicativo hello pode "corrigir" e forçar toowait até que ele ocorra novamente. Como a habilitação do diagnóstico no Azure não faz isso, você não pode começar a capturar informações de erro imediatamente.

### <a name="output-window-features"></a>Recursos da janela Saída
Olá **Logs do Azure** guia da saudação **saída** janela tem vários botões e uma caixa de texto:

![Botões da guia Logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Realizam Olá funções a seguir:

* Olá limpar **saída** janela.
* Habilite ou desabilite a quebra automática de linha.
* Inicie ou pare logs de monitoramento.
* Especificar quais logs toomonitor.
* Baixe logs.
* Filtre logs com base em uma cadeia de caracteres de pesquisa ou uma expressão regular.
* Olá fechar **saída** janela.

Se você inserir uma cadeia de caracteres ou expressão regular, o Visual Studio filtra informações de log no cliente de saudação. Isso significa que você pode inserir critérios de saudação depois Olá logs são exibidos no hello **saída** janela e alterar os critérios de filtragem sem ter que tooregenerate Olá logs.

## <a name="webserverlogs"></a>Exibir logs de servidor Web
Logs do servidor Web registram todas as atividades HTTP para o aplicativo web de saudação. Em ordem toosee em Olá **saída** janela tem tooenable-los para Olá aplicativo da web e informam o Visual Studio que você deseja toomonitor-los.

1. Em Olá **configuração de aplicativo Web do Azure** guia que você abriu da **Server Explorer**, alterar também o log de servidor Web**na**e, em seguida, clique em **salvar**.

    ![Habilitar o log de servidor web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. Em Olá **saída** janela, clique em Olá **especificar quais logs do Azure toomonitor** botão.

    ![Especifique quais toomonitor logs do Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. Em Olá **as opções de log do Azure** caixa de diálogo, selecione **Web logs do servidor**e, em seguida, clique em **Okey**.

    ![Monitorar logs de servidor Web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. Na janela de navegador Olá que mostra o aplicativo web de saudação, clique em **início**, em seguida, clique em **sobre**e, em seguida, clique em **entre em contato com**.

    logs de aplicativo Hello geralmente aparecem primeiro, seguido de logs do servidor web hello. Você pode ter toowait um pouco para Olá logs tooappear.

    ![Logs de servidor Web na janela Saída](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

Por padrão, quando você habilita logs do servidor web usando o Visual Studio, o Azure grava Olá logs toohello arquivo sistema. Como alternativa, você pode usar o hello Azure portal toospecify que web logs do servidor deve ser escrito tooa contêiner de blob de uma conta de armazenamento.

Se você usa servidor de web do portal tooenable Olá log tooan conta de armazenamento do Azure e, em seguida, desabilite o registro em log no Visual Studio, quando você habilitar novamente o registro em log no Visual Studio, as configurações de conta de armazenamento são restauradas.

## <a name="detailederrorlogs"></a>Exibir logs de mensagens de erro detalhadas
Os logs detalhados de erro fornecem algumas informações adicionais sobre solicitações HTTP que resultam em códigos de resposta de erro (400 ou acima). Em ordem toosee em Olá **saída** janela, você tem tooenable-los para Olá aplicativo da web e informam o Visual Studio que você deseja toomonitor-los.

1. Em Olá **configuração de aplicativo Web do Azure** guia que você abriu da **Server Explorer**, alterar **mensagens de erro detalhadas** muito**em**, e em seguida, clique em **salvar**.

    ![Habilitar mensagens de erro detalhadas](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. Em Olá **saída** janela, clique em Olá **especificar quais logs do Azure toomonitor** botão.
3. Em Olá **as opções de log do Azure** caixa de diálogo, clique em **todos os logs de**e, em seguida, clique em **Okey**.

    ![Monitorar todos os logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. Na barra de endereços de Olá Olá da janela do navegador, adicione um toocause de URL do caractere extra toohello um 404 erro (por exemplo, `http://localhost:53370/Home/Contactx`), e pressione Enter.

    Após alguns segundos log detalhado de erros de saudação aparece no hello Visual Studio **saída** janela.

    ![Log detalhado de erros na janela Saída](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    CTRL + clique em saída Olá link toosee Olá log formatada em um navegador:

    ![Log detalhado de erros na janela do navegador](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Baixar logs do sistema de arquivos
Os logs que você pode monitorar no hello **saída** janela também pode ser baixada como um *. zip* arquivo.

1. Em Olá **saída** janela, clique em **baixar Logs de Streaming**.

    ![Botões da guia Logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    Explorador de arquivos abre tooyour *Downloads* pasta com hello baixou o arquivo selecionado.

    ![Arquivo baixado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Extrair Olá *. zip* arquivo e você verá Olá estrutura de pasta a seguir:

    ![Arquivo baixado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * Logs de rastreamento de aplicativo estão em *. txt* arquivos Olá *LogFiles\Application* pasta.
   * Logs do servidor Web estão em *. log* arquivos Olá *LogFiles\http\RawLogs* pasta. Você pode usar uma ferramenta como [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview e manipular esses arquivos.
   * Logs de mensagem de erro detalhados estão no *. HTML* arquivos Olá *LogFiles\DetailedErrors* pasta.

     (Olá *implantações* pasta é para arquivos criados pelo controle de origem de publicação; ele não tem a publicação Studio tooVisual qualquer coisa relacionada. Olá *Git* pasta é para rastreamentos toosource relacionados controle publicação Olá arquivo de log e serviço de streaming.)  

## <a name="storagelogs"></a>Exibir logs de armazenamento
Logs de rastreamento de aplicativo também podem ser enviados tooan conta de armazenamento do Azure, e você pode exibi-los no Visual Studio. toodo que você criará uma conta de armazenamento, habilitar os logs de armazenamento no portal clássico do hello e exibi-los no hello **Logs** guia da saudação **aplicativo Web do Azure** janela.

Você pode enviar logs tooany ou todos os três destinos:

* sistema de arquivo Hello.
* Tabelas de conta de armazenamento.
* Blobs de conta de armazenamento.

Você pode especificar um nível de gravidade diferente para cada destino.

Tabelas torná-lo fácil tooview detalhes dos logs on-line e oferecem suporte a streaming; Você pode consultar os logs em tabelas e consulte novos logs conforme eles são criados. BLOBs tornar fácil toodownload logs nos arquivos e tooanalyze-los usando o HDInsight, porque o HDInsight sabe como toowork com armazenamento de blob. Para obter mais informações, consulte **Hadoop e MapReduce** em [Opções de armazenamento de dados (Compilando aplicativos de nuvem do mundo real com o Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

Atualmente você tem o nível de tooverbose do conjunto de logs de sistema de arquivos; Olá etapas a seguir orientam você durante a configuração de tabelas de conta informações sobre logs de nível toogo toostorage. O nível de informações significa que todos os logs criados chamando `Trace.TraceInformation`, `Trace.TraceWarning` e `Trace.TraceError` serão exibidos, mas não os logs criados chamando `Trace.WriteLine`.

Contas de armazenamento oferecem mais armazenamento e retenção de maior duração para logs em comparação com o sistema de arquivos toohello. Outra vantagem do aplicativo de envio toostorage logs de rastreamento é que algumas informações adicionais com cada log do qual você não obtiver de logs do sistema de arquivos.

1. Clique com botão direito **armazenamento** em Olá nó do Azure e, em seguida, clique em **criar conta de armazenamento**.

![Criar conta de armazenamento](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. Em Olá **criar conta de armazenamento** caixa de diálogo, digite um nome para a conta de armazenamento hello.

    nome da saudação deve ser exclusivo (nenhuma outra conta de armazenamento do Azure pode ter Olá mesmo nome). Se nome hello inserido já está em uso, obterá uma chance toochange-lo.

    Olá URL tooaccess sua conta de armazenamento será *{name}*. t.
2. Saudação de conjunto **região ou grupo de afinidade** tooyou mais próximo da lista suspensa toohello região.

    Essa configuração especifica qual datacenter do Azure hospedará a conta de armazenamento. Para este tutorial, sua escolha não fazer uma diferença notável, mas para um aplicativo da web de produção que você deseja o servidor web e o toobe de conta de armazenamento no hello encargos de saída de dados e latência de toominimize mesma região. aplicativo web de saudação (que você criará mais tarde) deve ser executado em uma região mais próximo navegadores toohello possível acessar seu aplicativo web na latência de toominimize de ordem.
3. Saudação de conjunto **replicação** suspensa lista muito**localmente redundante**.
   
    Quando a replicação geográfica é habilitada para uma conta de armazenamento, o conteúdo de Olá armazenado é replicado tooa datacenter secundário tooenable failover toothat local em caso de um grande desastre no local principal hello. A replicação geográfica pode incorrer em custos adicionais. Para contas de teste e desenvolvimento, geralmente você não quiser toopay para replicação geográfica. Para saber mais, confira [Criar, gerenciar ou excluir uma conta de armazenamento](../storage/common/storage-create-storage-account.md).
4. Clique em **Criar**.

    ![Nova conta de armazenamento](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. No Visual Studio de saudação **aplicativo Web do Azure** janela, clique em Olá **Logs** guia e, em seguida, clique em **configurar o log no Portal de gerenciamento**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![Configurar o registro em log](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Isso abre o hello **configurar** no portal clássico de saudação para seu aplicativo web.
6. No portal clássico hello **configurar** guia, role para baixo da seção de diagnóstico de aplicativos toohello e, em seguida, alterar **(armazenamento de tabela) de log de aplicativo** muito**em**.
7. Alterar **nível de log** muito**informações**.
8. Clique em **Gerenciar Armazenamento da Tabela**.

    ![Clicar em Gerenciar Armazenamento da Tabela](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    Em Olá **gerenciar armazenamento de tabelas para diagnóstico do aplicativo** caixa, você pode escolher sua conta de armazenamento se você tiver mais de um. Você pode criar uma nova tabela ou usar uma existente.

    ![Gerenciar Armazenamento da Tabela](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. Em Olá **gerenciar armazenamento de tabelas para diagnóstico do aplicativo** caixa de Olá Olá marca de seleção tooclose clique em.
10. No portal clássico hello **configurar** , clique em **salvar**.
11. Na janela de navegador Olá que exibe o aplicativo de web do aplicativo hello, clique em **início**, em seguida, clique em **sobre**e, em seguida, clique em **entre em contato com**.

     informações de registro em log Olá produzidas navegando essas páginas da web serão gravadas toohello conta de armazenamento.
12. Em Olá **Logs** guia da saudação **aplicativo Web do Azure** janela no Visual Studio, clique em **atualizar** em **resumo de diagnóstico**.

     ![Clicar em Atualizar](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Olá **resumo de diagnóstico** seção mostra logs para Olá últimos 15 minutos por padrão. Você pode alterar toosee período hello mais logs.

     (Se você receber um erro de "tabela não encontrado", verifique se que você pesquisou páginas toohello Olá rastreamento após a habilitação **log de aplicativo (armazenamento)** e depois que você clicou **salvar**.)

     ![Logs de armazenamento](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Observe que nessa exibição consulte **ID do processo** e **identificação do Thread** para cada log, que você não obtiver nos logs de sistema de arquivo hello. Você pode ver os campos adicionais exibindo tabela de armazenamento do Azure Olá diretamente.
13. Clique em **exibir todos os logs de aplicativo**.

     tabela de log de rastreamento de saudação aparece no Visualizador de tabela de armazenamento do Azure hello.

     (Se você receber um erro "sequência não contém elementos", abra **Server Explorer**, expanda para sua conta de armazenamento em Olá Olá **Azure** nó e, em seguida, clique com botão direito **tabelas**e clique em **atualizar**.)

     ![Logs de armazenamento na exibição de tabela](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Esta exibição mostra campos adicionais que você não vê em outros modos de exibição. Essa exibição também permite que você toofilter logs usando a interface do usuário construtor de consulta especial para construir uma consulta. Para obter mais informações, consulte Trabalhando com recursos de tabela - Filtrando entidades em [Procurando recursos de armazenamento com o Gerenciador de Servidores (a página pode estar em inglês)](http://msdn.microsoft.com/library/ff683677.aspx)
14. toolook detalhes da saudação de uma única linha, clique duas vezes em uma das linhas de saudação.

     ![Tabela de rastreamento no Gerenciador de Servidores](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Exibir logs de rastreamento de solicitações com falha
Logs de rastreamento de solicitação com falha são úteis quando precisar toounderstand Olá detalhes de como o IIS está lidando com uma solicitação HTTP, em cenários como problemas de autenticação ou reconfiguração de URL.

Saudação de usar aplicativos web do Azure mesmo falha solicitar a funcionalidade de rastreamento que está disponível com o IIS 7.0 e posterior. Você não tem acesso toohello configurações do IIS que configurar quais erros são registradas, no entanto. Quando você habilita o rastreamento de solicitação com falha, todos os erros são capturados.

Você pode habilitar o rastreamento de solicitação com falha usando o Visual Studio, mas não pode exibi-lo no Visual Studio. Esses logs são arquivos XML. Olá, somente o serviço de log de streaming monitora arquivos que são considerados legíveis no modo de texto sem formatação: *. txt*, *. HTML*, e *. log* arquivos.

Você pode exibir os logs de rastreamento de solicitação com falha em um navegador diretamente por meio de FTP ou localmente depois de usar um toodownload da ferramenta FTP-los computador local tooyour. Nesta seção você irá exibi-los diretamente em um navegador.

1. Em Olá **configuração** guia da saudação **aplicativo Web do Azure** janela aberta do **Server Explorer**, alterar **rastreamento de solicitação falha**muito**na**e, em seguida, clique em **salvar**.

    ![Habilitar o rastreamento de solicitações com falha](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. Na barra de endereços Olá Olá da janela do navegador que mostra o aplicativo de web hello, adicione uma URL de toohello caractere extra e clique em Enter toocause um erro 404.

    Isso faz com que um toobe de log de rastreamento de solicitação com falha criado e hello etapas a seguir mostram como tooview ou download Olá log.
3. No Visual Studio, no hello **configuração** guia da saudação **aplicativo Web do Azure** janela, clique em **abrir no Portal de gerenciamento**.
4. Em Olá [Portal do Azure](https://portal.azure.com) **configurações** folha para seu aplicativo web, clique em **credenciais de implantação**e, em seguida, digite um novo nome de usuário e senha.

    ![Novo nome de usuário e senha FTP](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    * * Ao efetuar login, você tem o nome de usuário completo Olá toouse com Olá web aplicativo nome prefixado tooit. Por exemplo, se você digitar "myid" como um nome de usuário e site hello "myexample", você faça logon como "myexample\myid".
5. Em uma nova janela do navegador, vá toohello URL que é mostrado em **hostname de FTP** ou **hostname FTPS** em Olá **aplicativo Web** folha para seu aplicativo web.
6. Faça logon usando credenciais de saudação FTP que você criou anteriormente (incluindo Olá o prefixo de nome de aplicativo de web para o nome de usuário Olá).

    navegador de saudação mostra a pasta raiz de saudação do aplicativo web de saudação.
7. Olá abrir *LogFiles* pasta.

    ![Abrir a pasta LogFiles](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. Abra a pasta de saudação chamado W3SVC mais de um valor numérico.

    ![Abrir a pasta W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    Olá contém arquivos XML para quaisquer erros que foram registrados depois que você habilitar o rastreamento de solicitação com falha e um arquivo XSL que um navegador pode usar tooformat Olá XML.

    ![Pasta W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Clique em arquivo XML de Olá Olá solicitação com falha que você deseja obter informações de rastreamento de toosee para.

    Olá ilustração a seguir mostra parte Olá de informações de rastreamento para um erro de exemplo.

    ![Rastreamento de solicitação com falha no navegador](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Próximas etapas
Você viu como o Visual Studio torna fácil tooview logs criados por um aplicativo web do Azure. Olá seções a seguir fornecem links toomore recursos sobre tópicos relacionados:

* Solução de problemas de aplicativo Web do Azure
* Depurando no Visual Studio
* Depuração remota no Azure
* Rastreando em aplicativos ASP.NET
* Analisando logs de servidor Web
* Analisando logs de rastreamento de solicitação com falha
* Depurando serviços de nuvem

### <a name="azure-web-app-troubleshooting"></a>Solução de problemas de aplicativo Web do Azure
Para obter mais informações sobre como solucionar problemas de aplicativos web no serviço de aplicativo do Azure, consulte Olá recursos a seguir:

* [Como toomonitor de aplicativos web](/manage/services/web-sites/how-to-monitor-websites/)
* [Investigando perdas de memória em aplicativos Web do Azure com o Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Postagem no blog do Microsoft ALM sobre os recursos do Visual Studio para análise de problemas de memória gerenciados.
* [Ferramentas online de aplicativos Web do Azure sobre as quais você deve saber](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Postagem de blog de Amit Apple.

Para obter ajuda com uma pergunta específica de solução de problemas, inicie um thread em uma saudação fóruns a seguir:

* [Olá Fórum do Azure no site do ASP.NET Olá](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [Olá Fórum do Azure no MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Depurando no Visual Studio
Para obter mais informações sobre como toouse depurar modo no Visual Studio, consulte Olá [depuração no Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) tópico do MSDN e [dicas de depuração com Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Depuração remota no Azure
Para obter mais informações sobre depuração remota para os aplicativos web do Azure e trabalhos da Web, consulte Olá recursos a seguir:

* [Introdução tooRemote depuração Azure aplicativo aplicativos Web do serviço](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Introdução tooRemote depuração aplicativo de serviço de aplicativos Web do Azure parte 2 - dentro de depuração remota](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Introdução tooRemote depuração de parte de aplicativos de Web do serviço de aplicativo do Azure 3 - ambiente de várias instâncias e GIT](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [Depuração de Trabalhos Web (vídeo)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Se seu aplicativo web usa um back-end de API da Web do Azure ou serviços móveis e você precisar toodebug que, consulte [depuração back-end .NET no Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>Rastreando em aplicativos ASP.NET
Não há nenhum tooASP.NET introduções completa e atualizada rastreamento disponíveis no hello da Internet. Olá melhor você pode fazer é começar antigo material introdutório escritos para o Web Forms porque MVC não ainda existe e complementar que com mais recente blog postagens que se concentram em problemas específicos. Alguns locais de BOM toostart são Olá recursos a seguir:

* [Monitoramento e telemetria (Compilando aplicativos de nuvem do mundo real com o Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  Capítulo do livro eletrônico com recomendações para rastreamento em aplicativos de nuvem do Azure.
* [Rastreamento do ASP.NET](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Antigo, mas ainda um bom recurso para um assunto de toohello introdução básica.
* [Ouvintes de rastreamento](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  Informações sobre ouvintes de rastreamento, mas não mencione Olá [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [Passo a passo: Integrando o rastreamento do ASP.NET com rastreamento do System.Diagnostics](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  Isso também é antigo, mas inclui algumas informações adicionais não cubra artigo introdutório hello.
* [Rastreamento em exibições do Razor do ASP.NET MVC](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Além de rastreamento em modos de exibição Razor, post Olá também explica como filtrar toocreate um erro na ordem toolog exceções sem tratamento tudo em um aplicativo MVC. Para obter informações sobre como sem tratamento toolog todas as exceções em um aplicativo de Web Forms, consulte o exemplo global. asax Olá [exemplo completo para manipuladores de erro](http://msdn.microsoft.com/library/bb397417.aspx) no MSDN. No MVC ou Web Forms, se você quiser toolog certas exceções, mas permitir que o framework de padrão de saudação tratamento entrarão em vigor para eles, você pode capturar e relançar como Olá exemplo a seguir:

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Fluxo de log de rastreamento de diagnóstico de saudação de linha de comando do Azure (mais prévia!)](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  Como toouse Olá toodo de linha de comando que este tutorial mostra como toodo no Visual Studio. [Glimpse (a página pode estar em inglês)](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) é uma ferramenta para depuração de aplicativos ASP.NET.
* [Usando diagnóstico e registro em log de Aplicativos Web – com David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) e [Logs de streaming dos Aplicativos Web – com David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  Vídeos de Scott Hanselman e David Ebbo.

Para o log de erro, uma alternativa toowriting seu próprio código de rastreamento é toouse uma código-fonte aberto log estrutura como [ELMAH](http://nuget.org/packages/elmah/). Para obter mais informações, consulte as [postagens no blog de Scott Hanselman sobre o ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Além disso, observe que você não tenha toouse ASP.NET ou logs de rastreamento de System. Diagnostics se você quiser tooget streaming do Azure. Olá aplicativo web do Azure serviço de log de streaming transmitirá qualquer *. txt*, *. HTML*, ou *. log* arquivo encontrado na Olá *LogFiles* pasta. Portanto, você pode criar seu próprio sistema de log que grava toohello sistema de arquivos do aplicativo da web de saudação e o arquivo será automaticamente streaming e baixado. Toodo se escrever um código aplicativo que cria arquivos Olá *d:\home\logfiles* pasta.

### <a name="analyzing-web-server-logs"></a>Analisando logs de servidor Web
Para obter mais informações sobre como analisar logs do servidor web, consulte Olá recursos a seguir:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Uma ferramenta para exibir dados em logs de servidor Web (arquivos*.log* ).
* [Solução de problemas de desempenho do IIS ou erros de aplicativo usando o LogParser](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Uma ferramenta de Log Parser Introdução toohello que você pode usar o servidor de web tooanalyze logs.
* [Postagens no blog por Robert McMurray sobre como usar o LogParser](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [Olá, código de status HTTP no IIS 7.0, IIS 7.5 e IIS 8.0](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Analisando logs de rastreamento de solicitação com falha
site do Microsoft TechNet Olá inclui um [usando rastreamento de solicitação falha](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) seção que pode ser útil para entender como toouse esses logs. No entanto, essa documentação se concentra principalmente na configuração do rastreamento de solicitação com falha no IIS, o que você não pode fazer em Aplicativos Web do Azure.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
