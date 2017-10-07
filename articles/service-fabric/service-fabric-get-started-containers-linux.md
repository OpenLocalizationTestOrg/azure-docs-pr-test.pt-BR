---
title: "aaaCreate um aplicativo de contêiner do Azure Service Fabric no Linux | Microsoft Docs"
description: "Crie seu primeiro aplicativo de contêiner do Linux no Azure Service Fabric.  Montar uma imagem do Docker com o seu aplicativo, enviar por push o registro de contêiner Olá imagem tooa, criar e implantar um aplicativo de contêiner do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Criar seu primeiro aplicativo de contêiner do Service Fabric no Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Executar um aplicativo existente em um contêiner do Linux em um cluster do Service Fabric não requer qualquer aplicativo tooyour de alterações. Este artigo orienta a criação de uma imagem do Docker que contém um Python [bulbo](http://flask.pocoo.org/) aplicativo e implantá-la tooa cluster de malha do serviço web.  Você também compartilhará seu aplicativo em contêineres pelo [Registro de Contêiner do Azure](/azure/container-registry/).  Este artigo pressupõe uma compreensão básica sobre o Docker. Você pode aprender sobre o Docker ao ler Olá [visão geral de Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Pré-requisitos
* Um computador de desenvolvimento executando:
  * [Ferramentas e SDK do Service Fabric](service-fabric-get-started-linux.md).
  * [Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [CLI do Service Fabric](service-fabric-cli.md)

* Um registro no Registro de Contêiner do Azure - [Crie um registro de contêiner](../container-registry/container-registry-get-started-portal.md) em sua assinatura do Azure. 

## <a name="define-hello-docker-container"></a>Definir o contêiner do Docker Olá
Criar uma imagem com base em Olá [imagem Python](https://hub.docker.com/_/python/) localizado no Hub do Docker. 

Defina o contêiner do Docker em um Dockerfile. Olá Dockerfile contém instruções para a configuração de ambiente hello dentro de seu contêiner, carregar o aplicativo hello deseja toorun e mapear portas. Olá Dockerfile é toohello de entrada hello `docker build` comando, que cria a imagem de saudação. 

Criar um diretório vazio e criar o arquivo hello *Dockerfile* (com nenhuma extensão de arquivo). Adicionar Olá seguir muito*Dockerfile* e salve as alterações:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Saudação de leitura [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para obter mais informações.

## <a name="create-a-simple-web-application"></a>Criar um aplicativo Web simples
Crie um aplicativo Web Flask que escuta a porta 80 retornar "Olá, Mundo!".  Em Olá mesmo diretório, crie o arquivo hello *requirements.txt*.  Adicione o seguinte de saudação e salve as alterações:
```
Flask
```

Também criar hello *app.py* de arquivo e adicione Olá seguinte:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a>Criar imagem Olá
Executar Olá `docker build` imagem de saudação do comando toocreate que executa o aplicativo da web. Abra uma janela do PowerShell e navegue muito*c:\temp\helloworldapp*. Execute Olá comando a seguir:

```bash
docker build -t helloworldapp .
```

Este comando compilações Olá nova imagem usando as instruções de saudação em seu Dockerfile, nomear (-t marcação) imagem hello "helloworldapp". Criando uma imagem extrai imagem base Olá para baixo do Hub do Docker e cria uma nova imagem que adiciona o seu aplicativo na parte superior da imagem base hello.  

Após a conclusão do comando de compilação hello, executar Olá `docker images` informações toosee na nova imagem de saudação do comando:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente
Verifique se que seu aplicativo em contêineres é executado localmente antes de enviar por push-registro de contêiner de saudação.  

Executar o aplicativo hello, mapeamento do contêiner do seu computador porta 4000 toohello expostos a porta 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*nome* oferece um toohello nome executando contêiner (em vez de ID de contêiner de saudação).

Conecte-se toohello executando o contêiner.  Abra um navegador da web apontando toohello endereço IP retornado na porta 4000, por exemplo "http://localhost:4000". Você deve ver Olá título "Hello World!" Exibir no navegador de saudação.

![Olá, Mundo!][hello-world]

toostop seu contêiner, execute:

```bash
docker stop my-web-site
```

Exclua contêiner de saudação do seu computador de desenvolvimento:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Registro de contêiner do push Olá imagem toohello
Depois de verificar que o aplicativo hello é executado no Docker, enviar por push do registro do hello imagem tooyour no registro de contêiner do Azure.

Executar `docker login` toolog tooyour registro de contêiner com o [credenciais de registro](../container-registry/container-registry-authentication.md).

Olá exemplo a seguir passa Olá ID e a senha de um Active Directory do Azure [entidade de serviço](../active-directory/active-directory-application-objects.md). Por exemplo, você pode ter atribuído um registro de tooyour principal do serviço para um cenário de automação.  Ou pode fazer logon usando o nome de usuário e a senha do registro.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Olá comando a seguir cria uma marca, ou alias, da imagem hello, com um registro de tooyour caminho totalmente qualificado. Este exemplo casas Olá imagem no hello `samples` namespace tooavoid desordem na raiz de saudação do registro hello.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registro de push Olá imagem tooyour contêiner:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Imagem de Docker de saudação do pacote com Yeoman
Olá SDK do Service Fabric para Linux inclui um [Yeoman](http://yeoman.io/) gerador que torna mais fácil toocreate seu aplicativo e adicione uma imagem de contêiner. Vamos usar Yeoman toocreate chamado de um aplicativo com um único contêiner de Docker *SimpleContainerApp*.

toocreate um aplicativo de contêiner de serviço de malha, abra uma janela do terminal e execute `yo azuresfcontainer`.  

Dê um nome para o seu aplicativo (por exemplo, “mycontainer”). 

Forneça a URL de saudação para imagem de contêiner de saudação em um registro de contêiner (por exemplo, ""). 

Esta imagem tem uma carga de trabalho-ponto de entrada definido, portanto precisa tooexplicitly especificar comandos de entrada (comandos executados dentro do contêiner Olá que manterá o contêiner de saudação em execução após a inicialização). 

Especifique a contagem de instâncias como "1".

![Gerador de Yeoman do Service Fabric para contêineres][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Configurar a autenticação de repositório de contêiner e o mapeamento de porta
O serviço em contêineres precisa de um ponto de extremidade para comunicação.  Agora adicione Olá protocolo, porta e tipo tooan `Endpoint` no arquivo ServiceManifest.xml de saudação. Neste artigo, o serviço de saudação em contêineres escuta na porta 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Fornecendo Olá `UriScheme` automaticamente registra Olá ponto de extremidade de contêiner com hello serviço de nomeação de malha do serviço de descoberta. Um arquivo de exemplo ServiceManifest.xml completo é fornecido no final deste artigo hello. 

Configurar o mapeamento de porta de host de contêiner porta Olá especificando um `PortBinding` política no `ContainerHostPolicies` do arquivo applicationmanifest. XML de saudação.  Neste artigo, `ContainerPort` é 80 (contêiner Olá expõe a porta 80, Olá especificado no Dockerfile) e `EndpointRef` é "myserviceTypeEndpoint" (ponto de extremidade Olá definido no manifesto do serviço de saudação).  Solicitações de entrada toohello na porta 4000 são mapeados tooport 80 no contêiner de saudação.  Se o contêiner deve tooauthenticate com um repositório privado, em seguida, adicione `RepositoryCredentials`.  Neste artigo, adicione Olá nome e a senha para o registro de contêiner myregistry.azurecr.io hello. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Compilação e o pacote de aplicativo do Service Fabric hello
modelos de serviço do Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que você pode usar o aplicativo hello toobuild Olá terminal. toobuild e pacote de aplicativo hello, execute Olá seguinte:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Implantar o aplicativo hello
Depois que o aplicativo hello é criado, você pode implantá-lo usando Olá CLI de malha do serviço de cluster local do toohello.

Conecte-se toohello cluster de malha do serviço local.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Olá Use o script de instalação fornecidas no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.

```bash
./install.sh
```

Abra um navegador e navegue tooService Fabric Explorer no http://localhost:19080/Explorer (substitua localhost com IP privada Olá Olá VM se usando Vagrant no Mac OS X). Expanda o nó de aplicativos hello e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.

Conecte-se toohello executando o contêiner.  Abra um navegador da web apontando toohello endereço IP retornado na porta 4000, por exemplo "http://localhost:4000". Você deve ver Olá título "Hello World!" Exibir no navegador de saudação.

![Olá, Mundo!][hello-world]

## <a name="clean-up"></a>Limpar
Usar script de desinstalação Olá fornecido na instância do aplicativo hello modelo toodelete saudação do cluster de desenvolvimento local hello e cancelar o registro do tipo de aplicativo hello.

```bash
./uninstall.sh
```

Depois que você enviar por push o registro de contêiner de toohello Olá imagem, você pode excluir imagem local saudação do seu computador de desenvolvimento:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Exemplo completo de manifestos de serviço e aplicativo do Service Fabric
Aqui estão os manifestos de aplicativo usados neste artigo e serviço completo hello.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Adicionar mais serviços tooan aplicativo

outro aplicativo de contêiner serviço tooan já criado usando yeoman, executar a tooadd Olá seguintes etapas:

1. Alterar o diretório raiz de toohello do aplicativo existente hello.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.
2. Execute o `yo azuresfcontainer:AddService`

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a>Configurar o intervalo de tempo antes do contêiner ser forçado a terminar

Você pode configurar um intervalo de tempo para Olá toowait de tempo de execução antes de contêiner de saudação é removida depois hello exclusão de serviço (ou um nó de tooanother mover) foi iniciado. Configurando intervalo de tempo de saudação envia Olá `docker stop <time in seconds>` contêiner de toohello de comando.   Para obter mais detalhes, consulte [parar docker](https://docs.docker.com/engine/reference/commandline/stop/). Olá toowait de intervalo de tempo especificado em Olá `Hosting` seção. Olá trecho do manifesto de cluster a seguir mostra como o intervalo de espera tooset hello:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Olá intervalo de tempo padrão é definido too10 segundos. Como essa configuração é dinâmica, uma configuração só atualizar no tempo limite de saudação de atualizações de cluster hello. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Configurar Olá runtime tooremove imagens de contêiner não utilizado

Você pode configurar Olá Service Fabric cluster tooremove imagens de contêiner não utilizados do nó de saudação. Essa configuração permite toobe de espaço em disco retomou se houver muitas imagens de contêiner no nó de saudação.  tooenable deste recurso, a atualização Olá `Hosting` seção no manifesto do cluster hello, conforme mostrado no hello trecho de código a seguir: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Para as imagens que não devem ser excluídas, você poderá especificá-los em Olá `ContainerImagesToSkip` parâmetro. 


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-containers-overview.md).
* Saudação de leitura [implantar um aplicativo .NET em um contêiner](service-fabric-host-app-in-a-container.md) tutorial.
* Saiba mais sobre Olá Service Fabric [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md).
* Saudação de check-out [exemplos de código do contêiner do Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) no GitHub.

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
