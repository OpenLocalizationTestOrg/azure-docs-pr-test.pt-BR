---
title: "aaaAzure aplicativo de no local/em nuvem híbrido de retransmissão do WCF (.NET) | Microsoft Docs"
description: "Saiba como aplicativo híbrido de toocreate uma .NET no local/em nuvem usando a retransmissão do WCF do Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="e4de7-103">Aplicativo híbrido .NET local/na nuvem usando a Retransmissão do WCF do Azure</span><span class="sxs-lookup"><span data-stu-id="e4de7-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="e4de7-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="e4de7-104">Introduction</span></span>

<span data-ttu-id="e4de7-105">Este artigo mostra como toobuild híbridos nuvem aplicativo com o Microsoft Azure e o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4de7-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="e4de7-106">tutorial de Olá pressupõe não que nenhuma experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="e4de7-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="e4de7-107">Em menos de 30 minutos, você terá um aplicativo que utiliza vários recursos do Azure e em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="e4de7-108">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="e4de7-108">You will learn:</span></span>

* <span data-ttu-id="e4de7-109">Como toocreate ou adaptar um serviço da web existente para consumo por uma solução de web.</span><span class="sxs-lookup"><span data-stu-id="e4de7-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="e4de7-110">Como toouse Olá tooshare dados do serviço de retransmissão do WCF do Azure entre um aplicativo do Azure e um serviço web hospedado em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="e4de7-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="e4de7-111">Como a Retransmissão do Azure ajuda com soluções híbridas</span><span class="sxs-lookup"><span data-stu-id="e4de7-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="e4de7-112">Soluções de negócios são geralmente compostas de uma combinação de código personalizado escrito tootackle novo e necessidades de negócios e a funcionalidade existente fornecidas por soluções e os sistemas que já estão em vigor.</span><span class="sxs-lookup"><span data-stu-id="e4de7-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="e4de7-113">Arquitetos de solução estão começando a nuvem de saudação toouse para manipular mais fácil de reduzir os custos operacionais e de requisitos de escala.</span><span class="sxs-lookup"><span data-stu-id="e4de7-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="e4de7-114">Dessa forma, eles localizam que ativos existentes do serviço eles gostariam tooleverage como blocos de construção para suas soluções estão dentro do firewall corporativo hello e fora de fácil acessar para acesso pela solução de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="e4de7-115">Muitos serviços internos não são criados ou hospedados de forma que eles podem ser facilmente expostos na borda da rede corporativa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="e4de7-116">[Retransmissão do Azure](https://azure.microsoft.com/services/service-bus/) foi projetado para Olá caso de uso de executar os serviços de web do Windows Communication Foundation (WCF) existentes e tornar os serviços acessíveis com segurança toosolutions que residem fora do perímetro corporativo Olá sem a necessidade de infraestrutura de rede corporativa toohello alterações intrusiva.</span><span class="sxs-lookup"><span data-stu-id="e4de7-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="e4de7-117">Esses serviços de retransmissão ainda estão hospedados dentro de seu ambiente existente, mas eles delegarem para o serviço de retransmissão hospedado na nuvem de toohello entrado de sessões e solicitações de escuta.</span><span class="sxs-lookup"><span data-stu-id="e4de7-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="e4de7-118">A Retransmissão do Azure também protege esses serviços contra acesso não autorizado usando a autenticação [SAS (Assinatura de Acesso Compartilhado)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="e4de7-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="e4de7-119">Cenário da solução</span><span class="sxs-lookup"><span data-stu-id="e4de7-119">Solution scenario</span></span>
<span data-ttu-id="e4de7-120">Neste tutorial, você criará um site ASP.NET que permite que você toosee uma lista de produtos na página de estoque de produto hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="e4de7-121">tutorial de saudação presume que você tem informações de produto em um sistema local existente e usa o Azure retransmissão tooreach no sistema.</span><span class="sxs-lookup"><span data-stu-id="e4de7-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="e4de7-122">Isso é simulado por um serviço Web executado em um aplicativo de console simples e com o suporte de um conjunto de produtos na memória.</span><span class="sxs-lookup"><span data-stu-id="e4de7-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="e4de7-123">Você será capaz de toorun esse aplicativo de console em seu próprio computador e implantar a função de web Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="e4de7-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="e4de7-124">Fazendo isso, você verá como função de web hello em execução no hello datacenter do Azure, na verdade, chamará em seu computador, mesmo que seu computador certamente residirá por trás de pelo menos um firewall e uma camada de conversão (NAT) do endereço de rede.</span><span class="sxs-lookup"><span data-stu-id="e4de7-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="e4de7-125">Configurar o ambiente de desenvolvimento Olá</span><span class="sxs-lookup"><span data-stu-id="e4de7-125">Set up hello development environment</span></span>

