---
title: "aaaCreate um aplicativo de contêiner do Azure Service Fabric | Microsoft Docs"
description: "Crie seu primeiro aplicativo de contêiner do Windows no Azure Service Fabric.  Montar uma imagem do Docker com um aplicativo de Python, enviar por push o registro de contêiner Olá imagem tooa, criar e implantar um aplicativo de contêiner do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Como criar seu primeiro aplicativo de contêiner do Service Fabric no Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Executando um aplicativo existente em um contêiner do Windows em um cluster do Service Fabric não requer qualquer aplicativo tooyour de alterações. Este artigo orienta a criação de uma imagem do Docker que contém um Python [bulbo](http://flask.pocoo.org/) aplicativo e implantá-la tooa cluster de malha do serviço web.  Você também compartilhará seu aplicativo em contêineres pelo [Registro de Contêiner do Azure](/azure/container-registry/).  Este artigo pressupõe uma compreensão básica sobre o Docker. Você pode aprender sobre o Docker ao ler Olá [visão geral de Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Pré-requisitos
Um computador de desenvolvimento executando:
* Visual Studio 2015 ou Visual Studio 2017.
* [Ferramentas e SDK do Service Fabric](service-fabric-get-started.md).
*  Docker para Windows.  [Obter Docker CE para o Windows (estável)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Depois de instalar e iniciar o Docker, com o botão direito no ícone de bandeja hello e selecione **alternar contêineres tooWindows**. Isso é necessário toorun imagens do Docker com base no Windows.

Um cluster do Windows com três ou mais nós em execução no Windows Server 2016 com contêineres - [Criar um cluster](service-fabric-cluster-creation-via-portal.md) ou [experimente o Service Fabric gratuitamente](https://aka.ms/tryservicefabric).

Um registro no Registro de Contêiner do Azure - [Crie um registro de contêiner](../container-registry/container-registry-get-started-portal.md) em sua assinatura do Azure.

## <a name="define-hello-docker-container"></a>Definir o contêiner do Docker Olá
Criar uma imagem com base em Olá [imagem Python](https://hub.docker.com/_/python/) localizado no Hub do Docker.

Defina o contêiner do Docker em um Dockerfile. Olá Dockerfile contém instruções para a configuração de ambiente hello dentro de seu contêiner, carregar o aplicativo hello deseja toorun e mapear portas. Olá Dockerfile é toohello de entrada hello `docker build` comando, que cria a imagem de saudação.

Criar um diretório vazio e criar o arquivo hello *Dockerfile* (com nenhuma extensão de arquivo). Adicionar Olá seguir muito*Dockerfile* e salve as alterações:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
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

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Criar imagem Olá
Executar Olá `docker build` imagem de saudação do comando toocreate que executa o aplicativo da web. Abra uma janela do PowerShell e navegue toohello diretório contendo Olá Dockerfile. Execute Olá comando a seguir:

```
docker build -t helloworldapp .
```

Este comando compilações Olá nova imagem usando as instruções de saudação em seu Dockerfile, nomear (-t marcação) imagem hello "helloworldapp". Criando uma imagem extrai imagem base Olá para baixo do Hub do Docker e cria uma nova imagem que adiciona o seu aplicativo na parte superior da imagem base hello.  

Após a conclusão do comando de compilação hello, executar Olá `docker images` informações toosee na nova imagem de saudação do comando:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente
Verifique se sua imagem localmente antes de enviar por push-registro de contêiner de saudação.  

Execute o aplicativo hello:

```
docker run -d --name my-web-site helloworldapp
```

*nome* oferece um toohello nome executando contêiner (em vez de ID de contêiner de saudação).

Depois de iniciada a contêiner hello, localize seu endereço IP para que você possa conectar tooyour executando o contêiner de um navegador:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Conecte-se toohello executando o contêiner.  Abra um navegador da web apontando o endereço IP de toohello retornado, por exemplo "http://172.31.194.61". Você deve ver Olá título "Hello World!" Exibir no navegador de saudação.

toostop seu contêiner, execute:

```
docker stop my-web-site
```

Exclua contêiner de saudação do seu computador de desenvolvimento:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Registro de contêiner do push Olá imagem toohello
Depois de verificar o que contêiner Olá é executado no computador de desenvolvimento, enviar por push do registro do hello imagem tooyour no registro de contêiner do Azure.

Executar ``docker login`` toolog tooyour registro de contêiner com o [credenciais de registro](../container-registry/container-registry-authentication.md).

Olá exemplo a seguir passa Olá ID e a senha de um Active Directory do Azure [entidade de serviço](../active-directory/active-directory-application-objects.md). Por exemplo, você pode ter atribuído um registro de tooyour principal do serviço para um cenário de automação. Ou pode fazer logon usando o nome de usuário e a senha do registro.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Olá comando a seguir cria uma marca, ou alias, da imagem hello, com um registro de tooyour caminho totalmente qualificado. Este exemplo casas Olá imagem no hello ```samples``` namespace tooavoid desordem na raiz de saudação do registro hello.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Registro de push Olá imagem tooyour contêiner:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Criar serviço Olá em contêineres no Visual Studio
Olá SDK do Service Fabric e ferramentas fornecem um toohelp de modelo de serviço é criar um aplicativo em contêineres.

1. Inicie o Visual Studio.  Selecione **Arquivo** > **Novo** > **Projeto**.
2. Selecione **Aplicativo do Service Fabric**, nomeie-o como "MyFirstContainer" e clique em **OK**.
3. Selecione **convidado contêiner** na lista de saudação do **modelos de serviço**.
4. Em **nome da imagem** insira "myregistry.azurecr.io/samples/helloworldapp," imagem Olá enviada por push tooyour repositório de contêiner.
5. Dê um nome ao seu serviço e clique em **OK**.

## <a name="configure-communication"></a>Configurar a comunicação
serviço de saudação em contêineres precisa de um ponto de extremidade de comunicação. Adicionar um `Endpoint` elemento com o arquivo do tipo toohello ServiceManifest.xml, porta e protocolo de saudação. Neste artigo, o serviço de saudação em contêineres escuta na porta 8081.  Neste exemplo, uma porta fixa 8081 é usada.  Se nenhuma porta for especificada, uma porta aleatória do intervalo de portas de aplicativo hello é escolhida.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

Definindo um ponto de extremidade, o Service Fabric publica toohello de ponto de extremidade Olá Naming service.  Outros serviços em execução no cluster Olá podem resolver este contêiner.  Você também pode executar a comunicação de contêiner para contêiner usando Olá [proxy reverso](service-fabric-reverseproxy.md).  A comunicação é executada, fornecendo a porta de escuta de proxy reverso HTTP de saudação e o nome de saudação do serviços de saudação que você deseja toocommunicate com como variáveis de ambiente.

## <a name="configure-and-set-environment-variables"></a>Configurar e definir as variáveis de ambiente
Variáveis de ambiente podem ser especificadas para cada pacote de código no manifesto do serviço de saudação. Esse recurso está disponível para todos os serviços, independentemente de eles serem implantados como contêineres ou processos ou executáveis convidados. Você pode substituir a variável de ambiente valores no aplicativo hello manifesto ou especificá-las durante a implantação como parâmetros de aplicativo.

Olá, serviço manifesto trecho XML a seguir mostra um exemplo de como toospecify variáveis de ambiente para um pacote de código:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Essas variáveis de ambiente podem ser substituídos no manifesto de aplicativo hello:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Configurar mapeamento de porta para host e descoberta de contêiner para contêiner
Configure toocommunicate de porta usada um host com o contêiner de saudação. associação de porta Olá mapeia a porta de saudação em qual Olá serviço está escutando em Olá contêiner tooa porta no host de saudação. Adicionar um `PortBinding` elemento `ContainerHostPolicies` elemento do arquivo de ApplicationManifest.xml hello.  Neste artigo, `ContainerPort` é 80 (contêiner Olá expõe a porta 80, Olá especificado no Dockerfile) e `EndpointRef` é "Guest1TypeEndpoint" (Olá definido anteriormente no manifesto do serviço de saudação do ponto de extremidade).  Solicitações de entrada toohello na porta 8081 são mapeados tooport 80 no contêiner de saudação.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Definir autenticação do registro de contêiner
Configurar a autenticação de registro de contêiner adicionando `RepositoryCredentials` muito`ContainerHostPolicies` do arquivo applicationmanifest. XML de saudação. Adicione Olá conta e senha Olá myregistry.azurecr.io contêiner do registro, que permite que a imagem de contêiner de Olá Olá serviço toodownload do repositório de saudação.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

É recomendável que você criptografe a senha do repositório hello usando um certificado de codificação que implantou tooall nós de cluster de saudação. Quando o Service Fabric implanta Olá serviço pacote toohello, certificado de codificação de saudação é toodecrypt usado Olá codificação texto.  Olá Invoke-ServiceFabricEncryptText cmdlet é usado toocreate Olá codificação texto senha hello, que é adicionado toohello ApplicationManifest.xml arquivo.

Olá script a seguir cria um novo certificado autoassinado e exporta-o arquivo PFX de tooa.  certificado de saudação é importado para um cofre de chave existente e, em seguida, implantados cluster do Service Fabric toohello.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Criptografar a senha hello usando Olá [ServiceFabricEncryptText Invoke](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Substitua a senha de saudação com texto cifrado de saudação retornado por Olá [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet e defina `PasswordEncrypted` muito "true".

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Configurar o modo de isolamento
O Windows dá suporte a dois modos de isolamento para contêineres: processo e Hyper-V. Com o modo de isolamento do processo de hello, todos os contêineres de saudação em execução no hello mesmo host máquina compartilhamento saudação do kernel com o host de saudação. Com o modo de isolamento Olá Hyper-V, kernels Olá são isolados entre cada contêiner do Hyper-V e o host do contêiner hello. modo de isolamento de saudação é especificado em Olá `ContainerHostPolicies` elemento no arquivo de manifesto de aplicativo hello. modos de isolamento de saudação que podem ser especificados são `process`, `hyperv`, e `default`. modo de isolamento padrão Olá padrões muito`process` no Windows Server hospeda e os padrões muito`hyperv` em hosts do Windows 10. Olá trecho a seguir mostra como o modo de isolamento de saudação é especificado no arquivo de manifesto de aplicativo hello.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Configurar governança de recursos
[Governança de recursos](service-fabric-resource-governance.md) restringe Olá podem usar recursos que Olá contêiner no host de saudação. Olá `ResourceGovernancePolicy` elemento, que é especificado no manifesto de aplicativo hello, é usado toodeclare limites de recurso para um pacote de código de serviço. Limites de recurso podem ser definidos para Olá recursos a seguir: memória, MemorySwap, CpuShares (peso relativo da CPU), MemoryReservationInMB, BlkioWeight (BlockIO peso relativo).  Neste exemplo, o pacote de serviço Guest1Pkg obtém um núcleo em nós de cluster Olá onde ele é colocado.  Limites de memória são absolutos, para o pacote de códigos Olá seja limitado too1024 MB de memória (e uma reserva de garantia de software de Olá mesmo). Pacotes de código (contêineres ou processos) não são tooallocate capaz de mais memória do que esse limite e tentar toodo pode resultar em uma exceção de falta de memória. Para toowork de imposição de limite de recursos, todos os pacotes de código dentro de um pacote de serviço devem ter limites de memória especificados.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Implantar o aplicativo de contêiner hello
Salvar todas as suas alterações e compile o aplicativo hello. toopublish seu aplicativo, o botão direito do mouse em **MyFirstContainer** no Gerenciador de soluções e selecione **publicar**.

Em **ponto de extremidade de Conexão**, insira o ponto de extremidade de gerenciamento Olá para cluster hello.  Por exemplo, "containercluster.westus2.cloudapp.azure.com:19000". Você pode encontrar a conexão de cliente Olá ponto de extremidade na folha de visão geral de saudação para seu cluster em Olá [portal do Azure](https://portal.azure.com).

Clique em **Publicar**.

O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos e nós em um cluster do Service Fabric. Abra um navegador e navegue toohttp://containercluster.westus2.cloudapp.azure.com:19080 Explorer/e siga a implantação do aplicativo hello.  aplicativo Hello implanta, mas está em estado de erro até Olá imagem é baixada em nós de cluster de saudação (que podem levar algum tempo, dependendo do tamanho da imagem Olá): ![erro][1]

aplicativo Hello está pronto quando ele está em ```Ready``` estado: ![pronto][2]

Abra um navegador e navegue toohttp://containercluster.westus2.cloudapp.azure.com:8081. Você deve ver Olá título "Hello World!" Exibir no navegador de saudação.

## <a name="clean-up"></a>Limpar
Continue tooincur encargos enquanto Olá cluster está em execução, considere [excluindo o cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  [Clusters de terceiros](http://tryazureservicefabric.westus.cloudapp.azure.com/) são excluídos automaticamente após algumas horas.

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
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

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

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
