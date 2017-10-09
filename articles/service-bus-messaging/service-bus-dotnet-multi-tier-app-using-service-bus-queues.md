---
title: "aplicativo de várias camadas aaa.NET usando o barramento de serviço do Azure | Microsoft Docs"
description: "Um tutorial do .NET que ajuda você a desenvolver um aplicativo de várias camado no Azure que usa toocommunicate de filas do barramento de serviço entre camadas."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="dadc4-103">Aplicativo multicamadas .NET usando filas do Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="dadc4-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="dadc4-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="dadc4-104">Introduction</span></span>
<span data-ttu-id="dadc4-105">Desenvolvendo para o Microsoft Azure é fácil de usar o Visual Studio e Olá gratuito do Azure SDK para .NET.</span><span class="sxs-lookup"><span data-stu-id="dadc4-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="dadc4-106">Este tutorial orienta Olá etapas toocreate um aplicativo que usa vários recursos do Azure em execução no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="dadc4-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="dadc4-107">Você aprenderá a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="dadc4-107">You will learn hello following:</span></span>

* <span data-ttu-id="dadc4-108">Como tooenable o computador para o desenvolvimento do Azure com um único baixar e instalar.</span><span class="sxs-lookup"><span data-stu-id="dadc4-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="dadc4-109">Como toouse toodevelop de Visual Studio para o Azure.</span><span class="sxs-lookup"><span data-stu-id="dadc4-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="dadc4-110">Como toocreate um aplicativo de várias camado no Azure usando funções web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="dadc4-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="dadc4-111">Como toocommunicate entre camadas usando filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="dadc4-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="dadc4-112">Neste tutorial você compilar e executar o aplicativo de várias camadas hello em um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="dadc4-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="dadc4-113">Olá front-end é uma função web do ASP.NET MVC e back-end Olá é uma função de trabalho que usa uma fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="dadc4-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="dadc4-114">Você pode criar hello mesmo aplicativo de várias camado com o front-end hello como um projeto da web, que é implantado tooan site do Azure, em vez de um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="dadc4-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="dadc4-115">Você também pode testar Olá [aplicativo do .NET no local/em nuvem híbrida](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="dadc4-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="dadc4-116">Olá, captura de tela a seguir mostra aplicativo hello concluída.</span><span class="sxs-lookup"><span data-stu-id="dadc4-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="dadc4-117">Visão geral de cenário: comunicação interfunções</span><span class="sxs-lookup"><span data-stu-id="dadc4-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="dadc4-118">toosubmit um pedido para processamento, o componente da UI front-end que hello, em execução na função de web hello, deve interagir com a lógica de camada intermediária Olá em execução na função de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="dadc4-119">Este exemplo usa o barramento de serviço do sistema de mensagens para comunicação de saudação entre camadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="dadc4-120">Usando o barramento de serviço de mensagens entre camadas intermediários e Olá web separam os dois componentes.</span><span class="sxs-lookup"><span data-stu-id="dadc4-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="dadc4-121">Em contraste toodirect mensagens (ou seja, TCP ou HTTP), Olá camada da web não se conecta camada intermediária toohello diretamente. em vez disso, ele envia unidades de trabalho, como mensagens, para o barramento de serviço, que retém até que seja de camada intermediária Olá tooconsume pronto e processá-los de maneira confiável.</span><span class="sxs-lookup"><span data-stu-id="dadc4-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="dadc4-122">Barramento de serviço fornece dois toosupport orientada de entidades de mensagens: filas e tópicos.</span><span class="sxs-lookup"><span data-stu-id="dadc4-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="dadc4-123">Com as filas, cada mensagem enviada toohello fila é consumida por um único destinatário.</span><span class="sxs-lookup"><span data-stu-id="dadc4-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="dadc4-124">O padrão de publicação/assinatura de saudação em que cada mensagem publicada é feita tooa disponível assinatura registrada com o tópico de saudação os tópicos oferecem suporte.</span><span class="sxs-lookup"><span data-stu-id="dadc4-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="dadc4-125">Cada assinatura mantém logicamente sua própria fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="dadc4-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="dadc4-126">As assinaturas também podem ser configuradas com as regras de filtro que restringem Olá conjunto de mensagens passado para Olá toothose de fila de assinatura que correspondem ao filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="dadc4-127">Olá, exemplo a seguir usa filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="dadc4-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="dadc4-128">Esse mecanismo de comunicação oferece diversas vantagens sobre mensagens diretas:</span><span class="sxs-lookup"><span data-stu-id="dadc4-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="dadc4-129">**Desacoplamento temporal.**</span><span class="sxs-lookup"><span data-stu-id="dadc4-129">**Temporal decoupling.**</span></span> <span data-ttu-id="dadc4-130">Com o padrão de mensagens assíncronas hello, produtores e consumidores não precisam ser online em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="dadc4-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="dadc4-131">Barramento de serviço confiável armazena as mensagens até a parte consumidora hello está pronta para recebê-los.</span><span class="sxs-lookup"><span data-stu-id="dadc4-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="dadc4-132">Isso permite que os componentes de saudação do hello distribuída application toobe desconectados ou voluntariamente, por exemplo, para manutenção, ou devido a falha do componente tooa, sem afetar o sistema como um todo.</span><span class="sxs-lookup"><span data-stu-id="dadc4-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="dadc4-133">Além disso, Olá consumindo o aplicativo pode precisar apenas de toocome online durante determinadas horas do dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="dadc4-134">**Nivelamento de carga.**</span><span class="sxs-lookup"><span data-stu-id="dadc4-134">**Load leveling.**</span></span> <span data-ttu-id="dadc4-135">Em muitos aplicativos, a carga do sistema varia ao longo do tempo, enquanto o tempo de processamento de saudação necessário para cada unidade de trabalho é normalmente constante.</span><span class="sxs-lookup"><span data-stu-id="dadc4-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="dadc4-136">A intermediação dos produtores e consumidores com uma fila significa que Olá consumindo aplicativo (trabalho Olá) somente necessidades toobe provisionado carga média tooaccommodate em vez de picos de carga.</span><span class="sxs-lookup"><span data-stu-id="dadc4-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="dadc4-137">profundidade de saudação da fila de saudação aumenta e diminui conforme a carga de entrada hello varia.</span><span class="sxs-lookup"><span data-stu-id="dadc4-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="dadc4-138">Isso economiza o dinheiro em relação à quantidade de saudação infraestrutura necessária tooservice Olá de carregamento de aplicativo diretamente.</span><span class="sxs-lookup"><span data-stu-id="dadc4-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="dadc4-139">**Balanceamento de carga.**</span><span class="sxs-lookup"><span data-stu-id="dadc4-139">**Load balancing.**</span></span> <span data-ttu-id="dadc4-140">Conforme a carga aumenta, mais processos de trabalho podem ser adicionados tooread da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="dadc4-141">Cada mensagem é processada por apenas um dos processos de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="dadc4-142">Além disso, esse balanceamento de carga baseado em pull permite o uso ideal de máquinas de trabalho Olá mesmo se as máquinas de trabalho diferem em termos de capacidade de processamento, como eles efetuarão pull das mensagens em sua própria velocidade máxima.</span><span class="sxs-lookup"><span data-stu-id="dadc4-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="dadc4-143">Esse padrão é geralmente denominado hello *consumidor concorrente* padrão.</span><span class="sxs-lookup"><span data-stu-id="dadc4-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="dadc4-144">Olá seções a seguir discutem código Olá que implementa essa arquitetura.</span><span class="sxs-lookup"><span data-stu-id="dadc4-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="dadc4-145">Configurar o ambiente de desenvolvimento Olá</span><span class="sxs-lookup"><span data-stu-id="dadc4-145">Set up hello development environment</span></span>
<span data-ttu-id="dadc4-146">Antes de começar a desenvolver aplicativos do Azure, obter ferramentas hello e configurar seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="dadc4-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="dadc4-147">Instalar hello Azure SDK para .NET de saudação SDK [página de downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dadc4-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dadc4-148">Em Olá **.NET** coluna, clique na versão de saudação do [Visual Studio](http://www.visualstudio.com) você está usando.</span><span class="sxs-lookup"><span data-stu-id="dadc4-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="dadc4-149">Olá as etapas deste tutorial usam Visual Studio 2015, mas elas também funcionam com o Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="dadc4-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="dadc4-150">Quando solicitado toorun ou salvar instalador hello, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="dadc4-151">Em Olá **Web Platform Installer**, clique em **instalar** e prosseguir com a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="dadc4-152">Após a conclusão da instalação hello, você terá tudo necessário toostart toodevelop Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dadc4-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="dadc4-153">Olá SDK inclui ferramentas que permitem a fácil desenvolver aplicativos do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dadc4-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="dadc4-154">Criar um namespace</span><span class="sxs-lookup"><span data-stu-id="dadc4-154">Create a namespace</span></span>
<span data-ttu-id="dadc4-155">Olá próxima etapa é toocreate um namespace de serviço e obter uma chave de assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="dadc4-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="dadc4-156">Um namespace fornece um limite de aplicativo para cada aplicativo exposto por meio do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="dadc4-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="dadc4-157">Uma chave SAS é gerada pelo sistema hello quando um namespace é criado.</span><span class="sxs-lookup"><span data-stu-id="dadc4-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="dadc4-158">combinação de saudação do namespace e a chave SAS fornece credenciais de saudação para aplicativo do barramento de serviço tooauthenticate access tooan.</span><span class="sxs-lookup"><span data-stu-id="dadc4-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="dadc4-159">Criar uma função Web</span><span class="sxs-lookup"><span data-stu-id="dadc4-159">Create a web role</span></span>
<span data-ttu-id="dadc4-160">Nesta seção, você deve criar front-end do seu aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="dadc4-161">Primeiro, crie páginas de saudação que exibe seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dadc4-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="dadc4-162">Depois disso, adicione o código que envia a fila do barramento de serviço de tooa de itens e exibe informações de status sobre a fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="dadc4-163">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="dadc4-163">Create hello project</span></span>
1. <span data-ttu-id="dadc4-164">Usando privilégios de administrador, inicie o Visual Studio: Olá atalho **Visual Studio** ícone do programa e, em seguida, clique em **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="dadc4-165">emulador de computação do Azure Hello, discutido posteriormente neste artigo, exige que o Visual Studio seja iniciado com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="dadc4-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="dadc4-166">No Visual Studio, no hello **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="dadc4-167">Em **Modelos Instalados**, em **Visual C#**, clique em **Nuvem** e em **Serviço de Nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="dadc4-168">Projeto de saudação do nome **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="dadc4-169">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="dadc4-170">Em funções do **.NET Framework 4.5**, clique duas vezes em **Função Web do ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="dadc4-171">Passe o mouse sobre **WebRole1** em **solução de serviço de nuvem do Azure**, clique o ícone de lápis hello e renomeie a função da web de saudação muito**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="dadc4-172">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-172">Then click **OK**.</span></span> <span data-ttu-id="dadc4-173">(Certifique-se de inserir "Frontend" com "e" minúsculo, não "FrontEnd".)</span><span class="sxs-lookup"><span data-stu-id="dadc4-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="dadc4-174">De saudação **novo projeto ASP.NET** caixa de diálogo Olá **selecionar um modelo de** lista, clique em **MVC**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="dadc4-175">Ainda no hello **novo projeto ASP.NET** caixa de diálogo, clique em Olá **alterar autenticação** botão.</span><span class="sxs-lookup"><span data-stu-id="dadc4-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="dadc4-176">Em Olá **alterar autenticação** caixa de diálogo, clique em **sem autenticação**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="dadc4-177">Para este tutorial, você está implantando um aplicativo que não precisa de um logon de usuário.</span><span class="sxs-lookup"><span data-stu-id="dadc4-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="dadc4-178">Em Olá **novo projeto ASP.NET** caixa de diálogo, clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="dadc4-179">No **Gerenciador de soluções**, em hello **FrontendWebRole** do projeto, clique no **referências**, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="dadc4-180">Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="dadc4-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="dadc4-181">Selecione Olá **windowsazure. ServiceBus** do pacote, clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="dadc4-182">Observe que Olá necessário assemblies de cliente agora são referenciados e adicionou alguns novos arquivos de código.</span><span class="sxs-lookup"><span data-stu-id="dadc4-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="dadc4-183">Em **Gerenciador de Soluções**, clique com o botão direito do mouse em **Modelos**, **Adicionar** e **Classe**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="dadc4-184">Em Olá **nome** caixa, digite o nome de saudação **Onlineorder**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="dadc4-185">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="dadc4-186">Escrever código Olá para sua função web</span><span class="sxs-lookup"><span data-stu-id="dadc4-186">Write hello code for your web role</span></span>
<span data-ttu-id="dadc4-187">Nesta seção, você criará Olá várias páginas que seu aplicativo é exibido.</span><span class="sxs-lookup"><span data-stu-id="dadc4-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="dadc4-188">No arquivo de Onlineorder Olá no Visual Studio, substitua a definição de namespace existentes Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dadc4-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="dadc4-189">No **Gerenciador de Soluções**, clique duas vezes em **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="dadc4-190">Adicione o seguinte Olá **usando** instruções na parte superior de saudação do hello tooinclude Olá namespaces para o modelo que você acabou de criar, bem como o barramento de serviço de arquivo.</span><span class="sxs-lookup"><span data-stu-id="dadc4-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="dadc4-191">Também no arquivo de HomeController Olá no Visual Studio, substitua a definição de namespace existentes Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="dadc4-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="dadc4-192">Este código contém métodos para manipular o envio de saudação da fila de toohello de itens.</span><span class="sxs-lookup"><span data-stu-id="dadc4-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="dadc4-193">De saudação **criar** menu, clique em **compilar solução** tootest precisão de saudação do seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="dadc4-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="dadc4-194">Agora, crie exibição Olá Olá `Submit()` método que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dadc4-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="dadc4-195">Clique com botão direito em Olá `Submit()` método (sobrecarga de saudação do `Submit()` que não usa nenhum parâmetro) e, em seguida, escolha **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="dadc4-196">Uma caixa de diálogo é exibida para a criação de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="dadc4-197">Em Olá **modelo** , escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="dadc4-198">Em Olá **classe modelo** lista, clique em Olá **OnlineOrder** classe.</span><span class="sxs-lookup"><span data-stu-id="dadc4-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="dadc4-199">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-199">Click **Add**.</span></span>
8. <span data-ttu-id="dadc4-200">Agora, altere o nome de saudação exibida do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dadc4-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="dadc4-201">Em **Gerenciador de soluções**, clique duas vezes o **exibições \ compartilhadas\\cshtml** arquivo tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="dadc4-202">Substitua todas as ocorrências de **Meu Aplicativo ASP.NET** para **Produtos da LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="dadc4-203">Remover Olá **início**, **sobre**, e **contato** links.</span><span class="sxs-lookup"><span data-stu-id="dadc4-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="dadc4-204">Exclua o código de saudação realçado:</span><span class="sxs-lookup"><span data-stu-id="dadc4-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="dadc4-205">Finalmente, modifique algumas informações sobre a fila de Olá Olá tooinclude de página de envio.</span><span class="sxs-lookup"><span data-stu-id="dadc4-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="dadc4-206">Em **Solution Explorer**, clique duas vezes o **Views\Home\Submit.cshtml** arquivo tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="dadc4-207">Olá seguinte linha depois de adicionar `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="dadc4-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="dadc4-208">Por enquanto, Olá `ViewBag.MessageCount` está vazio.</span><span class="sxs-lookup"><span data-stu-id="dadc4-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="dadc4-209">Você irá preenchê-lo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dadc4-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="dadc4-210">Você agora implementou a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="dadc4-210">You now have implemented your UI.</span></span> <span data-ttu-id="dadc4-211">Você pode pressionar **F5** toorun seu aplicativo e confirme que parece conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="dadc4-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="dadc4-212">Escrever código hello para enviar a fila de barramento de serviço tooa itens</span><span class="sxs-lookup"><span data-stu-id="dadc4-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="dadc4-213">Agora, adicione código para enviar itens tooa fila.</span><span class="sxs-lookup"><span data-stu-id="dadc4-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="dadc4-214">Primeiro, você cria uma classe que contém as informações de conexão de fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="dadc4-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="dadc4-215">Em seguida, você inicializa a conexão do Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="dadc4-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="dadc4-216">Por fim, atualize o código de envio de saudação que você criou anteriormente na fila do barramento de serviço do HomeController tooactually enviar itens tooa.</span><span class="sxs-lookup"><span data-stu-id="dadc4-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="dadc4-217">Em **Solution Explorer**, clique com botão direito **FrontendWebRole** (projeto de saudação do botão direito do mouse, não a função de saudação).</span><span class="sxs-lookup"><span data-stu-id="dadc4-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="dadc4-218">Clique em **Adicionar** e depois em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="dadc4-219">Nome de classe Olá **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="dadc4-220">Clique em **adicionar** toocreate classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="dadc4-221">Agora, adicione o código que encapsula as informações de conexão hello e inicializa a fila de barramento de serviço do hello conexão tooa.</span><span class="sxs-lookup"><span data-stu-id="dadc4-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="dadc4-222">Substitua todo o conteúdo de QueueConnector.cs Olá Olá código a seguir e insira valores para `your Service Bus namespace` (seu nome de namespace) e `yourKey`, que é hello **chave primária** obtido anteriormente saudação do Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dadc4-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="dadc4-223">Agora, garanta que o método **Initialize** seja chamado.</span><span class="sxs-lookup"><span data-stu-id="dadc4-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="dadc4-224">No **Gerenciador de Soluções**, clique duas vezes em **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="dadc4-225">Adicionar Olá a seguinte linha de código final Olá Olá **Application_Start** método.</span><span class="sxs-lookup"><span data-stu-id="dadc4-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="dadc4-226">Por fim, atualize o código de web de saudação criado anteriormente, para enviar itens toohello fila.</span><span class="sxs-lookup"><span data-stu-id="dadc4-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="dadc4-227">No **Gerenciador de Soluções**, clique duas vezes em **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="dadc4-228">Saudação de atualização `Submit()` método (sobrecarga de saudação sem parâmetros) da seguinte maneira mensagem de saudação tooget contagem para fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="dadc4-229">Saudação de atualização `Submit(OnlineOrder order)` método (sobrecarga de saudação que usa um parâmetro) da seguinte maneira toosubmit ordem de fila de toohello de informações.</span><span class="sxs-lookup"><span data-stu-id="dadc4-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="dadc4-230">Agora você pode executar o aplicativo hello novamente.</span><span class="sxs-lookup"><span data-stu-id="dadc4-230">You can now run hello application again.</span></span> <span data-ttu-id="dadc4-231">Cada vez que você enviar um pedido, aumenta a contagem de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="dadc4-232">Criar função de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="dadc4-232">Create hello worker role</span></span>
<span data-ttu-id="dadc4-233">Agora você irá criar função de trabalho Olá que processa o envio de pedidos de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="dadc4-234">Este exemplo usa Olá **função de trabalho com fila do barramento de serviço** modelo de projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dadc4-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="dadc4-235">Você já obtido credenciais Olá necessário do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="dadc4-236">Verifique se que você conectou tooyour do Visual Studio conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="dadc4-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="dadc4-237">No Visual Studio, no **Solution Explorer** com o botão direito do **funções** pasta sob Olá **MultiTierApp** projeto.</span><span class="sxs-lookup"><span data-stu-id="dadc4-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="dadc4-238">Clique em **Adicionar** e clique em **Novo Projeto da Função de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="dadc4-239">Olá **adicionar novo projeto de função** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="dadc4-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="dadc4-240">Em Olá **adicionar novo projeto de função** caixa de diálogo, clique em **função de trabalho com fila do barramento de serviço**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="dadc4-241">Em Olá **nome** caixa, projeto de saudação do nome **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="dadc4-242">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-242">Then click **Add**.</span></span>
6. <span data-ttu-id="dadc4-243">Copie a cadeia de caracteres de conexão de saudação que você obteve na etapa 9 da área de transferência do hello "Criar um namespace de barramento de serviço" seção toohello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="dadc4-244">Em **Solution Explorer**, Olá do botão direito do mouse **OrderProcessingRole** criado na etapa 5 (certifique-se de que você clique **OrderProcessingRole** em **Funções**, e não Olá classe).</span><span class="sxs-lookup"><span data-stu-id="dadc4-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="dadc4-245">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="dadc4-246">Em Olá **configurações** guia da saudação **propriedades** caixa de diálogo, clique em Olá **valor** caixa **Microsoft.ServiceBus.ConnectionString**e, em seguida, cole o valor de ponto de extremidade de saudação você copiou na etapa 6.</span><span class="sxs-lookup"><span data-stu-id="dadc4-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="dadc4-247">Criar um **OnlineOrder** toorepresent Olá pedidos de classe como processá-los da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="dadc4-248">Você pode reutilizar uma classe já criada.</span><span class="sxs-lookup"><span data-stu-id="dadc4-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="dadc4-249">No **Solution Explorer**, Olá atalho **OrderProcessingRole** classe (ícone de classe com o botão direito hello, não a função de saudação).</span><span class="sxs-lookup"><span data-stu-id="dadc4-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="dadc4-250">Clique em **Adicionar** e clique em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="dadc4-251">Procure a subpasta toohello para **FrontendWebRole\Models**e, em seguida, clique duas vezes em **Onlineorder** tooadd-toothis projeto.</span><span class="sxs-lookup"><span data-stu-id="dadc4-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="dadc4-252">Em **WorkerRole.cs**, alterar o valor Olá Olá **QueueName** variável do `"ProcessingQueue"` muito`"OrdersQueue"` conforme Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="dadc4-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="dadc4-253">Adicione o seguinte Olá usando a instrução na parte superior de saudação do arquivo WorkerRole.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="dadc4-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="dadc4-254">Em Olá `Run()` função dentro de saudação `OnMessage()` chamar, substitua o conteúdo de saudação do hello `try` cláusula com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="dadc4-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="dadc4-255">Você concluiu o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dadc4-255">You have completed hello application.</span></span> <span data-ttu-id="dadc4-256">Você pode testar o aplicativo completo hello clicando com o projeto de MultiTierApp Olá no Gerenciador de soluções, selecionando **definir como projeto de inicialização**e, em seguida, pressionando F5.</span><span class="sxs-lookup"><span data-stu-id="dadc4-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="dadc4-257">Observe que a contagem de mensagens não aumenta, porque a função de trabalho Olá processa os itens da fila de saudação e as marca como concluída.</span><span class="sxs-lookup"><span data-stu-id="dadc4-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="dadc4-258">Você pode ver a saída do rastreamento Olá sua função de trabalho exibindo Olá interface do usuário de emulador de computação do Azure.</span><span class="sxs-lookup"><span data-stu-id="dadc4-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="dadc4-259">Você pode fazer isso clicando duas vezes o ícone do emulador Olá na área de notificação de saudação da barra de tarefas e selecionando **Mostrar UI do emulador de computação**.</span><span class="sxs-lookup"><span data-stu-id="dadc4-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="dadc4-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dadc4-260">Next steps</span></span>
<span data-ttu-id="dadc4-261">toolearn mais sobre o barramento de serviço, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dadc4-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="dadc4-262">[Documentação do Barramento de Serviço do Azure][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="dadc4-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="dadc4-263">[Página de serviço do Barramento de Serviço][sbacom]</span><span class="sxs-lookup"><span data-stu-id="dadc4-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="dadc4-264">[Como tooUse filas do barramento de serviço][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="dadc4-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="dadc4-265">toolearn mais informações sobre cenários de várias camados, consulte:</span><span class="sxs-lookup"><span data-stu-id="dadc4-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="dadc4-266">[Aplicativo de várias camadas .NET usando tabelas de armazenamento, filas e blobs][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="dadc4-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