<span data-ttu-id="e4de7-126">Antes de começar a desenvolver aplicativos do Azure, baixe ferramentas hello e configurar seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="e4de7-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="e4de7-127">Instalar hello Azure SDK para .NET de saudação SDK [página de downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e4de7-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="e4de7-128">Em Olá **.NET** coluna, clique na versão de saudação do [Visual Studio](http://www.visualstudio.com) você está usando.</span><span class="sxs-lookup"><span data-stu-id="e4de7-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="e4de7-129">Olá as etapas deste tutorial usam Visual Studio 2015, mas elas também funcionam com o Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="e4de7-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="e4de7-130">Quando solicitado toorun ou salvar instalador hello, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="e4de7-131">Em Olá **Web Platform Installer**, clique em **instalar** e prosseguir com a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="e4de7-132">Após a conclusão da instalação hello, você terá tudo necessário toostart toodevelop Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="e4de7-133">Olá SDK inclui ferramentas que permitem a fácil desenvolver aplicativos do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4de7-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="e4de7-134">Criar um namespace</span><span class="sxs-lookup"><span data-stu-id="e4de7-134">Create a namespace</span></span>

<span data-ttu-id="e4de7-135">usando toobegin Olá recursos de retransmissão no Azure, você deve primeiro criar um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="e4de7-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="e4de7-136">Um namespace fornece um contêiner de escopo para endereçar recursos do Azure dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="e4de7-137">Siga Olá [as instruções aqui](relay-create-namespace-portal.md) toocreate um namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="e4de7-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="e4de7-138">Criar um servidor local</span><span class="sxs-lookup"><span data-stu-id="e4de7-138">Create an on-premises server</span></span>

