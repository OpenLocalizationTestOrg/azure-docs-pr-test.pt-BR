---
title: "Alterar as configurações de FabricTransport nos microsserviços do Azure | Microsoft Docs"
description: "Saiba como definir as configurações de comunicação de ator do Azure Service Fabric."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="87e1d-103">Definir as configurações de FabricTransport para os Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="87e1d-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="87e1d-104">Aqui estão as configurações que você pode configurar:</span><span class="sxs-lookup"><span data-stu-id="87e1d-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="87e1d-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="87e1d-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="87e1d-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="87e1d-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="87e1d-107">Modifique a configuração padrão de FabricTransport das seguintes maneiras.</span><span class="sxs-lookup"><span data-stu-id="87e1d-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="87e1d-108">Atributo de assembly</span><span class="sxs-lookup"><span data-stu-id="87e1d-108">Assembly attribute</span></span>

<span data-ttu-id="87e1d-109">O atributo [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) precisa ser aplicado no cliente do ator e nos assemblies do serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="87e1d-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="87e1d-110">O exemplo a seguir mostra como alterar o valor padrão das configurações OperationTimeout do FabricTransport:</span><span class="sxs-lookup"><span data-stu-id="87e1d-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="87e1d-111">O segundo exemplo altera os valores padrão de FabricTransport MaxMessageSize e OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="87e1d-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="87e1d-112">Pacote de configuração</span><span class="sxs-lookup"><span data-stu-id="87e1d-112">Config package</span></span>

<span data-ttu-id="87e1d-113">Você pode usar um [pacote de configuração](service-fabric-application-model.md) para modificar a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="87e1d-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="87e1d-114">Definir as configurações do FabricTransport para o serviço de ator</span><span class="sxs-lookup"><span data-stu-id="87e1d-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="87e1d-115">Adicione uma seção TransportSettings no arquivo settings.xml.</span><span class="sxs-lookup"><span data-stu-id="87e1d-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="87e1d-116">Por padrão, o código do ator procura SectionName como "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="87e1d-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="87e1d-117">Se isso não for encontrado, ele procurará SectionName como "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="87e1d-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="87e1d-118">Definir as configurações do FabricTransport para o assembly do cliente do ator</span><span class="sxs-lookup"><span data-stu-id="87e1d-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="87e1d-119">Se o cliente não estiver sendo executado como parte de um serviço, você poderá criar um arquivo "&lt;Client Exe Name&gt;.settings.xml" no mesmo local do arquivo .exe do cliente.</span><span class="sxs-lookup"><span data-stu-id="87e1d-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="87e1d-120">Em seguida, adicione uma seção TransportSettings a esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="87e1d-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="87e1d-121">O SectionName deve ser "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="87e1d-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="87e1d-122">Definindo as configurações de FabricTransport do cliente/serviço de ator seguro com certificado secundário.</span><span class="sxs-lookup"><span data-stu-id="87e1d-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="87e1d-123">Informações de certificado secundário podem ser adicionadas, incluindo o parâmetro CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="87e1d-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="87e1d-124">Abaixo está o exemplo para o ouvinte TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="87e1d-124">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="87e1d-125">Abaixo está o exemplo para o cliente TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="87e1d-125">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="87e1d-126">Definindo as configurações de FabricTransport do serviço/cliente do ator usando o nome do assunto.</span><span class="sxs-lookup"><span data-stu-id="87e1d-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="87e1d-127">O usuário precisa fornecer findType como FindBySubjectName, adicionar valores CertificateIssuerThumbprints e CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="87e1d-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="87e1d-128">Abaixo está o exemplo para o ouvinte TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="87e1d-128">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="87e1d-129">Abaixo está o exemplo para o cliente TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="87e1d-129">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
