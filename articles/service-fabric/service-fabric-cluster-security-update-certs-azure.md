---
title: aaaManage certificados em um cluster do Azure Service Fabric | Microsoft Docs
description: "Descreve como tooadd novos certificados, o certificado de substituição e remover certificados tooor de um cluster do Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Adicionar ou remover certificados para um cluster do Service Fabric no Azure
É recomendável que você se familiarize com como o serviço de malha usa certificados x. 509 e estar familiarizado com hello [cenários de segurança de Cluster](service-fabric-cluster-security.md). Você deve entender o que é um certificado de cluster e qual sua finalidade, antes de continuar.

Segurança do certificado de serviço permite a malha que você especificar que dois cluster certificados, um principal e um secundário, quando você configurar durante a criação do cluster, em certificados de tooclient de adição. Consulte também[criando um cluster do azure por meio do portal](service-fabric-cluster-creation-via-portal.md) ou [criando um cluster do azure por meio do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obter detalhes sobre a configuração no momento da criação. Se você especificar apenas um certificado de cluster no momento da criação, que será usado como certificado principal hello. Após a criação do cluster, é possível adicionar um novo certificado como um secundário.

> [!NOTE]
> Para um cluster seguro, sempre precisará de pelo menos um cluster (não revogado e não expirado) válido certificado (primário ou secundário) implantado (se não, Olá cluster parará de funcionar). 90 dias antes de todos os certificados válidos alcançar expiração, sistema hello gera um rastreamento de avisos e também um evento de integridade de aviso no nó de saudação. Atualmente, não há nenhum email nem qualquer outra notificação enviada pelo Service Fabric sobre esse tópico. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Adicionar um certificado de cluster secundário usando o portal de saudação

Certificado de cluster secundário não pode ser adicionado por meio de saudação portal do Azure. Você tem toouse Azure powershell para fazer isso. Olá processo é descrito neste documento.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Trocar Olá certificados de cluster usando o portal de saudação

Depois de ter implantado com êxito um certificado de cluster secundário, se você quiser tooswap Olá primários e secundários, em seguida, navegue toohello folha de segurança e selecione a opção de 'Troca com primário' de saudação da saudação contexto menu tooswap Olá secundário cert com cert primário da saudação.

![Trocar o certificado][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Remover um certificado de cluster usando o portal de saudação

Para um cluster seguro, sempre será necessário pelo menos um (não revogado e não expirado) certificado válido (primário ou secundário) implantado se não, Olá cluster parará de funcionar.

tooremove certificado secundário seja usado para segurança de cluster, folha de segurança toohello navegue e selecione Olá 'Delete' opção no menu de contexto de saudação no certificado secundário hello.

Se sua intenção for certificado Olá tooremove está marcado como primário, em seguida, você precisará tooswap com hello secundário primeiro e exclua Olá secundário após a atualização de saudação.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Adicionar um certificado secundário usando o Powershell do Resource Manager

Essas etapas pressupõem que estão familiarizados com o funcionamento do Gerenciador de recursos de ter implantado pelo menos um cluster de malha do serviço usando um modelo do Gerenciador de recursos e ter Olá modelo que você usou tooset útil do cluster de saudação. Presume-se também que você esteja familiarizado com o uso do JSON.

> [!NOTE]
> Se você estiver procurando um modelo de exemplo e parâmetros que você pode usar toofollow ao longo ou como um ponto de partida, baixá-lo neste [repositório git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Editar o modelo do Resource Manager

Para facilitar a seguir ao longo, o exemplo 5-VM-1-NodeTypes-Secure_Step2.JSON contém todas as edições de saudação que realizaremos. exemplo Hello está disponível em [repositório git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Verifique se toofollow todas as etapas de saudação**

**Etapa 1:** abra o modelo do Gerenciador de recursos de saudação usada toodeploy Cluster. (Se você baixou o exemplo hello Olá acima repositório, usar 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy um cluster seguro e, em seguida, abra o modelo).

**Etapa 2:** adicionar **dois novos parâmetros** "secCertificateThumbprint" e "secCertificateUrlValue" do tipo "cadeia de caracteres" toohello seção de parâmetro do modelo. Você pode copiar Olá trecho de código a seguir e adicione-o modelo toohello. Dependendo da fonte de saudação do seu modelo, você pode já ter definido, caso mover toohello próxima etapa. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Etapa 3:** fazer alterações toohello **Microsoft.ServiceFabric/clusters** recurso - Localizar a definição de recurso "Microsoft.ServiceFabric/clusters" hello em seu modelo. Propriedades dessa definição, você encontrará "Certificate" JSON marca, que deve ser algo como Olá trecho JSON a seguir:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Adicione uma nova marcação “thumbprintSecondary” e atribua a ela um valor de “[parameters('secCertificateThumbprint')]”.  

Agora, a definição de recurso Olá deve ser semelhante Olá seguinte (dependendo de sua fonte de modelo hello, pode não ser exatamente como Olá trecho abaixo). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Se você quiser muito**cert de saudação de substituição**, em seguida, especifique o novo certificado de saudação como primária atual do primário e movendo hello como secundário. Isso resulta na substituição de saudação do seu certificado de novo de toohello atual do certificado primário em uma etapa de implantação.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Etapa 4:** fazer alterações muito**todos os** Olá **Microsoft.Compute/virtualMachineScaleSets** definições de recursos - Localizar Olá Microsoft.Compute/virtualMachineScaleSets recurso definição. Role toohello "publisher": "Microsoft.Azure.ServiceFabric", em "virtualMachineProfile".

Configurações do publicador da malha Olá serviço, você verá algo assim.

![Json_Pub_Setting1][Json_Pub_Setting1]

Adicionar Olá novo certificado entradas tooit

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

Propriedades de saudação agora devem se parecer com

![Json_Pub_Setting2][Json_Pub_Setting2]

Se você quiser muito**cert de saudação de substituição**, em seguida, especifique o novo certificado de saudação como primária atual do primário e movendo hello como secundário. Isso resulta na substituição de saudação do seu certificado de novo de toohello atual do certificado em uma etapa de implantação. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
Propriedades de saudação agora devem se parecer com

![Json_Pub_Setting3][Json_Pub_Setting3]


**Etapa 5:** fazer alterações muito**todos os** Olá **Microsoft.Compute/virtualMachineScaleSets** definições de recursos - Localizar Olá Microsoft.Compute/virtualMachineScaleSets recurso definição. Role toohello "vaultCertificates":, em "OSProfile". O resultado deve ser semelhante a este.


![Json_Pub_Setting4][Json_Pub_Setting4]

Adicione Olá secCertificateUrlValue tooit. Use Olá trecho de código a seguir:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Agora Olá resultante Json deve ser semelhante isso.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Certifique-se de que tem repetido as etapas 4 e 5 para todas as definições de recursos de Nodetypes/Microsoft.Compute/virtualMachineScaleSets Olá no modelo. Se você perder um deles, certificado Olá não será instalado em que VMSS e você terá resultados imprevisíveis em seu cluster, incluindo cluster Olá ficar inativo (se você acabará com nenhum certificado válido que nesse cluster Olá pode usar para segurança. Portanto, verifique, antes de continuar.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Editar seu modelo arquivo tooreflect Olá novos parâmetros adicionados acima
Se você estiver usando o exemplo hello da saudação [repositório git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow, você pode iniciar toomake alterações no hello exemplo 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 

Editar seu arquivo de parâmetro de modelo do Gerenciador de recursos, adicione Olá dois novos parâmetros para secCertificateThumbprint e secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Implantar Olá modelo tooAzure

- Você está agora pronto toodeploy tooAzure seu modelo. Abra um prompt de comando do Azure PS versão 1+.
- Faça logon no tooyour conta do Azure e selecione a assinatura do azure específico do hello. Essa é uma etapa importante para quem tem acesso toomore que uma assinatura do azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Testar Olá modelo anterior toodeploying-lo. Use Olá mesmo grupo de recursos que o cluster está implantado atualmente.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Implante grupo de recursos de tooyour Olá modelo. Use Olá mesmo grupo de recursos que o cluster está implantado atualmente. Execute Olá AzureRmResourceGroupDeployment novo comando. Modo de saudação toospecify, não é necessário desde que o valor padrão de saudação é **incremental**.

> [!NOTE]
> Se você definir o modo tooComplete, você pode excluir por engano recursos que não estão no modelo. Portanto, não o use neste cenário.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Aqui está um preenchido saída de exemplo de hello mesmo powershell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Após a conclusão da implantação Olá, conecte-se usando o cluster tooyour Olá novo certificado e executar algumas consultas. Se você é capaz de toodo. Em seguida, você pode excluir o certificado antigo hello. 

Se você estiver usando um certificado autoassinado, não se esqueça de tooimport-los no repositório de certificados local TrustedPeople.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Para referência rápida aqui é cluster seguro do hello comando tooconnect tooa 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Para referência rápida aqui está a integridade do cluster tooget Olá comando

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Implantação de cluster de toohello de certificados do aplicativo.

Você pode usar o hello mesmo etapas, conforme descrito nas etapas 5 acima toohave Olá certificados implantados por meio de um toohello keyvault nós. apenas é necessário definir e usar parâmetros diferentes.


## <a name="adding-or-removing-client-certificates"></a>Adicionando ou removendo certificados de cliente

No certificado de cluster toohello adição, você pode adicionar operações de gerenciamento de tooperform de certificados de cliente em um cluster do service fabric.

Você pode adicionar dois tipos de certificados de cliente - Admin ou Somente leitura. Em seguida, podem ser usados toocontrol operações de administração de toohello de acesso e operações de consulta no cluster hello. Por padrão, os certificados de cluster de saudação são adicionados toohello administrador certificados lista de permissões.

Você pode especificar qualquer número de certificados de cliente. Cada adição ou exclusão resulta em um cluster do configuração update toohello service fabric


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>A adição de certificados de cliente - Admin ou somente leitura por meio do portal

1. Navegue toohello folha de segurança e selecione Olá '+ autenticação' botão na parte superior da folha de segurança hello.
2. Na folha de 'Adicionar autenticação' hello, escolha Olá 'Tipo de autenticação' - 'Cliente somente leitura' ou 'client Admin'
3. Escolha método de autorização de saudação. Isso indica tooService Fabric se ele deve pesquisar o certificado usando o nome da entidade hello ou impressão digital de saudação. Em geral, não é um método de autorização segurança boa prática toouse Olá do nome da entidade. 

![Adicionar certificado de cliente][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Exclusão de certificados de cliente - Admin ou somente leitura usando Olá portal

tooremove certificado secundário seja usado para segurança de cluster, folha de segurança toohello navegue e selecione Olá 'Delete' opção no menu de contexto de saudação no certificado específico Olá.



## <a name="next-steps"></a>Próximas etapas
Leia estes artigos para obter mais informações sobre gerenciamento de cluster:

* [Processo de atualização de Cluster de Malha do Serviço e as suas expectativas](service-fabric-cluster-upgrade.md)
* [Configurar o acesso baseado em funções para clientes](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