<span data-ttu-id="e4de7-139">Primeiro você irá criar um sistema de catálogo de produtos (fictício) local.</span><span class="sxs-lookup"><span data-stu-id="e4de7-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="e4de7-140">É bem simple; Você pode ver isso como a representação de um sistema de catálogo de produto real no local com uma superfície de serviço completo que estamos tentando toointegrate.</span><span class="sxs-lookup"><span data-stu-id="e4de7-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="e4de7-141">Este projeto é um aplicativo de console do Visual Studio e usa Olá [pacote NuGet do Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Olá bibliotecas de barramento de serviço e as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="e4de7-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="e4de7-142">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="e4de7-142">Create hello project</span></span>

1. <span data-ttu-id="e4de7-143">Utilizando privilégios do administrador, inicie o Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4de7-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="e4de7-144">toodo então, clique no ícone de programa do Visual Studio hello e clique **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="e4de7-145">No Visual Studio, no hello **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="e4de7-146">Em **Modelos Instalados**, em **Visual C#**, clique em **Aplicativo de Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="e4de7-147">Em Olá **nome** caixa, digite o nome de saudação **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="e4de7-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="e4de7-148">Clique em **Okey** toocreate Olá **ProductsServer** projeto.</span><span class="sxs-lookup"><span data-stu-id="e4de7-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="e4de7-149">Se você já tiver instalado o Gerenciador de pacotes do NuGet Olá para o Visual Studio, ignore toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e4de7-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="e4de7-150">Caso contrário, visite [NuGet][NuGet] e clique em [Instalar NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span><span class="sxs-lookup"><span data-stu-id="e4de7-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="e4de7-151">Siga os prompts Olá Olá tooinstall Gerenciador do pacote NuGet, em seguida, reinicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4de7-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="e4de7-152">No Gerenciador de soluções, clique com botão direito Olá **ProductsServer** projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="e4de7-153">Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="e4de7-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="e4de7-154">Selecione Olá **windowsazure. ServiceBus** pacote.</span><span class="sxs-lookup"><span data-stu-id="e4de7-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="e4de7-155">Clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="e4de7-156">Observe que Olá necessário assemblies de cliente agora são referenciados.</span><span class="sxs-lookup"><span data-stu-id="e4de7-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="e4de7-157">Adicione uma nova classe para seu contrato de produto.</span><span class="sxs-lookup"><span data-stu-id="e4de7-157">Add a new class for your product contract.</span></span> <span data-ttu-id="e4de7-158">No Gerenciador de soluções, clique com botão direito Olá **ProductsServer** do projeto e clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="e4de7-159">Em Olá **nome** caixa, digite o nome de saudação **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="e4de7-160">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-160">Then click **Add**.</span></span>
10. <span data-ttu-id="e4de7-161">Em **ProductsContract.cs**, substitua definição de namespace Olá Olá código, que define o contrato de saudação para serviço de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4de7-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="e4de7-162">Em Program.cs, substitua definição de namespace Olá Olá seguindo o código, que adiciona o serviço de perfil hello e host Olá para ele.</span><span class="sxs-lookup"><span data-stu-id="e4de7-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="e4de7-163">No Solution Explorer, clique duas vezes em Olá **App. config** arquivo tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="e4de7-164">Na parte inferior de saudação do hello `<system.ServiceModel>` elemento (mas ainda dentro `<system.ServiceModel>`), adicionar Olá código XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4de7-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="e4de7-165">Ser tooreplace se *yourServiceNamespace* com o nome de saudação do seu namespace, e *yourKey* com a chave SAS Olá anteriormente, você recuperou do portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="e4de7-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="e4de7-166">Ainda no App. config no hello `<appSettings>` elemento, substituir valor de cadeia de caracteres de conexão Olá com a cadeia de caracteres de conexão de saudação obtido anteriormente do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="e4de7-167">Pressione **Ctrl + Shift + B** ou de saudação **criar** menu, clique em **compilar solução** toobuild Olá aplicativo e verificar a precisão de saudação do seu trabalho até o momento.</span><span class="sxs-lookup"><span data-stu-id="e4de7-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="e4de7-168">Criar um aplicativo ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e4de7-168">Create an ASP.NET application</span></span>

<span data-ttu-id="e4de7-169">Nesta seção você criará um aplicativo ASP.NET simples que exibe os dados recuperados do seu serviço de produto.</span><span class="sxs-lookup"><span data-stu-id="e4de7-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="e4de7-170">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="e4de7-170">Create hello project</span></span>

1. <span data-ttu-id="e4de7-171">Certifique-se de que o Visual Studio está sendo executado com os privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="e4de7-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="e4de7-172">No Visual Studio, no hello **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="e4de7-173">Em **Modelos Instalados**, em **Visual C#**, clique em **Aplicativo Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="e4de7-174">Projeto de saudação do nome **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="e4de7-175">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="e4de7-176">De saudação **modelos ASP.NET** lista Olá **novo aplicativo Web ASP.NET** caixa de diálogo, clique em **MVC**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="e4de7-177">Clique em Olá **alterar autenticação** botão.</span><span class="sxs-lookup"><span data-stu-id="e4de7-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="e4de7-178">Em Olá **alterar autenticação** caixa de diálogo caixa, certifique-se de que **sem autenticação** está selecionado e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="e4de7-179">Para este tutorial, você está implantando um aplicativo que não precisa de um logon de usuário.</span><span class="sxs-lookup"><span data-stu-id="e4de7-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="e4de7-180">Em Olá **novo aplicativo Web ASP.NET** caixa de diálogo, clique em **Okey** toocreate Olá MVC aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="e4de7-181">Agora você deve configurar os recursos do Azure para um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e4de7-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="e4de7-182">Siga as etapas de Olá Olá [publicar tooAzure seção deste artigo](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e4de7-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="e4de7-183">Em seguida, retorne toothis tutorial e continue toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e4de7-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="e4de7-184">No Gerenciador de Soluções, clique com o botão direito do mouse em **Modelos**, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="e4de7-185">Em Olá **nome** caixa, digite o nome de saudação **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="e4de7-186">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="e4de7-187">Modificar o aplicativo da web hello</span><span class="sxs-lookup"><span data-stu-id="e4de7-187">Modify hello web application</span></span>

1. <span data-ttu-id="e4de7-188">No arquivo de Product.cs Olá no Visual Studio, substitua definição de namespace existentes Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4de7-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="e4de7-189">No Gerenciador de soluções, expanda Olá **controladores** pasta, clique duas vezes em hello **HomeController** tooopen de arquivo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4de7-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="e4de7-190">Em **HomeController**, substitua definição de namespace existentes Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4de7-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="e4de7-191">No Gerenciador de soluções, expanda a pasta exibições \ compartilhadas de saudação e, em seguida, clique duas vezes em **cshtml** tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="e4de7-192">Alterar todas as ocorrências de **meu aplicativo ASP.NET** muito**produtos da LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="e4de7-193">Remover Olá **início**, **sobre**, e **contato** links.</span><span class="sxs-lookup"><span data-stu-id="e4de7-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="e4de7-194">Olá exemplo a seguir, exclua código Olá realçado.</span><span class="sxs-lookup"><span data-stu-id="e4de7-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="e4de7-195">No Gerenciador de soluções, expanda a pasta de Views\Home de saudação e, em seguida, clique duas vezes em **cshtml** tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="e4de7-196">Substitua todo o conteúdo do arquivo de Olá Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4de7-196">Replace hello entire contents of hello file with hello following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="e4de7-197">precisão de saudação tooverify de seu trabalho até o momento, você pode pressionar **Ctrl + Shift + B** toobuild projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="e4de7-198">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="e4de7-198">Run hello app locally</span></span>

<span data-ttu-id="e4de7-199">Execute Olá aplicativo tooverify que ele funciona.</span><span class="sxs-lookup"><span data-stu-id="e4de7-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="e4de7-200">Certifique-se de que **ProductsPortal** é saudação do projeto ativo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="e4de7-201">Nome do projeto Olá no Gerenciador de soluções e selecione **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="e4de7-202">No Visual Studio, pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="e4de7-203">Seu aplicativo deve aparecer em execução em um navegador.</span><span class="sxs-lookup"><span data-stu-id="e4de7-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="e4de7-204">Juntar Olá peças</span><span class="sxs-lookup"><span data-stu-id="e4de7-204">Put hello pieces together</span></span>

<span data-ttu-id="e4de7-205">Olá próxima etapa é toohook servidor de produtos de local de saudação com hello aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e4de7-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="e4de7-206">Se ainda não estiver aberto, no Visual Studio reabra Olá **ProductsPortal** projeto criado no hello [criar um aplicativo ASP.NET](#create-an-aspnet-application) seção.</span><span class="sxs-lookup"><span data-stu-id="e4de7-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="e4de7-207">Etapa de toohello semelhante na seção de "Criar um servidor de local" Olá, adicionar referências de projeto toohello do pacote de NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="e4de7-208">No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="e4de7-209">Pesquisa por "Service Bus" e selecione Olá **windowsazure. ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="e4de7-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="e4de7-210">Em seguida, concluir instalação hello e fechar esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="e4de7-211">No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** projeto e, em seguida, clique em **adicionar**, em seguida, **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="e4de7-212">Navegue toohello **ProductsContract.cs** arquivo hello **ProductsServer** projeto de console.</span><span class="sxs-lookup"><span data-stu-id="e4de7-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="e4de7-213">Clique em toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="e4de7-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="e4de7-214">Clique Olá a seta para baixo próxima muito**adicionar**, em seguida, clique em **adicionar como vínculo**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="e4de7-215">Agora, abra Olá **HomeController** no editor do Visual Studio hello e substitua a definição de namespace Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4de7-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="e4de7-216">Ser tooreplace se *yourServiceNamespace* com o nome de saudação do seu namespace de serviço, e *yourKey* com a sua chave SAS.</span><span class="sxs-lookup"><span data-stu-id="e4de7-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="e4de7-217">Isso permitirá que o serviço Olá cliente toocall Olá local, retornando resultados de saudação da chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="e4de7-218">No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** solução (certifique-se de que tooright Olá solução clique, não o projeto Olá).</span><span class="sxs-lookup"><span data-stu-id="e4de7-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="e4de7-219">Clique em **Adicionar** e depois clique em **Projeto Existente**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="e4de7-220">Navegue toohello **ProductsServer** de projeto, clique duas vezes Olá **ProductsServer.csproj** tooadd do arquivo de solução-lo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="e4de7-221">**ProductsServer** devem ser executadas nos dados de saudação do pedido toodisplay na **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="e4de7-222">No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** solução e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="e4de7-223">Olá **páginas de propriedade** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="e4de7-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="e4de7-224">No lado esquerdo de saudação, clique em **projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="e4de7-225">Saudação de direita, clique em **vários projetos de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="e4de7-226">Certifique-se de que **ProductsServer** e **ProductsPortal** aparecer, em ordem, com **iniciar** definido como ação Olá para ambos.</span><span class="sxs-lookup"><span data-stu-id="e4de7-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="e4de7-227">Ainda no hello **propriedades** caixa de diálogo, clique em **dependências do projeto** no lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="e4de7-228">Em Olá **projetos** lista, clique em **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="e4de7-229">Confirme se **ProductsPortal** não está selecionado.</span><span class="sxs-lookup"><span data-stu-id="e4de7-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="e4de7-230">Em Olá **projetos** lista, clique em **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="e4de7-231">Verifique se **ServidorDeProdutos** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="e4de7-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="e4de7-232">Clique em **Okey** em Olá **páginas de propriedade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="e4de7-233">Executar projeto Olá localmente</span><span class="sxs-lookup"><span data-stu-id="e4de7-233">Run hello project locally</span></span>

<span data-ttu-id="e4de7-234">aplicativo de hello tootest localmente, no Visual Studio pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="e4de7-235">servidor de local de saudação (**ProductsServer**) deve iniciar primeiro, Olá **ProductsPortal** aplicativo deve ser iniciado em uma janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="e4de7-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="e4de7-236">Neste momento, você verá que o inventário de produto Olá lista os dados recuperados do hello produto serviço no sistema local.</span><span class="sxs-lookup"><span data-stu-id="e4de7-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="e4de7-237">Pressione **atualizar** em Olá **ProductsPortal** página.</span><span class="sxs-lookup"><span data-stu-id="e4de7-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="e4de7-238">Cada vez que você atualize a página de saudação, você verá Olá server app exibirá uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.</span><span class="sxs-lookup"><span data-stu-id="e4de7-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="e4de7-239">Feche ambos os aplicativos antes da próxima etapa de toohello de continuar.</span><span class="sxs-lookup"><span data-stu-id="e4de7-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="e4de7-240">Implantar o aplicativo web do Azure do hello ProductsPortal projeto tooan</span><span class="sxs-lookup"><span data-stu-id="e4de7-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="e4de7-241">Olá próxima etapa é toorepublish hello Azure Web aplicativo **ProductsPortal** front-end.</span><span class="sxs-lookup"><span data-stu-id="e4de7-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="e4de7-242">Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4de7-242">Do hello following:</span></span>

1. <span data-ttu-id="e4de7-243">No Gerenciador de soluções, clique com botão direito Olá **ProductsPortal** do projeto e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="e4de7-244">Em seguida, clique em **publicar** em Olá **publicar** página.</span><span class="sxs-lookup"><span data-stu-id="e4de7-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e4de7-245">Você verá uma mensagem de erro na janela de navegador hello quando hello **ProductsPortal** projeto da web é iniciado automaticamente após a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="e4de7-246">Isso é esperado e ocorre porque Olá **ProductsServer** aplicativo não está sendo executado ainda.</span><span class="sxs-lookup"><span data-stu-id="e4de7-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="e4de7-247">Copiar URL de saudação do hello implantado aplicativo web, pois você precisará Olá URL na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="e4de7-248">Você também pode obter essa URL da janela de atividade de serviço de aplicativo do Azure Olá no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e4de7-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="e4de7-249">Feche Olá navegador janela toostop Olá executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="e4de7-250">Defina ProductsPortal como o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e4de7-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="e4de7-251">Antes da aplicação de saudação em execução na nuvem hello, você deve garantir que **ProductsPortal** é iniciado a partir do Visual Studio como um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e4de7-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="e4de7-252">No Visual Studio, clique com botão direito Olá **ProductsPortal** do projeto e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="e4de7-253">Na coluna esquerda da saudação, clique em **Web**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="e4de7-254">Em Olá **iniciar ação** seção, clique em Olá **iniciar URL** botão e, na caixa de texto de saudação digite Olá URL para seu aplicativo da web implantados anteriormente; por exemplo, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="e4de7-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="e4de7-255">De saudação **arquivo** no Visual Studio, clique em **Salvar tudo**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="e4de7-256">No menu de compilação Olá no Visual Studio, clique em **recompilar solução**.</span><span class="sxs-lookup"><span data-stu-id="e4de7-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="e4de7-257">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="e4de7-257">Run hello application</span></span>

1. <span data-ttu-id="e4de7-258">Pressione F5 toobuild e execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e4de7-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="e4de7-259">servidor de local de Hello (Olá **ProductsServer** aplicativo de console) deve iniciar primeiro, Olá **ProductsPortal** aplicativo deve ser iniciado em uma janela de navegador, conforme mostrado no hello tela a seguir captura.</span><span class="sxs-lookup"><span data-stu-id="e4de7-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="e4de7-260">Observe novamente que o inventário de produto Olá lista os dados recuperados do sistema de local de serviço de produto hello e exibe esses dados de aplicativo da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="e4de7-261">Verificar Olá URL toomake-se de que **ProductsPortal** está em execução na nuvem hello, como um aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4de7-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="e4de7-262">Olá **ProductsServer** aplicativo de console deve estar em execução e é capaz de tooserve Olá dados toohello **ProductsPortal** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e4de7-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="e4de7-263">Se o navegador Olá exibirá um erro, aguarde alguns segundos mais para **ProductsServer** tooload e hello de exibição a seguir da mensagem.</span><span class="sxs-lookup"><span data-stu-id="e4de7-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="e4de7-264">Em seguida, pressione **atualização** no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4de7-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="e4de7-265">No navegador de hello, pressione **atualizar** em Olá **ProductsPortal** página.</span><span class="sxs-lookup"><span data-stu-id="e4de7-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="e4de7-266">Cada vez que você atualize a página de saudação, você verá Olá server app exibirá uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.</span><span class="sxs-lookup"><span data-stu-id="e4de7-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="e4de7-267">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4de7-267">Next steps</span></span>

<span data-ttu-id="e4de7-268">toolearn mais informações sobre a retransmissão do Azure, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4de7-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="e4de7-269">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="e4de7-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="e4de7-270">Como toouse de retransmissão</span><span class="sxs-lookup"><span data-stu-id="e4de7-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
