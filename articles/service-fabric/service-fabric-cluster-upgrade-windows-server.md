---
title: aaaUpgrade independente do Azure Service Fabric do cluster no Windows Server | Microsoft Docs
description: "Atualize o código do Azure Service Fabric hello e/ou configuração que é executado de um cluster de malha do serviço autônomo, incluindo a definição do modo de atualização de cluster hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Atualize seu cluster autônomo do Azure Service Fabric no Windows Server
> [!div class="op_single_selector"]
> * [Cluster do Azure](service-fabric-cluster-upgrade.md)
> * [Cluster Independente](service-fabric-cluster-upgrade-windows-server.md)
>
>

Para qualquer sistema moderno, Olá capacidade tooupgrade é um sucesso a longo prazo toohello chave do produto. Um cluster do Azure Service Fabric é um recurso que pertence a você. Este artigo descreve como você pode verificar se as que versões com suporte do código de malha do serviço e configurações de cluster Olá sempre é executado.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Versão do Service Fabric do controle Olá que é executado em seu cluster
tooset toodownload seu cluster de atualizações de malha do serviço quando a Microsoft lança uma nova versão, conjunto Olá **fabricClusterAutoupgradeEnabled** tootrue de configuração de cluster. uma versão com suporte de malha do serviço que você deseja que seu toobe de cluster no conjunto de saudação do tooselect **fabricClusterAutoupgradeEnabled** toofalse de configuração de cluster.

