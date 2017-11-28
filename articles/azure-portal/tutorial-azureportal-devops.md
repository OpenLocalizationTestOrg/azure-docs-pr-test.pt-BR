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
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="07c51-103">Tutorial: DevOps com hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07c51-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="07c51-104">Olá plataforma Windows Azure está cheio de fluxos de trabalho flexíveis DevOps.</span><span class="sxs-lookup"><span data-stu-id="07c51-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="07c51-105">Neste tutorial, você aprenderá como recursos de saudação tooleverage de saudação toodevelop do Portal do Azure, testar, implantar, solucionar problemas, monitorar e gerenciar aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="07c51-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="07c51-106">Este tutorial se concentra nos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="07c51-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="07c51-107">Criar um aplicativo Web e habilitar a implantação contínua</span><span class="sxs-lookup"><span data-stu-id="07c51-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="07c51-108">Desenvolver e testar aplicativos</span><span class="sxs-lookup"><span data-stu-id="07c51-108">Develop and test an app</span></span>
3. <span data-ttu-id="07c51-109">Monitorar e solucionar problemas de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="07c51-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="07c51-110">Tarefas de gerenciamento de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="07c51-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="07c51-111">Criar um aplicativo Web e habilitar a implantação contínua</span><span class="sxs-lookup"><span data-stu-id="07c51-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="07c51-112">Criar um aplicativo Web com [do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/), que você usará no restante deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="07c51-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="07c51-113">Inicialmente, você habilitará a implantação contínua de seu repositório de código fonte em nosso ambiente do Azure em execução.</span><span class="sxs-lookup"><span data-stu-id="07c51-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="07c51-114">Olá de logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07c51-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="07c51-115">Escolha **serviços de aplicativos** &gt; **ícone Adicionar** e insira um nome, escolha sua assinatura e criar um novo tooserve de grupo de recursos como contêiner Olá para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="07c51-116">Grupos de recursos permitem que você toomanage vários aspectos da solução hello como cobrança, implantações e monitoramento como um único grupo por meio de [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07c51-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="07c51-118">Após alguns instantes, o serviço de aplicativo será criado.</span><span class="sxs-lookup"><span data-stu-id="07c51-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="07c51-119">Levar Olá de tooexplore alguns minutos várias opções de menu para serviço Olá no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="07c51-121">Clique em URL hello.</span><span class="sxs-lookup"><span data-stu-id="07c51-121">Click hello URL.</span></span> <span data-ttu-id="07c51-122">Observe a variedade de saudação de opções disponíveis para ferramentas e repositórios.</span><span class="sxs-lookup"><span data-stu-id="07c51-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="07c51-123">Você também pode usar idiomas de saudação e estruturas de sua escolha, incluindo .NET, Java e Ruby.</span><span class="sxs-lookup"><span data-stu-id="07c51-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="07c51-125">Olá portal do Azure facilita a implantação contínua um processo simples que envolve apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="07c51-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="07c51-126">No Olá portal do Azure, escolha as configurações de ícone Olá para serviço de aplicativo hello que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="07c51-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="07c51-128">Na folha de saudação que é aberto no saudação à direita, role toohello seção de publicação.</span><span class="sxs-lookup"><span data-stu-id="07c51-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="07c51-130">Em seguida, configure alguns implantação contínua de tooenable configurações para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="07c51-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="07c51-131">Clique em Origem da Implantação e depois em Escolher Origem.</span><span class="sxs-lookup"><span data-stu-id="07c51-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="07c51-132">Observe a variedade de saudação de opções que disponíveis para fontes de repositório.</span><span class="sxs-lookup"><span data-stu-id="07c51-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="07c51-134">Para este exemplo, escolha GitHub.</span><span class="sxs-lookup"><span data-stu-id="07c51-134">For this example choose GitHub.</span></span> <span data-ttu-id="07c51-135">Opcionalmente escolher Olá repositório de sua escolha e credenciais de autorização de saudação de instalação.</span><span class="sxs-lookup"><span data-stu-id="07c51-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="07c51-137">Depois de repositório de tooyour de autorização, você pode escolher um projeto e desejar toodeploy de ramificação.</span><span class="sxs-lookup"><span data-stu-id="07c51-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="07c51-138">Confira vários exemplos fictícios abaixo.</span><span class="sxs-lookup"><span data-stu-id="07c51-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="07c51-140">Depois de escolher o projeto e a ramificação, clique em ok.</span><span class="sxs-lookup"><span data-stu-id="07c51-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="07c51-141">Você deve iniciar toosee notificações de uma implantação.</span><span class="sxs-lookup"><span data-stu-id="07c51-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="07c51-143">Navegue tooGitHub back toosee Olá webhook que foi criado o repositório de controle de origem toointegrate Olá com o Azure.</span><span class="sxs-lookup"><span data-stu-id="07c51-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="07c51-144">Olá Portal do Azure permite a integração com GitHub com apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="07c51-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="07c51-146">implantação contínua de toodemonstrate, adicionar rapidamente alguns repositório toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="07c51-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="07c51-147">Para obter um exemplo simple, adicione um repositório GitHub do exemplo texto arquivo tooa.</span><span class="sxs-lookup"><span data-stu-id="07c51-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="07c51-148">Você está livre toouse .NET, Ruby, Python ou algum outro tipo de aplicativo com o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="07c51-149">Sinta-se livre tooadd um arquivo de texto, repositório de toohello aplicativo ASP.NET MVC, Java e Ruby de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="07c51-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="07c51-151">Após a confirmação de repositório de tooyour alterações, você verá um novo iniciar a implantação na área de notificações do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="07c51-152">Se você não ver rapidamente as alterações após a confirmação tooyour repositório, clique em sincronizar.</span><span class="sxs-lookup"><span data-stu-id="07c51-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="07c51-154">Neste ponto, se você tentar e carrega a página Olá para o serviço de aplicativo hello, você receberá um erro 403.</span><span class="sxs-lookup"><span data-stu-id="07c51-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="07c51-155">Neste exemplo, é porque não há nenhuma configuração de documento padrão típica para página hello como um arquivo como index. htm ou default.</span><span class="sxs-lookup"><span data-stu-id="07c51-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="07c51-156">Você pode corrigir isso rapidamente com hello ferramentas no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07c51-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="07c51-157">No hello Portal do Azure, escolha configurações &gt; as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="07c51-159">Uma folha será aberta para as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-159">A blade opens for application settings.</span></span> <span data-ttu-id="07c51-160">Insira nome de saudação da página hello "SamplePage.html" e clique em Salvar.</span><span class="sxs-lookup"><span data-stu-id="07c51-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="07c51-161">Levar outras configurações de saudação de tooexplore alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="07c51-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![Imagem14][image14]
15. <span data-ttu-id="07c51-163">Opcionalmente, atualize seu tooensure de URL do navegador você verá as alterações de saudação esperada.</span><span class="sxs-lookup"><span data-stu-id="07c51-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="07c51-164">Nesse caso, há algum texto simple agora preencher a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="07c51-165">Cada repositório de toohello alteração adicional resulta em uma nova implantação automática.</span><span class="sxs-lookup"><span data-stu-id="07c51-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![Imagem15][image15]
    
    <span data-ttu-id="07c51-167">Habilitar implantação contínua com hello Portal do Azure é uma experiência de fácil.</span><span class="sxs-lookup"><span data-stu-id="07c51-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="07c51-168">Você também pode criar pipelines de lançamento mais complexas e usar muitas outras técnicas com controle de origem existente e tooAzure de toodeploy de sistemas de integração contínua, como aproveitar compilação automatizada e sistemas de gerenciamento de versão.</span><span class="sxs-lookup"><span data-stu-id="07c51-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="07c51-169">Desenvolver e testar aplicativos</span><span class="sxs-lookup"><span data-stu-id="07c51-169">Develop and test an app</span></span>
