---
title: "aaaAzure Service Fabric com início rápido do gerenciamento de API | Microsoft Docs"
description: "Este guia mostra como tooquickly Introdução ao gerenciamento de API do Azure e do Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Service Fabric com início rápido de Gerenciamento de API

Este guia mostra como tooset até gerenciamento de API do Azure com o Service Fabric e configurar sua primeira API operação toosend tráfego tooback ponta os serviços no Service Fabric. toolearn mais informações sobre cenários de gerenciamento de API do Azure com o Service Fabric, consulte Olá [visão geral](service-fabric-api-management-overview.md) artigo. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>Implantar o gerenciamento de API e do Service Fabric tooAzure

Olá primeira etapa é toodeploy gerenciamento de API e um tooAzure de cluster do Service Fabric em uma rede Virtual compartilhada. Isso permite que toocommunicate de gerenciamento de API diretamente com o Service Fabric para executar descoberta de serviço, resolução de partição de serviço e encaminhar o tráfego diretamente tooany back-end do serviço na malha do serviço.

### <a name="topology"></a>Topologia

Este guia implanta seguinte Olá tooAzure de topologia em que o gerenciamento de API e do Service Fabric estejam em sub-redes de Olá mesma rede Virtual:

 ![Legenda de imagem][sf-apim-topology-overview]

modelos do Gerenciador de recursos tooget início rápido, são fornecidos para cada etapa de implantação:

 - Topologia de rede:
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Cluster do Service Fabric:
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - Gerenciamento de API:
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>Entre no tooAzure e selecione sua assinatura

Este guia usa o [Azure PowerShell][azure-powershell]. Quando você inicia uma nova sessão do PowerShell, entre no tooyour conta do Azure e selecione sua assinatura antes de executar comandos do Azure.
 
Entre tooyour conta do Azure:

```powershell
PS > Login-AzureRmAccount
```

Selecione sua assinatura:

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Crie um novo grupo de recursos para sua implantação. Dê um nome e um local.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Implantar a topologia de rede Olá

Olá primeira etapa é tooset backup toowhich de topologia de rede Olá API de gerenciamento e cluster do Service Fabric Olá será implantado. Olá [network.json] [ network-arm] modelo do Gerenciador de recursos é toocreate configurado uma rede Virtual (VNET) com duas sub-redes e dois grupos de segurança de rede (NSG). 

Olá [network.parameters.json] [ network-parameters-arm] arquivo de parâmetros contém nomes de saudação de sub-redes hello e NSGs gerenciamento de API e a malha do serviço serão implantado. Para este guia, os valores de parâmetro hello não é necessário toobe alterado. modelos de gerenciamento de API e o Gerenciador de recursos de malha do serviço Olá usam esses valores, para que se eles são modificados, você deve modificar no hello outros modelos do Gerenciador de recursos adequadamente. 

 1. Baixe Olá arquivo de modelo e os parâmetros do Gerenciador de recursos a seguir:

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. Use Olá PowerShell toodeploy Olá Gerenciador de recursos modelo e o parâmetro de arquivos de comando para configurar uma rede Olá a seguir:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Implantar um cluster do Service Fabric Olá

Depois de terminarem de recursos de rede Olá implantando, Olá próxima etapa é toodeploy um toohello de cluster do Service Fabric rede virtual na sub-rede hello e NSG designado para o cluster do Service Fabric hello. Para este tutorial, o modelo de serviço Gerenciador de recursos de malha de Olá é toouse pré-configurado Olá nomes Olá rede virtual, sub-rede e NSG que você configurou na etapa anterior Olá. 

modelo de Gerenciador de recursos de cluster Olá Service Fabric é configurado toocreate um cluster seguro com segurança de certificado. certificado de saudação é comunicação de nó para nó toosecure usado para o cluster e o cluster do Service Fabric do toomanage usuário acesso tooyour. Gerenciamento de API usa saudação de tooaccess este certificado o serviço de nomes de malha de serviço para descoberta de serviço.

Esta etapa exige ter um certificado no Key Vault para segurança de cluster. Para obter mais informações sobre como configurar um cluster seguro com o Key Vault, consulte [este guia em criar um cluster no Azure usando o Resource Manager](service-fabric-cluster-creation-via-arm.md)

