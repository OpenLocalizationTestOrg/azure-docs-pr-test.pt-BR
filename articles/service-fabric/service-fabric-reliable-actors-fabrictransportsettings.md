---
title: "configurações de FabricTransport aaaChange no Azure microservices | Microsoft Docs"
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
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="dbb11-103">Definir as configurações de FabricTransport para os Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="dbb11-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="dbb11-104">Aqui estão as configurações de saudação que você pode configurar:</span><span class="sxs-lookup"><span data-stu-id="dbb11-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="dbb11-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="dbb11-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="dbb11-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="dbb11-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="dbb11-107">Você pode modificar a configuração padrão de saudação do FabricTransport maneiras a seguir.</span><span class="sxs-lookup"><span data-stu-id="dbb11-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="dbb11-108">Atributo de assembly</span><span class="sxs-lookup"><span data-stu-id="dbb11-108">Assembly attribute</span></span>

<span data-ttu-id="dbb11-109">Olá [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) atributo precisa toobe aplicado em assemblies de serviço Olá ator cliente e ator.</span><span class="sxs-lookup"><span data-stu-id="dbb11-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="dbb11-110">saudação de exemplo a seguir mostra como toochange Olá valor padrão de FabricTransport OperationTimeout configurações:</span><span class="sxs-lookup"><span data-stu-id="dbb11-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="dbb11-111">O segundo exemplo altera os valores padrão de FabricTransport MaxMessageSize e OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="dbb11-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="dbb11-112">Pacote de configuração</span><span class="sxs-lookup"><span data-stu-id="dbb11-112">Config package</span></span>

<span data-ttu-id="dbb11-113">Você pode usar um [pacote de configuração](service-fabric-application-model.md) configuração do toomodify saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="dbb11-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="dbb11-114">Definir configurações de FabricTransport para serviço de ator Olá</span><span class="sxs-lookup"><span data-stu-id="dbb11-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="dbb11-115">Adicione uma seção TransportSettings no arquivo settings.xml de saudação.</span><span class="sxs-lookup"><span data-stu-id="dbb11-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="dbb11-116">Por padrão, o código do ator procura SectionName como "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="dbb11-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="dbb11-117">Se isso não for encontrado, ele procurará SectionName como "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="dbb11-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

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

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="dbb11-118">Definir configurações de FabricTransport para o assembly de cliente de ator Olá</span><span class="sxs-lookup"><span data-stu-id="dbb11-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="dbb11-119">Se o cliente Olá não está em execução como parte de um serviço, você pode criar um "&lt;nome do Exe cliente&gt;. settings.xml" arquivo hello mesmo local do arquivo de .exe cliente hello.</span><span class="sxs-lookup"><span data-stu-id="dbb11-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="dbb11-120">Em seguida, adicione uma seção TransportSettings a esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="dbb11-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="dbb11-121">O SectionName deve ser "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="dbb11-121">SectionName should be "TransportSettings".</span></span>

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

  * <span data-ttu-id="dbb11-122">Definindo as configurações de FabricTransport do cliente/serviço de ator seguro com certificado secundário.</span><span class="sxs-lookup"><span data-stu-id="dbb11-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="dbb11-123">Informações de certificado secundário podem ser adicionadas, incluindo o parâmetro CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="dbb11-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="dbb11-124">Abaixo está o exemplo hello para Olá TransportSettings de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="dbb11-124">Below is hello example for hello Listener TransportSettings.</span></span>

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
     <span data-ttu-id="dbb11-125">Abaixo está o exemplo hello para Olá TransportSettings do cliente.</span><span class="sxs-lookup"><span data-stu-id="dbb11-125">Below is hello example for hello Client TransportSettings.</span></span>

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
    * <span data-ttu-id="dbb11-126">Definindo as configurações de FabricTransport do serviço/cliente do ator usando o nome do assunto.</span><span class="sxs-lookup"><span data-stu-id="dbb11-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="dbb11-127">Usuário necessidades tooprovide findType como FindBySubjectName, adicione os valores CertificateIssuerThumbprints e CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="dbb11-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="dbb11-128">Abaixo está o exemplo hello para Olá TransportSettings de ouvinte.</span><span class="sxs-lookup"><span data-stu-id="dbb11-128">Below is hello example for hello Listener TransportSettings.</span></span>

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
  <span data-ttu-id="dbb11-129">Abaixo está o exemplo hello para Olá TransportSettings do cliente.</span><span class="sxs-lookup"><span data-stu-id="dbb11-129">Below is hello example for hello Client TransportSettings.</span></span>

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