<span data-ttu-id="07c51-170">Em seguida, fazer algumas alterações toohello código base e implantar rapidamente essas alterações.</span><span class="sxs-lookup"><span data-stu-id="07c51-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="07c51-171">Você também irá configurar alguns testes para o aplicativo Web de saudação de desempenho.</span><span class="sxs-lookup"><span data-stu-id="07c51-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="07c51-172">No hello Portal do Azure escolher os serviços de aplicativo hello no painel de navegação e localize seu serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![Imagem16][image16]
2. <span data-ttu-id="07c51-174">Clique em Ferramentas</span><span class="sxs-lookup"><span data-stu-id="07c51-174">Click Tools</span></span>
   
   ![Imagem17][image17]
3. <span data-ttu-id="07c51-176">Observe o hello categoria em ferramentas de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="07c51-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="07c51-177">Há várias ferramentas úteis aqui que nos permitem toowork com aplicativos sem deixar Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07c51-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="07c51-178">Clique em Console.</span><span class="sxs-lookup"><span data-stu-id="07c51-178">Click on Console.</span></span>
   
   ![Imagem18][image18]
4. <span data-ttu-id="07c51-180">Na janela de console hello, você pode emitir comandos ao vivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="07c51-181">Digite o comando do hello dir e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="07c51-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="07c51-182">Observe que os comandos que exigem privilégios elevados não funcionam.</span><span class="sxs-lookup"><span data-stu-id="07c51-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![Imagem19][image19]
5. <span data-ttu-id="07c51-184">Voltar toohello desenvolver categoria e escolha Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="07c51-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="07c51-185">Observação: o Visual Studio Online agora se chama Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="07c51-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![Imagem20][image20]
6. <span data-ttu-id="07c51-187">Alternar a experiência de edição no navegador Olá para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![Imagem21][image21]
7. <span data-ttu-id="07c51-189">Uma extensão da Web é instalada para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-189">A web extension installs for your app.</span></span> <span data-ttu-id="07c51-190">Extensões de forma rápida e fácil adicionam funcionalidade tooapps no Azure.</span><span class="sxs-lookup"><span data-stu-id="07c51-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="07c51-191">Observe algumas Olá outros tipos de extensão disponíveis na captura de tela de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="07c51-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![Imagem22][image22]
8. <span data-ttu-id="07c51-193">Quando instala o hello extensão do Visual Studio Online, clique em Ir.</span><span class="sxs-lookup"><span data-stu-id="07c51-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![Imagem23][image23]
9. <span data-ttu-id="07c51-195">Um navegador guia abre onde você pode ver um IDE de desenvolvimento diretamente no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="07c51-196">Experiência de saudação do aviso abaixo é no Chrome.</span><span class="sxs-lookup"><span data-stu-id="07c51-196">Notice hello experience below is in Chrome.</span></span>
   
   ![Imagem24][image24]