> [!NOTE]
> Certifique-se de que o cluster sempre esteja executando uma versão do Service Fabric com suporte. Quando a Microsoft anuncia versão saudação de uma nova versão do Service Fabric, versão anterior do hello está marcado para fim do suporte depois que um mínimo de 60 dias da data de saudação do anúncio de saudação. Novas versões são anunciadas [no blog da equipe do Service Fabric Olá](https://blogs.msdn.microsoft.com/azureservicefabric/). Olá nova versão está disponível toochoose nesse ponto.
>
>

Você pode atualizar a nova versão do cluster toohello somente se você estiver usando uma configuração de nó de estilo de produção, onde cada nó do Service Fabric é alocado em uma máquina virtual ou física separada. Se você tiver um cluster de desenvolvimento, onde mais de um nó de malha do serviço estiver em um único computador físico ou virtual, você deve recriar Olá cluster com a nova versão de hello.

Dois fluxos de trabalho distintos podem atualizar sua versão mais recente do cluster toohello ou uma versão com suporte do Service Fabric. Um fluxo de trabalho é para clusters que têm a versão mais recente da conectividade toodownload Olá automaticamente. Olá outro fluxo de trabalho é para clusters que não têm conectividade toodownload hello mais recente do Service Fabric versão.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Atualizar clusters que têm a configuração e o código mais recente da conectividade toodownload Olá
Usar essas etapas tooupgrade sua versão de tooa com suporte de cluster se os nós de cluster tem conectividade com a Internet muito[http://download.microsoft.com](http://download.microsoft.com).

Para clusters que têm conectividade muito[http://download.microsoft.com](http://download.microsoft.com), Microsoft verifica periodicamente se há disponibilidade de saudação de novas versões do Service Fabric.

Quando uma nova versão do Service Fabric está disponível, o pacote de saudação seja baixado localmente toohello cluster e provisionado para atualização. Além disso, tooinform Prezado cliente dessa nova versão, o sistema Olá mostra um aviso de integridade do cluster explícita é toohello semelhante a seguir:

"suporte de versão [versão #] do cluster atual Olá termina [Date]."

Depois que o cluster de saudação está executando a versão mais recente do hello, aviso Olá desaparece.

#### <a name="cluster-upgrade-workflow"></a>Fluxo de trabalho de atualização do cluster
Depois de ver o aviso de integridade do cluster hello, Olá a seguir:

1. Conecte o cluster de toohello de qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós de cluster de saudação. máquina de saudação que esse script é executado no não tem toobe parte do cluster de saudação.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Obter lista de saudação de versões de malha do serviço que você pode atualizar para.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Você deve obter um toothis semelhante de saída:

    ![obter versões de malha][getfabversions]
3. Inicie uma versão disponível do tooan de atualização de cluster usando o [ServiceFabricClusterUpgrade início](https://msdn.microsoft.com/library/mt125872.aspx) cmd do PowerShell.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   progresso de saudação do toomonitor de atualização de hello, você pode usar o Service Fabric Explorer ou Olá executar comando do Windows PowerShell a seguir.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida. toospecify diretivas de integridade personalizado para Olá **início ServiceFabricClusterUpgrade** command, consulte a documentação para [ServiceFabricClusterUpgrade início](https://msdn.microsoft.com/library/mt125872.aspx).

Depois de corrigir problemas de saudação que resultaram em reversão Olá, inicie novamente a atualização de saudação Olá seguir as mesmas etapas conforme descritas anteriormente.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Atualizar clusters que têm <U>nenhuma conectividade</u> toodownload hello mais recente código e configuração
Usar essas etapas tooupgrade sua versão de tooa com suporte de cluster se os nós de cluster não tem conectividade com a Internet muito[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Se você estiver executando um cluster que não seja toohello conectado à Internet, você terá toomonitor Olá Service Fabric team blog toolearn sobre uma nova versão. Olá sistema não mostrar um tooalert de aviso de integridade do cluster de uma nova versão.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Provisionamento automático vs provisionamento manual
download automático de tooenable e o registro para a versão mais recente do código Olá, configurar o serviço de atualização de malha. Consulte toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro Olá [pacote autônomo](service-fabric-cluster-standalone-package-contents.md) para obter instruções.
Processo manual, siga as instruções de saudação abaixo.

Modifique seu Olá de tooset de configuração de cluster toofalse de propriedade a seguir antes de iniciar uma atualização de configuração.

        "fabricClusterAutoupgradeEnabled": false,

Consulte também[ServiceFabricClusterConfigurationUpgrade início PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para obter detalhes de uso. Verifique se tooupdate 'clusterConfigurationVersion' em seu JSON antes de iniciar a atualização de configuração de saudação.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Fluxo de trabalho de atualização do cluster

1. Execute Get-ServiceFabricClusterUpgrade em um de nós de saudação em cluster hello e anote Olá TargetCodeVersion.
2. Seguinte Olá execução de um toolist de computador conectado à internet todas as versões compatíveis com a versão atual do hello de atualização e baixar Olá correspondente do pacote de links de download associadas hello.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Conecte o cluster de toohello de qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós de cluster de saudação. máquina de saudação que esse script é executado no não tem toobe parte do cluster Olá

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Copie o pacote de saudação baixada no repositório de imagens de cluster hello.

5. Registre pacote hello copiado.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Inicie uma versão disponível do tooan de atualização de cluster.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Você pode monitorar o progresso de saudação de atualização de saudação no Gerenciador do Service Fabric, ou você pode executar Olá comando PowerShell a seguir.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Se as diretivas de integridade do cluster Olá não forem atendidas, atualização de saudação é revertida. políticas de integridade personalizado toospecify para hello **ServiceFabricClusterUpgrade início** command, consulte a documentação de saudação do [ServiceFabricClusterUpgrade início](https://msdn.microsoft.com/library/mt125872.aspx).

Depois de corrigir problemas de saudação que resultaram em reversão Olá, inicie novamente a atualização de saudação Olá seguir as mesmas etapas conforme descritas anteriormente.


## <a name="upgrade-hello-cluster-configuration"></a>Atualizar a configuração de cluster Olá
Antes de iniciar a atualização de configuração hello, você pode testar o json de configuração do cluster novo, executando o script do powershell Olá no pacote autônomo de saudação.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
ou o

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Algumas configurações não podem ser atualizadas, como pontos de extremidade, nome do cluster, nó IP, etc. Isso testará Olá novo cluster configuração json contra Olá antigo e geram erros na janela do Powershell hello, se houver qualquer problema.

atualização de configuração de cluster de saudação tooupgrade, execute **ServiceFabricClusterConfigurationUpgrade início**. atualização de configuração de saudação é processado domínio de atualização por domínio de atualização.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Atualização da configuração do certificado do cluster  
Certificado de cluster é usado para autenticação entre os nós de cluster, para o certificado de saudação sobrepor deve ser executada com muito cuidado porque falha bloqueará a comunicação de saudação entre nós de cluster.  
Tecnicamente, há três opções com suporte:  

1. Atualização de certificado único: caminho de atualização de saudação é ' certificado (primária) -> B de certificado (primária) -> C de certificado (primária) ->... '.   
2. Atualização de certificado duplo: Olá caminho de atualização é ' -> (primário) do certificado do certificado (primária) e B (secundários) -> B de certificado (primária) -> B de certificado (primária) e C (secundários) -> C de certificado (primária) ->... '.
3. Atualização do tipo de certificado: configuração de certificados com base em CommonName configuração <-> com base em impressão digital do certificado. Por exemplo, impressão digital do certificado (primária) e a impressão digital B (secundários) -> certificado CommonName C.


## <a name="next-steps"></a>Próximas etapas
* Saiba como toocustomize alguns [configurações de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).
* Saiba como muito[escalar horizontalmente o seu cluster](service-fabric-cluster-scale-up-down.md).
* Saiba mais sobre [atualizações de aplicativo](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
