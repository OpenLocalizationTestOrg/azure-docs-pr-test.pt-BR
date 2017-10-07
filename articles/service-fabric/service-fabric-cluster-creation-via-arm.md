---
title: "aaaCreate uma malha do Azure serviço de cluster de um modelo | Microsoft Docs"
description: "Este artigo descreve como tooset a uma malha seguros do serviço de cluster no Azure usando o Gerenciador de recursos do Azure, o Cofre de chaves do Azure e Azure Active Directory (AD do Azure) para autenticação de cliente."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Criar um cluster do Service Fabric usando o Azure Resource Manager
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos do Azure](service-fabric-cluster-creation-via-arm.md)
> * [Portal do Azure](service-fabric-cluster-creation-via-portal.md)
>
>

Este guia passo a passo orienta você pela configuração de um cluster do Azure Service Fabric seguro no Azure usando o Azure Resource Manager. Confirmamos o que artigo Olá é longo. No entanto, a menos que já esteja completamente familiarizado com conteúdo hello, ser toofollow-se de que cada etapa com cuidado.

Guia de saudação abrange Olá procedimentos a seguir:

* Configurando certificados de tooupload um cofre de chaves do Azure para segurança de aplicativos e de cluster
* Como criar um cluster seguro no Azure usando o Azure Resource Manager
* Como autenticar usuários usando o Azure AD (Azure Active Directory) para gerenciamento de cluster

Um cluster seguro é um cluster que impede que as operações de toomanagement de acesso não autorizado. Isso inclui implantar, atualizar e excluir aplicativos, serviços e dados de saudação que eles contêm. Um cluster não seguro é um cluster que qualquer pessoa pode se conectar tooat a qualquer momento e executar operações de gerenciamento. Embora seja possível toocreate um cluster não seguro, é altamente recomendável que você crie um cluster seguro desde o início de saudação. Um cluster não seguro não pode ser protegido posteriormente; um novo cluster deverá ser criado.

