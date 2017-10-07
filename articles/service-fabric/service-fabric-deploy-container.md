---
title: "aaaService malha e implantar contêineres | Microsoft Docs"
description: "Service Fabric e hello o uso de aplicativos de microsserviço toodeploy contêineres. Este artigo descreve os recursos de saudação do Service Fabric fornece para contêineres e como toodeploy um contêiner do Windows da imagem em um cluster."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Implantar um tooService de contêiner do Windows Fabric
> [!div class="op_single_selector"]
> * [Implantar contêiner do Windows](service-fabric-deploy-container.md)
> * [Implantar contêiner do Docker](service-fabric-deploy-container-linux.md)
> 
> 

Este artigo orienta você pelo processo de saudação da criação de serviços em contêineres em contêineres do Windows.

O Service Fabric tem vários recursos que ajudam na criação de aplicativos compostos de microsserviços em execução em contêineres. 

Olá recursos incluem:

* Implantação e ativação de imagens de contêiner
* Governança de recursos
* Autenticação do repositório
* Mapeamento de porta de contêiner para porta de host
* Descoberta e comunicação de contêiner para contêiner
* Capacidade tooconfigure e definir variáveis de ambiente

Vamos ver como cada um dos recursos funciona quando você estiver Empacotando uma toobe de serviço em contêineres incluído em seu aplicativo.

