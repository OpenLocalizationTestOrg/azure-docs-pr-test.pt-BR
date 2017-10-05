---
title: "Aplicativo multicamadas .NET usando o Barramento de Serviço do Azure | Microsoft Docs"
description: "Um tutorial .NET que ajuda você a desenvolver um aplicativo de várias camadas no Azure que usa filas do barramento de serviço para se comunicar entre camadas."
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
ms.openlocfilehash: 8b502f5ac5d89801d390a872e7a8b06e094ecbba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="d1cf5-103">Aplicativo multicamadas .NET usando filas do Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="d1cf5-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="d1cf5-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="d1cf5-104">Introduction</span></span>
<span data-ttu-id="d1cf5-105">O desenvolvimento para o Microsoft Azure é fácil usando o Visual Studio e o SDK do Azure gratuito para o .NET.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="d1cf5-106">Este tutorial orienta você nas etapas para criar um aplicativo que usa vários recursos do Azure em execução no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="d1cf5-107">Você aprenderá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d1cf5-107">You will learn the following:</span></span>

* <span data-ttu-id="d1cf5-108">Habilitar o computador para o desenvolvimento do Azure com um único download e instalar.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="d1cf5-109">Usar o Visual Studio para desenvolver para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="d1cf5-110">Criar um aplicativo multicamadas no Azure usando funções web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="d1cf5-111">Como comunicar-se entre camadas usando filas do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="d1cf5-112">Neste tutorial você compilará e executará o aplicativo de multicamadas em um serviço de nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="d1cf5-113">O front-end é uma função Web MVC do ASP.NET e o back-end é uma função de trabalho que usa uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="d1cf5-114">Você pode criar o mesmo aplicativo multicamadas com o front-end que o de um projeto Web, que é implantado em um site do Azure em vez de em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="d1cf5-115">Você também pode experimentar o tutorial [Aplicativo .NET híbrido local/na nuvem](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md).</span><span class="sxs-lookup"><span data-stu-id="d1cf5-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="d1cf5-116">A captura de tela a seguir mostra o aplicativo concluído.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="d1cf5-117">Visão geral de cenário: comunicação interfunções</span><span class="sxs-lookup"><span data-stu-id="d1cf5-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="d1cf5-118">Para enviar um pedido para processamento, o componente de UI de front-end, executando a função web, é necessário interagir com a lógica de camada intermediária em execução na função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="d1cf5-119">Este exemplo usa a mensagem do Barramento de Serviço para a comunicação entre as camadas.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="d1cf5-120">Usar a mensagem do Barramento de Serviço entre a Web e as camadas intermediárias separa os dois componentes.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="d1cf5-121">Ao contrário das mensagens diretas (isto é, TCP ou HTTP), a camada da Web não se conecta com a camada intermediária diretamente; em vez disso, envia unidades de trabalho, como mensagens, para o Barramento de Serviço, que mantém confiável até a camada intermediária estar pronta para os consumir e processar.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="d1cf5-122">O Barramento de Serviço fornece duas entidades para dar suporte ao sistema de mensagens agenciado: filas e tópicos.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="d1cf5-123">Com filas, cada mensagem enviada para a fila é consumida por um único destinatário.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="d1cf5-124">Os tópicos dão suporte ao padrão de publicação/assinatura em que cada mensagem publicada é disponibilizada para uma assinatura registrada com o tópico.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="d1cf5-125">Cada assinatura mantém logicamente sua própria fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="d1cf5-126">As assinaturas também podem ser configuradas com as regras de filtro que restringem o conjunto de mensagens passado para a fila de assinatura para aquelas que correspondem ao filtro.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="d1cf5-127">O exemplo a seguir usa filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="d1cf5-128">Esse mecanismo de comunicação oferece diversas vantagens sobre mensagens diretas:</span><span class="sxs-lookup"><span data-stu-id="d1cf5-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="d1cf5-129">**Desacoplamento temporal.**</span><span class="sxs-lookup"><span data-stu-id="d1cf5-129">**Temporal decoupling.**</span></span> <span data-ttu-id="d1cf5-130">Com o padrão de mensagens assíncrono, os produtores e consumidores não precisam estar online ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="d1cf5-131">O ServiceBus armazena de forma confiável as mensagens até que a parte de consumo esteja prontapara recebê-las.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="d1cf5-132">Isso permite que os componentes do aplicativo distribuído sejam desconectados voluntariamente, por exemplo, para manutenção ou devido a uma falha de componente, sem afetar o sistema como um todo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="d1cf5-133">Além disso, o aplicativo de consumo só precisa ser colocado online durante determinadas horas do dia.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="d1cf5-134">**Nivelamento de carga.**</span><span class="sxs-lookup"><span data-stu-id="d1cf5-134">**Load leveling.**</span></span> <span data-ttu-id="d1cf5-135">Em muitos aplicativos, a carga do sistema varia ao longo do tempo enquanto o tempo de processamento necessário para cada unidade de trabalho for normalmente constante.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="d1cf5-136">Intermediar produtores de mensagem e consumidorescom uma fila significa que o aplicativo de consumo (o função de trabalho) sóprecisa ser configurado para acomodar a carga média em vez de pico decarga.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="d1cf5-137">A profundidade da fila aumentará e diminuirá conforme a carga de entrada variar.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="d1cf5-138">Isso economiza dinheiro diretamente em termos da quantidade deinfraestrutura necessária para atender à carga do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="d1cf5-139">**Balanceamento de carga.**</span><span class="sxs-lookup"><span data-stu-id="d1cf5-139">**Load balancing.**</span></span> <span data-ttu-id="d1cf5-140">Conforme a carga aumenta, mais processos de função de trabalho podem seradicionados à leitura da fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="d1cf5-141">Cada mensagem é processada por apenas umdos processos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="d1cf5-142">Além disso, esse balanceamento de carga com base em recepção permite uma utilização ideal das máquinas de trabalho mesmo se as máquinas de trabalho diferem em termos de capacidade de processamento, pois elas irão receber mensagens em sua própria taxa máxima.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="d1cf5-143">Esse padrão geralmente é chamado de padrão de *consumidor concorrente*.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="d1cf5-144">As seções a seguir discutem o código que implementa essa arquitetura.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="d1cf5-145">Configurar o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d1cf5-145">Set up the development environment</span></span>
<span data-ttu-id="d1cf5-146">Antes começar a desenvolver os aplicativos do Azure, obtenha as ferramentas e configure seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="d1cf5-147">Instale o Azure SDK para .NET da [página de downloads](https://azure.microsoft.com/downloads/) do SDK.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d1cf5-148">Na coluna **.NET**, clique na versão do [Visual Studio](http://www.visualstudio.com) que você está usando.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="d1cf5-149">As etapas neste tutorial usam o Visual Studio 2015, mas também funcionam com o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="d1cf5-150">Quando for solicitado a executar ou salvar o instalador, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="d1cf5-151">No **Web Platform Installer**, clique em **Instalar** e prossiga com a instalação.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="d1cf5-152">Quando a instalação estiver concluída, você terá tudo o que é necessário para iniciar o desenvolvimento do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="d1cf5-153">O SDK inclui ferramentas que permitem que você desenvolva facilmente aplicativos do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="d1cf5-154">Criar um namespace</span><span class="sxs-lookup"><span data-stu-id="d1cf5-154">Create a namespace</span></span>
<span data-ttu-id="d1cf5-155">A próxima etapa é para criar um namespace de serviço e obter uma chave de Assinatura de Acesso Compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="d1cf5-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="d1cf5-156">Um namespace fornece um limite de aplicativo para cada aplicativo exposto por meio do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="d1cf5-157">A chave SAS é gerada pelo sistema quando um namespace de serviço é criado.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="d1cf5-158">A combinação do namespace e a chave SAS fornece as credenciais para o Barramento de Serviço autenticar o acesso a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="d1cf5-159">Criar uma função Web</span><span class="sxs-lookup"><span data-stu-id="d1cf5-159">Create a web role</span></span>
<span data-ttu-id="d1cf5-160">Nesta seção, você compila o front-end de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="d1cf5-161">Primeiro, você cria as páginas que seu aplicativo exibe.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="d1cf5-162">Depois, adiciona o código que envia os itens para uma fila do Barramento de Serviço e exibe as informações de status sobre a fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="d1cf5-163">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="d1cf5-163">Create the project</span></span>
1. <span data-ttu-id="d1cf5-164">Usando os privilégios de administrador, inicie o Visual Studio: clique com o botão direito no ícone do programa do **Visual Studio**, em seguida, clique em **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="d1cf5-165">O emulador de computação do Azure, discutido mais adiante neste artigo, exige iniciar o Visual Studio com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="d1cf5-166">No Visual Studio, no menu **Arquivo**, clique em **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="d1cf5-167">Em **Modelos Instalados**, em **Visual C#**, clique em **Nuvem** e em **Serviço de Nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="d1cf5-168">Nomeie o projeto como **AppVáriasCamadas**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="d1cf5-169">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="d1cf5-170">Em funções do **.NET Framework 4.5**, clique duas vezes em **Função Web do ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="d1cf5-171">Focalize **WebRole1** em solução do **Serviço de Nuvem do Azure**, clique no ícone de lápis e renomeie a função web para **FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="d1cf5-172">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-172">Then click **OK**.</span></span> <span data-ttu-id="d1cf5-173">(Certifique-se de inserir "Frontend" com "e" minúsculo, não "FrontEnd".)</span><span class="sxs-lookup"><span data-stu-id="d1cf5-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="d1cf5-174">Na caixa de diálogo **Novo Projeto ASP.NET** na lista **Selecionar um modelo**, clique em **MVC**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="d1cf5-175">Ainda na caixa de diálogo **Novo projeto ASP.NET**, clique no botão **Alterar Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="d1cf5-176">Na caixa de diálogo **Alterar Autenticação**, clique em **Sem Autenticação** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="d1cf5-177">Para este tutorial, você está implantando um aplicativo que não precisa de um logon de usuário.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="d1cf5-178">De novo na caixa de diálogo **Novo Projeto ASP .NET**, clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="d1cf5-179">No **Gerenciador de Soluções**, no projeto **FrontendWebRole**, clique com botão direito do mouse em **Referências** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="d1cf5-180">Clique na guia **Procurar** e procure `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="d1cf5-181">Selecione o pacote **WindowsAzure.ServiceBus**, clique em **Instalar** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="d1cf5-182">Os assemblies de cliente obrigatórios agora são referenciados e alguns arquivos de código novos foram adicionados.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="d1cf5-183">Em **Gerenciador de Soluções**, clique com o botão direito do mouse em **Modelos**, **Adicionar** e **Classe**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="d1cf5-184">Na caixa **Nome**, digite o nome **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="d1cf5-185">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="d1cf5-186">Escreva o código para a função Web</span><span class="sxs-lookup"><span data-stu-id="d1cf5-186">Write the code for your web role</span></span>
<span data-ttu-id="d1cf5-187">Nesta seção, você cria várias páginas que exibem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="d1cf5-188">No arquivo OnlineOrder.cs do Visual Studio, substitua a definição do namespace existente pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="d1cf5-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
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
2. <span data-ttu-id="d1cf5-189">No **Gerenciador de Soluções**, clique duas vezes em **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="d1cf5-190">Adicione as seguintes instruções **using** na parte superior do arquivo para incluir os namespaces do modelo que você acabou de criar, bem como o Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="d1cf5-191">Também no arquivo HomeController.cs do Visual Studio, substitua a definição do namespace existente pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="d1cf5-192">Esse código contém métodos para processar o envio de itens para a fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
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
4. <span data-ttu-id="d1cf5-193">No menu **Compilar**, clique em **Compilar Solução** para testar a precisão de seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="d1cf5-194">Agora, crie a exibição do método `Submit()` criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="d1cf5-195">Clique com o botão direito no método `Submit()` (a sobrecarga de `Submit()` que não usa nenhum parâmetro), em seguida, escolha **Adicionar Exibição**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="d1cf5-196">É exibida uma caixa de diálogo para criar a exibição.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="d1cf5-197">Na lista **Modelo**, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="d1cf5-198">Na lista **Classe do modelo**, clique na classe **OnlineOrder**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="d1cf5-199">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-199">Click **Add**.</span></span>
8. <span data-ttu-id="d1cf5-200">Agora, você alterará o nome exibido de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="d1cf5-201">No **Gerenciador de Soluções**, clique duas vezes no arquivo **Views\Shared\\_Layout.cshtml** para abrir no editor do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="d1cf5-202">Substitua todas as ocorrências de **Meu Aplicativo ASP.NET** para **Produtos da LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="d1cf5-203">Remova os links **Página Inicial**, **Sobre** e **Contato**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="d1cf5-204">Exclua o código destacado:</span><span class="sxs-lookup"><span data-stu-id="d1cf5-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="d1cf5-205">Por fim, modifique a página de envio para incluir algumas informações sobre a fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="d1cf5-206">No **Gerenciador de Soluções**, clique duas vezes no arquivo **Views\Home\Submit.cshtml** para abri-lo no editor do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="d1cf5-207">Adicione a seguinte linha após `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="d1cf5-208">Por enquanto, `ViewBag.MessageCount` está vazio.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="d1cf5-209">Você irá preenchê-lo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="d1cf5-210">Você agora implementou a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-210">You now have implemented your UI.</span></span> <span data-ttu-id="d1cf5-211">Você pode pressionar **F5** para executar o aplicativo e confirmar que parece conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="d1cf5-212">Escreva o código para enviar itens para uma fila do Brramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="d1cf5-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="d1cf5-213">Agora, adicione o código para enviar itens para uma fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="d1cf5-214">Primeiro, você cria uma classe que contém as informações de conexão de fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="d1cf5-215">Em seguida, você inicializa a conexão do Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="d1cf5-216">Por fim, você atualiza o código de envio criado anteriormente em HomeController.cs para efetivamente enviar itens para uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="d1cf5-217">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **FrontendWebRole** (clique com o botão direito no projeto, e não na função).</span><span class="sxs-lookup"><span data-stu-id="d1cf5-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="d1cf5-218">Clique em **Adicionar** e depois em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="d1cf5-219">Nomeie a classe **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="d1cf5-220">Clique em **Adicionar** para criar a classe.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="d1cf5-221">Agora, você adiciona o código que encapsula as informações da conexão e inicializa a conexão em uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="d1cf5-222">Substitua todo o conteúdo de QueueConnector.cs pelo código a seguir e insira valores para `your Service Bus namespace` (nome do namespace) e `yourKey`, que é a **chave primária** obtida anteriormente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
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
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="d1cf5-223">Agora, garanta que o método **Initialize** seja chamado.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="d1cf5-224">No **Gerenciador de Soluções**, clique duas vezes em **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="d1cf5-225">Adicione a linha de código a seguir ao fim do método **Application_Start**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="d1cf5-226">Por fim, atualize o código da Web criado anteriormente, para enviar itens para a fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="d1cf5-227">No **Gerenciador de Soluções**, clique duas vezes em **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="d1cf5-228">Atualize o método `Submit()` (a sobrecarga sem parâmetros) da seguinte maneira para obter a contagem de mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="d1cf5-229">Atualize o método `Submit(OnlineOrder order)` (a sobrecarga com um parâmetro) da seguinte maneira para enviar as informações do pedido para a fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="d1cf5-230">Agora você pode executar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-230">You can now run the application again.</span></span> <span data-ttu-id="d1cf5-231">Cada vez que você enviar umpedido, o número de mensagens aumenta.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="d1cf5-232">Criar a função de trabalho</span><span class="sxs-lookup"><span data-stu-id="d1cf5-232">Create the worker role</span></span>
<span data-ttu-id="d1cf5-233">Agora você criará a função de trabalho que processa o envio de pedidos.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="d1cf5-234">Este exemplo usa o modelo de projeto do Visual Studio **Função de Trabalho com Fila do Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="d1cf5-235">Você já obteve as credenciais necessárias no portal.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="d1cf5-236">Certifique-se de ter conectado o Visual Studio à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="d1cf5-237">No Visual Studio, no **Gerenciador de Soluções**, clique com o botão direito na pasta **Funções** no projeto **AppVáriasCamadas**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="d1cf5-238">Clique em **Adicionar** e clique em **Novo Projeto da Função de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="d1cf5-239">A caixa de diálogo **Adicionar Novo Projeto da Função** é exibida.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="d1cf5-240">Na caixa de diálogo **Adicionar Novo Projeto** de Função, clique em **Função de Trabalho com Fila do Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="d1cf5-241">Na caixa **Nome**, nomeie o projeto **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="d1cf5-242">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-242">Then click **Add**.</span></span>
6. <span data-ttu-id="d1cf5-243">Copie a cadeia de conexão que você obteve na etapa 9 da seção "Criar um namespace do Barramento de Serviço" para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="d1cf5-244">No **Gerenciador de Soluções**, clique com botão direito do mouse em **OrderProcessingRole** criado na etapa 5 (não se esqueça de clicar com o botão direito do mouse em **OrderProcessingRole** em **Funções**, e não na classe).</span><span class="sxs-lookup"><span data-stu-id="d1cf5-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="d1cf5-245">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="d1cf5-246">Na guia **Configurações** da caixa de diálogo **Propriedades**, clique dentro da caixa **Valor** para **Microsoft.ServiceBus.ConnectionString** e cole o valor do ponto de extremidade que você copiou na etapa 6.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="d1cf5-247">Crie uma classe **OnlineOrder** para representar os pedidos conforme você os processa na fila.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="d1cf5-248">Você pode reutilizar uma classe já criada.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="d1cf5-249">No **Gerenciador de Soluções**, clique com o botão direito na classe **OrderProcessingRole** (clique com o botão direito no ícone da classe, não na função).</span><span class="sxs-lookup"><span data-stu-id="d1cf5-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="d1cf5-250">Clique em **Adicionar** e clique em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="d1cf5-251">Navegue até a subpasta para **FrontendWebRole\Models** e clique duas vezes em **OnlineOrder.cs** para adicioná-la a esse projeto.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="d1cf5-252">Em **WorkerRole.cs**, altere o valor da variável **QueueName** de `"ProcessingQueue"` para `"OrdersQueue"`, como mostrado no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="d1cf5-253">Adicione a seguinte instrução using na parte superior do arquivo WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="d1cf5-254">Na função `Run()`, dentro da chamada `OnMessage()`, substitua o conteúdo da cláusula `try` pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="d1cf5-255">Você concluiu o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-255">You have completed the application.</span></span> <span data-ttu-id="d1cf5-256">Você pode testar o aplicativo completo clicando com o botão direito do mouse no projeto AppVáriasCamadas no Gerenciador de Soluções, selecionando **Definir como Projeto de Inicialização** e pressionando F5.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="d1cf5-257">Observe que o número de mensagens não é incrementado porque a função de trabalho processa itens da fila e os marca como concluído.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="d1cf5-258">Você pode ver a saída do rastreamento da função de trabalho, exibindo a interface do usuário do emulador de computação do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="d1cf5-259">É possível fazer isso clicando com o botão direito do mouse no ícone do emulador na área de notificação da sua barra de tarefas e selecionando **Mostrar Interface do Usuário do Emulador de Computação**.</span><span class="sxs-lookup"><span data-stu-id="d1cf5-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="d1cf5-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1cf5-260">Next steps</span></span>
<span data-ttu-id="d1cf5-261">Para obter mais informações sobre o Barramento de Serviço, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="d1cf5-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="d1cf5-262">[Documentação do Barramento de Serviço do Azure][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="d1cf5-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="d1cf5-263">[Página de serviço do Barramento de Serviço][sbacom]</span><span class="sxs-lookup"><span data-stu-id="d1cf5-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="d1cf5-264">[Como usar filas do Barramento de Serviço][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="d1cf5-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="d1cf5-265">Para saber mais sobre os cenários com várias camadas, consulte:</span><span class="sxs-lookup"><span data-stu-id="d1cf5-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="d1cf5-266">[Aplicativo de várias camadas .NET usando tabelas de armazenamento, filas e blobs][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="d1cf5-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

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