> [!NOTE]
> Você pode adicionar a autenticação do Active Directory do Azure em adição toohello certificado usado para acesso ao cluster. Active Directory do Azure é hello recomendado cluster do Service Fabric tooyour de acesso do modo toomanage usuário, mas é toocomplete não é necessário neste tutorial. Um certificado é exigido de qualquer forma para a segurança de nó para nó de cluster e para autenticação de Gerenciamento de API do Azure, que atualmente não oferece suporte para autenticação com Azure Active Directory para back-end do Service Fabric.

 1. Baixe Olá arquivo de modelo e os parâmetros do Gerenciador de recursos a seguir:
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. Preenchimento nos parâmetros vazio Olá Olá `cluster.parameters.json` arquivo para sua implantação, incluindo Olá [informações de Cofre de chaves](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) para o seu certificado de cluster.

 3. Use Olá PowerShell comando toodeploy Olá Gerenciador de recursos modelo e o parâmetro arquivos toocreate Olá cluster do Service Fabric a seguir:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Implantar o Gerenciamento de API

Por fim, implantar o gerenciamento de API toohello rede virtual na sub-rede hello e NSG designado para gerenciamento de API. Você não precisa toowait para Olá toofinish de implantação de cluster de malha do serviço antes de implantar o gerenciamento de API. 

Para este tutorial, modelo do Gerenciador de recursos de gerenciamento de API de saudação é pré-configurado toouse Olá nomes Olá rede virtual, sub-rede e NSG que você configurou na etapa anterior hello. 

 1. Baixe Olá arquivo de modelo e os parâmetros do Gerenciador de recursos a seguir:
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. Preenchimento nos parâmetros vazio Olá Olá `apim.parameters.json` para sua implantação.

 3. Use Olá seguintes PowerShell comando toodeploy Olá Gerenciador de recursos modelo e o parâmetro de arquivos para o gerenciamento de API:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>Configurar o Gerenciamento de API

Uma vez que o cluster do Service Fabric e o Gerenciamento de API tenha sido implantado será possível configurar um back-end do Service Fabric no Gerenciamento de API. Isso permite que você toocreate uma política de serviço de back-end que envia o cluster do tráfego tooyour do Service Fabric.

### <a name="api-management-security"></a>Segurança de Gerenciamento de API

back-end do Service Fabric de saudação tooconfigure, é necessário primeiro tooconfigure as configurações de segurança do gerenciamento de API. configurações de segurança tooconfigure, vá tooyour API do serviço de gerenciamento em Olá portal do Azure.

#### <a name="enable-hello-api-management-rest-api"></a>Habilitar Olá API de REST de gerenciamento de API

Olá API REST de API de gerenciamento está atualmente Olá tooconfigure somente da forma um serviço de back-end. Olá primeira etapa é tooenable hello API de REST de gerenciamento de API e protegê-lo.

 1. No serviço de gerenciamento de API de Olá, selecione **API de gerenciamento - visualização** em **segurança**.
 2. Verificar Olá **Habilitar API REST de gerenciamento de API** caixa de seleção.
 3. Observação: Olá URL da API de gerenciamento - esta é a URL Olá usaremos posterior tooset o back-end do Service Fabric de saudação
 4. Gerar um **Token de acesso** selecionando uma data de expiração e uma chave, em seguida, clique em Olá **gerar** botão em direção à parte inferior de saudação da página de saudação.
 5. Saudação de cópia **token de acesso** e salvá-lo - usaremos isso Olá etapas a seguir. Observe que isso é diferente da chave de saudação primária e secundária.

#### <a name="upload-a-service-fabric-client-certificate"></a>Upload de um certificado do cliente do Service Fabric

Gerenciamento de API deve ser autenticado com o cluster do Service Fabric para descoberta de serviço usando um certificado de cliente que tem acesso tooyour cluster. Para simplificar, este tutorial usa Olá mesmo certificado especificado durante a criação de cluster do Service Fabric hello, o que, por padrão, pode ser usado tooaccess seu cluster.

 1. No serviço de gerenciamento de API de Olá, selecione **certificados de cliente - visualização** em **segurança**.
 2. Clique em Olá **+ adicionar** botão
 2. Selecione Olá arquivo de chave privada (. pfx) do certificado de cluster Olá que você especificou ao criar o cluster do Service Fabric, dê a ele um nome e fornecer a senha da chave privada hello.

> [!NOTE]
> Este tutorial usa Olá mesmo certificado de segurança do cliente autenticação e o cluster de nó para nó. Você pode usar um certificado de cliente separados se você tiver um tooaccess configurado o cluster do Service Fabric.

### <a name="configure-hello-backend"></a>Configurar Olá back-end

Agora que a configuração de segurança do gerenciamento de API, você pode configurar o back-end do hello Service Fabric. Para a malha do serviço back-ends, cluster do Service Fabric Olá é Olá back-end, em vez de um serviço de malha do serviço específico. Isso permite que toomore de tooroute uma única política de um serviço em cluster hello.

Esta etapa requer um token de acesso de saudação gerada anteriormente e Olá a impressão digital do seu certificado de cluster que você carregou tooAPI gerenciamento na etapa anterior hello.