## <a name="package-a-windows-container"></a>Empacotar um contêiner do Windows
Ao empacotar um contêiner, você pode escolher toouse um modelo de projeto Visual Studio ou [criar manualmente o pacote de aplicativo hello](#manually).  Quando você usa o Visual Studio, a estrutura do pacote de aplicativo hello e arquivos de manifesto são criados pelo modelo de projeto novo Olá para você.

> [!TIP]
> toopackage de maneira mais fácil de saudação uma imagem de contêiner existente em um serviço é toouse Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Use o Visual Studio toopackage uma imagem de contêiner existente
O Visual Studio fornece uma estrutura de serviço toohelp de modelo de serviço é implantar um cluster do contêiner tooa Service Fabric.

1. Escolha **Arquivo** > **Novo Projeto** e crie um aplicativo de Service Fabric.
2. Escolha **convidado contêiner** como modelo de serviço hello.
3. Escolha **nome da imagem** e fornecer Olá caminho toohello imagem no repositório de contêiner. Por exemplo, `myrepo/myimage:v1` em https://hub.docker.com
4. Dê um nome ao seu serviço e clique em **OK**.
5. Se seu serviço em contêineres precisa de um ponto de extremidade de comunicação, agora você pode adicionar arquivos do tipo toohello ServiceManifest.xml, porta e protocolo de saudação. Por exemplo: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Fornecendo Olá `UriScheme`, Service Fabric registra automaticamente o ponto de extremidade de contêiner de saudação com hello Naming Service, serviço de descoberta. porta Olá pode ser fixa (conforme mostrado no hello anterior exemplo) ou alocada dinamicamente. Se você não especificar uma porta, ela é alocada dinamicamente do intervalo de portas de aplicativo hello (como acontece com qualquer serviço).
    Você também precisa de mapeamento de porta tooconfigure Olá contêiner toohost especificando um `PortBinding` política no manifesto de aplicativo hello. Para obter mais informações, consulte [Configurar mapeamento de porta do contêiner toohost](#Portsection).
6. Se seu contêiner precisar de governança de recursos, adicione `ResourceGovernancePolicy`.
8. Se o contêiner deve tooauthenticate com um repositório privado, em seguida, adicione `RepositoryCredentials`.
7. Se você estiver executando em um computador Windows Server 2016 com suporte de contêiner habilitado, você pode usar pacote de hello e publicar o cluster local da ação toodeploy tooyour. 
8. Quando estiver pronto, você pode publicar cluster remoto da saudação aplicativo tooa ou check-in de controle de toosource Olá solução. 

Para obter um exemplo, a saudação de check-out [exemplos de código do contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Criar um cluster do Windows Server 2016
toodeploy seu aplicativo em contêineres, você precisa toocreate habilitado de um cluster executando o Windows Server 2016 com suporte do contêiner. O cluster pode estar em execução localmente ou ser implantado por meio do Azure Resource Manager no Azure. 

toodeploy um cluster usando o Gerenciador de recursos do Azure, escolha Olá **Windows Server 2016 com contêineres** imagem opção no Azure. Consulte o artigo Olá [criar um cluster do Service Fabric usando o Gerenciador de recursos do Azure](service-fabric-cluster-creation-via-arm.md). Certifique-se de que você use hello Azure Resource Manager configurações a seguir:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Você também pode usar o hello [modelo de cinco nós do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate um cluster. Como alternativa, leia uma [postagem de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) da comunidade sobre o uso de contêineres do Windows e do Service Fabric.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Empacotar e implantar manualmente uma imagem de contêiner
processo de saudação do empacotamento manualmente um serviço em contêineres se baseia na Olá etapas a seguir:

1. Publica Olá contêineres tooyour repositório.
2. Crie estrutura de diretório do pacote de saudação.
3. Edite o arquivo de manifesto de serviço hello.
4. Edite o arquivo de manifesto de aplicativo hello.

## <a name="deploy-and-activate-a-container-image"></a>Implantar e ativar uma imagem de contêiner
Em Olá Service Fabric [modelo de aplicativo](service-fabric-application-model.md), um contêiner representa um host de aplicativo no qual o serviço várias réplicas são colocadas. toodeploy e ativar um contêiner, um nome de saudação put da imagem de contêiner de saudação em um `ContainerHost` elemento no manifesto do serviço de saudação.

No manifesto do serviço hello, adicione um `ContainerHost` para o ponto de entrada hello. Em seguida, o conjunto de saudação `ImageName` toobe nome de saudação do repositório de contêiner hello e imagem. Olá, manifesto parcial a seguir mostra um exemplo de como o contêiner de saudação toodeploy chamado `myimage:v1` de um repositório chamado `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

Você pode especificar comandos opcionais toorun durante a inicialização do contêiner de saudação em Olá `Commands` elemento. Para vários comandos, delimite-os com vírgulas. 

## <a name="understand-resource-governance"></a>Compreender a governança de recursos
Governança de recursos é um recurso de contêiner de saudação que restringe os recursos de Olá Olá contêiner pode usar no host de saudação. Olá `ResourceGovernancePolicy`, que é especificado no manifesto de aplicativo hello é usado toodeclare limites de recurso para um pacote de código de serviço. Limites de recursos podem ser definidos para Olá recursos a seguir:

* Memória
* MemorySwap
* CpuShares (peso relativo da CPU)
* MemoryReservationInMB  
* BlkioWeight (peso relativo do BlockIO).

> [!NOTE]
> o Suporte para especificar os limites de e/s de bloco específicoS como IOPs, leitura/gravação BPS e outros estão planejados para uma versão futura.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Autenticar um repositório
toodownload um contêiner, você pode ter um repositório de contêiner de toohello tooprovide credenciais de logon. Olá credenciais de logon, especificadas no manifesto de aplicativo hello, são usadas toospecify Olá entrar informações ou uma chave SSH, para baixar a imagem de contêiner de saudação do repositório de imagens de saudação. Olá, exemplo a seguir mostra uma conta chamada *TestUser* junto com a senha Olá em texto não criptografado (*não* recomendado):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

É recomendável que você criptografe senha hello usando um certificado que tenha implantado toohello máquina.

Olá, exemplo a seguir mostra uma conta chamada *TestUser*, onde a senha de saudação foi criptografada usando um certificado chamado *MyCert*. Você pode usar o hello `Invoke-ServiceFabricEncryptText` PowerShell comando toocreate Olá secreta de criptografia texto para senha hello. Para obter mais informações, consulte o artigo Olá [gerenciar segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md).

chave privada de saudação do certificado de saudação que usou a senha de saudação toodecrypt deve ser implantado toohello o computador local em um método fora de banda. (No Azure, esse método é o Azure Resource Manager.) Em seguida, quando o Service Fabric implanta a máquina de toohello de pacote de serviço Olá, ele pode descriptografar o segredo de hello. Usando o segredo Olá junto com o nome da conta Olá, em seguida, pode autenticar com o repositório de contêiner de saudação.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a>Configurar o mapeamento de porta do contêiner toohost
Você pode configurar toocommunicate de porta usada um host com o contêiner de saudação especificando um `PortBinding` no manifesto de aplicativo hello. Olá porta associação mapas Olá porta toowhich Olá serviço está escutando em Olá contêiner tooa porta no host de saudação.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Configurar descoberta e comunicação de contêiner para contêiner
Você pode usar o hello `PortBinding` elemento toomap um ponto de extremidade de tooan de porta de contêiner no manifesto do serviço de saudação. Em Olá exemplo a seguir, Olá ponto de extremidade `Endpoint1` Especifica uma porta fixa, 8905. Ele também não pode especificar nenhuma porta, caso em que uma porta aleatória do intervalo de portas de aplicativo do cluster Olá é escolhida para você.


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
Se você especificar um ponto de extremidade, usando Olá `Endpoint` marca no manifesto do serviço de saudação de um contêiner de convidado, o Service Fabric pode publicar automaticamente toohello esse ponto de extremidade Naming service. Outros serviços que são executados no cluster hello, portanto, podem descobrir esse contêiner usando consultas REST Olá para resolver.

Registrando Olá Naming service, você pode executar o contêiner para contêiner comunicação dentro de seu contêiner usando Olá [proxy reverso](service-fabric-reverseproxy.md). A comunicação é executada, fornecendo a porta de escuta Olá proxy reverso http e o nome de saudação do serviços de saudação que você deseja toocommunicate com como variáveis de ambiente. Para obter mais informações, consulte Olá próxima seção. 

## <a name="configure-and-set-environment-variables"></a>Configurar e definir as variáveis de ambiente
Variáveis de ambiente podem ser especificadas para cada pacote de código no manifesto do serviço de saudação. Esse recurso está disponível para todos os serviços, independentemente de eles serem implantados como contêineres ou processos ou executáveis convidados. Você pode substituir a variável de ambiente valores no aplicativo hello manifesto ou especificá-las durante a implantação como parâmetros de aplicativo.

Olá, serviço manifesto trecho XML a seguir mostra um exemplo de como toospecify variáveis de ambiente para um pacote de código:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Essas variáveis de ambiente podem ser substituídos no nível de manifesto de aplicativo hello:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

No exemplo anterior de saudação, especificamos um valor explícito para Olá `HttpGateway` (19000), enquanto definimos Olá valor de variável de ambiente `BackendServiceName` parâmetro via Olá `[BackendSvc]` parâmetro de aplicativo. Essas configurações permitem que você valor Olá toospecify `BackendServiceName`quando você implanta o aplicativo hello e não tem um valor fixo no manifesto de saudação do valor.

## <a name="configure-isolation-mode"></a>Configurar o modo de isolamento

L Windows dá suporte a dois modos de isolamento para contêineres: processo e Hyper-V.  Com o modo de isolamento do processo de hello, todos os contêineres de saudação em execução no hello mesmo host máquina compartilhamento saudação do kernel com o host de saudação. Com o modo de isolamento Olá Hyper-V, kernels Olá são isolados entre cada contêiner do Hyper-V e o host do contêiner hello. modo de isolamento de saudação é especificado em Olá `ContainerHostPolicies` marca no arquivo de manifesto de aplicativo hello.  modos de isolamento de saudação que podem ser especificados são `process`, `hyperv`, e `default`. Olá `default` modo de isolamento padrão é muito`process` no Windows Server hospeda e os padrões muito`hyperv` em hosts do Windows 10.  Olá trecho a seguir mostra como o modo de isolamento de saudação é especificado no arquivo de manifesto de aplicativo hello.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>Exemplos completos de aplicativo e manifesto do serviço

Aqui está um exemplo de manifesto de aplicativo:

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Um manifesto de serviço de exemplo (especificado na Olá precede o manifesto do aplicativo) a seguir:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Próximas etapas
Agora que você implantou um serviço em contêineres, saiba como toomanage seu ciclo de vida lendo [ciclo de vida do aplicativo de malha do serviço](service-fabric-application-lifecycle.md).

* [Visão geral do Service Fabric e contêineres](service-fabric-containers-overview.md)
* Por exemplo, confira [Exemplos de código do contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
