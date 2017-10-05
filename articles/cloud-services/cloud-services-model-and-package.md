---
title: "O que é um modelo do Serviço de Nuvem e pacote | Microsoft Docs"
description: "Descreve o modelo de serviço de nuvem (.csdef, .cscfg) e o pacote (.cspkg) no Azure"
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="13a52-103">Qual é o modelo de serviço de nuvem e como empacotá-lo?</span><span class="sxs-lookup"><span data-stu-id="13a52-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="13a52-104">Um serviço de nuvem é criado a partir de três componentes, a definição do serviço *(.csdef)*, configuração do serviço *(.cscfg)* e pacote do serviço *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="13a52-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="13a52-105">Os arquivos **ServiceDefinition.csdef** e **ServiceConfig.cscfg** são baseados no XML, descrevem a estrutura do serviço de nuvem e como ela é configurada; coletivamente são chamados de modelo.</span><span class="sxs-lookup"><span data-stu-id="13a52-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="13a52-106">O **ServicePackage.cspkg** é um arquivo zip gerado do **ServiceDefinition.csdef** e entre outras coisas, contém todas as dependências necessárias com base no binário.</span><span class="sxs-lookup"><span data-stu-id="13a52-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="13a52-107">O Azure cria um serviço de nuvem para o **ServicePackage.cspkg** e o **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="13a52-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="13a52-108">Quando o serviço de nuvem estiver em execução no Azure, você poderá reconfigurá-lo por meio do arquivo **ServiceConfig.cscfg** , mas você não pode alterar a definição.</span><span class="sxs-lookup"><span data-stu-id="13a52-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="13a52-109">O que você deseja saber mais?</span><span class="sxs-lookup"><span data-stu-id="13a52-109">What would you like to know more about?</span></span>
* <span data-ttu-id="13a52-110">Quero saber mais sobre os arquivos [ServiceDefinition.csdef](#csdef) e [ServiceConfig.cscfg](#cscfg).</span><span class="sxs-lookup"><span data-stu-id="13a52-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="13a52-111">Já sei sobre isso, dê-me [alguns exemplos](#next-steps) sobre o que posso configurar.</span><span class="sxs-lookup"><span data-stu-id="13a52-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="13a52-112">Quero criar o [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="13a52-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="13a52-113">Estou usando o Visual Studio e desejo...</span><span class="sxs-lookup"><span data-stu-id="13a52-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="13a52-114">[Criar um serviço de nuvem][vs_create]</span><span class="sxs-lookup"><span data-stu-id="13a52-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="13a52-115">[Reconfigurar um serviço de nuvem existente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="13a52-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="13a52-116">[Implantar um projeto do serviço de nuvem][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="13a52-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="13a52-117">[Área de trabalho remota em uma instância de serviço de nuvem][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="13a52-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="13a52-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="13a52-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="13a52-119">O arquivo **ServiceDefinition.csdef** especifica as configurações que são usadas pelo Azure para configurar um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="13a52-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="13a52-120">O [esquema de definição de serviço do Azure (arquivo .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fornece o formato permitido para um arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="13a52-121">O exemplo a seguir mostra as configurações que podem ser definidas para as funções da Web e de trabalho:</span><span class="sxs-lookup"><span data-stu-id="13a52-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="13a52-122">Você pode consultar o [Esquema de Definição de Serviço](https://msdn.microsoft.com/library/azure/ee758711.aspx) para uma melhor compreensão sobre o esquema XML usado aqui, no entanto, eis uma breve explicação de alguns dos elementos:</span><span class="sxs-lookup"><span data-stu-id="13a52-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="13a52-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="13a52-123">**Sites**</span></span>  
<span data-ttu-id="13a52-124">contêm as definições para sites da Web ou aplicativos Web hospedados no IIS7.</span><span class="sxs-lookup"><span data-stu-id="13a52-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="13a52-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="13a52-125">**InputEndpoints**</span></span>  
<span data-ttu-id="13a52-126">contém as definições para pontos de extremidade usados para entrar em contato com o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="13a52-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="13a52-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="13a52-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="13a52-128">contém as definições para pontos de extremidade que são usados por instâncias de função para se comunicar entre si.</span><span class="sxs-lookup"><span data-stu-id="13a52-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="13a52-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="13a52-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="13a52-130">contém as definições de configuração para recursos de uma função específica.</span><span class="sxs-lookup"><span data-stu-id="13a52-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="13a52-131">**Certificados**</span><span class="sxs-lookup"><span data-stu-id="13a52-131">**Certificates**</span></span>  
<span data-ttu-id="13a52-132">contêm as definições para certificados que são necessárias para uma função.</span><span class="sxs-lookup"><span data-stu-id="13a52-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="13a52-133">O exemplo de código anterior mostra um certificado que é usado para a configuração do Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="13a52-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="13a52-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="13a52-134">**LocalResources**</span></span>  
<span data-ttu-id="13a52-135">contém as definições para recursos de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="13a52-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="13a52-136">Um recurso de armazenamento local é um diretório reservado no sistema de arquivos da máquina virtual no qual uma instância de uma função está em execução.</span><span class="sxs-lookup"><span data-stu-id="13a52-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="13a52-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="13a52-137">**Imports**</span></span>  
<span data-ttu-id="13a52-138">contém as definições para módulos importados.</span><span class="sxs-lookup"><span data-stu-id="13a52-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="13a52-139">O exemplo de código anterior mostra os módulos para conexão de área de trabalho remota e Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="13a52-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="13a52-140">**Inicialização**</span><span class="sxs-lookup"><span data-stu-id="13a52-140">**Startup**</span></span>  
<span data-ttu-id="13a52-141">contém tarefas que são executadas quando a função é iniciada.</span><span class="sxs-lookup"><span data-stu-id="13a52-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="13a52-142">As tarefas são definidas em um arquivo executável ou o .cmd.</span><span class="sxs-lookup"><span data-stu-id="13a52-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="13a52-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="13a52-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="13a52-144">A definição das configurações do serviço de nuvem é determinada pelos valores do arquivo **ServiceConfiguration.cscfg** .</span><span class="sxs-lookup"><span data-stu-id="13a52-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="13a52-145">Especifique o número de instâncias que você deseja implantar para cada função nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="13a52-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="13a52-146">Os valores para os parâmetros de configuração que você definiu no arquivo de definição de serviço são adicionados ao arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="13a52-147">As impressões digitais para qualquer certificado de gerenciamento que estão associadas ao serviço de nuvem também são adicionadas ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="13a52-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="13a52-148">O [esquema de configuração de serviço do Azure (arquivo .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fornece o formato permitido para um arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="13a52-149">O arquivo de configuração de serviço não é fornecido com o aplicativo, mas é carregado no Azure como um arquivo separado e é usado para configurar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="13a52-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="13a52-150">Você pode carregar um novo arquivo de configuração de serviço sem reimplantar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="13a52-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="13a52-151">Os valores de configuração do serviço de nuvem podem ser alterados enquanto o serviço de nuvem está em execução.</span><span class="sxs-lookup"><span data-stu-id="13a52-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="13a52-152">O exemplo a seguir mostra as definições de configuração que podem ser definidas para as funções da Web e de trabalho:</span><span class="sxs-lookup"><span data-stu-id="13a52-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="13a52-153">Você pode consultar o [esquema de configuração de serviço](https://msdn.microsoft.com/library/azure/ee758710.aspx) para entender melhor o esquema XML usado aqui, no entanto, eis uma breve explicação dos elementos:</span><span class="sxs-lookup"><span data-stu-id="13a52-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="13a52-154">**Instâncias**</span><span class="sxs-lookup"><span data-stu-id="13a52-154">**Instances**</span></span>  
<span data-ttu-id="13a52-155">configura o número de instâncias em execução para a função.</span><span class="sxs-lookup"><span data-stu-id="13a52-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="13a52-156">Para impedir que seu serviço de nuvem fique potencialmente indisponível durante atualizações, é recomendável implantar mais de uma instância das suas funções da Web.</span><span class="sxs-lookup"><span data-stu-id="13a52-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="13a52-157">Ao implantar mais de uma instância, você estará aderindo às diretrizes do [Contrato de nível de serviço de computação do Azure (SLA)](http://azure.microsoft.com/support/legal/sla/), que garante 99,95% de conectividade externa para funções de Internet quando duas ou mais instâncias de função são implantadas para um serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="13a52-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="13a52-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="13a52-159">define as configurações para as instâncias em execução para uma função.</span><span class="sxs-lookup"><span data-stu-id="13a52-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="13a52-160">O nome dos `<Setting>` elementos deve corresponder às definições no arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="13a52-161">**Certificados**</span><span class="sxs-lookup"><span data-stu-id="13a52-161">**Certificates**</span></span>  
<span data-ttu-id="13a52-162">configura os certificados que são usados pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="13a52-163">O exemplo de código anterior mostra como definir o certificado para o módulo RemoteAccess.</span><span class="sxs-lookup"><span data-stu-id="13a52-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="13a52-164">O valor do atributo *impressão digital* deve ser definido como a impressão digital do certificado que será usado.</span><span class="sxs-lookup"><span data-stu-id="13a52-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="13a52-165">A impressão digital do certificado pode ser adicionada ao arquivo de configuração usando um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="13a52-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="13a52-166">Ou então, o valor pode ser adicionado na guia **Certificados** da página **Propriedades** da função no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13a52-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="13a52-167">Definindo as portas para instâncias de função</span><span class="sxs-lookup"><span data-stu-id="13a52-167">Defining ports for role instances</span></span>
<span data-ttu-id="13a52-168">O Azure permite apenas um ponto de entrada para uma função web.</span><span class="sxs-lookup"><span data-stu-id="13a52-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="13a52-169">Isso significa que todo o tráfego ocorre por meio de um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="13a52-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="13a52-170">Você pode configurar seus sites para compartilhar uma porta ao configurar o cabeçalho do host para direcionar a solicitação para o local correto.</span><span class="sxs-lookup"><span data-stu-id="13a52-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="13a52-171">Você também pode configurar seus aplicativos para escutar portas conhecidas no endereço IP.</span><span class="sxs-lookup"><span data-stu-id="13a52-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="13a52-172">O exemplo a seguir mostra a configuração de uma função web com um site e o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="13a52-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="13a52-173">O site é configurado como o local de entrada padrão na porta 80, e os aplicativos web são configurados para receber solicitações de um cabeçalho de host alternativo que é chamado de "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="13a52-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="13a52-174">Alterar a configuração de uma função</span><span class="sxs-lookup"><span data-stu-id="13a52-174">Changing the configuration of a role</span></span>
<span data-ttu-id="13a52-175">Você pode atualizar a configuração do seu serviço de nuvem enquanto ele é executado no Azure, sem que o serviço fique offline.</span><span class="sxs-lookup"><span data-stu-id="13a52-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="13a52-176">Para alterar informações de configuração, você pode carregar um novo arquivo de configuração, ou editar o arquivo de configuração no local e aplicá-lo ao seu serviço em execução.</span><span class="sxs-lookup"><span data-stu-id="13a52-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="13a52-177">As seguintes alterações podem ser feitas na configuração de um serviço:</span><span class="sxs-lookup"><span data-stu-id="13a52-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="13a52-178">**Alterando os valores das configurações**</span><span class="sxs-lookup"><span data-stu-id="13a52-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="13a52-179">Quando uma configuração é alterada, uma instância de função pode optar por aplicar a alteração enquanto a instância está online ou reciclar a instância normalmente e aplicar a alteração enquanto a instância está offline.</span><span class="sxs-lookup"><span data-stu-id="13a52-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="13a52-180">**Alterando a topologia de serviço das instâncias da função**</span><span class="sxs-lookup"><span data-stu-id="13a52-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="13a52-181">As alterações da topologia não afetam as instâncias em execução, exceto quando uma instância está sendo removida.</span><span class="sxs-lookup"><span data-stu-id="13a52-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="13a52-182">Todas as instâncias restantes geralmente não precisam ser recicladas. No entanto, você pode optar por reciclar instâncias de função em resposta a uma alteração de topologia.</span><span class="sxs-lookup"><span data-stu-id="13a52-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="13a52-183">**Alterando a impressão digital do certificado**</span><span class="sxs-lookup"><span data-stu-id="13a52-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="13a52-184">Somente é possível atualizar um certificado quando uma instância de função está offline.</span><span class="sxs-lookup"><span data-stu-id="13a52-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="13a52-185">Se um certificado é adicionado, excluído ou alterado enquanto uma instância de função estiver online, o Azure deixará a instância offline normalmente para atualizar o certificado e a deixará online novamente após a alteração ser concluída.</span><span class="sxs-lookup"><span data-stu-id="13a52-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="13a52-186">Tratando alterações de configuração com eventos de tempo de execução do serviço</span><span class="sxs-lookup"><span data-stu-id="13a52-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="13a52-187">A [Biblioteca de Tempo de Execução do Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) inclui o namespace [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx), que fornece classes para interagir com o ambiente do Azure de uma função.</span><span class="sxs-lookup"><span data-stu-id="13a52-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="13a52-188">A classe [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) define os seguintes eventos que são disparados antes e depois de uma alteração de configuração:</span><span class="sxs-lookup"><span data-stu-id="13a52-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="13a52-189">**[Alterando](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) eventos**</span><span class="sxs-lookup"><span data-stu-id="13a52-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="13a52-190">Isso ocorre antes que a alteração de configuração seja aplicada a uma instância específica de uma função, fornecendo a oportunidade de desativar as instâncias de função, se necessário.</span><span class="sxs-lookup"><span data-stu-id="13a52-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="13a52-191">**[Evento](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) alterado**</span><span class="sxs-lookup"><span data-stu-id="13a52-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="13a52-192">Ocorre depois que a alteração de configuração é aplicada a uma instância específica de uma função.</span><span class="sxs-lookup"><span data-stu-id="13a52-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="13a52-193">Como as alterações de certificado sempre tornam as instâncias de uma função offline, elas não geram os eventos RoleEnvironment.Changing ou RoleEnvironment.Changed.</span><span class="sxs-lookup"><span data-stu-id="13a52-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="13a52-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="13a52-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="13a52-195">Para implantar um aplicativo como um serviço de nuvem no Azure, primeiro você deve empacotar o aplicativo no formato apropriado.</span><span class="sxs-lookup"><span data-stu-id="13a52-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="13a52-196">Você pode usar a ferramenta de linha de comando **CSPack** (instalada com o [SDK do Azure](https://azure.microsoft.com/downloads/)) para criar o arquivo de pacote como uma alternativa para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13a52-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="13a52-197">**CSPack** usa o conteúdo do arquivo de definição de serviço e arquivo de configuração de serviço para definir o conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="13a52-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="13a52-198">**CSPack** gera um arquivo de pacote de aplicativos (.cspkg) que você pode carregar no Azure usando o [Portal do Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="13a52-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="13a52-199">Por padrão, o pacote é denominado `[ServiceDefinitionFileName].cspkg`, mas você pode especificar um nome diferente usando a opção `/out` de **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="13a52-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="13a52-200">**CSPack** está localizado em</span><span class="sxs-lookup"><span data-stu-id="13a52-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="13a52-201">O CSPack.exe (no Windows) está disponível executando o atalho do **prompt de comando do Microsoft Azure** que é instalado com o SDK.</span><span class="sxs-lookup"><span data-stu-id="13a52-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="13a52-202">Execute o programa CSPack.exe por ele mesmo para ver a documentação sobre todos os comandos e opções possíveis.</span><span class="sxs-lookup"><span data-stu-id="13a52-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="13a52-203">Para executar o serviço de nuvem localmente no **Emulador de Computação do Microsoft Azure**, use a opção **/copyonly**.</span><span class="sxs-lookup"><span data-stu-id="13a52-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="13a52-204">Esta opção copia os arquivos binários do aplicativo para um layout de diretório do qual eles podem ser executados no emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="13a52-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="13a52-205">Exemplo de comando para empacotar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="13a52-205">Example command to package a cloud service</span></span>
<span data-ttu-id="13a52-206">O exemplo a seguir cria um pacote de aplicativos que contém as informações para uma função web.</span><span class="sxs-lookup"><span data-stu-id="13a52-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="13a52-207">O comando especifica o arquivo de definição de serviço para usar, o diretório onde os arquivos binários podem ser encontrados e o nome do arquivo do pacote.</span><span class="sxs-lookup"><span data-stu-id="13a52-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="13a52-208">Se o aplicativo contém uma função web e uma função de trabalho, o comando a seguir será usado:</span><span class="sxs-lookup"><span data-stu-id="13a52-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="13a52-209">Onde as variáveis são definidas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="13a52-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="13a52-210">Variável</span><span class="sxs-lookup"><span data-stu-id="13a52-210">Variable</span></span> | <span data-ttu-id="13a52-211">Valor</span><span class="sxs-lookup"><span data-stu-id="13a52-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="13a52-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="13a52-212">\[DirectoryName\]</span></span> |<span data-ttu-id="13a52-213">O subdiretório no diretório do projeto raiz que contém o arquivo .csdef do projeto do Azure.</span><span class="sxs-lookup"><span data-stu-id="13a52-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="13a52-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="13a52-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="13a52-215">O nome do arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-215">The name of the service definition file.</span></span> <span data-ttu-id="13a52-216">Por padrão, esse arquivo é chamado de ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="13a52-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="13a52-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="13a52-217">\[OutputFileName\]</span></span> |<span data-ttu-id="13a52-218">O nome do arquivo de pacote gerado.</span><span class="sxs-lookup"><span data-stu-id="13a52-218">The name for the generated package file.</span></span> <span data-ttu-id="13a52-219">Normalmente, isso é definido como o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="13a52-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="13a52-220">Se nenhum nome de arquivo for especificado, o pacote de aplicativos será criado como \[NomeAplicativo\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="13a52-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="13a52-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="13a52-221">\[RoleName\]</span></span> |<span data-ttu-id="13a52-222">O nome da função, conforme definido no arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="13a52-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="13a52-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="13a52-224">O local dos arquivos binários da função.</span><span class="sxs-lookup"><span data-stu-id="13a52-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="13a52-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="13a52-225">\[VirtualPath\]</span></span> |<span data-ttu-id="13a52-226">Os diretórios físicos para cada caminho virtual definido na seção Sites da definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="13a52-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="13a52-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="13a52-228">Os diretórios físicos do conteúdo de cada caminho virtual definido no nó de site da definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="13a52-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="13a52-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="13a52-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="13a52-230">O nome do arquivo binário para a função.</span><span class="sxs-lookup"><span data-stu-id="13a52-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13a52-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13a52-231">Next steps</span></span>
<span data-ttu-id="13a52-232">Estou criando um pacote de serviço de nuvem e desejo...</span><span class="sxs-lookup"><span data-stu-id="13a52-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="13a52-233">[Configurar área de trabalho remota para uma instância de serviço de nuvem][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="13a52-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="13a52-234">[Implantar um projeto do serviço de nuvem][deploy]</span><span class="sxs-lookup"><span data-stu-id="13a52-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="13a52-235">Estou usando o Visual Studio e desejo...</span><span class="sxs-lookup"><span data-stu-id="13a52-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="13a52-236">[Criar um novo serviço de nuvem][vs_create]</span><span class="sxs-lookup"><span data-stu-id="13a52-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="13a52-237">[Reconfigurar um serviço de nuvem existente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="13a52-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="13a52-238">[Implantar um projeto do serviço de nuvem][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="13a52-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="13a52-239">[Configurar área de trabalho remota para uma instância de serviço de nuvem][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="13a52-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
