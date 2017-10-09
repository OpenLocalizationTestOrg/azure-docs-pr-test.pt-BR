---
title: "aaaCreate malha do serviço de cluster no hello portal do Azure | Microsoft Docs"
description: "Este artigo descreve como tooset um cluster do Service Fabric segura no Azure usando Olá portal do Azure e o Azure Key Vault."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Criar um cluster do Service Fabric no Azure usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos do Azure](service-fabric-cluster-creation-via-arm.md)
> * [Portal do Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Este é um guia passo a passo que guiará você pelas etapas de saudação de configuração de um cluster do Service Fabric seguro no Azure usando Olá portal do Azure. Este guia aborda Olá etapas a seguir:

* Configure chaves do Cofre de chaves toomanage para segurança de cluster.
* Crie um cluster protegido no Azure por meio de saudação portal do Azure.
* Autentique os administradores que usam certificados.

> [!NOTE]
> Para obter opções de segurança mais avançadas, como autenticação de usuário com o Azure Active Directory e configurar certificados para a segurança de aplicativo, [crie o cluster usando o Azure Resource Manager][create-cluster-arm].
> 
> 

Um cluster seguro é um cluster que impede que as operações de toomanagement de acesso não autorizado, que inclui a implantar, atualizar e excluir dados Olá que eles contêm, serviços e aplicativos. Um cluster não seguro é um cluster que qualquer pessoa pode se conectar tooat a qualquer momento e executar operações de gerenciamento. Embora seja possível toocreate um cluster não seguro, é **altamente recomendável toocreate um cluster seguro**. Um cluster não seguro **não pode ser protegido posteriormente** - um novo cluster deverá ser criado.

conceitos de saudação são Olá mesmo para a criação de clusters seguros, clusters de saudação são clusters do Linux ou clusters do Windows. Para obter mais informações e scripts auxiliares para criar clusters do Linux seguras, consulte [Criando clusters seguros no Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Olá parâmetros obtidos pelo script de auxiliar Olá fornecida podem ser inseridos diretamente no portal de saudação conforme descrito na seção de saudação [criar um cluster no portal do Azure de saudação](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Faça logon no tooAzure
Este guia usa o [Azure PowerShell][azure-powershell]. Ao iniciar uma nova sessão do PowerShell, faça logon no tooyour conta do Azure e selecione sua assinatura antes de executar comandos do Azure.

Faça logon na conta tooyour do azure:

```powershell
Login-AzureRmAccount
```

Selecione sua assinatura:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Configurar o Cofre de Chaves
Esta parte do guia de saudação orienta a criação de um cofre de chaves para um cluster do Service Fabric no Azure e para aplicativos do Service Fabric. Para obter um guia completo no cofre de chaves, consulte Olá [guia de Introdução ao Cofre de chaves][key-vault-get-started].

Serviço de malha usa toosecure de certificados x. 509 um cluster. Cofre de chaves do Azure é toomanage usados certificados para clusters de malha do serviço no Azure. Quando um cluster é implantado no Azure, o provedor de recursos do Azure de saudação responsável pela criação de clusters Service Fabric recebe certificados de Cofre de chaves e instala-os em máquinas virtuais do cluster hello.

Olá diagrama a seguir ilustra a relação Olá entre Cofre de chaves, um cluster do Service Fabric e o provedor de recursos do Azure Olá que usa certificados armazenados no cofre de chaves ao criar um cluster:

![Instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Criar um grupo de recursos
Olá primeira etapa é toocreate um novo grupo de recursos especificamente para o Cofre de chaves. Colocar chave de cofre em seu próprio grupo de recursos é recomendado para que você possa remover grupos de recursos de computação e armazenamento - como o grupo de recursos de saudação que tem o cluster do Service Fabric - sem perder suas chaves e segredos. grupo de recursos de saudação que tem seu Cofre de chaves deve estar no hello mesma região Olá cluster que está em uso.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Criar Cofre da Chave
Crie um cofre de chaves no novo grupo de recursos hello. Olá Cofre de chaves **deve ser habilitado para implantação** tooallow Olá certificados de tooget de provedor de recursos de malha do serviço-lo e instalar em nós de cluster:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

Se você tiver um Cofre de Chaves existente, poderá habilitá-lo para implantação usando a CLI do Azure:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Adicionar certificados tooKey cofre
Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos. Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Certificado de cluster e de servidor (necessário)
Esse certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit. Ele fornece segurança de cluster de duas maneiras:

* **Autenticação do cluster:** autentica a comunicação de nó para nó para a federação de cluster. Somente nós que podem provar sua identidade com esse certificado podem ingressar o cluster de saudação.
* **Autenticação de servidor:** autentica o cliente de gerenciamento do tooa pontos de extremidade do hello cluster management, para que hello gerenciamento cliente sabe que está se comunicando cluster real toohello. Este certificado também fornece SSL para Olá API de gerenciamento de HTTPS e Service Fabric Explorer via HTTPS.

tooserve esses fins, Olá certificado deve atender a saudação requisitos a seguir:

* certificado de saudação deve conter uma chave privada.
* certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).
* Olá nome da entidade do certificado deve corresponder Olá domínio usado tooaccess Olá malha do serviço cluster. Isso é necessário tooprovide SSL para pontos de extremidade de gerenciamento de HTTPS e o Gerenciador do Service Fabric do cluster hello. Não é possível obter um certificado SSL de uma autoridade de certificação (CA) Olá `.cloudapp.azure.com` domínio. Adquira um nome de domínio personalizado para seu cluster. Quando você solicitar um certificado do nome da entidade do certificado de saudação uma autoridade de certificação deve corresponder a nome de domínio personalizado Olá usado para o cluster.

### <a name="client-authentication-certificates"></a>Certificados de autenticação de cliente
Os certificados de cliente adicionais autenticam os administradores para tarefas de gerenciamento de cluster. O Service Fabric tem dois níveis de acesso: **administrador** e **usuário somente leitura**. No mínimo, um único certificado para acesso administrativo deve ser usado. Para acesso de nível de usuário adicional, deve ser fornecido um certificado diferente. Para obter mais informações sobre as funções de acesso, consulte [Controle de acesso baseado em função para clientes do Service Fabric][service-fabric-cluster-security-roles].

Não é necessário tooupload cliente autenticação certificados tooKey cofre toowork com o Service Fabric. Esses certificados só precisam toobe fornecida toousers autorizados para o gerenciamento de cluster. 

> [!NOTE]
> Active Directory do Azure é Olá operações de gerenciamento de clientes de tooauthenticate de maneira para cluster recomendada. toouse Active Directory do Azure, você deve [criar um cluster usando o Gerenciador de recursos do Azure][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Certificados de aplicativo (opcionais)
Qualquer número de certificados adicionais pode ser instalado em um cluster para fins de segurança do aplicativo. Antes de criar o cluster, considere os cenários de segurança de aplicativo hello que exigem um toobe certificado instalado em nós hello, como:

* Criptografia e descriptografia de valores de configuração de aplicativo
* Criptografia de dados entre nós durante a replicação 

Certificados de aplicativo não podem ser configurados ao criar um cluster por meio de saudação portal do Azure. certificados de aplicativo tooconfigure no momento da instalação de cluster, você deve [criar um cluster usando o Gerenciador de recursos do Azure][create-cluster-arm]. Você também pode adicionar o cluster de toohello de certificados do aplicativo após ele ter sido criado.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formatação de certificados para uso do provedor de recursos do Azure
Os arquivos de chave privada (.pfx) podem ser adicionados e usados diretamente por meio do Cofre de Chaves. No entanto, o provedor de recursos do Azure Olá requer toobe chaves armazenada em um formato JSON especial que inclui o. pfx de saudação como uma base 64 codificados hello e cadeia de caracteres de senha da chave privada. tooaccommodate esses requisitos, as chaves devem ser colocados em uma cadeia de caracteres JSON e, em seguida, são armazenados como *segredos* no cofre de chaves.

toomake esse processo mais fácil, um módulo do PowerShell é [disponível no GitHub][service-fabric-rp-helpers]. Execute o módulo de saudação de toouse essas etapas:

1. Baixe todo o conteúdo do repositório de Olá Olá em um diretório local. 
2. Importe o módulo de saudação na janela do PowerShell:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell formata uma chave privada do certificado em uma cadeia de caracteres JSON e carrega tooKey cofre automaticamente. Use-certificado de cluster Olá tooadd e quaisquer certificados de aplicativo adicionais tooKey cofre. Repita essa etapa para todos os certificados adicionais que você deseja tooinstall em seu cluster.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Esses são todos os pré-requisitos de Cofre de chaves Olá para configurar um modelo do Gerenciador de recursos de cluster do Service Fabric que instala certificados para autenticação de nó, segurança de ponto de extremidade de gerenciamento e autenticação e segurança de todos os aplicativos adicionais recursos que usam certificados x. 509. Neste ponto, você deve ter agora Olá após a instalação no Azure:

* Grupo de recursos do Cofre de Chaves
  * Cofre da Chave
    * Certificado de autenticação de servidor de cluster

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Criar o cluster no hello portal do Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Pesquisar Olá recurso de cluster do Service Fabric
![Procure o modelo de cluster do Service Fabric em Olá portal do Azure.][SearchforServiceFabricClusterTemplate]

1. Entrar toohello [portal do Azure][azure-portal].
2. Clique em **novo** tooadd um novo modelo de recurso. Procure o modelo de Cluster do Service Fabric Olá Olá **Marketplace** em **tudo**.
3. Selecione **Cluster do Service Fabric** da lista de saudação.
4. Navegue toohello **Cluster do Service Fabric** folha, clique em **criar**,
5. Olá **cluster do Service Fabric criar** folha tem Olá quatro etapas a seguir.

#### <a name="1-basics"></a>1. Noções básicas
![Captura de tela da criação de um novo grupo de recursos.][CreateRG]

Na folha de Noções básicas de saudação precisar detalhes básicos do tooprovide Olá para seu cluster.

1. Insira o nome de saudação do cluster.
2. Insira um **nome de usuário** e **senha** para a área de trabalho remota para Olá VMs.
3. Verifique se Olá de tooselect **assinatura** que você deseja que seu toobe cluster implantado, especialmente se você tiver várias assinaturas.
4. Crie um **novo grupo de recursos**. É melhor toogive-Olá mesmo nome de cluster hello, pois ela ajuda a localizá-los mais tarde, especialmente quando você está tentando toomake alterações tooyour implantação ou excluir o cluster.
   
   > [!NOTE]
   > Embora você possa decidir toouse um grupo de recursos existente, é uma boa prática toocreate um novo grupo de recursos. Isso torna fácil toodelete clusters que não é necessário.
   > 
   > 
5. Selecione Olá **região** no qual você deseja que o cluster de saudação toocreate. Você deve usar o hello está mesma região que sua chave de cofre em.

#### <a name="2-cluster-configuration"></a>2. Configuração do cluster
![Criar um tipo de nó][CreateNodeType]

Configure os nós de cluster. Tipos de nós definem tamanhos de VM hello, número de saudação de VMs e suas propriedades. O cluster pode ter mais de um tipo de nó, mas o tipo de nó primário hello (Olá a primeira alteração que você definir no portal de saudação) deve ter pelo menos cinco VMs, como esse é o tipo de nó Olá onde os serviços do sistema do Service Fabric são colocados. Não configure as **Propriedades de Posicionamento**, pois uma propriedade de posicionamento padrão de "NodeTypeName" é adicionada automaticamente.

> [!NOTE]
> Um cenário comum para vários tipos de nó é um aplicativo que contém um serviço front-end e um serviço back-end. Você deseja tooput serviço front-end do hello em VMs menores (tamanhos de VM como D2) com portas abertas toohello da Internet, mas deseja tooput serviço de back-end de saudação em VMs maior (com tamanhos de VM como D4, D6, D15 e assim por diante) sem abrir de portas para a Internet.
> 
> 

1. Escolha um nome para o tipo de nó (1 too12 caracteres que contém apenas letras e números).
2. Olá mínimo **tamanho** de VMs de nó primário Olá tipo é orientado por Olá **durabilidade** camada que você escolher para cluster hello. saudação padrão da camada de durabilidade de saudação é bronze. Para obter mais informações sobre a durabilidade, consulte [como toochoose Olá malha do serviço de cluster confiabilidade e durabilidade][service-fabric-cluster-capacity].
3. Selecione o tamanho da VM hello e preço. As VMs da série D têm unidades SSD e são altamente recomendadas para aplicativos com monitoração de estado. Não use nenhuma SKU de VM com núcleos parciais ou que tenham menos de 7 GB de capacidade em disco disponível. 
4. Olá mínimo **número** de VMs de nó primário Olá tipo é orientado por Olá **confiabilidade** camada que você escolher. saudação padrão da camada de confiabilidade de saudação é prata. Para obter mais informações sobre a confiabilidade, consulte [como toochoose Olá malha do serviço de cluster confiabilidade e durabilidade][service-fabric-cluster-capacity].
5. Escolha o número de saudação de VMs para o tipo de nó de saudação. Você pode expandir ou reduzir o número de saudação de VMs em um tipo de nó mais tarde, mas no tipo de nó primário hello, Olá mínimo é orientada por nível de confiabilidade de saudação que você escolheu. Os outros tipos de nó podem ter um mínimo de 1 VM.
6. Configure pontos de extremidade personalizados. Este campo permite que você tooenter uma lista separada por vírgulas de portas que você deseja tooexpose por meio de saudação balanceador de carga do Azure toohello Internet pública para seus aplicativos. Por exemplo, se você planejar toodeploy um cluster de tooyour de aplicativo da web, digite "80" aqui tooallow tráfego na porta 80 em seu cluster. Para obter mais informações sobre pontos de extremidade, consulte [Comunicando-se com aplicativos][service-fabric-connect-and-communicate-with-services]
7. Configure o **diagnóstico**do cluster. Por padrão, os diagnósticos são habilitados no seu tooassist de cluster com a solução de problemas. Se você desejar alterar de diagnóstico toodisable Olá **Status** alternar muito**Off**. **Não** é recomendável desligar o diagnóstico.
8. Selecione Olá deseja definir seu cluster o modo de atualização do Fabric. Selecione **automáticas**, se você quiser tooautomatically escolha sistema Olá Olá versão mais recente e tente tooupgrade tooit seu cluster. Definir o modo de saudação muito**Manual**, se você quiser toochoose uma versão com suporte.

> [!NOTE]
> Damos suporte somente para clusters que executam versões com suporte do Service Fabric. Selecionando Olá **Manual** modo, você está aproveitando em Olá responsabilidade tooupgrade sua versão de tooa suporte para cluster. Para obter mais detalhes sobre o modo de atualização de malha Olá Olá, consulte [documento de serviço-malha-atualização de cluster.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Segurança
![Captura de tela das configurações de segurança no Portal do Azure][SecurityConfigs]

Olá última etapa é cluster tooprovide certificado informações toosecure hello usando hello Cofre de chaves e certificados informações criadas anteriormente.

* Preencher os campos de certificado principal de saudação à saída de hello obtida Carregando Olá **certificado de cluster** tooKey cofre usando Olá `Invoke-AddCertToKeyVault` comando do PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Verificar Olá **definir configurações avançadas** caixa tooenter certificados de cliente para **cliente administrador** e **cliente somente leitura**. Nesses campos, insira a impressão digital de saudação do seu certificado de cliente do administrador e a impressão digital de saudação do seu certificado de cliente do usuário somente leitura, se aplicável. Quando os administradores tentam tooconnect toohello cluster, eles recebem acesso somente se tiverem um certificado com uma impressão digital que faz a correspondência de valores de impressão digital Olá inserido aqui.  

#### <a name="4-summary"></a>4. Resumo
![Captura de tela de quadro de início Olá exibindo "Implantando Cluster do Service Fabric." ][Notifications]

criação do cluster Olá toocomplete, clique em **resumo** configurações de saudação toosee que você forneceu ou baixa hello Azure Resource Manager modelo que que usada toodeploy seu cluster. Depois que você forneceu configurações obrigatórias hello, Olá **Okey** botão ficará verde e você pode iniciar o processo de criação de cluster Olá clicando nele.

Você pode ver o progresso da criação da saudação em notificações de saudação. (Clique ícone de sino"hello" próximo a barra de status de saudação do superior de saudação à direita da tela). Se você clicou **Pin tooStartboard** durante a criação de cluster hello, você verá **implantação de Cluster do Service Fabric** fixado toohello **iniciar** quadro.

### <a name="view-your-cluster-status"></a>Exibir o status do cluster
![Captura de tela de detalhes no painel de saudação do cluster.][ClusterDashboard]

Quando o cluster é criado, você pode inspecionar o cluster no portal de saudação:

1. Vá muito**procurar** e clique em **Clusters de malha do serviço**.
2. Localize o cluster e clique nele.
3. Agora você pode ver detalhes de saudação do cluster no painel hello, incluindo o ponto de extremidade do cluster Olá público e um link de tooService Fabric Explorer.

Olá **nó Monitor** seção na folha do painel de controle do cluster Olá indica o número de saudação de máquinas virtuais que estiverem íntegros e não está íntegro. Você pode encontrar mais detalhes sobre a integridade do cluster Olá em [introdução de modelo de integridade do Service Fabric][service-fabric-health-introduction].

> [!NOTE]
> Clusters Service Fabric exigem um determinado número de nós toobe sempre toomaintain disponibilidade e preservam o estado - tooas chamado "mantêm o quórum". Therfore, geralmente não é seguro tooshut todas as máquinas no cluster hello, a menos que você tiver executado pela primeira vez um [backup completo do estado do seu][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Conexão remota tooa instância de conjunto de escala de máquina Virtual ou um nó de cluster
Cada Olá NodeTypes você especificar nos resultados de cluster em um conjunto de escala de máquina Virtual ao obter a configuração. Consulte [remoto conecte-se a instância de conjunto de escala de máquinas virtuais de tooa] [ remote-connect-to-a-vm-scale-set] para obter detalhes.

## <a name="next-steps"></a>Próximas etapas
Neste ponto, você tem um cluster seguro usando certificados para autenticação de gerenciamento. Em seguida, [conecte cluster tooyour](service-fabric-connect-to-secure-cluster.md) e saiba como muito[gerenciar segredos do aplicativo](service-fabric-application-secret-management.md).  Além disso, saiba mais sobre as [Azure Service Fabric support options](service-fabric-support.md) (Opções de suporte do Service Fabric).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
