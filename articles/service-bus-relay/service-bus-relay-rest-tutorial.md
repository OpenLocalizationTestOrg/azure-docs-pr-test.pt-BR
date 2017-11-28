---
title: "tutorial de REST de barramento aaaService usando a retransmissão do Azure | Microsoft Docs"
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
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="3b5d7-103">Tutorial do REST de Retransmissão de WCF do Azure</span><span class="sxs-lookup"><span data-stu-id="3b5d7-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="3b5d7-104">Este tutorial descreve como toobuild uma retransmissão Azure simples hospedar o aplicativo que expõe uma interface baseada em REST.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="3b5d7-105">REST permite que um cliente da web, como um navegador da web, Olá tooaccess solicitações de APIs do barramento de serviço por meio de HTTP.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="3b5d7-106">Olá tutorial usa o modelo tooconstruct programação Olá REST do Windows Communication Foundation (WCF) um serviço REST no barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="3b5d7-107">Para obter mais informações, consulte [modelo de programação WCF REST](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) e [Projetando e Implementando serviços](/dotnet/framework/wcf/designing-and-implementing-services) em Olá documentação do WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="3b5d7-108">Etapa 1: criar um namespace</span><span class="sxs-lookup"><span data-stu-id="3b5d7-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="3b5d7-109">usando toobegin Olá recursos de retransmissão no Azure, você deve primeiro criar um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="3b5d7-110">Um namespace fornece um contêiner de escopo para endereçar recursos do Azure dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="3b5d7-111">Siga Olá [as instruções aqui](relay-create-namespace-portal.md) toocreate um namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="3b5d7-112">Etapa 2: Definir uma toouse de contrato de serviço WCF com base em REST com retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="3b5d7-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="3b5d7-113">Quando você cria um serviço WCF no estilo REST, você deve definir o contrato de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="3b5d7-114">contrato de saudação especifica quais operações Olá host oferece suporte a.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="3b5d7-115">Uma operação de serviço pode ser considerada um método de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="3b5d7-116">Os contratos são criados pela definição de uma interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="3b5d7-117">Cada método na interface de saudação corresponde tooa operação de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="3b5d7-118">Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo deve ser aplicado tooeach interface e Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atributo deve ser aplicado tooeach operação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="3b5d7-119">Se um método em uma interface que tem Olá [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) não tem Olá [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), tal método não será exposto.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="3b5d7-120">código de saudação usado para essas tarefas é mostrado no exemplo de Olá Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="3b5d7-121">Olá, principal diferença entre um contrato WCF e um contrato estilo REST é Olá adição de uma propriedade toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b5d7-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="3b5d7-122">Essa propriedade permite que você toomap um método em seu método tooa de interface em hello outro lado da interface de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="3b5d7-123">Nesse caso, usaremos [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP um método GET.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="3b5d7-124">Isso permite que o barramento de serviço tooaccurately recuperar e interprete os comandos enviados toohello interface.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="3b5d7-125">toocreate um contrato com uma interface</span><span class="sxs-lookup"><span data-stu-id="3b5d7-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="3b5d7-126">Abra o Visual Studio como administrador: programa de saudação com o botão direito no hello **iniciar** menu e clique **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="3b5d7-127">Crie um novo projeto de aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-127">Create a new console application project.</span></span> <span data-ttu-id="3b5d7-128">Clique em Olá **arquivo** menu e selecione **novo**, em seguida, selecione **projeto**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="3b5d7-129">Em Olá **novo projeto** caixa de diálogo, clique em **Visual C#**, selecione Olá **aplicativo de Console** modelo e nomeie-o **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="3b5d7-130">Usar saudação padrão **local**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-130">Use hello default **Location**.</span></span> <span data-ttu-id="3b5d7-131">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="3b5d7-132">Para um projeto C#, o Visual Studio cria um arquivo `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="3b5d7-133">Essa classe contém vazio `Main()` método, necessário para um toobuild de projeto de aplicativo de console corretamente.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="3b5d7-134">Adicionar referências tooService barramento e **System.ServiceModel.dll** toohello projeto instalando o pacote do NuGet do barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="3b5d7-135">Esse pacote adiciona automaticamente referências toohello Service Bus bibliotecas, bem como Olá WCF **System. ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="3b5d7-136">No Gerenciador de soluções, clique com botão direito Olá **ImageListener** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="3b5d7-137">Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="3b5d7-138">Clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="3b5d7-139">Você deve adicionar explicitamente uma referência muito**System** toohello projeto:</span><span class="sxs-lookup"><span data-stu-id="3b5d7-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="3b5d7-140">a.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-140">a.</span></span> <span data-ttu-id="3b5d7-141">No Gerenciador de soluções, clique com botão direito Olá **referências** pasta sob a pasta do projeto hello e depois clique em **adicionar referência**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="3b5d7-142">b.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-142">b.</span></span> <span data-ttu-id="3b5d7-143">Em Olá **adicionar referência** caixa de diálogo, clique em Olá **Framework** guia no lado esquerdo da saudação e em Olá **pesquisa** , digite **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="3b5d7-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="3b5d7-144">Selecione Olá **System.ServiceModel.Web** caixa de seleção e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="3b5d7-145">Adicione o seguinte Olá `using` instruções na parte superior de saudação do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="3b5d7-146">[System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) é namespace Olá que habilita os recursos de toobasic acesso programático do WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="3b5d7-147">Retransmissão do WCF usa muitos dos objetos hello e atributos de contratos de serviço do WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="3b5d7-148">Você usará este namespace na maioria dos seus aplicativos de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="3b5d7-149">Da mesma forma, [Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) ajuda a definir canal hello, que é o objeto Olá por meio do qual você se comunica com o navegador de cliente de retransmissão do Azure e hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="3b5d7-150">Por fim, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contém tipos de saudação que permitem a você aplicativos toocreate da web.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="3b5d7-151">Renomear Olá `ImageListener` namespace muito**Samples**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="3b5d7-152">Diretamente após Olá chave de abertura da declaração de namespace hello, definir uma nova interface chamada **IImageContract** e aplicar Olá **ServiceContractAttribute** interface de toohello de atributo com um valor de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="3b5d7-153">valor de namespace Olá difere do namespace Olá que você usa em todo o escopo de saudação do seu código.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="3b5d7-154">valor de namespace Olá é usado como um identificador exclusivo para este contrato e deve ter informações de versão.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="3b5d7-155">Para saber mais, veja [Controle de Versão do Serviço](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="3b5d7-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="3b5d7-156">Especificar explicitamente o namespace de saudação impede que o valor de namespace padrão Olá seja adicionado a toohello do nome do contrato.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="3b5d7-157">Dentro de saudação `IImageContract` interface, declare um método para Olá Olá de única operação `IImageContract` expõe contrato em Olá interface e aplique Olá `OperationContractAttribute` toohello método que você deseja tooexpose como parte do serviço de público Olá barramento de atributo contrato.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="3b5d7-158">Em Olá **OperationContract** atributo, adicionar Olá **WebGet** valor.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="3b5d7-159">Isso permite Olá tooroute do serviço de retransmissão solicitações HTTP GET muito`GetImage`e tootranslate hello retornar valores de `GetImage` em uma resposta HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="3b5d7-160">Posteriormente no tutorial hello, você usará um tooaccess do navegador da web este método e imagem de saudação toodisplay no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="3b5d7-161">Depois de saudação `IImageContract` definição, declare um canal que herda de ambos os Olá `IImageContract` e `IClientChannel` interfaces.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="3b5d7-162">Um canal é o objeto WCF de saudação por meio do qual cliente e serviço Olá passam informações tooeach outros.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="3b5d7-163">Posteriormente, você criará o canal Olá em seu aplicativo de host.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="3b5d7-164">Retransmissão do Azure, em seguida, usa esse canal toopass Olá das solicitações HTTP GET do hello navegador tooyour **GetImage** implementação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="3b5d7-165">retransmissão de saudação também usa Olá Olá de tootake de canal **GetImage** valor de retorno e convertê-lo em uma GETRESPONSE HTTP para o navegador de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="3b5d7-166">De saudação **criar** menu, clique em **compilar solução** tooconfirm precisão de saudação do seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="3b5d7-167">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3b5d7-167">Example</span></span>
<span data-ttu-id="3b5d7-168">saudação de código a seguir mostra uma interface básica que define um contrato de retransmissão do WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="3b5d7-169">Etapa 3: Implementar uma toouse de contrato de serviço WCF com base em REST do barramento do serviço</span><span class="sxs-lookup"><span data-stu-id="3b5d7-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="3b5d7-170">Criar um serviço de retransmissão do WCF no estilo REST requer que você primeiro crie contrato hello, que é definido por meio de uma interface.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="3b5d7-171">Olá próxima etapa é a interface de saudação tooimplement.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="3b5d7-172">Isso envolve a criação de uma classe denominada **ImageService** que implementa Olá definidos pelo usuário **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="3b5d7-173">Depois de implementar o contrato hello, você configura Olá interface usando um arquivo App. config.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="3b5d7-174">arquivo de configuração de saudação contém as informações necessárias para o aplicativo hello, como nome de saudação do serviço Olá, nome de saudação do contrato hello e tipo de saudação do protocolo é toocommunicate usado com o serviço de retransmissão hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="3b5d7-175">código de saudação usado para essas tarefas é fornecido no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="3b5d7-176">Como com as etapas anteriores do hello, há muito pouca diferença entre implementar um contrato estilo REST e um contrato de retransmissão do WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="3b5d7-177">contrato do barramento de serviço tooimplement um estilo REST</span><span class="sxs-lookup"><span data-stu-id="3b5d7-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="3b5d7-178">Criar uma nova classe chamada **ImageService** diretamente após a definição de saudação do hello **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="3b5d7-179">Olá **ImageService** classe implementa Olá **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="3b5d7-180">Implementações de interface tooother semelhante, você pode implementar definição Olá em um arquivo diferente.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="3b5d7-181">No entanto, para este tutorial, implementação Olá aparece no hello mesmo arquivo como definição de interface hello e `Main()` método.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="3b5d7-182">Aplicar Olá [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello **IImageService** tooindicate de classe que Olá classe é uma implementação de um contrato WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="3b5d7-183">Conforme mencionado anteriormente, esse namespace não é um namespace tradicional.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="3b5d7-184">Em vez disso, ele faz parte da saudação arquitetura do WCF que identifica o contrato de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="3b5d7-185">Para obter mais informações, consulte Olá [nomes de contrato de dados](https://msdn.microsoft.com/library/ms731045.aspx) tópico Olá documentação do WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="3b5d7-186">Adicione um projeto de tooyour de imagem. jpg.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="3b5d7-187">Esta é uma imagem que exibe serviço Olá Olá recebendo o navegador.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="3b5d7-188">Clique com o botão direito do mouse em seu projeto e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="3b5d7-189">Em seguida, clique em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-189">Then click **Existing Item**.</span></span> <span data-ttu-id="3b5d7-190">Saudação de uso **Add Existing Item** tooan de toobrowse de caixa de diálogo apropriado. jpg e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="3b5d7-191">Ao adicionar arquivo hello, certifique-se de que **todos os arquivos** está selecionado no hello lista suspensa próxima toohello **nome do arquivo:** campo.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="3b5d7-192">rest Olá deste tutorial presume que Olá nome da imagem de saudação é "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="3b5d7-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="3b5d7-193">Se você tiver um arquivo diferente, você será ter toorename Olá imagem ou alterar toocompensate seu código.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="3b5d7-194">toomake-se de que Olá executando o serviço pode encontrar o arquivo de imagem de hello, em **Solution Explorer** clique com o arquivo de imagem hello e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="3b5d7-195">Em Olá **propriedades** painel, defina **copiar tooOutput diretório** muito**copiar se mais recente**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="3b5d7-196">Adicionar uma referência toohello **System.Drawing.dll** toohello de assembly do projeto e também adicionar seguintes Olá `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="3b5d7-197">Em Olá **ImageService** de classe, adicione Olá seguinte construtor que carrega Olá bitmap e prepara toosend-toohello o navegador do cliente.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
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
7. <span data-ttu-id="3b5d7-198">Diretamente após o código anterior do hello, adicione o seguinte de saudação **GetImage** método hello **ImageService** mensagem tooreturn um HTTP de classe que contém a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
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
   
    <span data-ttu-id="3b5d7-199">Essa implementação usa **MemoryStream** tooretrieve Olá imagem e prepará-la para streaming toohello navegador.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="3b5d7-200">Inicia a posição de fluxo de saudação em zero, declara o conteúdo de fluxo hello como jpeg e transmite informações hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="3b5d7-201">De saudação **criar** menu, clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="3b5d7-202">configuração de saudação toodefine para executar o serviço da web de saudação no barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="3b5d7-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="3b5d7-203">Em **Solution Explorer**, clique duas vezes em **App. config** tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="3b5d7-204">Olá **App. config** arquivo inclui Olá nome, o ponto de extremidade (ou seja, local Olá retransmissão Azure expõe para clientes e hosts toocommunicate uns com os outros) e associação (tipo de saudação do protocolo é usado toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="3b5d7-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="3b5d7-205">Olá diferença principal aqui é aquele ponto de extremidade de serviço Olá configurado refere-se tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) associação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="3b5d7-206">Olá `<system.serviceModel>` XML é um elemento WCF que define um ou mais serviços.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="3b5d7-207">Aqui, é o ponto de extremidade e o nome de serviço de saudação toodefine usado.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="3b5d7-208">Na parte inferior de saudação do hello `<system.serviceModel>` elemento (mas ainda dentro `<system.serviceModel>`), adicione um `<bindings>` elemento que tem Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="3b5d7-209">Isso define associações de saudação usadas no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="3b5d7-210">É possível definir várias associações, mas para este tutorial você definirá apenas uma.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="3b5d7-211">código anterior Olá define uma retransmissão WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) associação com **relayClientAuthenticationType** definido muito**nenhum**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="3b5d7-212">Essa configuração indica que um ponto de extremidade usando essa associação não exige uma credencial de cliente.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="3b5d7-213">Depois de saudação `<bindings>` elemento, adicionar um `<services>` elemento.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="3b5d7-214">Associações toohello semelhante, você pode definir vários serviços em um único arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="3b5d7-215">No entanto, para este tutorial, você definirá apenas um.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="3b5d7-216">Esta etapa configura um serviço que usa o padrão de saudação definida anteriormente **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="3b5d7-217">Ele também usa o padrão de saudação **sbTokenProvider**, que é definida na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="3b5d7-218">Depois de saudação `<services>` elemento, criar um `<behaviors>` elemento com hello conteúdo a seguir, substituindo "SAS_KEY" com hello *assinatura de acesso compartilhado* chave (SAS) obtido anteriormente Olá [portal do Azure ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3b5d7-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="3b5d7-219">Ainda no App. config no hello `<appSettings>` elemento, substituir valor de cadeia de caracteres de conexão inteira Olá com a cadeia de caracteres de conexão de saudação obtido anteriormente do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="3b5d7-220">De saudação **criar** menu, clique em **compilar solução** toobuild Olá toda a solução.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="3b5d7-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3b5d7-221">Example</span></span>
<span data-ttu-id="3b5d7-222">Olá, código seguinte mostra Olá implementação de contrato e serviço para um serviço baseado em REST que está em execução no barramento de serviço usando Olá **WebHttpRelayBinding** associação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="3b5d7-223">Olá, exemplo a seguir mostra arquivo App. config de saudação associado ao serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
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

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="3b5d7-224">Etapa 4: Host Olá WCF com base em REST serviço toouse retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="3b5d7-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="3b5d7-225">Essa etapa descreve como toorun um web serviço usando um aplicativo de console com retransmissão do WCF.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="3b5d7-226">Uma lista completa de código Olá gravado nesta etapa é fornecida no exemplo hello Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="3b5d7-227">um endereço base para o serviço de saudação do toocreate</span><span class="sxs-lookup"><span data-stu-id="3b5d7-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="3b5d7-228">Em Olá `Main()` declaração de função, criar um namespace de saudação toostore variável do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="3b5d7-229">Certifique-se de que tooreplace `yourNamespace` com o nome de saudação do namespace de retransmissão Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="3b5d7-230">Barramento de serviço usa o nome de saudação do seu namespace de toocreate um URI exclusivo.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="3b5d7-231">Criar um `Uri` instância para endereço básico de saudação do serviço de saudação que é baseado no namespace de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="3b5d7-232">toocreate e configurar o host de serviço da web hello</span><span class="sxs-lookup"><span data-stu-id="3b5d7-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="3b5d7-233">Crie o host de serviço web hello, usando o endereço URI Olá criado anteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="3b5d7-234">host de serviço de saudação é objeto WCF Olá que instancia o aplicativo de host hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="3b5d7-235">Este exemplo passa o tipo de saudação de host que você deseja toocreate (um **ImageService**), e também Olá endereço no qual você deseja que o aplicativo de host tooexpose hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="3b5d7-236">host de serviço toorun Olá web</span><span class="sxs-lookup"><span data-stu-id="3b5d7-236">toorun hello web service host</span></span>
1. <span data-ttu-id="3b5d7-237">Abra o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="3b5d7-238">serviço de saudação agora está em execução.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-238">hello service is now running.</span></span>
2. <span data-ttu-id="3b5d7-239">Exiba uma mensagem indicando que o serviço hello está sendo executado e como toostop Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="3b5d7-240">Quando terminar, feche o host de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="3b5d7-241">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3b5d7-241">Example</span></span>
<span data-ttu-id="3b5d7-242">saudação de exemplo a seguir inclui o contrato de serviço hello e a implementação de etapas anteriores no serviço de saudação tutorial e hosts de saudação em um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="3b5d7-243">Compile Olá código a seguir em um executável chamado ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="3b5d7-244">Compilando o código de saudação</span><span class="sxs-lookup"><span data-stu-id="3b5d7-244">Compiling hello code</span></span>
<span data-ttu-id="3b5d7-245">Depois de criar a solução hello, Olá toorun Olá aplicativos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b5d7-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="3b5d7-246">Pressione **F5**, ou procure o local do arquivo executável toohello (ImageListener\bin\Debug\ImageListener.exe), serviço de saudação toorun.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="3b5d7-247">Lembre-Olá aplicativo em execução, pois ela será necessária a próxima etapa do tooperform Olá.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="3b5d7-248">Copie e cole o endereço de saudação do prompt de comando de saudação em uma imagem de saudação do navegador toosee.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="3b5d7-249">Quando tiver terminado, pressione **Enter** no aplicativo de Olá Olá prompt de comando janela tooclose.</span><span class="sxs-lookup"><span data-stu-id="3b5d7-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b5d7-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b5d7-250">Next steps</span></span>
<span data-ttu-id="3b5d7-251">Agora que você construiu um aplicativo que usa o serviço de retransmissão do barramento de serviço hello, consulte Olá toolearn artigos mais sobre Azure retransmissão a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b5d7-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="3b5d7-252">Visão geral da arquitetura de Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="3b5d7-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="3b5d7-253">Visão geral da Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="3b5d7-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="3b5d7-254">Como o serviço com o .NET de retransmissão toouse Olá WCF</span><span class="sxs-lookup"><span data-stu-id="3b5d7-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
