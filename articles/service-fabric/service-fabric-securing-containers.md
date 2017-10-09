---
title: "aaaAzure segurança de contêiner do Service Fabric | Microsoft Docs"
description: "Saiba mais serviços de contêiner toosecure agora."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="358b5-103">Segurança do contêiner</span><span class="sxs-lookup"><span data-stu-id="358b5-103">Container security</span></span>

<span data-ttu-id="358b5-104">Serviço de malha fornece um mecanismo para serviços dentro de um contêiner tooaccess um certificado que é instalado em nós de saudação em um cluster do Windows ou Linux (versão 5.7 ou superior).</span><span class="sxs-lookup"><span data-stu-id="358b5-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="358b5-105">Além disso, o Service Fabric também dá suporte a gMSA (Contas de Serviço Gerenciado do grupo) para contêineres do Windows.</span><span class="sxs-lookup"><span data-stu-id="358b5-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="358b5-106">Gerenciamento de certificados para contêineres</span><span class="sxs-lookup"><span data-stu-id="358b5-106">Certificate management for containers</span></span>

<span data-ttu-id="358b5-107">Você pode proteger seus serviços de contêiner especificando um certificado.</span><span class="sxs-lookup"><span data-stu-id="358b5-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="358b5-108">certificado de saudação deve ser instalado em nós de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="358b5-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="358b5-109">Olá informações do certificado são fornecidas no manifesto de aplicativo hello em Olá `ContainerHostPolicies` marca como Olá trecho a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="358b5-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="358b5-110">Ao iniciar o aplicativo hello, o tempo de execução de saudação lê certificados hello e gera um arquivo PFX e senha para cada certificado.</span><span class="sxs-lookup"><span data-stu-id="358b5-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="358b5-111">Este arquivo PFX e senha são acessíveis dentro do contêiner hello usando Olá variáveis de ambiente a seguir:</span><span class="sxs-lookup"><span data-stu-id="358b5-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="358b5-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="358b5-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="358b5-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="358b5-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="358b5-114">Olá contêiner serviço ou processo é responsável para importar o arquivo PFX de saudação para contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="358b5-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="358b5-115">certificado de saudação tooimport, você pode usar `setupentrypoint.sh` da execução de código personalizado no processo do contêiner de saudação ou scripts.</span><span class="sxs-lookup"><span data-stu-id="358b5-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="358b5-116">Código de exemplo em c# para importar o arquivo PFX de saudação segue:</span><span class="sxs-lookup"><span data-stu-id="358b5-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="358b5-117">Esse certificado PFX pode ser usado para o aplicativo hello de autenticar ou serviço ou commmunication segura com outros serviços.</span><span class="sxs-lookup"><span data-stu-id="358b5-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="358b5-118">Configurar o gMSA para contêineres do Windows</span><span class="sxs-lookup"><span data-stu-id="358b5-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="358b5-119">tooset a gMSA (grupo de contas de serviço gerenciado), um arquivo de especificação de credencial (`credspec`) é colocado em todos os nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="358b5-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="358b5-120">arquivo Hello pode ser copiado em todos os nós usando uma extensão de VM.</span><span class="sxs-lookup"><span data-stu-id="358b5-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="358b5-121">Olá `credspec` arquivo deve conter informações da conta gMSA hello.</span><span class="sxs-lookup"><span data-stu-id="358b5-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="358b5-122">Para obter mais informações sobre Olá `credspec` de arquivos, consulte [contas de serviço](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="358b5-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="358b5-123">especificação de credencial Hello e hello `Hostname` marca são especificadas no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="358b5-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="358b5-124">Olá `Hostname` marca deve corresponder o nome da conta gMSA Olá que Olá é executado de contêiner com.</span><span class="sxs-lookup"><span data-stu-id="358b5-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="358b5-125">Olá `Hostname` marca permite Olá tooauthenticate de contêiner em si tooother serviços no domínio hello usando a autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="358b5-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="358b5-126">Um exemplo para especificar Olá `Hostname` e hello `credspec` Olá manifesto do aplicativo é mostrado em Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="358b5-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="358b5-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="358b5-127">Next steps</span></span>

* [<span data-ttu-id="358b5-128">Implantar um contêiner de Windows tooService malha no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="358b5-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="358b5-129">Implantar um contêiner de Docker tooService malha no Linux</span><span class="sxs-lookup"><span data-stu-id="358b5-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