conceito de saudação de criação de clusters seguros é Olá mesmo, independentemente de estarem clusters do Linux ou Windows. Para obter mais informações e scripts auxiliares para criar clusters do Linux seguras, consulte [Criando clusters seguros no Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Entrar tooyour conta do Azure
Este guia usa o [Azure PowerShell][azure-powershell]. Quando você inicia uma nova sessão do PowerShell, entre no tooyour conta do Azure e selecione sua assinatura antes de executar comandos do Azure.

Entre tooyour conta do Azure:

```powershell
Login-AzureRmAccount
```

Selecione sua assinatura:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Configurar um cofre de chaves
Esta seção trata da criação de um cofre de chaves para um cluster do Service Fabric no Azure e para aplicativos do Service Fabric. Para obter um guia completo tooAzure Cofre de chaves, consulte toohello [guia de Introdução ao Cofre de chaves][key-vault-get-started].

Service Fabric usa toosecure de certificados x. 509 um cluster e fornecer recursos de segurança do aplicativo. Você pode usar certificados de toomanage de Cofre de chaves para clusters de malha do serviço no Azure. Quando um cluster é implantado no Azure, provedor de recursos do Azure de saudação que é responsável pela criação de clusters Service Fabric recebe certificados de Cofre de chaves e os instala no cluster Olá VMs.

Olá diagrama a seguir ilustra a relação Olá entre o Cofre de chaves do Azure, um cluster do Service Fabric e provedor de recursos do Azure Olá que usa certificados armazenados em um cofre de chaves ao criar um cluster:

![Diagrama da instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Criar um grupo de recursos
Olá primeira etapa é toocreate um grupo de recursos especificamente para o Cofre de chaves. É recomendável que você coloque o Cofre de chaves de saudação em seu próprio grupo de recursos. Essa ação permite remover Olá computação e armazenamento de grupos de recursos, incluindo o grupo de recursos de saudação que contém o cluster do Service Fabric, sem perder suas chaves e segredos. grupo de recursos de saudação que contém seu Cofre de chaves _deve estar no hello mesma região_ como cluster Olá que ele está em uso.

Se você planejar toodeploy clusters em várias regiões, sugerimos que você nomear o grupo de recursos de saudação e Olá cofre da chave de forma que indica a região que pertence a.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
saída de Hello deve ter esta aparência:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Criar um cofre de chaves no novo grupo de recursos Olá
Cofre de chaves Olá _deve ser habilitado para implantação_ tooallow Olá certificados de tooget de provedor de recursos de computação-lo e instalá-lo em instâncias de máquina virtual:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

saída de Hello deve ter esta aparência:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Usar um cofre de chave existente

toouse um cofre de chave existente, você _deve habilitá-la para implantação_ tooallow Olá certificados de tooget de provedor de recursos de computação-lo e instalá-lo em nós de cluster:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Adicionar o Cofre de chaves de tooyour de certificados

Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos. Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Certificado de cluster e de servidor (necessário)
Esse certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit. Ele fornece segurança de cluster de duas maneiras:

* Autenticação do cluster: autentica a comunicação de nó para nó para a federação de cluster. Somente nós que podem provar sua identidade com esse certificado podem ingressar o cluster de saudação.
* Autenticação de servidor: autentica o cliente de gerenciamento do tooa pontos de extremidade do hello cluster management, para que hello gerenciamento cliente sabe que está se comunicando cluster real toohello. Este certificado também fornece um SSL para Olá API de gerenciamento de HTTPS e Service Fabric Explorer via HTTPS.

tooserve esses fins, Olá certificado deve atender a saudação requisitos a seguir:

* certificado de saudação deve conter uma chave privada.
* certificado de saudação deve ser criado para troca de chaves, que é exportável tooa arquivo de troca de informações pessoais (. pfx).
* nome da entidade do certificado Olá deve corresponder domínio Olá que você use o cluster do tooaccess saudação do Service Fabric. Esse correspondente é necessário tooprovide um SSL para pontos de extremidade do gerenciamento do cluster Olá HTTPS e o Service Fabric Explorer. Não é possível obter um certificado SSL de uma autoridade de certificação (CA) hello. cloudapp.azure.com domínio. Você deve obter um nome de domínio personalizado para seu cluster. Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.

### <a name="application-certificates-optional"></a>Certificados de aplicativo (opcionais)
Qualquer número de certificados adicionais pode ser instalado em um cluster para fins de segurança do aplicativo. Antes de criar o cluster, considere os cenários de segurança de aplicativo hello que exigem um toobe certificado instalado em nós hello, como:

* Criptografia e descriptografia de valores de configuração de aplicativo.
* Criptografia de dados entre nós durante a replicação.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formatação de certificados para uso do provedor de recursos do Azure
Você pode adicionar e usar arquivos de chave privada (.pfx) diretamente pelo cofre de chaves. No entanto, o provedor de recursos de computação do Azure Olá requer toobe chaves armazenada em um formato de notação JSON (JavaScript Object) especial. formato de saudação inclui arquivo.pfx hello como uma base cadeia de caracteres codificada de 64 e a senha da chave privada hello. tooaccommodate esses requisitos, Olá chaves devem ser colocadas em uma cadeia de caracteres JSON e, em seguida, são armazenadas como "segredos" na chave Olá cofre.

toomake esse processo mais fácil, uma [módulo PowerShell está disponível no GitHub][service-fabric-rp-helpers]. módulo de saudação toouse, Olá a seguir:

1. Baixe todo o conteúdo do repositório de Olá Olá em um diretório local.
2. Vá toohello a pasta local.
2. Importe o módulo de ServiceFabricRPHelpers de saudação na janela do PowerShell:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell formata uma chave privada do certificado em uma cadeia de caracteres JSON e carrega o Cofre de chaves toohello automaticamente. Usar certificado de cluster Olá comando tooadd hello e cofre da chave toohello qualquer aplicativo adicional certificados. Repita essa etapa para todos os certificados adicionais que você deseja tooinstall em seu cluster.

#### <a name="uploading-an-existing-certificate"></a>Carregando um certificado existente

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Se você receber um erro, como Olá mostrada aqui, isso normalmente significa que você tem um conflito de URL de recurso. conflito de saudação tooresolve, alterar nome do Cofre de chaves hello.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Depois de saudação conflito seja resolvido, saída de hello deve ter esta aparência:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>Você precisa Olá três anterior cadeias de caracteres, CertificateThumbprint, SourceVault e CertificateURL, tooset um cluster do Service Fabric seguro e tooobtain quaisquer certificados de aplicativo que você pode usar para segurança do aplicativo. Se você não salvar cadeias de caracteres hello, pode ser difícil tooretrieve-los consultando chave Olá cofre mais tarde.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Criando um certificado autoassinado e carregá-lo toohello Cofre de chaves

Se você já carregou seu Cofre de chaves de certificados toohello, ignore esta etapa. Esta etapa é para gerar um novo certificado autoassinado e carregá-lo tooyour Cofre de chaves. Depois de alterar parâmetros Olá Olá script a seguir e, em seguida, executá-lo, você deve ser solicitado para uma senha do certificado.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Se você receber um erro, como Olá mostrada aqui, isso normalmente significa que você tem um conflito de URL de recurso. conflito de saudação tooresolve, alterar nome do Cofre de chaves Olá, nome do RG e assim por diante.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Depois de saudação conflito seja resolvido, saída de hello deve ter esta aparência:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>Você precisa Olá três anterior cadeias de caracteres, CertificateThumbprint, SourceVault e CertificateURL, tooset um cluster do Service Fabric seguro e tooobtain quaisquer certificados de aplicativo que você pode usar para segurança do aplicativo. Se você não salvar cadeias de caracteres hello, pode ser difícil tooretrieve-los consultando chave Olá cofre mais tarde.

 Neste ponto, você deve ter Olá elementos no local a seguir:

* grupo de recursos do Cofre de chaves Hello.
* Olá Cofre de chaves e a URL (chamado SourceVault em Olá precede a saída do PowerShell).
* certificado de autenticação de servidor de cluster Hello e sua URL no cofre de chaves hello.
* certificados de aplicativo Hello e suas URLs no cofre de chaves hello.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Configurar o Azure Active Directory para autenticação de cliente

AD do Azure permite que as organizações (conhecido como locatários) toomanage usuário acesso tooapplications. Os aplicativos são divididos entre os que têm IU de entrada na Web e os que têm experiência de cliente nativa. Neste artigo, partimos do pressuposto que você já tenha criado um locatário. Se você não tiver, comece lendo [como tooget um Active Directory do Azure locatário][active-directory-howto-tenant].

Um cluster do Service Fabric oferece várias tooits de pontos de entrada de funcionalidade de gerenciamento, incluindo Olá baseado na web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] e [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Como resultado, você criar o cluster de toohello de acesso de toocontrol do AD do Azure aplicativos dois, um aplicativo web e um aplicativo nativo.

toosimplify algumas das etapas de saudação envolvidas na configuração do AD do Azure com um cluster do Service Fabric, criamos um conjunto de scripts do Windows PowerShell.

> [!NOTE]
> Você deve concluir Olá etapas a seguir antes de criar o cluster de saudação. Porque os scripts de saudação esperam que os pontos de extremidade e nomes de cluster, os valores de Olá deve ser planejado e não os valores que você já tenha criado.

1. [Baixe os scripts de saudação] [ sf-aad-ps-script-download] tooyour computador.
2. Arquivo de zip Olá com o botão direito, selecione **propriedades**, selecione Olá **desbloquear** caixa de seleção e, em seguida, clique em **aplicar**.
3. Extraia o arquivo zip de saudação.
4. Executar `SetupApplications.ps1`e fornecer Olá TenantId, ClusterName e WebApplicationReplyUrl como parâmetros. Por exemplo:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Você pode encontrar o TenantId executando o comando do PowerShell Olá `Get-AzureSubscription`. A execução desse comando exibe o saudação TenantId para cada assinatura.

    ClusterName é tooprefix usados aplicativos de saudação do AD do Azure que são criados pelo script hello. Nome do toomatch Olá real do cluster não é necessário exatamente. É pretendido toomake somente ele mais fácil toomap AD do Azure artefatos toohello Service Fabric cluster estão sendo usada em.

    WebApplicationReplyUrl é saudação padrão ponto de extremidade do AD do Azure retorna tooyour usuários após a conclusão entrar. Defina esse ponto de extremidade como ponto de extremidade de Service Fabric Explorer Olá para o cluster, que é por padrão:

    https://&lt;cluster_domain&gt;:19080/Explorer

    Você é solicitado toosign tooan conta que tenha privilégios administrativos para o locatário de saudação do AD do Azure. Depois que você entrar, Olá script cria Olá web e aplicativos nativos toorepresent o cluster do Service Fabric. Se você examinar aplicativos do locatário Olá Olá [portal clássico do Azure][azure-classic-portal], você deve ver duas novas entradas:

   * *ClusterName*\_Cluster
   * *ClusterName*\_Cliente

   script Hello imprime Olá JSON necessário pelo modelo do Azure Resource Manager hello quando você cria o cluster de saudação na próxima seção, Olá, portanto, é uma janela do PowerShell boa ideia tookeep Olá abrir.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Criar um modelo do Resource Manager do cluster do Service Fabric
Nesta seção, Olá saídas de saudação anterior comandos do PowerShell são usados em um modelo do Gerenciador de recursos de cluster do Service Fabric.

Modelos do Gerenciador de recursos de exemplo estão disponíveis no hello [Galeria de modelos de início rápido do Azure no GitHub][azure-quickstart-templates]. Esses modelos podem ser usados como ponto de partida para o modelo de cluster.

### <a name="create-hello-resource-manager-template"></a>Criar o modelo do Gerenciador de recursos de saudação
Este guia usa Olá [cluster seguro 5 nós] [ service-fabric-secure-cluster-5-node-1-nodetype] modelo de exemplo e parâmetros de modelo. Baixar `azuredeploy.json` e `azuredeploy.parameters.json` tooyour computador e abra ambos os arquivos em seu editor de texto favorito.

### <a name="add-certificates"></a>Adicionar certificados
Adicionar o modelo de Gerenciador de recursos de cluster certificados tooa referenciando o Cofre de chaves de saudação que contém as chaves de certificado de saudação. É recomendável que você coloque os valores hello Cofre de chaves em um arquivo de parâmetros de modelo do Gerenciador de recursos. Isso impede que Olá Gerenciador de recursos de arquivo de modelo reutilizáveis e livre de implantação de tooa específico de valores.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Adicionar que conjunto de escala de máquinas virtuais do todos os certificados toohello osProfile
Cada certificado que é instalado no cluster Olá deve ser configurado na seção de osProfile de saudação do recurso de conjunto de escala hello (Microsoft.Compute/virtualMachineScaleSets). Essa ação instrui Olá recurso provedor tooinstall Olá certificado Olá VMs. Esta instalação inclui o certificado de cluster hello e quaisquer certificados de segurança do aplicativo que você planeje toouse para seus aplicativos:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Configurar o certificado de cluster do Service Fabric Olá
certificado de autenticação de cluster Olá deve ser configurado em ambos os recurso de cluster do Service Fabric hello (Microsoft.ServiceFabric/clusters) e Olá extensão Service Fabric para a escala de máquina virtual define Olá recurso de conjunto de escala de máquina virtual. Essa organização permite Olá Service Fabric recurso provedor tooconfigure-lo para ser usado para autenticação do cluster e autenticação de servidor para pontos de extremidade de gerenciamento.

##### <a name="virtual-machine-scale-set-resource"></a>Recurso Conjunto de dimensionamento de máquinas virtuais:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Recursos do Service Fabric:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Inserir configuração do Azure AD
configuração de saudação do AD do Azure que você criou anteriormente pode ser inserida diretamente no seu modelo do Gerenciador de recursos. No entanto, é recomendável que você primeiro extrair valores hello em um reutilizável de modelo parâmetros arquivo tookeep Olá Gerenciador de recursos e livre de implantação de tooa específico de valores.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a>Configurar os parâmetros do modelo do Resource Manager
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Por fim, use os valores de saída de saudação do Cofre de chaves de saudação e o arquivo de parâmetros do PowerShell do Azure AD comandos toopopulate hello:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
Neste ponto, você deve ter Olá elementos no local a seguir:

* Grupo de recursos do cofre de chaves
  * Cofre de chaves
  * Certificado de autenticação de servidor de cluster
  * Certificado de codificação de dados
* Locatário do Azure Active Directory
  * Aplicativo Azure AD para gerenciamento baseado na Web e no Service Fabric Explorer
  * Aplicativo Azure AD para o gerenciamento de clientes nativos
  * Usuários e suas funções atribuídas
* Modelo do Resource Manager de cluster do Service Fabric
  * Certificados configurados por meio do cofre de chaves
  * Azure Active Directory configurado

Olá diagrama a seguir ilustra onde seu Cofre de chaves e a configuração do AD do Azure se encaixam seu modelo do Gerenciador de recursos.

![Mapa de dependências do Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Criar cluster Olá
Agora você está pronto toocreate cluster de saudação usando [implantação de modelo de recurso do Azure][resource-group-template-deploy].

#### <a name="test-it"></a>Testá-lo
Olá tootest de comando do PowerShell a seguir ao Use o modelo do Gerenciador de recursos com um arquivo de parâmetros:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Implantá-lo
Se o teste de modelo do Gerenciador de recursos de Olá passa, use Olá toodeploy de comando do PowerShell a seguir o modelo do Gerenciador de recursos com um arquivo de parâmetros:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Atribuir usuários tooroles
Depois que você criou Olá aplicativos toorepresent seu cluster, atribuir usuários toohello funções com suporte do Service Fabric: somente leitura e administrador. Você pode atribuir funções hello usando Olá [portal clássico do Azure][azure-classic-portal].

1. No hello portal do Azure, vá tooyour locatário e, em seguida, selecione **aplicativos**.
2. Selecionar aplicativo de web hello, que tem um nome como `myTestCluster_Cluster`.
3. Clique em Olá **usuários** guia.
4. Selecione um usuário tooassign e clique em Olá **atribuir** botão Olá final da tela hello.

    ![Os usuários tooroles botão atribuir][assign-users-to-roles-button]
5. Selecione Olá função tooassign toohello usuário.

    ![Caixa de diálogo "Atribuir Usuários"][assign-users-to-roles-dialog]

> [!NOTE]
> Para saber mais sobre as funções no Service Fabric, veja [Controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Criar clusters seguros no Linux
processo de saudação toomake mais fácil, fornecemos um [script auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Antes de usar esse script auxiliar, verifique se você já tem a CLI (interface de linha de comando) do Azure instalada e se ele está em seu caminho. Certifique-se de que o script hello tem permissões tooexecute executando `chmod +x cert_helper.py` após fazer o download. Olá primeira etapa é toosign em tooyour conta do Azure usando a CLI com hello `azure login` comando. Depois de entrar no tooyour conta do Azure, use Olá auxiliar script com sua CA certificado autoassinado, como Olá comando mostra a seguir:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

parâmetro de IArquivo - Olá pode usar um arquivo. pfx ou. PEM como entrada, com o tipo de certificado da saudação (pfx ou pem ou ss se ele for um certificado autoassinado).
Olá parâmetro -h imprime o texto de ajuda hello.


Esse comando retorna Olá três cadeias de caracteres a seguir como a saída de hello:

* SourceVaultID, que é a ID Olá Olá novo KeyVault ResourceGroup ele criado para você
* CertificateUrl para acessar o certificado de saudação
* CertificateThumbprint, que é usado para autenticação

saudação de exemplo a seguir mostra como toouse Olá comando:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Executando Olá anterior oferece comando você Olá três cadeias de caracteres, da seguinte maneira:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

nome da entidade do certificado Olá deve corresponder domínio Olá que você use o cluster do tooaccess saudação do Service Fabric. Esse correspondente é necessário tooprovide um SSL para pontos de extremidade do gerenciamento do cluster Olá HTTPS e o Service Fabric Explorer. Não é possível obter um certificado SSL de uma autoridade de certificação para Olá `.cloudapp.azure.com` domínio. Você deve obter um nome de domínio personalizado para seu cluster. Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.

Esses nomes de entidade são entradas Olá necessárias toocreate um cluster do Service Fabric seguro (sem AD do Azure), conforme descrito em [parâmetros de modelo de configurar o Gerenciador de recursos](#configure-arm). Você pode se conectar a cluster seguro toohello seguindo as instruções de saudação para [autenticando o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md). Os clusters de visualização do Linux não dão suporte à autenticação do Azure AD. Você pode atribuir funções de administrador e o cliente conforme descrito em Olá [atribuir funções toousers](#assign-roles) seção. Quando você especificar funções de administrador e o cliente para um cluster de visualização do Linux, você tem tooprovide impressões digitais de certificado para autenticação. (Você não fornecer nome do assunto hello, porque nenhuma validação de cadeia ou a revogação está sendo executada nessa versão de visualização.)

Se você quiser toouse um certificado autoassinado para testes, você pode usar Olá mesmo toogenerate script um. É possível carregar o Cofre de chaves Olá certificado tooyour fornecendo sinalizador Olá `ss` em vez de fornecer o nome de caminho e o certificado do certificado hello. Por exemplo, consulte Olá comando para criar e carregar um certificado autoassinado a seguir:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Esse comando retorna Olá mesmo três cadeias de caracteres: SourceVault, CertificateUrl e CertificateThumbprint. Você pode usar toocreate de cadeias de caracteres de saudação um cluster Linux seguro e um local onde o certificado autoassinado Olá é colocado. Pode ser necessário Olá certificado autoassinado tooconnect toohello cluster. Você pode se conectar a cluster seguro toohello seguindo as instruções de saudação para [autenticando o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md).

nome da entidade do certificado Olá deve corresponder domínio Olá que você use o cluster do tooaccess saudação do Service Fabric. Esse correspondente é necessário tooprovide um SSL para pontos de extremidade do gerenciamento do cluster Olá HTTPS e o Service Fabric Explorer. Não é possível obter um certificado SSL de uma autoridade de certificação para Olá `.cloudapp.azure.com` domínio. Você deve obter um nome de domínio personalizado para seu cluster. Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.

Você pode preencher os parâmetros de saudação do script auxiliar Olá Olá portal do Azure, conforme descrito em Olá [criar um cluster no portal do Azure de saudação](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) seção.

## <a name="next-steps"></a>Próximas etapas
Neste ponto, você tem um cluster seguro com o Azure Active Directory fornecendo autenticação de gerenciamento. Em seguida, [conecte cluster tooyour](service-fabric-connect-to-secure-cluster.md) e saiba como muito[gerenciar segredos do aplicativo](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Solucionar problemas na configuração do Azure Active Directory para autenticação de cliente
Se você tiver um problema enquanto você estiver configurando o Azure AD para autenticação de cliente, examine as possíveis soluções Olá nesta seção.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric Explorer solicita tooselect um certificado
#### <a name="problem"></a>Problema
Depois que você entrar com êxito tooAzure AD no Gerenciador do Service Fabric, navegador Olá retorna home page do toohello, mas uma mensagem solicitará que você tooselect um certificado.

![Caixa de diálogo de seleção de certificado SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a>Motivo
usuário Olá não está atribuído a uma função no hello aplicativo de cluster do AD do Azure. Assim, a autenticação do Azure AD falha no cluster do Service Fabric. Gerenciador do Service Fabric reverterá toocertificate autenticação.

#### <a name="solution"></a>Solução
Siga as instruções de saudação para a configuração do AD do Azure e atribuir funções de usuário. Além disso, é recomendável que você ativar "Aplicativo de tooaccess necessária de atribuição de usuário", como `SetupApplications.ps1` does.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Conexão com o PowerShell falha com erro: "hello especificado credenciais são inválidas"
#### <a name="problem"></a>Problema
Quando você usar o PowerShell tooconnect toohello cluster usando o modo de segurança "AzureActiveDirectory", depois que você entra com êxito tooAzure AD, conexão Olá falhará com um erro: "hello especificado credenciais são inválidas."

#### <a name="solution"></a>Solução
Essa solução é hello que igual Olá precedentes.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>O Service Fabric Explorer retorna uma falha quando você entra: "AADSTS50011"
#### <a name="problem"></a>Problema
Quando você tenta toosign em tooAzure AD no Gerenciador do Service Fabric, página Olá retorna uma falha: "AADSTS50011: Olá endereço de resposta &lt;url&gt; não coincide com os endereços de resposta de saudação configurados para o aplicativo hello: &lt;guid&gt;."

![O endereço de resposta SFX não corresponde][sfx-reply-address-not-match]

#### <a name="reason"></a>Motivo
aplicativo de cluster (web) Hello que representa o Gerenciador do Service Fabric tentativas tooauthenticate no AD do Azure e como parte da solicitação de saudação fornece Olá URL de retorno de redirecionamento. Mas Olá URL não está listado no aplicativo hello AD do Azure **URL de resposta** lista.

#### <a name="solution"></a>Solução
Em Olá **configurar** guia da saudação aplicativo (web) do cluster, adicione Olá URL do Gerenciador do Service Fabric toohello **URL de resposta** lista ou substituir um Olá itens na lista de saudação. Quando terminar, salve a alteração.

![URL de resposta do aplicativo Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Conecte-se o cluster hello usando a autenticação do AD do Azure por meio do PowerShell
Olá tooconnect cluster do Service Fabric, use Olá exemplo de comando do PowerShell a seguir:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn sobre Olá Connect-ServiceFabricCluster cmdlet, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Posso reutilizar o locatário Olá mesmo Azure AD em vários clusters?
Sim. Mas, lembre-se o aplicativo de cluster (web) tooadd hello URL do Gerenciador do Service Fabric tooyour. Caso contrário, o Service Fabric Explorer não funcionará.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Por que eu ainda preciso de um certificado de servidor quando o Azure AD está habilitado?
FabricClient e FabricGateway realizam autenticação mútua. Durante a autenticação do AD do Azure, integração do AD do Azure fornece um cliente para servidor toohello de identidade e certificado do servidor de saudação é a identidade do servidor de saudação tooverify usado. Para saber mais sobre certificados do Service Fabric, confira [Certificados X.509 e Service Fabric][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

