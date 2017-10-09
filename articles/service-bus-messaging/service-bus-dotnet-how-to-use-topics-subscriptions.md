---
title: "aaaGet iniciado com assinaturas e tópicos do barramento de serviço do Azure | Microsoft Docs"
description: "Escreva um aplicativo de console em C# que usa tópicos e assinaturas de mensagens do Barramento de Serviço."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="028ca-103">Introdução aos tópicos do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="028ca-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="028ca-104">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="028ca-104">What will be accomplished</span></span>

<span data-ttu-id="028ca-105">Este tutorial aborda Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="028ca-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="028ca-106">Crie um namespace de barramento de serviço, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="028ca-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="028ca-107">Crie um tópico do barramento de serviço, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="028ca-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="028ca-108">Crie um tópico de toothat de assinatura do barramento de serviço, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="028ca-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="028ca-109">Escreva um toosend do aplicativo de console em um tópico de toohello de mensagem.</span><span class="sxs-lookup"><span data-stu-id="028ca-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="028ca-110">Escreva um tooreceive do aplicativo de console que uma mensagem de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="028ca-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="028ca-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="028ca-111">Prerequisites</span></span>

1. <span data-ttu-id="028ca-112">[Visual Studio 2015 ou superior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="028ca-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="028ca-113">exemplos de saudação neste tutorial usam 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="028ca-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="028ca-114">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="028ca-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="028ca-115">1. Criar um namespace usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="028ca-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="028ca-116">Se você já tiver criado um namespace do sistema de mensagens do barramento de serviço, ir toohello [criar um tópico usando o portal do Azure de saudação](#2-create-a-topic-using-the-azure-portal) seção.</span><span class="sxs-lookup"><span data-stu-id="028ca-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="028ca-117">2. Criar um tópico usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="028ca-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="028ca-118">Faça logon no toohello [portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="028ca-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="028ca-119">No painel de navegação à esquerda de saudação do portal de saudação, clique em **Service Bus** (se você não vir **Service Bus**, clique em **mais serviços**).</span><span class="sxs-lookup"><span data-stu-id="028ca-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="028ca-120">Clique em Olá namespace em que você gostaria que o tópico de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="028ca-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="028ca-121">folha de visão geral do namespace Olá aparece:</span><span class="sxs-lookup"><span data-stu-id="028ca-121">hello namespace overview blade appears:</span></span>
   
    ![Criar um tópico][createtopic1]
4. <span data-ttu-id="028ca-123">Em Olá **namespace de barramento de serviço** folha, clique em **tópicos**, em seguida, clique em **Adicionar tópico**.</span><span class="sxs-lookup"><span data-stu-id="028ca-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Selecionar tópicos][createtopic2]
5. <span data-ttu-id="028ca-125">Insira um nome para o tópico hello e desmarque Olá **ativar particionamento** opção.</span><span class="sxs-lookup"><span data-stu-id="028ca-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="028ca-126">Deixe Olá outras opções com seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="028ca-126">Leave hello other options with their default values.</span></span>
   
    ![Selecionar Nova][createtopic3]
6. <span data-ttu-id="028ca-128">Na parte inferior de saudação da folha de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="028ca-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="028ca-129">3. Criar um tópico de toohello de assinatura</span><span class="sxs-lookup"><span data-stu-id="028ca-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="028ca-130">No painel de recursos de portal hello, clique Olá namespace criado na etapa 1, clique em nome do tópico Olá criado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="028ca-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="028ca-131">Um top de saudação do painel de visão geral do hello, clique hello mais entrar Avançar muito**assinatura** tooadd um tópico de toothis de assinatura.</span><span class="sxs-lookup"><span data-stu-id="028ca-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Criar assinatura][createtopic4]

3. <span data-ttu-id="028ca-133">Insira um nome para a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="028ca-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="028ca-134">Deixe Olá outras opções com seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="028ca-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="028ca-135">4. Enviar tópico toohello de mensagens</span><span class="sxs-lookup"><span data-stu-id="028ca-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="028ca-136">tópico de toohello mensagens toosend, podemos gravar um aplicativo de console c# usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="028ca-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="028ca-137">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="028ca-137">Create a console application</span></span>

<span data-ttu-id="028ca-138">Inicie o Visual Studio e crie um novo projeto de **Aplicativo de console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="028ca-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="028ca-139">Adicionar o pacote do NuGet do barramento de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="028ca-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="028ca-140">Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="028ca-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="028ca-141">Clique em Olá **procurar** guia, procure **barramento de serviço do Microsoft Azure**e, em seguida, selecione Olá **windowsazure. ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="028ca-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="028ca-142">Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="028ca-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Selecionar um pacote NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="028ca-144">Escrever algum código toosend um tópico de toohello de mensagem</span><span class="sxs-lookup"><span data-stu-id="028ca-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="028ca-145">Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="028ca-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="028ca-146">Adicionar Olá toohello de código a seguir `Main` método.</span><span class="sxs-lookup"><span data-stu-id="028ca-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="028ca-147">Saudação de conjunto `connectionString` conexão toohello variável de cadeia de caracteres obtido ao criar namespace hello e definir `topicName` toohello nome que você usou ao criar tópico hello.</span><span class="sxs-lookup"><span data-stu-id="028ca-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="028ca-148">Seu arquivo Program.cs deve ficar assim.</span><span class="sxs-lookup"><span data-stu-id="028ca-148">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="028ca-149">Execute o programa hello e verifique Olá portal do Azure: clique em nome de saudação do seu tópico no namespace Olá **visão geral** folha.</span><span class="sxs-lookup"><span data-stu-id="028ca-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="028ca-150">tópico de saudação **Essentials** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="028ca-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="028ca-151">Olá assinatura (s) listado inferior Olá da folha de hello, observe que Olá **contagem de mensagem** valor para cada assinatura agora deve ser 1.</span><span class="sxs-lookup"><span data-stu-id="028ca-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="028ca-152">Cada vez que você executar o aplicativo de remetente hello sem recuperar mensagens de saudação (conforme descrito na próxima seção, Olá), esse valor aumenta em 1.</span><span class="sxs-lookup"><span data-stu-id="028ca-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="028ca-153">Observe também que tamanho atual da saudação de Olá Olá de incrementos de tópico **atual** valor Olá **Essentials** folha sempre que o aplicativo hello adiciona uma mensagem toohello tópico/assinatura.</span><span class="sxs-lookup"><span data-stu-id="028ca-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Tamanho da mensagem][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="028ca-155">5. Receber mensagens de saudação assinatura</span><span class="sxs-lookup"><span data-stu-id="028ca-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="028ca-156">mensagem de saudação tooreceive ou as mensagens enviadas apenas, criar um novo aplicativo de console e adicionar um pacote de NuGet do barramento de serviço do toohello de referência, aplicativo de remetente anterior toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="028ca-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="028ca-157">Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="028ca-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="028ca-158">Adicionar Olá toohello de código a seguir `Main` método.</span><span class="sxs-lookup"><span data-stu-id="028ca-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="028ca-159">Saudação de conjunto `connectionString` conexão toohello variável de cadeia de caracteres é obtido durante a criação de namespace hello e defina `topicName` toohello nome que você usou ao criar tópico hello.</span><span class="sxs-lookup"><span data-stu-id="028ca-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="028ca-160">O arquivo Program.cs deve ficar assim:</span><span class="sxs-lookup"><span data-stu-id="028ca-160">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="028ca-161">Executar programa hello e verificar novamente o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="028ca-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="028ca-162">Observe que Olá **contagem de mensagem** e **atual** valores agora são 0.</span><span class="sxs-lookup"><span data-stu-id="028ca-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Tamanho do tópico][topic-message-receive]

<span data-ttu-id="028ca-164">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="028ca-164">Congratulations!</span></span> <span data-ttu-id="028ca-165">Agora você criou um tópico e uma assinatura, enviou uma mensagem e recebeu essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="028ca-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="028ca-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="028ca-166">Next steps</span></span>

<span data-ttu-id="028ca-167">Confira nosso [repositório GitHub com exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que demonstram algumas das mais recursos avançados do barramento de serviço de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="028ca-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