> [!NOTE]
> Se você usou um certificado de cliente separado na etapa anterior Olá para gerenciamento de API, você precisa de impressão digital de Olá Olá certificado de cliente em adição toohello cluster impressão digital de certificado nesta etapa.

Envie Olá toohello de solicitação HTTP PUT URL de API de gerenciamento de API observado anteriormente ao habilitar o serviço de back-end do hello API de REST de gerenciamento de API tooconfigure Olá malha do serviço a seguir. Você deve ver uma `HTTP 201 Created` resposta ao comando Olá terá êxito. Para obter mais informações sobre cada campo, consulte Olá gerenciamento de API [documentação de referência de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

Comando HTTP e URL:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

Cabeçalhos de solicitação:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Corpo da solicitação:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Olá **url** parâmetro aqui é um nome de serviço totalmente qualificado de um serviço em cluster que todas as solicitações são roteadas tooby padrão se nenhum nome de serviço é especificado em uma política de back-end. Você pode usar um nome de serviço falsos, como "fabric: / falso/serviço" Se você não pretende toohave um serviço de fallback.

Consulte toohello gerenciamento de API [documentação de referência de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) para obter mais detalhes sobre cada campo.

#### <a name="example"></a>Exemplo

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Implantar um serviço de back-end do Service Fabric

Agora que você tem Olá que Service Fabric configurado como um gerenciamento de tooAPI de back-end, você pode criar políticas de back-end para suas APIs que enviam tráfego tooyour os serviços do Service Fabric. Mas primeiro você precisa de um serviço em execução no Service Fabric tooaccept solicitações.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Criar um serviço do Service Fabric com um ponto de extremidade HTTP

Para este tutorial, criaremos um básica sem monitoração de estado ASP.NET Core serviço confiável usando o modelo de projeto de API da Web saudação padrão. Isso cria um ponto de extremidade HTTP para o seu serviço que será exposto através do Gerenciamento de API do Azure:

```
/api/values
```

Inicie [configurando seu ambiente de desenvolvimento para o desenvolvimento de ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Após configurar seu ambiente de desenvolvimento, inicie o Visual Studio como Administrador e crie um serviço ASP.NET Core:

 1. No Visual Studio, selecione Arquivo -> Novo projeto.
 2. Selecione o modelo de aplicativo do Service Fabric Olá em nuvem e nomeie- **"ApiApplication"**.
 3. Selecione hello modelo de serviço do ASP.NET Core e o projeto de saudação do nome **"WebApiService"**.
 4. Selecione o modelo de projeto Olá Web API ASP.NET Core 1.1.
 5. Depois de criar o projeto hello, abra `PackageRoot\ServiceManifest.xml` e remover Olá `Port` atributo da configuração de recurso de ponto de extremidade de saudação:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Isso permite Service Fabric toospecify uma porta dinamicamente a partir do intervalo de portas do aplicativo hello, que são abertas pelo Olá grupo de segurança de rede no modelo de Gerenciador de recursos de cluster Olá, permitindo que o tráfego tooflow tooit do gerenciamento de API.
 
 6. Pressione F5 na API da web do hello Visual Studio tooverify está disponível localmente. 

    Abra o Gerenciador do Service Fabric e Detalhar tooa a instância específica de saudação ASP.NET Core toosee Olá endereço base Olá serviço está escutando. Adicionar `/api/values` toohello endereço base e abri-lo em um navegador. Isso chama Olá método Get em Olá ValuesController no modelo de API da Web hello. Ele retorna a resposta padrão Olá fornecida pelo modelo hello, uma matriz JSON que contém duas cadeias de caracteres:

    ```json
    ["value1", "value2"]`
    ```

    Este é o ponto de extremidade de saudação que irá expor por meio do gerenciamento de API no Azure.

 7. Por fim, implante o cluster de tooyour Olá aplicativo no Azure. [Usando o Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), projeto de aplicativo hello e selecione **publicar**. Forneça seu ponto de extremidade do cluster (por exemplo, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy Olá aplicativo tooyour malha do serviço de cluster no Azure.

Um serviço sem estado ASP.NET Core nomeado `fabric:/ApiApplication/WebApiService` agora deve estar em execução no seu cluster do Service Fabric no Azure.

## <a name="create-an-api-operation"></a>Criar uma operação de API

Agora estamos pronto toocreate uma operação no gerenciamento de API que toocommunicate de uso de clientes externos com hello serviço sem monitoração de estado do ASP.NET Core em execução no cluster do Service Fabric hello.

 1. Faça logon no portal do Azure de toohello e navegue tooyour implantação do serviço de gerenciamento de API.
 2. Na folha de serviço de gerenciamento de API hello, selecione **APIs - visualização**
 3. Adicionar uma nova API clicando Olá **API em branco** caixa e preenchendo a caixa de diálogo hello:

     - **URL do serviço Web**: para back-ends do Service Fabric esse valor de URL não é utilizado. Aqui, você pode colocar qualquer valor. Neste tutorial, utilize: `http://servicefabric`.
     - **Nome**: forneça qualquer nome para sua API. Neste tutorial, utilize `Service Fabric App`.
     - **Esquema de URL**: selecione HTTP, HTTPS ou ambos. Neste tutorial, utilize `both`.
     - **Sufixo de URL da API**: forneça um sufixo para a API. Neste tutorial, utilize `myapp`.
 
 4. Depois de criar hello API, clique em **+ Adicionar operação** operação tooadd uma API de front-end. Preencha valores hello:
    
     - **URL**: selecione `GET` e fornecer um caminho de URL para Olá API. Neste tutorial, utilize `/api/values`.
     
       Por padrão, o caminho de URL Olá especificado aqui é o caminho da URL Olá enviado toohello serviço de malha do serviço de back-end. Se você usar o hello mesmo caminho URL aqui que o serviço usa, nesse caso `/api/values`, em seguida, a operação de saudação funciona sem modificações adicionais. Você também pode especificar um caminho de URL aqui o que é diferente do caminho da URL Olá usado pelo seu back-end, o serviço de malha do serviço, caso em que você vai também toospecify necessidade de reconfiguração de um caminho em sua política de operação mais tarde.
     - **Nome de exibição**: forneça qualquer nome para Olá API. Neste tutorial, utilize `Values`.

## <a name="configure-a-backend-policy"></a>Configure uma política de back-end

política de back-end Olá reúne tudo. Isso é onde você configura o back-end Olá Service Fabric toowhich solicitações são roteadas. Você pode aplicar essa operação da API tooany política. Olá [configuração de back-end para a malha do serviço](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) fornece controles de roteamentos de solicitação a seguir hello: 
 - Seleção de instância de serviço especificando um nome de instância de serviço do Service Fabric, ou codificados (por exemplo, `"fabric:/myapp/myservice"`) ou gerado a partir da solicitação HTTP de saudação (por exemplo, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Resolução de partição gerando uma chave de partição utilizando qualquer esquema de particionamento do Service Fabric.
 - Seleção de réplica para serviços com estado.
 - Resolução Repita condições que permitem que você toospecify condições de saudação para resolver novamente um local de serviço e reenviar uma solicitação.

Para este tutorial, crie uma política de back-end que rotas diretamente solicitações toohello serviço sem monitoração de estado do ASP.NET Core implantado anteriormente:

 1. Selecionar e editar Olá **políticas de entrada** para Olá `Values` operação clicando em Editar hello e, em seguida, selecionando **visualização de código**.
 2. No editor de código de diretiva hello, adicione um `set-backend-service` política em políticas de entrada, conforme mostrado a seguir e clique em Olá **salvar** botão:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Para um conjunto completo de atributos de política de back-end do Service Fabric, consulte toohello [documentação de back-end do gerenciamento de API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Adicione Olá API tooa produto. 

Antes de chamar a API de hello, ele deve ser adicionado tooa produto onde você pode conceder acesso toousers. 

 1. No serviço de gerenciamento de API de Olá, selecione **produtos - visualização**.
 2. Por padrão, o Gerenciamento de API oferece dois produtos: Starter e Ilimitado. Selecione produto ilimitados hello.
 3. Selecione APIs.
 4. Clique em Olá **+ adicionar** botão.
 5. Selecione Olá `Service Fabric App` API que você criou nas etapas anteriores hello e clique em Olá **selecione** botão.

### <a name="test-it"></a>Testá-lo

Agora você pode tentar enviar uma solicitação de serviço de back-end de tooyour na malha do serviço por meio do gerenciamento de API diretamente da saudação portal do Azure.

 1. No serviço de gerenciamento de API de Olá, selecione **API - visualização**.
 2. Em Olá `Service Fabric App` API que você criou nas etapas anteriores do hello, selecione Olá **teste** guia.
 3. Clique em Olá **enviar** botão toosend um serviço de back-end de toohello de solicitação de teste.

## <a name="next-steps"></a>Próximas etapas

Neste ponto, é possível ter uma configuração básica com o Service Fabric e o Gerenciamento de API.

Este tutorial usa a autenticação do usuário básica baseada em certificado para sua tooget de cluster do Service Fabric que configurar rapidamente. A autenticação de usuário mais avançada para o cluster do Service Fabric é preferível com a [autenticação Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Em seguida, [criar e configurar as configurações avançadas de produto no gerenciamento de API do Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare seu aplicativo para o tráfego do mundo real.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
