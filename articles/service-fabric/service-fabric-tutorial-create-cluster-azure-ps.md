---
title: "aaaCreate uma malha do serviço de cluster no Azure | Microsoft Docs"
description: Saiba como toocreate um Windows ou Linux Service Fabric do cluster no Azure usando o PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Criar um cluster seguro no Azure usando o PowerShell
Este tutorial mostra como toocreate uma malha do serviço de cluster (Windows ou Linux) em execução no Azure. Quando você terminar, você tem um cluster em execução na nuvem Olá que você pode implantar aplicativos.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um cluster do Service Fabric seguro no Azure usando o PowerShell
> * Cluster Olá seguro com um certificado x. 509
> * Conecte-se o cluster toohello usando o PowerShell
> * Remover um cluster

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial:
- Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Instalar Olá [módulo SDK do Service Fabric e do PowerShell](service-fabric-get-started.md)
- Instalar Olá [Azure Powershell versão 4.1 ou superior do módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Olá procedimento a seguir cria uma visualização (única máquina virtual) de nó único cluster do Service Fabric. cluster de saudação é protegida por um certificado autoassinado que obtém criado juntamente com cluster hello e, em seguida, é colocado em um cofre de chaves. Clusters de nó único não podem ser escaladas além de uma máquina virtual e clusters de visualização não podem ser atualizado toonewer versões.

custo toocalculate executando em um cluster do Service Fabric no uso do Azure Olá [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/).
Para obter mais informações sobre a criação de clusters do Service Fabric, confira [Criar um cluster do Service Fabric usando o Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Criar cluster hello usando o PowerShell do Azure
1. Baixar uma cópia local do modelo do Azure Resource Manager hello e arquivo de parâmetro de saudação do hello [modelo do Gerenciador de recursos do Azure para Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repositório GitHub.  *azuredeploy.JSON* é hello Azure Resource Manager modelo que define um cluster do Service Fabric. *azuredeploy.Parameters.JSON* é um arquivo de parâmetros para a implantação de cluster toocustomize hello.

2. Personalizar Olá Olá parâmetros a seguir *azuredeploy.parameters.json* arquivo de parâmetros:

   | Parâmetro       | Descrição | Valor sugerido |
   | --------------- | ----------- | --------------- |
   | clusterLocation | cluster do Hello região do Azure toowhich toodeploy hello. | *Por exemplo, westeurope, eastasia, eastus* |
   | clusterName     | Nome do cluster Olá deseja toocreate. | *Por exemplo, bobs-sfpreviewcluster* |
   | adminUserName   | conta de administrador local Olá em Olá cluster das máquinas virtuais. | *Qualquer nome de usuário válido do Windows Server* |
   | adminPassword   | Senha da conta de administrador local Olá em Olá cluster das máquinas virtuais. | *Qualquer senha válida do Windows Server* |
   | clusterCodeVersion | Olá toorun de versão do Service Fabric. (255.255.X.255 são versões de visualização). | **255.255.5718.255** |
   | vmInstanceCount | número de saudação de máquinas virtuais no cluster (pode ser 1 ou 3-99). | **1** | *Para um cluster de visualização, especifique apenas uma máquina virtual* |

3. Abra um console do PowerShell, tooAzure de logon e selecione assinatura Olá desejada toodeploy Olá cluster em:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Criar e criptografar uma senha para Olá toobe de certificado usado pelo serviço de malha.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Crie cluster hello e seu certificado executando Olá comando a seguir:

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >Olá `-CertificateSubjectName` parâmetro deve ser alinhadas com o parâmetro hello clusterName especificado no arquivo de parâmetros de hello, bem como Olá domínio vinculado toohello região do Azure você escolher, como: `clustername.eastus.cloudapp.azure.com`.

Quando termina a configuração hello, ele produz informações sobre cluster Olá criado no Azure. Ele também copia Olá cluster certificado toohello - CertificateOutputFolder directory no caminho de saudação especificado para esse parâmetro. É necessário tooaccess esse certificado Service Fabric Explorer e exibir a integridade de saudação do cluster.

Anote a URL Olá para o cluster, o que pode ser semelhante toohello URL a seguir: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>& Modificar certificado Olá acessar Gerenciador do Service Fabric ##

1. Clique duas vezes em Olá tooopen de certificado Olá Assistente de importação de certificado.

2. Usar as configurações padrão, mas verifique se Olá de toocheck **marcar esta chave como exportável.** caixa de seleção, Olá **proteção de chave privada** etapa. O Visual Studio precisa certificado de saudação tooexport ao configurar a autenticação de Cluster de malha do registro de contêiner do Azure tooService posteriormente neste tutorial.

3. Agora você pode abrir o Service Fabric Explorer em um navegador. toodo assim, navegar toohello **ManagementEndpoint** URL para o cluster usando um navegador da web e um certificado de saudação select que foi salvo no seu computador.

>[!NOTE]
>Ao abrir o Service Fabric Explorer, você verá um erro de certificado, pois está usando um certificado autoassinado. Na borda, você tem tooclick *detalhes* e, em seguida, Olá *ir na página da Web de toohello* link. No Chrome, você tem tooclick *avançado* e, em seguida, Olá *continuar* link.

>[!NOTE]
>Se a criação do cluster Olá falhar, sempre pode ser executada comando hello, que atualiza os recursos de saudação já implantados. Se um certificado foi criado como parte da implantação de saudação falhada, um novo será gerado. tootroubleshoot criação do cluster, consulte [criar um cluster do Service Fabric usando o Gerenciador de recursos do Azure](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Conecte-se o cluster seguro toohello
Conecte o cluster toohello usando Olá Service Fabric PowerShell module instalada com hello SDK do Service Fabric.  Primeiro, instale o certificado de saudação no repositório de pessoal (Meu) de saudação do usuário atual de saudação em seu computador.  Execute Olá comando PowerShell a seguir:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Agora você está pronto tooconnect tooyour segura cluster.

Olá **Service Fabric** módulo do PowerShell fornece vários cmdlets para gerenciar clusters, aplicativos e serviços do Service Fabric.  Saudação de uso [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) tooconnect de cmdlet toohello cluster seguro. Olá a impressão digital do certificado e detalhes de ponto de extremidade de conexão são encontrados na saída de saudação de uma etapa anterior.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Verifique se você está conectado e cluster hello está íntegro usando Olá [ServiceFabricClusterHealth Get](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Limpar recursos

Um cluster é composto por outros recursos do Azure além de recurso de cluster toohello propriamente dito. cluster do Hello mais simples maneira toodelete hello e todos os recursos de saudação consome é o grupo de recursos de saudação do toodelete.

Faça logon no tooAzure e selecione Olá ID da assinatura com a qual você deseja que o cluster de saudação tooremove.  Você pode encontrar sua ID de assinatura fazendo logon em toohello [portal do Azure](http://portal.azure.com). Excluir grupo de recursos de saudação e todos os recursos de cluster de saudação usando Olá [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Criar um cluster do Service Fabric no Azure
> * Cluster Olá seguro com um certificado x. 509
> * Conecte-se o cluster toohello usando o PowerShell
> * Remover um cluster

Em seguida, Avançar toohello toolearn tutorial a seguir como toodeploy um aplicativo existente.
> [!div class="nextstepaction"]
> [Implantar um aplicativo existente do .NET com o Docker Compose](service-fabric-host-app-in-a-container.md)
