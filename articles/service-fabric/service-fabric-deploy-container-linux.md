---
title: "aaaService malha e implantar contêineres do Linux | Microsoft Docs"
description: "Serviço de malha e hello usam contêineres toodeploy microsserviço aplicativos do Linux. Este artigo descreve recursos de saudação do Service Fabric fornece para contêineres e como toodeploy um contêiner de Linux a imagem em um cluster"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Implantar um contêiner de Linux tooService malha
> [!div class="op_single_selector"]
> * [Implantar contêiner do Windows](service-fabric-deploy-container.md)
> * [Implantar contêiner do Linux](service-fabric-deploy-container-linux.md)
>
>

Este artigo orienta a criação de serviços contentorizados em contêineres do Docker no Linux.

O Service Fabric tem vários recursos de contêiner que ajudam na compilação de aplicativos que são compostos por microsserviços que estão em contêineres. Esses serviços são chamados de serviços em contêineres.

recursos de saudação incluem;

* Implantação e ativação de imagens de contêiner
* Governança de recursos
* Autenticação do repositório
* Mapeamento de porta de toohost de porta de contêiner
* Descoberta e comunicação de contêiner para contêiner
* Capacidade tooconfigure e definir variáveis de ambiente

## <a name="packaging-a-docker-container-with-yeoman"></a>Empacotando um contêiner do Docker com yeoman
Ao empacotar um contêiner no Linux, você pode escolher qualquer toouse um modelo de yeoman ou [criar manualmente o pacote de aplicativo hello](#manually).

Um aplicativo de malha do serviço pode conter um ou mais contêineres, cada um com uma função específica no fornecimento de funcionalidade do aplicativo hello. Olá SDK do Service Fabric para Linux inclui um [Yeoman](http://yeoman.io/) gerador que torna mais fácil toocreate seu aplicativo e adicione uma imagem de contêiner. Vamos usar Yeoman toocreate chamado de um aplicativo com um único contêiner de Docker *SimpleContainerApp*. Você pode adicionar mais serviços mais tarde editando os arquivos de manifesto Olá gerado.

## <a name="install-docker-on-your-development-box"></a>Instalar o Docker em sua caixa de desenvolvimento

A seguir Olá execução comandos docker tooinstall na caixa de desenvolvimento do Linux (se você estiver usando a imagem vagrant Olá no OSX, docker já está instalado):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Criar um aplicativo hello
1. Em um terminal, digite `yo azuresfcontainer`.
2. Dê um nome para o seu aplicativo, por exemplo, mycontainerap
3. Forneça a URL de saudação para imagem de contêiner de saudação de um repositório DockerHub. Olá imagem parâmetro usa Olá formulário [repositório] / [nome da imagem]
4. Se Olá imagem não tiver um carga de trabalho-ponto de entrada definido, você precisará tooexplicitly especificar comandos de entrada com um conjunto delimitado por vírgulas de comandos toorun Olá contêiner, que manterá o contêiner de saudação em execução após a inicialização.

![Gerador de Yeoman do Service Fabric para contêineres][sf-yeoman]

## <a name="deploy-hello-application"></a>Implantar o aplicativo hello

### <a name="using-xplat-cli"></a>Usando a CLI XPlat
Depois que o aplicativo hello é criado, você pode implantar toohello cluster local usando Olá CLI do Azure.

1. Conecte-se toohello cluster de malha do serviço local.

    ```bash
    azure servicefabric cluster connect
    ```

2. Olá Use o script de instalação fornecidas no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.

    ```bash
    ./install.sh
    ```

3. Abra um navegador e navegue tooService Fabric Explorer no http://localhost:19080/Explorer (substitua localhost com IP privada Olá Olá VM se usando Vagrant no Mac OS X).
4. Expanda o nó de aplicativos hello e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.
5. Usar script de desinstalação Olá fornecido na instância de aplicativo hello modelo toodelete hello e cancelar o registro do tipo de aplicativo hello.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Usando a CLI do Azure 2.0

Consulte o documento de referência de saudação sobre como gerenciar uma [ciclo de vida do aplicativo usando hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Para um aplicativo de exemplo, [Olá check-out código do contêiner do Service Fabric amostras no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Adicionar mais serviços tooan aplicativo

tooadd outro contêiner de serviço tooan aplicativo já criado usando `yo`, executar Olá etapas a seguir:

1. Alterar o diretório raiz de toohello do aplicativo existente hello.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.
2. Execute o `yo azuresfcontainer:AddService`

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

Você pode fornecer entrada de comandos, especificando Olá opcional `Commands` elemento com um conjunto delimitado por vírgulas de comandos toorun dentro do contêiner de saudação.

> [!NOTE]
> Se Olá imagem não tiver um carga de trabalho-ponto de entrada definido, você precisará tooexplicitly especificar entrados comandos dentro `Commands` elemento com um conjunto delimitado por vírgulas de comandos toorun Olá contêiner, que manterá o contêiner de saudação em execução inicialização.

## <a name="understand-resource-governance"></a>Compreender a governança de recursos
Governança de recursos é um recurso de contêiner de saudação que restringe os recursos de Olá Olá contêiner pode usar no host de saudação. Olá `ResourceGovernancePolicy`, que é especificado no manifesto de aplicativo hello é usado toodeclare limites de recurso para um pacote de código de serviço. Limites de recursos podem ser definidos para Olá recursos a seguir:

* Memória
* MemorySwap
* CpuShares (peso relativo da CPU)
* MemoryReservationInMB  
* BlkioWeight (peso relativo do BlockIO).

> [!NOTE]
> Em uma versão futura, será incluído suporte para especificar limites de E/S de um bloco específico, como IOPs, leitura/gravação de BPS e outros.
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

## <a name="configure-container-port-to-host-port-mapping"></a>Configurar mapeamento de porta do contêiner para o porta de host
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
Usando Olá `PortBinding` política, você pode mapear uma porta de contêiner tooan `Endpoint` no manifesto do serviço de saudação. ponto de extremidade de Olá `Endpoint1` pode especificar uma porta fixa (por exemplo, a porta 80). Ele também não pode especificar nenhuma porta, caso em que uma porta aleatória do intervalo de portas de aplicativo do cluster Olá é escolhida para você.

Se você especificar um ponto de extremidade, usando Olá `Endpoint` marca no manifesto do serviço de saudação de um contêiner de convidado, o Service Fabric pode publicar automaticamente toohello esse ponto de extremidade Naming service. Outros serviços que são executados no cluster hello, portanto, podem descobrir esse contêiner usando consultas REST Olá para resolver.

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

Registrando Olá Naming service, você poderá facilmente fazer comunicação de contêiner para contêiner no código hello dentro de seu contêiner usando Olá [proxy reverso](service-fabric-reverseproxy.md). A comunicação é executada, fornecendo a porta de escuta Olá proxy reverso http e o nome de saudação do serviços de saudação que você deseja toocommunicate com como variáveis de ambiente. Para obter mais informações, consulte Olá próxima seção.

## <a name="configure-and-set-environment-variables"></a>Configurar e definir as variáveis de ambiente
Variáveis de ambiente podem ser especificadas para cada pacote de códigos no manifesto do serviço hello, tanto para serviços que são implantados em contêineres ou para serviços que são implantados como executáveis processos/convidado. Esses valores de variáveis de ambiente podem ser substituídas especificamente no manifesto do aplicativo hello ou especificados durante a implantação como parâmetros de aplicativo.

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
* [Interagir com clusters de malha do serviço usando Olá CLI do Azure](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Artigos relacionados

* [Introdução ao Service Fabric e a CLI do Azure 2.0](service-fabric-azure-cli-2-0.md)
* [Introdução à CLI XPlat do Service Fabric](service-fabric-azure-cli.md)
