---
title: "tutorial de retransmissão do WCF do Service Bus aaaAzure | Microsoft Docs"
description: "Compilar um serviço e um aplicativo cliente do Barramento de Serviço usando a Retransmissão WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="b4e3b-103">Tutorial de Retransmissão de WCF do Azure</span><span class="sxs-lookup"><span data-stu-id="b4e3b-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="b4e3b-104">Este tutorial descreve como toobuild um simple WCF retransmissão aplicativo cliente e o serviço de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="b4e3b-105">Para obter um tutorial semelhante que usa o [Sistema de Mensagens do Barramento de Serviço](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte a [Introdução às filas do Barramento de Serviço](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="b4e3b-106">Trabalhando com este tutorial fornece uma compreensão das etapas Olá toocreate necessário um aplicativo de cliente e o serviço de retransmissão do WCF.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="b4e3b-107">Assim como suas contrapartes WCF originais, um serviço é um constructo que expõe um ou mais pontos de extremidade, cada um dos quais expõe uma ou mais operações de serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="b4e3b-108">ponto de extremidade de saudação de um serviço Especifica um endereço onde o serviço Olá pode ser encontrado, uma associação que contém informações de saudação que um cliente deve se comunicar com o serviço de Olá e um contrato que define Olá funcionalidade fornecida por Olá serviço tooits clientes.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="b4e3b-109">Olá principal diferença entre o WCF e a retransmissão do WCF é que esse ponto de extremidade de saudação é exposto na nuvem de saudação em vez de localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="b4e3b-110">Depois de você trabalhar com sequência de saudação de tópicos neste tutorial, você terá um serviço em execução e um cliente pode invocar operações de saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="b4e3b-111">Olá primeiro tópico descreve como tooset uma conta.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="b4e3b-112">as próximas etapas Olá descrevem como toodefine um serviço que usa um contrato, como tooimplement Olá serviço e como tooconfigure Olá serviço em código.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="b4e3b-113">Eles também descrevem como serviço de saudação toohost e execução.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="b4e3b-114">Olá serviço que é criado é auto-hospedado e Olá cliente e serviço executado em Olá mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="b4e3b-115">Você pode configurar o serviço de saudação usando código ou um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="b4e3b-116">etapas de três finais Olá descrevem como toocreate um aplicativo cliente, configurar o aplicativo de cliente hello e criar e usar um cliente que pode acessar a funcionalidade de saudação do host de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4e3b-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b4e3b-117">Prerequisites</span></span>

<span data-ttu-id="b4e3b-118">toocomplete neste tutorial, você precisará Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="b4e3b-119">[Microsoft Visual Studio 2015 ou superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="b4e3b-120">Este tutorial usa o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="b4e3b-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-121">An active Azure account.</span></span> <span data-ttu-id="b4e3b-122">Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="b4e3b-123">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="b4e3b-124">Criar um namespace de serviço</span><span class="sxs-lookup"><span data-stu-id="b4e3b-124">Create a service namespace</span></span>

<span data-ttu-id="b4e3b-125">Olá primeira etapa é toocreate um namespace e tooobtain um [assinatura de acesso compartilhado (SAS)](../service-bus-messaging/service-bus-sas.md) chave.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="b4e3b-126">Um namespace fornece um limite de aplicativo para cada aplicativo exposto por meio do serviço de retransmissão hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="b4e3b-127">Uma chave SAS é gerada automaticamente pelo sistema hello quando um namespace de serviço é criado.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="b4e3b-128">combinação de saudação do namespace de serviço e a chave SAS fornece credenciais de saudação para aplicativo do Azure tooauthenticate access tooan.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="b4e3b-129">Siga Olá [as instruções aqui](relay-create-namespace-portal.md) toocreate um namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="b4e3b-130">Definir um contrato de serviço do WCF</span><span class="sxs-lookup"><span data-stu-id="b4e3b-130">Define a WCF service contract</span></span>

<span data-ttu-id="b4e3b-131">contrato de serviço Olá Especifica que o serviço de saudação de operações (Olá terminologia do serviço web para funções ou métodos) dá suporte.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="b4e3b-132">Os contratos são criados pela definição de uma interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="b4e3b-133">Cada método na interface de saudação corresponde tooa operação de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="b4e3b-134">Cada interface deve ter Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo aplicado tooit e cada operação deve ter Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit atributo aplicado.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="b4e3b-135">Se um método em uma interface que tem Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo não tem Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) de atributo, que o método não é exposto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="b4e3b-136">código de saudação para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="b4e3b-137">Para obter uma discussão maior de contratos e serviços, consulte [Projetando e Implementando serviços](https://msdn.microsoft.com/library/ms729746.aspx) em Olá documentação do WCF.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="b4e3b-138">Criar um contrato de retransmissão com uma interface</span><span class="sxs-lookup"><span data-stu-id="b4e3b-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="b4e3b-139">Abra o Visual Studio como administrador clicando com o programa Olá Olá **iniciar** menu e selecionando **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="b4e3b-140">Crie um novo projeto de aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-140">Create a new console application project.</span></span> <span data-ttu-id="b4e3b-141">Clique em Olá **arquivo** menu e selecione **novo**, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="b4e3b-142">Em Olá **novo projeto** caixa de diálogo, clique em **Visual C#** (se **Visual C#** não aparecer, procure em **outras linguagens**).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="b4e3b-143">Clique em Olá **aplicativo de Console (.NET Framework)** modelo e nomeie-o **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="b4e3b-144">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="b4e3b-145">Instale o pacote do NuGet do barramento de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="b4e3b-146">Esse pacote adiciona automaticamente referências toohello Service Bus bibliotecas, bem como Olá WCF **System. ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="b4e3b-147">[System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) é Olá namespace que permite que recursos básicos de saudação do acesso de tooprogrammatically do WCF.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="b4e3b-148">Barramento de serviço usa muitos dos objetos hello e atributos de contratos de serviço do WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="b4e3b-149">No Gerenciador de soluções, clique com botão direito hello e, em seguida, clique em **gerenciar pacotes NuGet...** . Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b4e3b-150">Certifique-se de que esse nome de projeto hello está selecionado no hello **versões** caixa.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="b4e3b-151">Clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="b4e3b-152">No Solution Explorer, clique duas vezes em tooopen de arquivo Program.cs Olá-lo no editor de saudação, se ele não ainda estiver aberto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="b4e3b-153">Adicione Olá seguinte usando as instruções na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="b4e3b-154">Alterar o nome de namespace de saudação de seu nome padrão de **EchoService** muito**Samples**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b4e3b-155">Este tutorial usa o namespace Olá c# **Samples**, que é o namespace de saudação do hello com base no contrato gerenciado tipo que é usado no arquivo de configuração de saudação em Olá [cliente do WCF configurar Olá](#configure-the-wcf-client) etapa.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="b4e3b-156">Você pode especificar qualquer namespace desejado ao criar este exemplo; No entanto, Olá tutorial não funcionará a menos que você modifique Olá namespaces de contrato hello e do serviço da mesma forma, no arquivo de configuração de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="b4e3b-157">Olá namespace especificado em Olá App. config arquivo deve ser Olá mesmo Olá namespace especificado em seus arquivos c#.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="b4e3b-158">Depois de saudação `Microsoft.ServiceBus.Samples` declaração de namespace, mas no namespace hello, definir uma nova interface chamada `IEchoContract` e aplicar Olá `ServiceContractAttribute` interface de toohello de atributo com um valor de namespace de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="b4e3b-159">valor de namespace Olá difere do namespace Olá que você usa em todo o escopo de saudação do seu código.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="b4e3b-160">Em vez disso, o valor do namespace Olá é usado como um identificador exclusivo para este contrato.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="b4e3b-161">Especificar explicitamente o namespace de saudação impede que o valor de namespace padrão Olá seja adicionado a toohello do nome do contrato.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="b4e3b-162">Cole Olá código a seguir após a declaração de namespace hello:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="b4e3b-163">Normalmente, o namespace de contrato de serviço Olá contém um esquema de nomenclatura que inclui informações de versão.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="b4e3b-164">Incluindo informações de versão no namespace de contrato de serviço Olá permite alterações principais do serviços tooisolate definindo um novo contrato de serviço com um novo namespace e expondo-o em um novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="b4e3b-165">Dessa maneira, os clientes podem continuar toouse Olá antigo contrato de serviço sem ter que toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="b4e3b-166">Informações de versão podem consistir de uma data ou um número da versão.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="b4e3b-167">Para saber mais, veja [Controle de Versão do Serviço](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="b4e3b-168">Para fins de saudação deste tutorial, Olá esquema do namespace de contrato de serviço de saudação de nomenclatura não contém informações de versão.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="b4e3b-169">Dentro de saudação `IEchoContract` interface, declare um método para Olá Olá de única operação `IEchoContract` expõe contrato em Olá interface e aplique Olá `OperationContractAttribute` método toohello de atributo que você deseja tooexpose como parte do hello pública retransmissão do WCF contrato, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="b4e3b-170">Depois de saudação `IEchoContract` definição de interface, declare um canal que herde das `IEchoContract` e também toohello `IClientChannel` interface, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="b4e3b-171">Um canal é o objeto WCF de saudação por meio do qual clientes e host Olá passam informações tooeach outros.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="b4e3b-172">Posteriormente, você escreverá código em relação às informações de tooecho Olá canal entre dois aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="b4e3b-173">De saudação **criar** menu, clique em **compilar solução** ou pressione **Ctrl + Shift + B** tooconfirm precisão de saudação do seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="b4e3b-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e3b-174">Example</span></span>

<span data-ttu-id="b4e3b-175">saudação de código a seguir mostra uma interface básica que define um contrato de retransmissão do WCF.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="b4e3b-176">Agora que hello interface foi criada, você pode implementar a interface de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="b4e3b-177">Contrato de implementar saudação do WCF</span><span class="sxs-lookup"><span data-stu-id="b4e3b-177">Implement hello WCF contract</span></span>

<span data-ttu-id="b4e3b-178">Criar um relé do Azure requer que você primeiro crie contrato hello, que é definido por meio de uma interface.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="b4e3b-179">Para obter mais informações sobre como criar interface hello, consulte a etapa anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="b4e3b-180">Olá próxima etapa é a interface de saudação tooimplement.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="b4e3b-181">Isso envolve a criação de uma classe denominada `EchoService` que implementa Olá definidos pelo usuário `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="b4e3b-182">Depois de implementar a interface hello, você configura Olá interface usando um arquivo de configuração App. config.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="b4e3b-183">arquivo de configuração de saudação contém as informações necessárias para o aplicativo hello, como nome de saudação do serviço Olá, nome de saudação do contrato hello e tipo de saudação do protocolo é toocommunicate usado com o serviço de retransmissão hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="b4e3b-184">código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="b4e3b-185">Para obter uma discussão mais geral sobre como tooimplement um serviço de contrato, consulte [implementando contratos de serviço](https://msdn.microsoft.com/library/ms733764.aspx) em Olá documentação do WCF.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="b4e3b-186">Criar uma nova classe chamada `EchoService` diretamente após a definição de saudação do hello `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="b4e3b-187">Olá `EchoService` classe implementa Olá `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="b4e3b-188">Implementações de interface tooother semelhante, você pode implementar definição Olá em um arquivo diferente.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="b4e3b-189">No entanto, para este tutorial, implementação hello está localizada no hello mesmo arquivo como definição de interface hello e hello `Main` método.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="b4e3b-190">Aplicar Olá [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="b4e3b-191">atributo Olá Especifica o namespace e o nome do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="b4e3b-192">Depois de fazer isso, Olá `EchoService` classe aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="b4e3b-193">Saudação de implementar `Echo` método definido no hello `IEchoContract` interface Olá `EchoService` classe.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="b4e3b-194">Clique em **criar**, em seguida, clique em **compilar solução** tooconfirm precisão de saudação de seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="b4e3b-195">Definir a configuração de saudação para o host de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="b4e3b-196">arquivo de configuração de saudação é muito semelhante arquivo de configuração do WCF tooa.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="b4e3b-197">Ele inclui o nome do serviço hello, ponto de extremidade (ou seja, a localização de saudação que expõe a retransmissão do Azure para clientes e hosts toocommunicate uns com os outros) e Olá associação (tipo de saudação do protocolo é usado toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="b4e3b-198">Olá principal diferença é que este ponto de extremidade de serviço configurado refere-se tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) associação, que não faz parte de saudação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="b4e3b-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) é uma das associações de saudação definidas pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="b4e3b-200">Em **Solution Explorer**, clique duas vezes em Olá App. config arquivo tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="b4e3b-201">Em Olá `<appSettings>` elemento, substitua os espaços reservados de saudação pelo nome de Olá do seu namespace de serviço e Olá chave SAS que você copiou em uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="b4e3b-202">Dentro de saudação `<system.serviceModel>` marcas, adicione um `<services>` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="b4e3b-203">Assim como nas associações, você pode definir vários aplicativos de retransmissão em um único arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="b4e3b-204">Este tutorial, porém, define apenas um.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="b4e3b-205">Dentro de saudação `<services>` elemento, adicionar um `<service>` nome do elemento toodefine saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="b4e3b-206">Dentro de saudação `<service>` elemento, definir local de saudação do contrato de ponto de extremidade hello e Olá também o tipo de associação para o ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="b4e3b-207">ponto de extremidade Olá define onde Olá cliente procurará o aplicativo de host hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="b4e3b-208">Posteriormente, o tutorial Olá usa toocreate esta etapa um URI que expõe totalmente host Olá por meio de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="b4e3b-209">associação de saudação declara que estamos usando TCP como Olá toocommunicate de protocolo com o serviço de retransmissão hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="b4e3b-210">De saudação **criar** menu, clique em **compilar solução** tooconfirm precisão de saudação de seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="b4e3b-211">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e3b-211">Example</span></span>

<span data-ttu-id="b4e3b-212">Olá código a seguir mostra a implementação Olá Olá do contrato de serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-212">hello following code shows hello implementation of hello service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="b4e3b-213">Olá código a seguir mostra formato básico de Olá Olá App. config arquivo associado ao host de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="b4e3b-214">Hospedar e executar um tooregister de serviço web básico com o serviço de retransmissão Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="b4e3b-215">Essa etapa descreve como toorun um Azure retransmissão serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="b4e3b-216">Criar hello credenciais de retransmissão</span><span class="sxs-lookup"><span data-stu-id="b4e3b-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="b4e3b-217">Em `Main()`, crie duas variáveis no namespace de saudação quais toostore e Olá chave SAS que são lidos da janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="b4e3b-218">a chave de SAS Olá será usado tooaccess posterior seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="b4e3b-219">Olá namespace também é passado como um parâmetro`CreateServiceUri` toocreate um URI de serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="b4e3b-220">Usando um [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) de objeto, declare que você usando uma chave SAS como tipo de credencial de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="b4e3b-221">Adicione Olá código a seguir diretamente após Olá código adicionado na última etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="b4e3b-222">Criar um endereço base para serviço Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-222">Create a base address for hello service</span></span>

<span data-ttu-id="b4e3b-223">Depois de código Olá você adicionou na última etapa do hello, crie um `Uri` instância para o endereço de base de saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="b4e3b-224">Esse URI especifica esquema de barramento de serviço de hello, Olá namespace e o caminho de saudação da interface de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="b4e3b-225">"sb" é uma abreviação para o esquema de barramento de serviço hello e indica que estamos usando TCP como protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="b4e3b-226">Isso também foi indicado no arquivo de configuração hello, quando [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) foi especificado como associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="b4e3b-227">Para este tutorial, hello URI é `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="b4e3b-228">Criar e configurar o host de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="b4e3b-229">Definir o modo de conectividade de saudação muito`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="b4e3b-230">modo de conectividade Olá descreve Olá protocolo hello serviço usa toocommunicate com serviço de retransmissão Olá; HTTP ou TCP.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="b4e3b-231">Usando a configuração padrão de saudação `AutoDetect`, serviço de saudação tenta tooconnect tooAzure retransmissão via TCP se estiver disponível e HTTP se TCP não está disponível.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="b4e3b-232">Observe que isso é diferente do serviço de saudação do protocolo de saudação especifica para comunicação do cliente.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="b4e3b-233">Esse protocolo é determinado pela associação Olá usada.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="b4e3b-234">Por exemplo, um serviço pode usar Olá [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) associação, que especifica que seu ponto de extremidade se comunica com os clientes por HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="b4e3b-235">Se o mesmo serviço pode especificar **Connectivitymode** para que o serviço de saudação se comunica com Azure retransmissão por TCP.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="b4e3b-236">Crie saudação do host de serviço, usando Olá que URI criado anteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="b4e3b-237">host de serviço de saudação é objeto WCF Olá que instancia o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="b4e3b-238">Aqui, você passá-lo tipo hello de serviço que você deseja toocreate (um `EchoService` tipo) e também endereço toohello no qual você deseja que o serviço de saudação tooexpose.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="b4e3b-239">Na parte superior de saudação do arquivo do hello Program.cs, adicione referências muito[ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) e [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="b4e3b-240">Em `Main()`, configurar o acesso do hello ponto de extremidade tooenable público.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="b4e3b-241">Essa etapa informa ao serviço de retransmissão Olá que seu aplicativo pode ser encontrado publicamente ao examinar Olá ATOM feed para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="b4e3b-242">Se você definir **DiscoveryType** muito**privada**, um cliente ainda será capaz de tooaccess serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="b4e3b-243">No entanto, o serviço de saudação não seria exibido, quando ele procura Olá retransmissão namespace.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="b4e3b-244">Em vez disso, Olá cliente terá tooknow caminho de ponto de extremidade de saudação com antecedência.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="b4e3b-245">Aplicar pontos de extremidade do serviço toohello definidos no arquivo App. config de saudação de credenciais do serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="b4e3b-246">Conforme mencionado na etapa anterior hello, você poderia ter declarado vários serviços e pontos de extremidade no arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="b4e3b-247">Se você tivesse, esse código percorreria o arquivo de configuração de saudação e pesquisa para cada ponto de extremidade toowhich deveria aplicar suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="b4e3b-248">No entanto, para este tutorial, o arquivo de configuração de saudação tem apenas um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="b4e3b-249">Host de serviço abrir Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-249">Open hello service host</span></span>

1. <span data-ttu-id="b4e3b-250">Abra o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="b4e3b-251">Informar usuário Olá Olá serviço está em execução e explique como tooshut para baixo serviço hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="b4e3b-252">Quando terminar, feche o host de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="b4e3b-253">Pressione **Ctrl + Shift + B** toobuild projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="b4e3b-254">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e3b-254">Example</span></span>

<span data-ttu-id="b4e3b-255">O código de serviço concluído deve aparecer conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="b4e3b-256">código de saudação inclui o contrato de serviço hello e a implementação de etapas anteriores no tutorial Olá e hosts Olá serviço em um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="b4e3b-257">Criar um cliente WCF Olá contrato de serviço</span><span class="sxs-lookup"><span data-stu-id="b4e3b-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="b4e3b-258">Olá próxima etapa é toocreate um aplicativo cliente e definir Olá contrato de serviço você implementará em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="b4e3b-259">Observe que muitas dessas etapas são semelhantes a etapas Olá usado toocreate um serviço: definir um contrato, edição de um App. config arquivo, usando o serviço de retransmissão do credenciais tooconnect toohello e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="b4e3b-260">código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="b4e3b-261">Crie um novo projeto na solução atual de Visual Studio Olá para cliente Olá Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="b4e3b-262">No Solution Explorer, no hello mesma solução que contém o serviço de saudação, clique a solução atual da saudação (não projeto Olá) e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="b4e3b-263">Em seguida, clique em **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="b4e3b-264">Em Olá **adicionar novo projeto** caixa de diálogo, clique em **Visual C#** (se **Visual C#** não aparecer, procure em **outras linguagens**), selecione Olá **Aplicativo de console (.NET Framework)** modelo e nomeie-o **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="b4e3b-265">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="b4e3b-266">No Solution Explorer, clique duas vezes no arquivo Program.cs Olá Olá **EchoClient** projeto tooopen-lo no editor de saudação, se ele não ainda estiver aberto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="b4e3b-267">Alterar o nome de namespace de saudação de seu nome padrão de `EchoClient` muito`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="b4e3b-268">Instalar Olá [pacote NuGet do barramento de serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus): no Solution Explorer, clique com botão direito Olá **EchoClient** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b4e3b-269">Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b4e3b-270">Clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="b4e3b-271">Adicionar um `using` instrução Olá [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace no arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="b4e3b-272">Adicione o namespace de toohello definição do contrato de serviço hello, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="b4e3b-273">Observe que essa definição é toohello idênticos definição usada no hello **Service** projeto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="b4e3b-274">Você deve adicionar esse código na parte superior de saudação do hello `Microsoft.ServiceBus.Samples` namespace.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="b4e3b-275">Pressione **Ctrl + Shift + B** toobuild cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="b4e3b-276">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e3b-276">Example</span></span>

<span data-ttu-id="b4e3b-277">Olá código a seguir mostra Olá status atual do arquivo Program.cs de saudação em hello **EchoClient** projeto.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="b4e3b-278">Configurar o cliente do WCF Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-278">Configure hello WCF client</span></span>

<span data-ttu-id="b4e3b-279">Nesta etapa, você deve criar um arquivo App. config para um aplicativo cliente básico que acessa o serviço de saudação criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="b4e3b-280">Esse arquivo App. config define o contrato hello, associação e o nome do ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="b4e3b-281">código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="b4e3b-282">No Solution Explorer, no hello **EchoClient** de projeto, clique duas vezes em **App. config** tooopen arquivo de saudação no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="b4e3b-283">Em Olá `<appSettings>` elemento, substitua os espaços reservados de saudação pelo nome de Olá do seu namespace de serviço e Olá chave SAS que você copiou em uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="b4e3b-284">Dentro do elemento de System. ServiceModel hello, adicione um `<client>` elemento.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="b4e3b-285">Essa etapa declara que você está definindo um aplicativo de cliente no estilo WCF.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="b4e3b-286">Dentro de saudação `client` elemento, definir nome hello, contrato e o tipo de associação para o ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="b4e3b-287">Esta etapa define o nome de saudação do ponto de extremidade hello, contrato de saudação definido no serviço hello e fatos Olá que o aplicativo de cliente de saudação usa TCP toocommunicate com retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="b4e3b-288">Olá nome de ponto de extremidade é usado em Olá próxima etapa toolink essa configuração de ponto de extremidade com o URI do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="b4e3b-289">Clique em **Arquivo**, depois em **Salvar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="b4e3b-290">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e3b-290">Example</span></span>

<span data-ttu-id="b4e3b-291">Olá código a seguir mostra arquivo App. config de saudação para cliente de eco de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-291">hello following code shows hello App.config file for hello Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="b4e3b-292">Cliente WCF implementar Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-292">Implement hello WCF client</span></span>
<span data-ttu-id="b4e3b-293">Nesta etapa, você deve implementar um aplicativo cliente básico que acessa o serviço de saudação criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="b4e3b-294">Serviço toohello semelhante, o cliente de saudação executa muitas das Olá mesmo operações tooaccess retransmissão do Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e3b-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="b4e3b-295">Define o modo de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="b4e3b-296">Cria Olá URI que localiza o serviço de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="b4e3b-297">Define as credenciais de segurança de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="b4e3b-298">Aplica-se a conexão do hello credenciais toohello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="b4e3b-299">Abre a conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-299">Opens hello connection.</span></span>
6. <span data-ttu-id="b4e3b-300">Executa tarefas específicas do aplicativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="b4e3b-301">Fecha a conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-301">Closes hello connection.</span></span>

<span data-ttu-id="b4e3b-302">No entanto, uma das principais diferenças de saudação é que o aplicativo de cliente hello usa um serviço de retransmissão do canal tooconnect toohello, enquanto o serviço de saudação usa uma chamada muito**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="b4e3b-303">código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="b4e3b-304">Implementar um aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="b4e3b-304">Implement a client application</span></span>
1. <span data-ttu-id="b4e3b-305">Definir o modo de conectividade de saudação muito**detecção automática**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="b4e3b-306">Adicionar Olá seguindo o código dentro de saudação `Main()` método hello **EchoClient** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="b4e3b-307">Defina variáveis toohold Olá valores para namespace de serviço Olá e a chave SAS que são lidos a partir do console de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="b4e3b-308">Crie hello URI que define o local de saudação do host de saudação em seu projeto de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="b4e3b-309">Crie objeto de credencial de saudação para seu ponto de extremidade do namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="b4e3b-310">Crie a fábrica de canais de saudação que carrega a configuração de saudação descrita no arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="b4e3b-311">Uma fábrica de canais é um objeto WCF que cria um canal por meio do qual os aplicativos de serviço e cliente Olá se comunicar.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="b4e3b-312">Aplique as credenciais de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="b4e3b-313">Crie e abra Olá canal toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="b4e3b-314">Grave a interface do usuário básica hello e funcionalidade de eco de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="b4e3b-315">Observe que o código Olá usa instância de saudação do objeto do canal de saudação como um proxy para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="b4e3b-316">Feche o canal hello e fábrica Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="b4e3b-317">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e3b-317">Example</span></span>

<span data-ttu-id="b4e3b-318">O código completo deve aparecer como segue, mostrar como toocreate um aplicativo cliente, como toocall Olá operações do serviço de saudação e como tooclose Olá cliente após a operação de saudação chamam é concluída.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a><span data-ttu-id="b4e3b-319">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="b4e3b-319">Run hello applications</span></span>

1. <span data-ttu-id="b4e3b-320">Pressione **Ctrl + Shift + B** toobuild solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="b4e3b-321">Isso cria o projeto de saudação do cliente e o projeto de serviço de saudação que você criou nas etapas anteriores Olá.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="b4e3b-322">Antes da aplicação de cliente Olá em execução, você deve se certificar que o aplicativo de serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="b4e3b-323">No Gerenciador de soluções no Visual Studio, clique com botão direito Olá **EchoService** solução, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="b4e3b-324">Na caixa de diálogo de propriedades de solução de saudação, clique em **projeto de inicialização**, em seguida, clique em Olá **vários projetos de inicialização** botão.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="b4e3b-325">Certifique-se de **EchoService** aparece primeiro na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="b4e3b-326">Saudação de conjunto **ação** caixa para ambos os Olá **EchoService** e **EchoClient** projetos muito**iniciar**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="b4e3b-327">Clique em **Dependências do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="b4e3b-328">Em Olá **projetos** selecione **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="b4e3b-329">Em Olá **depende** caixa, certifique-se de **EchoService** é verificada.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="b4e3b-330">Clique em **Okey** toodismiss Olá **propriedades** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="b4e3b-331">Pressione **F5** toorun os dois projetos.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="b4e3b-332">Ambas as janelas do console abrirem e solicitar o nome do namespace hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="b4e3b-333">Olá serviço deve ser executado pela primeira vez, isso em Olá **EchoService** janela de console, digite Olá namespace e, em seguida, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="b4e3b-334">Em seguida, será solicitado que você informe a sua chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="b4e3b-335">Insira a chave de SAS hello e pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="b4e3b-336">Aqui está o exemplo de saída da janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-336">Here is example output from hello console window.</span></span> <span data-ttu-id="b4e3b-337">Observe que os valores hello fornecidos aqui são apenas para fins de por exemplo.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="b4e3b-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="b4e3b-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="b4e3b-339">aplicativo de serviço Hello imprime o endereço de saudação do toohello console janela na qual ele está escutando, como visto no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="b4e3b-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="b4e3b-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="b4e3b-341">Em Olá **EchoClient** janela de console, digite Olá as mesmas informações que você inseriu anteriormente para o aplicativo de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="b4e3b-342">Siga Olá Olá de tooenter etapas anteriores mesmo namespace de serviço e a SAS valores para o aplicativo de cliente hello de chave.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="b4e3b-343">Depois de inserir esses valores, o cliente de saudação abre um canal toohello serviço e solicita que você tooenter algum texto, como visto no hello exemplo de saída do console a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="b4e3b-344">Insira algum aplicativo de serviço do texto toosend toohello e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="b4e3b-345">Esse texto é enviado toohello serviço por meio de operação de serviço de eco de saudação e aparece na janela de console de serviço hello como Olá saída de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="b4e3b-346">aplicativo de cliente Hello recebe o valor de retorno de saudação do hello `Echo` operação, que é o texto de saudação original e a imprime tooits janela de console.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="b4e3b-347">a seguir Olá é exemplo de saída da janela de console de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="b4e3b-348">Você pode continuar a enviar mensagens de texto do serviço de toohello cliente Olá dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="b4e3b-349">Quando tiver terminado, pressione Enter no hello cliente e serviço console windows tooend ambos os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4e3b-350">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4e3b-350">Next steps</span></span>

<span data-ttu-id="b4e3b-351">Este tutorial mostrou como toobuild um aplicativo de cliente de retransmissão do Azure e o serviço usando Olá recursos de retransmissão do WCF do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="b4e3b-352">Para obter um tutorial semelhante que usa o [Sistema de Mensagens do Barramento de Serviço](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte a [Introdução às filas do Barramento de Serviço](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="b4e3b-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="b4e3b-353">toolearn mais informações sobre a retransmissão do Azure, consulte Olá tópicos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e3b-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="b4e3b-354">Visão geral da arquitetura de Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="b4e3b-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="b4e3b-355">Visão geral da Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="b4e3b-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b4e3b-356">Como o serviço com o .NET de retransmissão toouse Olá WCF</span><span class="sxs-lookup"><span data-stu-id="b4e3b-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
