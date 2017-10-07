---
title: "aaaWhat é um modelo de serviço de nuvem e o pacote | Microsoft Docs"
description: "Descreve o modelo de serviço de nuvem hello (. csdef,. cscfg) e o pacote (. cspkg) no Azure"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="3f7e9-103">O que é o modelo de serviço de nuvem hello e como empacotá-lo?</span><span class="sxs-lookup"><span data-stu-id="3f7e9-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="3f7e9-104">Um serviço de nuvem é criado de três componentes, definição de serviço Olá *(. csdef)*, Olá a configuração de serviço *(. cscfg)*e um pacote de serviço *(. cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="3f7e9-105">Ambos os Olá **servicedefinition. Csdef** e **ServiceConfig.cscfg** arquivos são baseados em XML e descrevem a estrutura de saudação do serviço de nuvem hello e como ele é configurado; coletivamente chamados de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="3f7e9-106">Olá **ServicePackage.cspkg** é um arquivo zip que é gerado a partir Olá **servicedefinition. Csdef** e entre outras coisas, contém todas as dependências de binário Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="3f7e9-107">O Azure cria um serviço de nuvem de ambos os Olá **ServicePackage.cspkg** e hello **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="3f7e9-108">Quando o serviço de nuvem Olá estiver em execução no Azure, você pode reconfigurá-lo por meio de saudação **ServiceConfig.cscfg** arquivo, mas você não pode alterar a definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="3f7e9-109">O que você gostaria que tooknow mais sobre?</span><span class="sxs-lookup"><span data-stu-id="3f7e9-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="3f7e9-110">Desejo tooknow mais sobre Olá [servicedefinition. Csdef](#csdef) e [ServiceConfig.cscfg](#cscfg) arquivos.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="3f7e9-111">Já sei sobre isso, dê-me [alguns exemplos](#next-steps) sobre o que posso configurar.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="3f7e9-112">Desejo Olá toocreate [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="3f7e9-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="3f7e9-113">Estou usando o Visual Studio e desejo...</span><span class="sxs-lookup"><span data-stu-id="3f7e9-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="3f7e9-114">[Criar um serviço de nuvem][vs_create]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="3f7e9-115">[Reconfigurar um serviço de nuvem existente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="3f7e9-116">[Implantar um projeto do serviço de nuvem][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="3f7e9-117">[Área de trabalho remota em uma instância de serviço de nuvem][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="3f7e9-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="3f7e9-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="3f7e9-119">Olá **servicedefinition. Csdef** arquivo Especifica configurações de saudação que são usadas pelo Azure tooconfigure um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="3f7e9-120">Olá [esquema de definição de serviço do Azure (arquivo. csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fornece o formato permitido Olá para um arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="3f7e9-121">Olá, exemplo a seguir mostra as configurações de saudação que podem ser definidas para Olá Web e funções de trabalho:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="3f7e9-122">Você pode consultar toohello [esquema de definição de serviço](https://msdn.microsoft.com/library/azure/ee758711.aspx) para melhor compreensão de esquema XML, Olá usada aqui, no entanto, aqui está uma breve explicação de alguns dos elementos de saudação:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="3f7e9-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-123">**Sites**</span></span>  
<span data-ttu-id="3f7e9-124">Contém definições de saudação para sites ou aplicativos web hospedados no IIS7.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="3f7e9-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-125">**InputEndpoints**</span></span>  
<span data-ttu-id="3f7e9-126">Contém definições de saudação para pontos de extremidade que usou o serviço de nuvem de saudação toocontact.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="3f7e9-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="3f7e9-128">Contém as definições de saudação para pontos de extremidade que são usados por toocommunicate de instâncias de função com o outro.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="3f7e9-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="3f7e9-130">Contém as definições de configuração Olá para recursos de uma função específica.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="3f7e9-131">**Certificados**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-131">**Certificates**</span></span>  
<span data-ttu-id="3f7e9-132">Contém definições de saudação para certificados que são necessários para uma função.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="3f7e9-133">o exemplo de código anterior Olá mostra um certificado que é usado para a configuração de saudação do Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="3f7e9-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-134">**LocalResources**</span></span>  
<span data-ttu-id="3f7e9-135">Contém definições de saudação para recursos de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="3f7e9-136">Um recurso de armazenamento local é um diretório reservado no sistema de arquivos de saudação da máquina virtual de saudação no qual uma instância de uma função está em execução.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="3f7e9-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-137">**Imports**</span></span>  
<span data-ttu-id="3f7e9-138">Contém definições de saudação para módulos importados.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="3f7e9-139">o exemplo de código anterior Olá mostra módulos Olá para Conexão de área de trabalho remota e o Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="3f7e9-140">**Inicialização**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-140">**Startup**</span></span>  
<span data-ttu-id="3f7e9-141">Contém tarefas que são executadas quando a função hello for iniciada.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="3f7e9-142">Olá tarefas são definidas em um arquivo executável ou. cmd.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="3f7e9-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="3f7e9-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="3f7e9-144">configuração de saudação de configurações de saudação para seu serviço de nuvem é determinada pelos valores Olá Olá **ServiceConfiguration** arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="3f7e9-145">Você especifica o número de saudação de instâncias que você deseja toodeploy para cada função nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="3f7e9-146">valores de Olá Olá as definições de configuração que você definiu no arquivo de definição de serviço Olá são adicionados toohello arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="3f7e9-147">impressões digitais de saudação para qualquer certificado de gerenciamento que estão associado com o serviço de nuvem Olá também são adicionadas toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="3f7e9-148">Olá [esquema de configuração de serviço do Azure (arquivo. cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fornece o formato permitido Olá para um arquivo de configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="3f7e9-149">Olá arquivo de configuração de serviço não é fornecido com o aplicativo hello, mas é tooAzure carregado como um arquivo separado e é usado tooconfigure hello serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="3f7e9-150">Você pode carregar um novo arquivo de configuração de serviço sem reimplantar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="3f7e9-151">os valores de configuração Olá Olá serviço de nuvem podem ser alterados enquanto o serviço de nuvem hello está em execução.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="3f7e9-152">Olá, exemplo a seguir mostra as definições de configuração de saudação que podem ser definidas para Olá Web e funções de trabalho:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="3f7e9-153">Você pode consultar toohello [esquema de configuração de serviço](https://msdn.microsoft.com/library/azure/ee758710.aspx) para melhor compreensão Olá esquema XML usado aqui, no entanto, aqui está uma breve explicação de elementos de saudação:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="3f7e9-154">**Instâncias**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-154">**Instances**</span></span>  
<span data-ttu-id="3f7e9-155">Configura o número de saudação de instâncias em execução para a função hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="3f7e9-156">tooprevent sua nuvem de serviço de fique indisponível durante atualizações, é recomendável que você implantar mais de uma instância de suas funções para a web.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="3f7e9-157">Ao implantar mais de uma instância, você está aderindo diretrizes toohello Olá [contrato de nível de serviço de computação do Azure (SLA)](http://azure.microsoft.com/support/legal/sla/), que garante 99,95% de conectividade externa para funções da Internet quando duas ou mais funções instâncias são implantadas para um serviço.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="3f7e9-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="3f7e9-159">Define as configurações de saudação para Olá instâncias em execução para uma função.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="3f7e9-160">nome de saudação do hello `<Setting>` elementos devem coincidir com as definições de configuração Olá no arquivo de definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="3f7e9-161">**Certificados**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-161">**Certificates**</span></span>  
<span data-ttu-id="3f7e9-162">Configura os certificados de saudação que são usados pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="3f7e9-163">o exemplo de código anterior Olá mostra como toodefine Olá certificado para o módulo RemoteAccess de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="3f7e9-164">Olá valor Olá *impressão digital* atributo deve ser definido como impressão digital de toohello de saudação toouse de certificado.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="3f7e9-165">pode ser adicionado a impressão digital de saudação do certificado de saudação toohello arquivo de configuração usando um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="3f7e9-166">Ou, Olá valor pode ser adicionado em Olá **certificados** guia da saudação **propriedades** página da função hello no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="3f7e9-167">Definindo as portas para instâncias de função</span><span class="sxs-lookup"><span data-stu-id="3f7e9-167">Defining ports for role instances</span></span>
<span data-ttu-id="3f7e9-168">O Azure permite apenas uma função de web tooa de ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="3f7e9-169">Isso significa que todo o tráfego ocorre por meio de um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="3f7e9-170">Você pode configurar seu sites tooshare uma porta Configurando Olá host cabeçalho toodirect Olá solicitação toohello local correto.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="3f7e9-171">Você também pode configurar as portas do aplicativos toolisten toowell conhecidas no endereço IP hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="3f7e9-172">Olá, exemplo a seguir mostra a configuração Olá para uma função web com um aplicativo web e o site.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="3f7e9-173">Olá site está configurado como local de entrada hello padrão na porta 80 e aplicativos da web de saudação são solicitações tooreceive configurado de um cabeçalho de host alternativo que é chamado de "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="3f7e9-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="3f7e9-174">Alterando a configuração de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="3f7e9-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="3f7e9-175">Você pode atualizar a configuração de saudação de seu serviço de nuvem enquanto está em execução no Azure, sem colocar offline o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="3f7e9-176">toochange informações de configuração, você pode carregar um novo arquivo de configuração ou editar Olá arquivo de configuração de colocar e aplicá-lo tooyour executando o serviço.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="3f7e9-177">Olá alterações a seguir podem ser feitas toohello configuração de um serviço:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="3f7e9-178">**Alterando os valores hello definições de configuração**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="3f7e9-179">Quando uma configuração de alterações, de configuração uma instância de função pode escolher tooapply Olá alteração Olá instância está online ou toorecycle Olá instância normalmente e aplique a alteração de saudação enquanto Olá instância está offline.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="3f7e9-180">**A alteração de topologia do serviço de saudação de instâncias de função**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="3f7e9-181">As alterações da topologia não afetam as instâncias em execução, exceto quando uma instância está sendo removida.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="3f7e9-182">Todas as instâncias restantes geralmente não é necessário toobe reciclado; No entanto, você pode escolher toorecycle instâncias de função na alteração de topologia de tooa de resposta.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="3f7e9-183">**Alterando a impressão digital do certificado Olá**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="3f7e9-184"> Somente é possível atualizar um certificado quando uma instância de função está offline.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="3f7e9-185">Se um certificado for adicionado, excluído ou alterado enquanto uma instância de função estiver online, o Azure normalmente usa certificados de Olá Olá instância tooupdate off-line e colocá-lo novamente online após a conclusão da alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="3f7e9-186">Tratando alterações de configuração com eventos de tempo de execução do serviço</span><span class="sxs-lookup"><span data-stu-id="3f7e9-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="3f7e9-187">Olá [biblioteca de tempo de execução do Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) inclui Olá [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, que fornece classes para interagir com hello ambiente do Azure de uma função.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="3f7e9-188">Olá [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) classe define Olá eventos que são disparados antes e após uma alteração de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="3f7e9-189">**[Alterando](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) eventos**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="3f7e9-190">Isso ocorre antes que alterações de configuração de saudação tooa aplicada a instância especificada de uma função fornecendo tootake uma chance para instâncias de função hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="3f7e9-191">**[Evento](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) alterado**</span><span class="sxs-lookup"><span data-stu-id="3f7e9-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="3f7e9-192">Ocorre após a alteração de configuração Olá tooa aplicada a instância especificada de uma função.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="3f7e9-193">Como alterações de certificado sempre usa instâncias de saudação de uma função off-line, elas não geram eventos de saudação Changing ou RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="3f7e9-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="3f7e9-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="3f7e9-195">toodeploy um aplicativo como um serviço de nuvem no Azure, você deve primeiro aplicativo hello de pacote no formato apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="3f7e9-196">Você pode usar o hello **CSPack** ferramenta de linha de comando (instalado com hello [SDK do Azure](https://azure.microsoft.com/downloads/)) toocreate arquivo de pacote hello como uma alternativa tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="3f7e9-197">**CSPack** usa Olá conteúdo da saudação serviço definição serviço de configuração toodefine Olá conteúdo do arquivo de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="3f7e9-198">**CSPack** gera um arquivo de pacote de aplicativo (. cspkg) que você pode carregar tooAzure usando Olá [portal do Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="3f7e9-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="3f7e9-199">Por padrão, o pacote de saudação é chamado `[ServiceDefinitionFileName].cspkg`, mas você pode especificar um nome diferente usando Olá `/out` opção de **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="3f7e9-200">**CSPack** está localizado em</span><span class="sxs-lookup"><span data-stu-id="3f7e9-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="3f7e9-201">CSPack.exe (no windows) está disponível executando Olá **Prompt de comando do Microsoft Azure** atalho que é instalado com o SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="3f7e9-202">Execute o programa de CSPack.exe de saudação por si só toosee documentação sobre todas as opções possíveis hello e comandos.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="3f7e9-203">Executar seu serviço de nuvem localmente no hello **emulador de computação do Microsoft Azure**, use Olá **/copyonly** opção.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="3f7e9-204">Esta opção copia arquivos binários de saudação para layout de diretório Olá aplicativo tooa do qual eles podem ser executados no emulador de computação hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="3f7e9-205">Comando de exemplo toopackage um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="3f7e9-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="3f7e9-206">Olá, exemplo a seguir cria um pacote de aplicativo que contém informações de saudação para uma função web.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="3f7e9-207">comando Olá Especifica Olá toouse de arquivo de definição de serviço, diretório Olá onde os arquivos binários podem ser encontrado e Olá o nome do arquivo de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="3f7e9-208">Se o aplicativo hello contém uma função web e uma função de trabalho, hello comando a seguir é usado:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="3f7e9-209">Onde as variáveis de saudação são definidas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3f7e9-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="3f7e9-210">Variável</span><span class="sxs-lookup"><span data-stu-id="3f7e9-210">Variable</span></span> | <span data-ttu-id="3f7e9-211">Valor</span><span class="sxs-lookup"><span data-stu-id="3f7e9-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3f7e9-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-212">\[DirectoryName\]</span></span> |<span data-ttu-id="3f7e9-213">Olá subdiretório no diretório do projeto Olá raiz que contém o arquivo. csdef Olá Olá projeto do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="3f7e9-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="3f7e9-215">nome de saudação do arquivo de definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-215">hello name of hello service definition file.</span></span> <span data-ttu-id="3f7e9-216">Por padrão, esse arquivo é chamado de ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="3f7e9-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-217">\[OutputFileName\]</span></span> |<span data-ttu-id="3f7e9-218">nome Olá Olá gerou o arquivo de pacote.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-218">hello name for hello generated package file.</span></span> <span data-ttu-id="3f7e9-219">Normalmente, isso é definido toohello nome do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="3f7e9-220">Se nenhum nome de arquivo for especificado, o pacote de aplicativo hello é criado como \[ApplicationName\]. cspkg.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="3f7e9-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-221">\[RoleName\]</span></span> |<span data-ttu-id="3f7e9-222">nome de saudação da função de saudação conforme definido no arquivo de definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="3f7e9-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="3f7e9-224">local de saudação de arquivos binários para função Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="3f7e9-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-225">\[VirtualPath\]</span></span> |<span data-ttu-id="3f7e9-226">diretórios físicos de saudação para cada caminho virtual definido na seção de Sites de saudação da definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="3f7e9-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="3f7e9-228">Olá diretórios físicos do conteúdo de saudação de cada caminho virtual definido no nó do site Olá da definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="3f7e9-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="3f7e9-230">nome de saudação do arquivo binário Olá função hello.</span><span class="sxs-lookup"><span data-stu-id="3f7e9-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f7e9-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f7e9-231">Next steps</span></span>
<span data-ttu-id="3f7e9-232">Estou criando um pacote de serviço de nuvem e desejo...</span><span class="sxs-lookup"><span data-stu-id="3f7e9-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="3f7e9-233">[Configurar área de trabalho remota para uma instância de serviço de nuvem][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="3f7e9-234">[Implantar um projeto do serviço de nuvem][deploy]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="3f7e9-235">Estou usando o Visual Studio e desejo...</span><span class="sxs-lookup"><span data-stu-id="3f7e9-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="3f7e9-236">[Criar um novo serviço de nuvem][vs_create]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="3f7e9-237">[Reconfigurar um serviço de nuvem existente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="3f7e9-238">[Implantar um projeto do serviço de nuvem][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="3f7e9-239">[Configurar área de trabalho remota para uma instância de serviço de nuvem][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="3f7e9-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
