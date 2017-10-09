---
title: aaaSet um cluster do Azure Service Fabric | Microsoft Docs
description: "Guia de início rápido - criar um cluster do Service Fabric do Windows ou Linux no Azure."
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
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Criar seu primeiro cluster do Service Fabric no Azure
Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto de máquinas físicas ou virtuais conectadas em rede, no qual os microsserviços são implantados e gerenciados. Este guia de início rápido ajuda toocreate um cluster de cinco nós, em execução no Windows ou Linux, a saudação [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) ou [portal do Azure](http://portal.azure.com) em apenas alguns minutos.  

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.


## <a name="use-hello-azure-portal"></a>Use Olá portal do Azure

Faça logon no toohello portal do Azure em [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Criar cluster Olá

1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.
2. Selecione **de computação** de saudação **novo** folha e, em seguida, selecione **Cluster do Service Fabric** de saudação **de computação** folha.
3. Preenchimento de saudação do Service Fabric **Noções básicas sobre** formulário. Para **sistema operacional**, selecione a versão de saudação do Windows ou Linux que você deseja Olá toorun de nós de cluster. nome de usuário de saudação e a senha digitada aqui é toolog usada na máquina virtual de toohello. Para **Grupo de Recursos**, crie um novo. Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são criados e gerenciados coletivamente. Ao concluir, clique em **OK**.

    ![Saída da instalação do cluster][cluster-setup-basics]

4. Preencha Olá **configuração de Cluster** formulário.  Em **Contagem do tipo de nó**, digite "1".

5. Selecione **1 (primário) do tipo de nó** e o preenchimento Olá **configuração do tipo de nó** formulário.  Insira um nome de tipo de nó e defina Olá [a camada de durabilidade](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) muito "Bronze".  Selecione um tamanho de VM.

    Tipos de nós definem tamanho da VM hello, número de VMs, pontos de extremidade personalizados e outras configurações para Olá VMs desse tipo. Cada tipo de nó definido é configurado como um conjunto de escala de máquina virtual separada, que é usado toodeploy e máquinas virtuais gerenciadas como um conjunto. Cada tipo de nó pode ser dimensionado para cima ou para baixo de forma independente, tem conjuntos diferentes de portas abertas e pode ter métricas de capacidade diferentes.  Olá primeiro ou primário, tipo de nó é onde os serviços do sistema do Service Fabric hospedados e devem ter cinco ou mais VMs.

    Para qualquer implantação de produção, o [planejamento da capacidade](service-fabric-cluster-capacity.md) é uma etapa importante.  Para esse início rápido, no entanto, você não está executando aplicativos, portanto, escolha um tamanho de VM *DS1_v2 Padrão*.  Selecione "Prata" hello [camada de confiabilidade](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) e capacidade de 5 do conjunto de uma escala de inicial da máquina virtual.  

    Pontos de extremidade personalizados abrem portas no balanceador de carga do Azure Olá para que você pode se conectar com aplicativos em execução no cluster de saudação.  Insira "80, 8172" tooopen as portas 80 e 8172.

    Não verificar Olá **definir configurações avançadas** caixa, que é usada para personalizar os pontos de extremidade de gerenciamento de TCP/HTTP, intervalos de porta de aplicativo, [restrições de posicionamento](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), e [capacidade propriedades](service-fabric-cluster-resource-manager-metrics.md).    

    Selecione **OK**.

6. Em Olá **configuração de Cluster** formulário, defina **diagnóstico** muito**em**.  Para este guia de início rápido, você não precisa tooenter qualquer [configuração de malha](service-fabric-cluster-fabric-settings.md) propriedades.  Em **versão do Fabric**, selecione **automáticas** modo de atualização para que a Microsoft atualiza automaticamente a versão de saudação do código-malha Olá executando Olá cluster.  Definir o modo de saudação muito**Manual** se você quiser muito[escolher uma versão com suporte](service-fabric-cluster-upgrade.md) tooupgrade para. 

    ![Configuração do tipo de nó][node-type-config]

    Selecione **OK**.

7. Preencha Olá **segurança** formulário.  Para esse início rápido, selecione **Não seguro**.  É altamente recomendável toocreate um cluster seguro para cargas de trabalho de produção, no entanto, já que qualquer pessoa pode conectar-se o cluster não segura tooan anonimamente e executar operações de gerenciamento.  

    Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos. Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric](service-fabric-cluster-security.md).  usando o Active Directory do Azure ou tooset certificados para segurança de aplicativo de autenticação de usuário tooenable [criar um cluster de um modelo do Gerenciador de recursos](service-fabric-cluster-creation-via-arm.md).

    Selecione **OK**.

8. Saudação de revisão resumida.  Se você gostaria que toodownload um modelo do Gerenciador de recursos criado a partir de configurações de saudação inserido, selecione **baixar modelo e parâmetros de**.  Selecione **criar** toocreate cluster de saudação.

    Você pode ver o progresso da criação da saudação em notificações de saudação. (Clique ícone de sino"hello" próximo a barra de status de saudação do superior de saudação à direita da tela). Se você clicou **Pin tooStartboard** durante a criação de cluster hello, você verá **implantação de Cluster do Service Fabric** fixado toohello **iniciar** quadro.

### <a name="view-cluster-status"></a>Exibir o status do cluster
Quando o cluster é criado, você pode inspecionar o seu cluster em Olá **visão geral** folha no portal de saudação. Agora você pode ver detalhes de saudação do cluster no painel hello, incluindo o ponto de extremidade do cluster Olá público e um link de tooService Fabric Explorer.

![Status do cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizar cluster hello usando o Gerenciador do Service Fabric
O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o cluster e gerenciar os aplicativos.  Gerenciador do Service Fabric é um serviço que é executado no cluster hello.  Acessá-lo usando um navegador da web clicando Olá **Service Fabric Explorer** link de cluster Olá **visão geral** página no portal de saudação.  Você também pode inserir o endereço de saudação diretamente no navegador Olá: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

painel do cluster Olá fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó. exibição do nó de saudação mostra o layout físico de saudação do cluster hello. Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Conecte-se o cluster toohello usando o PowerShell
Verifique se que esse cluster hello está em execução ao se conectar usando o PowerShell.  Olá ServiceFabric do PowerShell é instalado com o hello [SDK do Service Fabric](service-fabric-get-started.md).  Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet estabelece um cluster de toohello de conexão.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Consulte [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter outros exemplos de cluster de tooa conexão. Depois de cluster toohello conexão, use Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet uma lista de nós no hello cluster e informações de status para cada nó. **HealthState** deve ser *OK* para cada nó.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Remover cluster Olá
Um cluster do Service Fabric é composto por outros recursos do Azure além de recurso de cluster toohello propriamente dito. Para toocompletely exclua um cluster do Service Fabric também é necessário toodelete que todos Olá recursos que é formado. cluster do Hello mais simples maneira toodelete hello e todos os recursos de saudação consome é o grupo de recursos de saudação do toodelete. Para outros toodelete de maneiras que um cluster ou toodelete alguns (mas não todos) recursos de saudação em um grupo de recursos, consulte [excluir um cluster](service-fabric-cluster-delete.md)

Exclua um grupo de recursos em Olá portal do Azure:
1. Navegue cluster do Service Fabric toohello toodelete desejado.
2. Clique em Olá **grupo de recursos** nome na página de recursos básicos de cluster hello.
3. Em Olá **princípios básicos de grupo de recursos** , clique em **excluir grupo de recursos** e siga as instruções de saudação que página toocomplete Olá a exclusão do grupo de recursos de saudação.
    ![Excluir grupo de recursos de saudação][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Usar o Azure Powershell toodeploy um cluster seguro
1. Baixar Olá [Azure Powershell versão 4.0 ou superior do módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) em seu computador.

2. Abra uma janela do Windows PowerShell, Olá executar comando a seguir. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Você verá uma saída semelhante toohello a seguir.

    ![ps-list][ps-list]

3. Logon tooAzure e selecione Olá assinatura toowhich toocreate Olá pelo cluster

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Olá execução toonow de comando a seguir criar um cluster seguro. Não se esqueça de parâmetros de saudação toocustomize. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    comando Olá pode levar de 10 minutos too30 minutos toocomplete, no final de saudação do mesmo, você deve obter uma saída semelhante toohello a seguir. saída de Hello tem informações sobre o certificado hello, Olá KeyVault onde ele foi carregado, e Olá pasta local em que o certificado de saudação é copiado. 

    ![ps-out][ps-out]

5. Copiar saída inteiro hello e salvar o arquivo de texto tooa conforme necessário toorefer tooit. Anote Olá informações a seguir da saída de hello. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Instalar o certificado de saudação em seu computador local
  
tooconnect toohello cluster, você precisa de tooinstall Olá certificado no repositório de pessoal (Meu) de saudação do usuário atual Olá. 

Saudação de execução do PowerShell a seguir

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Agora você está pronto tooconnect tooyour segura cluster.

### <a name="connect-tooa-secure-cluster"></a>Conecte-se o cluster seguro tooa 

Execute Olá cluster seguro do PowerShell comando tooconnect tooa a seguir. detalhes do certificado Olá devem corresponder a um certificado que foi usado tooset cluster hello. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Olá Olá do exemplo mostra a seguir concluída parâmetros: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Execute Olá toocheck de comando que você está conectado a seguir e Olá cluster está íntegro.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Publicar seu cluster tooyour de aplicativos do Visual Studio

Agora que você configurou um cluster do Azure, você pode publicar seu tooit de aplicativos do Visual Studio pelo seguinte Olá [publicar tooan cluster](service-fabric-publish-app-remote-cluster.md) documento. 

### <a name="remove-hello-cluster"></a>Remover cluster Olá
Um cluster é composto por outros recursos do Azure além de recurso de cluster toohello propriamente dito. cluster do Hello mais simples maneira toodelete hello e todos os recursos de saudação consome é o grupo de recursos de saudação do toodelete. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Próximas etapas
Agora que você configurou um cluster de desenvolvimento, tente o seguinte hello:
* [Criar um cluster seguro no portal de saudação](service-fabric-cluster-creation-via-portal.md)
* [Criar um cluster a partir de um modelo](service-fabric-cluster-creation-via-arm.md) 
* [Implantar aplicativos usando o PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
