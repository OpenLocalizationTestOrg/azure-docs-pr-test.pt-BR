---
title: "Tutorial do REST do Barramento de Serviço usando a Retransmissão do Azure | Microsoft Docs"
description: "Compile um aplicativo host simples de retransmissão do Barramento de Serviço do Azure que expõe uma interface baseada em REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="b6aab-103">Tutorial do REST de Retransmissão de WCF do Azure</span><span class="sxs-lookup"><span data-stu-id="b6aab-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="b6aab-104">Este tutorial descreve como compilar um aplicativo host simples da Retransmissão do Azure que expõe uma interface baseada em REST.</span><span class="sxs-lookup"><span data-stu-id="b6aab-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="b6aab-105">O REST permite que um cliente da Web, como, por exemplo, um navegador da Web, acesse as APIs de Barramento de Serviço por meio de solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="b6aab-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="b6aab-106">Este tutorial usa o modelo de programação REST do WCF (Windows Communication Foundation) para construir um serviço REST no Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="b6aab-107">Para saber mais, confira [Modelo de programação REST WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) e [Criando e implementando serviços](/dotnet/framework/wcf/designing-and-implementing-services) na documentação do WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="b6aab-108">Etapa 1: criar um namespace</span><span class="sxs-lookup"><span data-stu-id="b6aab-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="b6aab-109">Para começar a usar os recursos de retransmissão no Azure, você deve primeiro criar um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="b6aab-110">Um namespace fornece um contêiner de escopo para endereçar recursos do Azure dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6aab-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="b6aab-111">Siga as [instruções aqui](relay-create-namespace-portal.md) para criar um namespace de Retransmissão.</span><span class="sxs-lookup"><span data-stu-id="b6aab-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="b6aab-112">Etapa 2: Definir um contrato de serviço WCF baseado em REST para usar com a Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="b6aab-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="b6aab-113">Quando você cria um serviço no estilo REST do WCF, é preciso definir o contrato.</span><span class="sxs-lookup"><span data-stu-id="b6aab-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="b6aab-114">O contrato especifica para quais operações o host oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="b6aab-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="b6aab-115">Uma operação de serviço pode ser considerada um método de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="b6aab-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="b6aab-116">Os contratos são criados pela definição de uma interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="b6aab-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="b6aab-117">Cada método na interface corresponde a uma operação de serviço específica.</span><span class="sxs-lookup"><span data-stu-id="b6aab-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="b6aab-118">O atributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) deve ser aplicado a cada interface, e o atributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) deve ser aplicado a cada operação.</span><span class="sxs-lookup"><span data-stu-id="b6aab-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="b6aab-119">Se um método em uma interface que tem o [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) não tiver o [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), tal método não será exposto.</span><span class="sxs-lookup"><span data-stu-id="b6aab-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="b6aab-120">O código usado para essas tarefas é mostrado no exemplo logo após o procedimento.</span><span class="sxs-lookup"><span data-stu-id="b6aab-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="b6aab-121">A principal diferença entre um contrato básico do WCF e um contrato no estilo REST é a adição de uma propriedade para o atributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6aab-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="b6aab-122">Esta propriedade permite mapear um método em sua interface para um método no outro lado da interface.</span><span class="sxs-lookup"><span data-stu-id="b6aab-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="b6aab-123">Nesse caso, usaremos [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) para vincular um método a HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="b6aab-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="b6aab-124">Isso permite que o Barramento de Serviço recupere e interprete de forma precisa os comandos enviados à interface.</span><span class="sxs-lookup"><span data-stu-id="b6aab-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="b6aab-125">Para criar um contrato com uma interface</span><span class="sxs-lookup"><span data-stu-id="b6aab-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="b6aab-126">Abra o Visual Studio como administrador: clique com o botão direito no programa no menu **Iniciar** e, em seguida, clique em **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="b6aab-127">Crie um novo projeto de aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="b6aab-127">Create a new console application project.</span></span> <span data-ttu-id="b6aab-128">Clique no menu **Arquivo** e selecione **Novo** e, em seguida, **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="b6aab-129">Na caixa de diálogo **Novo Projeto**, clique em **Visual C#**, selecione o modelo **Aplicativo de Console** e chame-o de **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="b6aab-130">Use o **Local** padrão.</span><span class="sxs-lookup"><span data-stu-id="b6aab-130">Use the default **Location**.</span></span> <span data-ttu-id="b6aab-131">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="b6aab-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="b6aab-132">Para um projeto C#, o Visual Studio cria um arquivo `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="b6aab-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="b6aab-133">Essa classe contém um método `Main()` vazio, necessário para um projeto de aplicativo de console ser criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="b6aab-134">Adicione referências ao Barramento de Serviço e ao **System.ServiceModel.dll** ao projeto instalando o pacote do NuGet do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="b6aab-135">Esse pacote adiciona automaticamente referências para as bibliotecas do Barramento de Serviço, bem como o WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="b6aab-136">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **ImageListener** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b6aab-137">Clique na guia **Procurar** e procure `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="b6aab-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b6aab-138">Clique em **Instalar**e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="b6aab-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="b6aab-139">Você precisa adicionar explicitamente uma referência a **System.ServiceModel.Web.dll** ao projeto:</span><span class="sxs-lookup"><span data-stu-id="b6aab-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="b6aab-140">a.</span><span class="sxs-lookup"><span data-stu-id="b6aab-140">a.</span></span> <span data-ttu-id="b6aab-141">No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Referências**, na pasta do projeto e clique em **Adicionar Referência**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="b6aab-142">b.</span><span class="sxs-lookup"><span data-stu-id="b6aab-142">b.</span></span> <span data-ttu-id="b6aab-143">Na caixa de diálogo **Adicionar Referência**, clique na guia **Estrutura** no lado esquerdo e, na caixa **Pesquisar**, digite **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="b6aab-144">Marque a caixa de seleção **System.ServiceModel.Web** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="b6aab-145">Adicione as instruções `using` abaixo na parte superior do arquivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="b6aab-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="b6aab-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) é o namespace que permite o acesso programático aos recursos básicos do WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="b6aab-147">A Retransmissão de WCF usa vários dos objetos e atributos do WCF para definir contratos de serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="b6aab-148">Você usará este namespace na maioria dos seus aplicativos de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="b6aab-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="b6aab-149">Da mesma forma, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) ajuda a definir o canal, que é o objeto por meio do qual você se comunica com a Retransmissão do Azure e o navegador da Web do cliente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="b6aab-150">Por fim, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contém os tipos que permitem a criação de aplicativos baseados na Web.</span><span class="sxs-lookup"><span data-stu-id="b6aab-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="b6aab-151">Renomeie o namespace `ImageListener` para **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="b6aab-152">Imediatamente após a chave de abertura da declaração do namespace, defina uma nova interface chamada **IImageContract** e aplique o atributo **ServiceContractAttribute** à interface com um valor de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="b6aab-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="b6aab-153">O valor do namespace é diferente do namespace que você usa em todo o escopo do seu código.</span><span class="sxs-lookup"><span data-stu-id="b6aab-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="b6aab-154">O valor do namespace é usado como um identificador exclusivo para este contrato e deve ter informações sobre a versão.</span><span class="sxs-lookup"><span data-stu-id="b6aab-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="b6aab-155">Para saber mais, veja [Controle de Versão do Serviço](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="b6aab-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="b6aab-156">Especificar o namespace de forma explícita impede a adição do valor de namespace padrão ao nome do contrato.</span><span class="sxs-lookup"><span data-stu-id="b6aab-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="b6aab-157">Dentro da interface `IImageContract`, declare um método para a operação individual exposta pelo contrato `IImageContract` na interface e aplique o atributo `OperationContractAttribute` ao método que você deseja expor como parte do contrato de Barramento de Serviço público.</span><span class="sxs-lookup"><span data-stu-id="b6aab-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="b6aab-158">No atributo **OperationContract**, adicione o valor **WebGet**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="b6aab-159">Isso permite que o serviço de retransmissão encaminhe as solicitações HTTP GET para `GetImage` e converta os valores retornados de `GetImage` em uma resposta HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="b6aab-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="b6aab-160">Posteriormente no tutorial, você usará um navegador da Web para acessar esse método e exibir a imagem no navegador.</span><span class="sxs-lookup"><span data-stu-id="b6aab-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="b6aab-161">Logo após a definição `IImageContract`, declare um canal que herde das interfaces `IImageContract` e `IClientChannel`.</span><span class="sxs-lookup"><span data-stu-id="b6aab-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="b6aab-162">Um canal é o objeto WCF por meio do qual o serviço e o cliente trocam informações.</span><span class="sxs-lookup"><span data-stu-id="b6aab-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="b6aab-163">Posteriormente, você criará o canal em seu aplicativo host.</span><span class="sxs-lookup"><span data-stu-id="b6aab-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="b6aab-164">A Retransmissão do Azure usa este canal para passar as solicitações HTTP GET do navegador para a implementação **GetImage**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="b6aab-165">A retransmissão também usa o canal para obter o valor retornado de **GetImage** e convertê-lo em uma GETRESPONSE HTTP para o navegador do cliente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="b6aab-166">No menu **Compilar**, clique em **Compilar Solução** para confirmar a precisão de seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="b6aab-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="b6aab-167">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b6aab-167">Example</span></span>
<span data-ttu-id="b6aab-168">O código a seguir mostra uma interface básica que define um contrato de Retransmissão de WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="b6aab-169">Etapa 3: implementar um contrato de serviço WCF baseado em REST para usar no Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="b6aab-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="b6aab-170">A criação de um serviço de Retransmissão de WCF no estilo REST exige primeiro a criação do contrato, que é definido por meio de uma interface.</span><span class="sxs-lookup"><span data-stu-id="b6aab-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="b6aab-171">A próxima etapa é implementar a interface.</span><span class="sxs-lookup"><span data-stu-id="b6aab-171">The next step is to implement the interface.</span></span> <span data-ttu-id="b6aab-172">Isso envolve a criação de uma classe chamada **ImageService** que implementa a interface **IImageContract** definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="b6aab-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="b6aab-173">Depois de implementar o contrato, configure a interface usando um arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="b6aab-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="b6aab-174">O arquivo de configuração contém as informações necessárias para o aplicativo, como o nome do serviço, o nome do contrato e o tipo de protocolo usado para se comunicar com o serviço de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="b6aab-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="b6aab-175">O código usado para essas tarefas é fornecido no exemplo logo após o procedimento.</span><span class="sxs-lookup"><span data-stu-id="b6aab-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="b6aab-176">Assim como nas etapas anteriores, há pouca diferença entre a implementação de um contrato no estilo REST e um contrato de Retransmissão de WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="b6aab-177">Para implementar um contrato de Barramento de Serviço no estilo REST</span><span class="sxs-lookup"><span data-stu-id="b6aab-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="b6aab-178">Crie uma nova classe chamada **ImageService** diretamente após a definição da interface **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="b6aab-179">A classe **ImageService** implementa a interface **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="b6aab-180">Assim como outras implementações de interface, você pode implementar a definição em um arquivo diferente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="b6aab-181">No entanto, para este tutorial, a implementação é exibida no mesmo arquivo que a definição de interface e o método `Main()`.</span><span class="sxs-lookup"><span data-stu-id="b6aab-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="b6aab-182">Aplique o atributo [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) à classe **IImageService** para indicar que a classe é uma implementação de um contrato do WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="b6aab-183">Conforme mencionado anteriormente, esse namespace não é um namespace tradicional.</span><span class="sxs-lookup"><span data-stu-id="b6aab-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="b6aab-184">Em vez disso, ele faz parte da arquitetura do WCF que identifica o contrato.</span><span class="sxs-lookup"><span data-stu-id="b6aab-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="b6aab-185">Para saber mais, confira o tópico [Nomes de Contrato de Dados](https://msdn.microsoft.com/library/ms731045.aspx) na documentação do WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="b6aab-186">Adicione uma imagem .jpg ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b6aab-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="b6aab-187">Esta é uma imagem exibida pelo serviço no navegador receptor.</span><span class="sxs-lookup"><span data-stu-id="b6aab-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="b6aab-188">Clique com o botão direito do mouse em seu projeto e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="b6aab-189">Em seguida, clique em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-189">Then click **Existing Item**.</span></span> <span data-ttu-id="b6aab-190">Use a caixa de diálogo **Adicionar Item Existente** para navegar até um .jpg adequado e,em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="b6aab-191">Ao adicionar o arquivo, certifique-se de que a opção **Todos os Arquivos** esteja selecionada na lista suspensa ao lado do campo **Nome do arquivo:**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="b6aab-192">O restante deste tutorial supõe que o nome da imagem seja "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="b6aab-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="b6aab-193">Se você tiver um arquivo diferente, será necessário renomear a imagem ou alterar o código para compensar.</span><span class="sxs-lookup"><span data-stu-id="b6aab-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="b6aab-194">Para ter certeza de que o serviço em execução consegue encontrar o arquivo de imagem, no **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo de imagem e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="b6aab-195">No painel **Propriedades**, defina **Copiar para o Diretório de Saída** como **Copiar se for mais recente**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="b6aab-196">Adicione uma referência ao assembly **System.Drawing.dll** ao projeto, e adicione também as seguintes instruções `using` associadas.</span><span class="sxs-lookup"><span data-stu-id="b6aab-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="b6aab-197">Na classe **ImageService**, adicione o seguinte construtor que carrega o bitmap e o prepara para envio ao navegador do cliente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="b6aab-198">Logo após o código anterior, adicione o seguinte método **GetImage** à classe **ImageService** para retornar uma mensagem HTTP que contém a imagem.</span><span class="sxs-lookup"><span data-stu-id="b6aab-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="b6aab-199">Essa implementação usa **MemoryStream** para recuperar a imagem e prepará-la para transmissão por streaming para o navegador.</span><span class="sxs-lookup"><span data-stu-id="b6aab-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="b6aab-200">Ela começa a posição da transmissão em zero, declara o conteúdo da transmissão como jpeg e transmite as informações.</span><span class="sxs-lookup"><span data-stu-id="b6aab-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="b6aab-201">No menu **Compilar**, clique em **Solução de Compilação**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="b6aab-202">Para definir a configuração a fim de executar o serviço da Web no Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="b6aab-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="b6aab-203">No **Gerenciador de Soluções**, clique duas vezes em **App.config** para abri-lo no editor do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6aab-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="b6aab-204">O arquivo **App.config** inclui o nome do serviço, o ponto de extremidade (ou seja, o local que a Retransmissão do Azure expõe para os clientes e hosts se comunicarem) e a associação (o tipo de protocolo usado para comunicação).</span><span class="sxs-lookup"><span data-stu-id="b6aab-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="b6aab-205">A principal diferença é que o ponto de extremidade de serviço configurado refere-se a uma associação [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding).</span><span class="sxs-lookup"><span data-stu-id="b6aab-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="b6aab-206">O elemento XML `<system.serviceModel>` é um elemento WCF que define um ou mais serviços.</span><span class="sxs-lookup"><span data-stu-id="b6aab-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="b6aab-207">Aqui, ele é usado para definir o nome do serviço e o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b6aab-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="b6aab-208">Na parte inferior do elemento `<system.serviceModel>` (mas ainda dentro de `<system.serviceModel>`), adicione um elemento `<bindings>` que tenha o seguinte conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b6aab-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="b6aab-209">Isso define as associações usadas no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6aab-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="b6aab-210">É possível definir várias associações, mas para este tutorial você definirá apenas uma.</span><span class="sxs-lookup"><span data-stu-id="b6aab-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="b6aab-211">O código anterior define uma associação [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) da Retransmissão de WCF com **relayClientAuthenticationType** definido como **None**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="b6aab-212">Essa configuração indica que um ponto de extremidade usando essa associação não exige uma credencial de cliente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="b6aab-213">Após o elemento `<bindings>`, adicione um elemento `<services>`.</span><span class="sxs-lookup"><span data-stu-id="b6aab-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="b6aab-214">Assim como nas associações, você pode definir vários serviços em um único arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="b6aab-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="b6aab-215">No entanto, para este tutorial, você definirá apenas um.</span><span class="sxs-lookup"><span data-stu-id="b6aab-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="b6aab-216">Esta etapa configura um serviço que usa o padrão previamente definido **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="b6aab-217">Ele também usa o padrão **sbTokenProvider**, definido na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="b6aab-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="b6aab-218">Após o elemento `<services>`, crie um elemento `<behaviors>` com o conteúdo a seguir, substituindo "SAS_KEY" pela chave *Assinatura de Acesso Compartilhado* (SAS) obtida anteriormente no [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b6aab-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="b6aab-219">Ainda em App.config, no elemento `<appSettings>`, substitua todo o valor da cadeia de conexão pela cadeia de conexão obtida anteriormente no portal.</span><span class="sxs-lookup"><span data-stu-id="b6aab-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="b6aab-220">No menu **Compilar**, clique em **Compilar Solução** para compilar a solução inteira.</span><span class="sxs-lookup"><span data-stu-id="b6aab-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="b6aab-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b6aab-221">Example</span></span>
<span data-ttu-id="b6aab-222">O código a seguir mostra o contrato e a implementação do serviço para um serviço baseado em REST que está em execução no Barramento de Serviço usando a associação **WebHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="b6aab-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="b6aab-223">O exemplo a seguir mostra o arquivo App.config associado ao serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="b6aab-224">Etapa 4: hospedar o serviço WCF baseado em REST para usar a Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="b6aab-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="b6aab-225">Esta etapa descreve como executar um serviço Web usando um aplicativo de console com Retransmissão de WCF.</span><span class="sxs-lookup"><span data-stu-id="b6aab-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="b6aab-226">Confira uma lista completa com os códigos escritos nesta etapa logo após o procedimento.</span><span class="sxs-lookup"><span data-stu-id="b6aab-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="b6aab-227">Para criar um endereço base para o serviço</span><span class="sxs-lookup"><span data-stu-id="b6aab-227">To create a base address for the service</span></span>
1. <span data-ttu-id="b6aab-228">Na declaração de função `Main()`, crie uma variável para armazenar o namespace de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b6aab-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="b6aab-229">Substitua `yourNamespace` pelo nome do namespace de Retransmissão que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b6aab-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="b6aab-230">O Barramento de Serviço usa o nome do namespace para criar um URI exclusivo.</span><span class="sxs-lookup"><span data-stu-id="b6aab-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="b6aab-231">Crie uma instância de `Uri` para o endereço básico do serviço que está baseado no namespace.</span><span class="sxs-lookup"><span data-stu-id="b6aab-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="b6aab-232">Para criar e configurar o host do serviço Web</span><span class="sxs-lookup"><span data-stu-id="b6aab-232">To create and configure the web service host</span></span>
* <span data-ttu-id="b6aab-233">Crie o host do serviço Web usando o endereço URI criado anteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b6aab-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="b6aab-234">O host do serviço é o objeto do WCF que instancia o aplicativo host.</span><span class="sxs-lookup"><span data-stu-id="b6aab-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="b6aab-235">Este exemplo passa o tipo de host que você deseja criar (um **ImageService**) e também o endereço no qual você deseja expor o aplicativo host.</span><span class="sxs-lookup"><span data-stu-id="b6aab-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="b6aab-236">Para executar o host do serviço Web</span><span class="sxs-lookup"><span data-stu-id="b6aab-236">To run the web service host</span></span>
1. <span data-ttu-id="b6aab-237">Abra o arquivo serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="b6aab-238">O serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="b6aab-238">The service is now running.</span></span>
2. <span data-ttu-id="b6aab-239">É exibida uma mensagem indicando que o serviço está em execução e dizendo como parar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="b6aab-240">Quando terminar, feche o host do serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="b6aab-241">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b6aab-241">Example</span></span>
<span data-ttu-id="b6aab-242">O exemplo a seguir inclui o contrato e a implementação do serviço das etapas anteriores no tutorial e hospeda o serviço em um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="b6aab-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="b6aab-243">Compile o código a seguir em um arquivo executável chamado ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="b6aab-243">Compile the following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="b6aab-244">Compilando o código</span><span class="sxs-lookup"><span data-stu-id="b6aab-244">Compiling the code</span></span>
<span data-ttu-id="b6aab-245">Após compilar a solução, faça o seguinte para executar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="b6aab-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="b6aab-246">Pressione **F5** ou navegue até a localização do arquivo executável (ImageListener\bin\Debug\ImageListener.exe) para executar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b6aab-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="b6aab-247">Mantenha o aplicativo em execução, pois ele é necessário para executar a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="b6aab-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="b6aab-248">Copie e cole o endereço do prompt de comando em um navegador para ver a imagem.</span><span class="sxs-lookup"><span data-stu-id="b6aab-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="b6aab-249">Quando tiver terminado, pressione **Enter** na janela do prompt de comando para fechar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6aab-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6aab-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6aab-250">Next steps</span></span>
<span data-ttu-id="b6aab-251">Agora que você compilou um aplicativo que usa o serviço de retransmissão do Barramento de Serviço, confira os seguintes artigos para saber mais sobre a Retransmissão do Azure:</span><span class="sxs-lookup"><span data-stu-id="b6aab-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="b6aab-252">Visão geral da arquitetura de Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="b6aab-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="b6aab-253">Visão geral da Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="b6aab-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b6aab-254">Como usar o serviço de Retransmissão de WCF com o .NET</span><span class="sxs-lookup"><span data-stu-id="b6aab-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