10. <span data-ttu-id="07c51-198">Você pode executar várias atividades, como editar arquivos, adicionar arquivos e pastas e baixar conteúdo de site dinâmico Olá.</span><span class="sxs-lookup"><span data-stu-id="07c51-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="07c51-199">Verifique o arquivo de SamplePage.html de toohello edição rápida.</span><span class="sxs-lookup"><span data-stu-id="07c51-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![Imagem25][image25]
11. <span data-ttu-id="07c51-201">Em alguns instantes, Olá alterações são salvas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07c51-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="07c51-202">Se você navegar toohello back página, você pode ver as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="07c51-203">Lembre-se de que edições ao vivo como essas provavelmente não são adequadas para ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="07c51-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="07c51-204">No entanto, ferramentas Olá é muito fácil toomake alterações para desenvolvimento e ambientes de teste.</span><span class="sxs-lookup"><span data-stu-id="07c51-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![Imagem26][image26]
    
    ![Imagem27][image27]
12. <span data-ttu-id="07c51-207">Voltar a folha de ferramentas toohello e na categoria de desenvolver Olá, clique no teste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="07c51-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![Imagem28][image28]
13. <span data-ttu-id="07c51-209">É necessário tooset uma conta do team services.</span><span class="sxs-lookup"><span data-stu-id="07c51-209">You need tooset a team services account.</span></span> <span data-ttu-id="07c51-210">Confira aqui mais detalhes: [Criar uma conta do Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="07c51-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="07c51-211">Clique em novo toocreate um teste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="07c51-211">Click on New toocreate a performance test.</span></span>
    
    ![Imagem29][image29]
    
    <span data-ttu-id="07c51-213">Configurar Olá vários valores e clique em Executar teste final Olá Olá caixa de diálogo tooinitiate um teste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="07c51-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![Imagem30][image30]
    
    ![Imagem31][image31]
15. <span data-ttu-id="07c51-216">Depois que o teste de saudação inicia a execução, você pode monitorar o estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![Imagem32][image32]
    
    <span data-ttu-id="07c51-218">Quando termina de teste hello, clicando no resultado de saudação mostra mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="07c51-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![Imagem33][image33]
16. <span data-ttu-id="07c51-220">Neste exemplo, você criou um pequeno teste executado, portanto, há tooanalyze de dados limitada, mas você pode ver várias métricas bem como executar novamente o teste da exibição.</span><span class="sxs-lookup"><span data-stu-id="07c51-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="07c51-221">Olá Portal do Azure torna criar, executar e analisar testes de desempenho web um processo fácil.</span><span class="sxs-lookup"><span data-stu-id="07c51-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="07c51-222">Olá capturas de tela abaixo exibem dados de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-222">hello screenshots below display hello performance data.</span></span>
    
    ![Imagem34][image34]
    
    ![Imagem35][image35]
    
    ![Imagem36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="07c51-226">Monitorar e solucionar problemas de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="07c51-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="07c51-227">O Azure oferece muitos recursos de monitoramento e solução de problemas de aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="07c51-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="07c51-228">Escolha Ferramentas Olá Portal do Azure para o nosso aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="07c51-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![Imagem37][image37]
2. <span data-ttu-id="07c51-230">Em categoria de solução de problemas do hello, observe Olá várias opções para o uso de possíveis problemas de ferramentas de tootroubleshoot com um aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="07c51-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="07c51-231">Você pode fazer coisas como monitorar o tráfego Live HTTP, habilitar a autorrecuperação, exibir view e muito mais.</span><span class="sxs-lookup"><span data-stu-id="07c51-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![Imagem38][image38]
3. <span data-ttu-id="07c51-233">Escolha métricas do Site tooquickly obter uma exibição de alguns códigos de HTTP.</span><span class="sxs-lookup"><span data-stu-id="07c51-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![Imagem39][image39]
4. <span data-ttu-id="07c51-235">Escolha Diagnóstico como Serviço.</span><span class="sxs-lookup"><span data-stu-id="07c51-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="07c51-236">Escolha o tipo de aplicativo e depois Executar.</span><span class="sxs-lookup"><span data-stu-id="07c51-236">Choose your application type, then choose Run.</span></span>
   
   ![Imagem40][image40]
   
   <span data-ttu-id="07c51-238">Começa a coleta.</span><span class="sxs-lookup"><span data-stu-id="07c51-238">A collection begins.</span></span>
   
   ![Imagem41][image41]
5. <span data-ttu-id="07c51-240">Você pode escolher problemas potenciais do toodiagnose Olá log apropriado.</span><span class="sxs-lookup"><span data-stu-id="07c51-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="07c51-241">Você precisa de tooenable toosee de registro em log todos os dados disponíveis Olá opções como Logs de HTTP.</span><span class="sxs-lookup"><span data-stu-id="07c51-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![Imagem42][image42]
   
   <span data-ttu-id="07c51-243">Clicando no arquivo de despejo de memória Olá você pode baixar e analisar um DebugDiag toohelp do relatório de análise encontrar problemas potenciais.</span><span class="sxs-lookup"><span data-stu-id="07c51-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![Imagem43][image43]
6. <span data-ttu-id="07c51-245">tooview mais dados, você precisa tooenable adicionais de log.</span><span class="sxs-lookup"><span data-stu-id="07c51-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="07c51-246">No hello Portal do Azure, navegue toohello Web app e escolha as configurações.</span><span class="sxs-lookup"><span data-stu-id="07c51-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![Imagem44][image44]
7. <span data-ttu-id="07c51-248">Role para baixo de categoria de recursos toohello e escolha os logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="07c51-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![Imagem45][image45]
8. <span data-ttu-id="07c51-250">Observe Olá várias opções para registro em log.</span><span class="sxs-lookup"><span data-stu-id="07c51-250">Notice hello various options for logging.</span></span> <span data-ttu-id="07c51-251">Ative o registro em log do servidor Web e clique em Salvar.</span><span class="sxs-lookup"><span data-stu-id="07c51-251">Toggle on Web server logging and click save.</span></span>
   
   ![Imagem46][image46]
9. <span data-ttu-id="07c51-253">Voltar à área de ferramentas toohello para o aplicativo hello e escolha diagnóstico como um serviço e clique em executar toorerun Olá a coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="07c51-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![Imagem47][image47]
10. <span data-ttu-id="07c51-255">Com a configuração de registro em log Olá HTTP ativada, você verá os dados coletados para Logs de HTTP.</span><span class="sxs-lookup"><span data-stu-id="07c51-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![Imagem48][image48]
11. <span data-ttu-id="07c51-257">Ao clicar em log do arquivo hello HTML, você produzir um relatório de baseado em navegador avançado para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="07c51-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![Imagem49][image49]
12. <span data-ttu-id="07c51-259">Volta toohello seção ferramentas Olá Portal do Azure para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="07c51-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="07c51-260">Rolar toohello seção de ferramentas e escolha o Explorador de processos.</span><span class="sxs-lookup"><span data-stu-id="07c51-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![Imagem50][image50]
13. <span data-ttu-id="07c51-262">Ao escolher Gerenciador de Processos, é possível exibir detalhes sobre os processos em execução.</span><span class="sxs-lookup"><span data-stu-id="07c51-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="07c51-263">Aviso abaixo, você pode detalhar processos e até mesmo interromper processos todos do hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07c51-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![Imagem51][image51]
    
    ![Imagem52][image52]
14. <span data-ttu-id="07c51-266">Mova folha de configurações toohello Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="07c51-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="07c51-267">Clique em Nova solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="07c51-267">Click New support request.</span></span>
    
    ![Imagem53][image53]
15. <span data-ttu-id="07c51-269">Na folha de saudação em saudação à direita, preencha os detalhes sobre problemas de hello, insira informações de contato e até mesmo, carregar dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="07c51-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="07c51-270">Olá Portal do Azure permite trabalhar com o suporte da Microsoft uma experiência perfeita.</span><span class="sxs-lookup"><span data-stu-id="07c51-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![Imagem54][image54]
    
    ![Imagem55][image55]
    
    <span data-ttu-id="07c51-273">Olá Portal do Azure ajuda a fornecer poderoso e familiar ferramentas experiências toohelp monitor e solucionar problemas de nossos aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="07c51-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="07c51-274">Também é possível tootake ação rapidamente, executando tarefas como a reciclagem de processos, habilitar e desabilitar vários conjuntos de dados e até mesmo integrar com o suporte da Microsoft professional.</span><span class="sxs-lookup"><span data-stu-id="07c51-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="07c51-275">Gerenciamento geral de aplicativos</span><span class="sxs-lookup"><span data-stu-id="07c51-275">General Application Management</span></span>
<span data-ttu-id="07c51-276">Quando o gerenciamento de aplicativos, muitas vezes é preciso tooperform uma ampla variedade de atividades, como configurar estratégias de backup, implementar e gerenciar provedores de identidade e configurando o controle de acesso baseado em função.</span><span class="sxs-lookup"><span data-stu-id="07c51-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="07c51-277">Como com hello outras experiências DevOps, Olá plataforma Windows Azure integra essas tarefas diretamente no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="07c51-278">tooensure esteja mantendo Olá aplicativo Web protegido contra perda de dados é necessário tooconfigure backups.</span><span class="sxs-lookup"><span data-stu-id="07c51-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="07c51-279">Navegue toohello área de configurações para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="07c51-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![Imagem56][image56]
2. <span data-ttu-id="07c51-281">Na folha de saudação em saudação à direita, role para baixo toohello categoria de recursos.</span><span class="sxs-lookup"><span data-stu-id="07c51-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![Imagem57][image57]
3. <span data-ttu-id="07c51-283">Escolha os Backups; uma folha é aberta no saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="07c51-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![Imagem58][image58]
4. <span data-ttu-id="07c51-285">Clique em configurar, escolha uma conta de armazenamento na folha de saudação no saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="07c51-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![Imagem59][image59]
5. <span data-ttu-id="07c51-287">Agora crie e escolha um toohold de contêiner de armazenamento dos backups.</span><span class="sxs-lookup"><span data-stu-id="07c51-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="07c51-288">Clique em criar na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="07c51-289">Em seguida, selecione o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-289">Then select hello container.</span></span>
   
   ![Imagem60][image60]
6. <span data-ttu-id="07c51-291">Depois de ter escolhido o contêiner hello, você pode configurar agendamentos, bem como os backups de configuração para bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="07c51-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="07c51-292">Para este cenário, clique em Olá salvar ícone.</span><span class="sxs-lookup"><span data-stu-id="07c51-292">For this scenario, click hello save icon.</span></span>
   
    ![Imagem61][image61]
7. <span data-ttu-id="07c51-294">Depois de salvar, role folha toohello back Olá esquerda para Backups.</span><span class="sxs-lookup"><span data-stu-id="07c51-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="07c51-295">Clique em aplicativo de hello tooback Backup agora.</span><span class="sxs-lookup"><span data-stu-id="07c51-295">Click Backup Now tooback hello application.</span></span>
   
    ![Imagem62][image62]
8. <span data-ttu-id="07c51-297">Em poucos instantes, verá um backup criado.</span><span class="sxs-lookup"><span data-stu-id="07c51-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="07c51-298">Saudação de aviso Restaurar agora a opção de saudação captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="07c51-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![Imagem63][image63]
9. <span data-ttu-id="07c51-300">Clique em Restaurar agora e examine a folha de toohello Olá opções em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="07c51-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="07c51-301">Você pode escolher que um backup apropriado e fácil restauração tooan anteriormente estado conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="07c51-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="07c51-302">Olá portal do Azure nos ajudou a habilitar facilmente uma estratégia de recuperação de desastres simples para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="07c51-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![Imagem64][image64]
10. <span data-ttu-id="07c51-304">Mover de folha de configurações toohello Olá esquerda e, em recursos e escolher a autenticação/autorização.</span><span class="sxs-lookup"><span data-stu-id="07c51-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![Imagem65][image65]
11. <span data-ttu-id="07c51-306">Na folha de saudação em Olá direita escolha autenticação do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07c51-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="07c51-307">Observe a variedade de saudação das opções que você pode configurar com provedores populares.</span><span class="sxs-lookup"><span data-stu-id="07c51-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![Imagem66][image66]
12. <span data-ttu-id="07c51-309">Escolha provedor Olá de sua escolha e observe Olá opções para escopo de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="07c51-310">Você pode fornecer uma ID do aplicativo e o segredo do aplicativo e habilitar a autenticação do Facebook para o aplicativo hello rapidamente.</span><span class="sxs-lookup"><span data-stu-id="07c51-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="07c51-311">Olá Portal do Azure permite a autenticação como uma solução completa para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07c51-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![Imagem67][image67]
13. <span data-ttu-id="07c51-313">Voltar toohello folha de configurações e escolha os usuários na categoria de gerenciamento de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="07c51-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![Imagem68][image68]
14. <span data-ttu-id="07c51-315">Na folha de saudação em Olá direita examinar Olá várias opções para adicionar funções e usuários.</span><span class="sxs-lookup"><span data-stu-id="07c51-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="07c51-316">Olá Portal do Azure lhe permite controlar facilmente RBAC (controle de acesso baseado em função) para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="07c51-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![Imagem69][image69]

## <a name="summary"></a><span data-ttu-id="07c51-318">Resumo</span><span class="sxs-lookup"><span data-stu-id="07c51-318">Summary</span></span>
<span data-ttu-id="07c51-319">Este tutorial demonstrado alguns energia Olá com hello plataforma Windows Azure rapidamente a implantação contínua para um aplicativo web, realizam o desenvolvimento de vários e as atividades de teste, monitorando e Solucionando problemas de um aplicativo em tempo real e finalmente gerenciar chave estratégias, como recuperação de desastres, identidade e controle de acesso baseado em função.</span><span class="sxs-lookup"><span data-stu-id="07c51-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="07c51-320">Olá plataforma Windows Azure permite uma experiência integrada para esses fluxos de trabalho de DevOps e você pode trabalhar com eficiência permanecendo no contexto para a tarefa de saudação em questão.</span><span class="sxs-lookup"><span data-stu-id="07c51-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07c51-321">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07c51-321">Next steps</span></span>
* <span data-ttu-id="07c51-322">Gerenciador de recursos do Azure é importante para habilitar DevOps Olá plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="07c51-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="07c51-323">toolearn mais visitar [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07c51-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="07c51-324">toolearn mais sobre a implantação do serviço de aplicativo do Azure, visite [implantar tooAzure seu aplicativo do serviço de aplicativo](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="07c51-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
