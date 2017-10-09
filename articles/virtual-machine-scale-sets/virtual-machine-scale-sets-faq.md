---
title: "escala de máquinas virtuais aaaAzure define perguntas frequentes | Microsoft Docs"
description: "Obtenha respostas toofrequently perguntas frequentes sobre conjuntos de escala de máquina virtual."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Perguntas frequentes sobre os conjuntos de dimensionamento de máquinas virtuais do Azure

Obtenha respostas define toofrequently perguntas frequentes sobre a escala de máquina virtual no Azure.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>Quais são as práticas recomendadas para o Dimensionamento Automático do Azure?

Para obter as práticas recomendadas para o Dimensionamento Automático, consulte as [Práticas recomendadas para o dimensionamento automático das máquinas virtuais](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Onde localizar os nomes de métrica para o dimensionamento automático usando as métricas baseadas em host?

Para ver os nomes de métrica para o dimensionamento automático que usa as medidas baseadas em host, consulte o [Suporte para as métricas com o Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Há exemplos de dimensionamento automático baseado em um tópico de Azure Service Bus e comprimento da fila?

Sim. Para obter exemplos de dimensionamento automático baseado em um tópico de Azure Service Bus e comprimento de fila, consulte as [Métricas comuns do dimensionamento automático do Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Para uma fila do barramento de serviço, use Olá JSON a seguir:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Para uma fila de armazenamento, use Olá JSON a seguir:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Substitua os valores de exemplo pelos URIs (Uniform Resource Identifier) do recurso.


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Devo dimensionar automaticamente usando as métricas baseadas em host ou uma extensão de diagnóstico?

Você pode criar uma configuração de AutoEscala em um métricas de nível de host VM toouse ou métricas de baseado no sistema operacional convidado.

Para obter uma lista das métricas com suporte, consulte [Métricas comuns de dimensionamento automático do Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Para obter um exemplo completo dos conjuntos de dimensionamento de máquinas virtuais, consulte a [Configuração avançada do dimensionamento automático usando modelos do Resource Manager para os conjuntos de dimensionamento de máquinas virtuais](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

exemplo Hello usa a métrica de CPU de nível de host hello e uma métrica de contagem de mensagem.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Como defino as regras de alerta em um conjunto de dimensionamento de máquinas virtuais?

Você pode criar alertas nas métricas dos conjuntos de dimensionamento de máquinas virtuais via PowerShell ou CLI do Azure. Para obter mais informações, consulte [Exemplos de início rápido do PowerShell do Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) e [Exemplos de início rápido da CLI de plataforma cruzada do Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Olá TargetResourceId do conjunto de escalas da máquina virtual Olá tem esta aparência: 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

Você pode escolher qualquer contador de desempenho da VM como tooset métrica Olá um alerta para. Para obter mais informações, consulte [métricas do sistema operacional convidado para VMs com base no Gerenciador de recursos do Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [métricas do sistema operacional convidado para VMs do Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) em Olá [métricas comuns de dimensionamento automático do Monitor do Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artigo.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Como configuro o dimensionamento automático em um conjunto de dimensionamento de máquinas virtuais usando o PowerShell?

tooset o dimensionamento automático em uma escala de máquina virtual definido usando o PowerShell, consulte Olá postagem de blog [como tooadd AutoEscala tooan escala de máquina virtual do Azure definir](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificados

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Como enviar com segurança o toohello um certificado VM? Como provisionar o um toorun de conjunto de escala de máquina virtual um site onde hello SSL para o site de saudação é fornecido com segurança de uma configuração de certificado? (operação de rotação de certificado comum Olá poderia ser quase Olá mesmo que uma operação de atualização de configuração.) Você tem um exemplo de como toodo isso? 

toosecurely enviar um toohello certificado VM, você pode instalar um certificado de cliente diretamente em um repositório de certificados do Windows do Cofre de chaves do cliente hello.

Use Olá JSON a seguir:

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

código Olá compatível com Windows e Linux.

Para obter mais informações, veja [Criar ou atualizar um conjunto de dimensionamento de máquinas virtuais](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Exemplo de Certificado autoassinado

1.  Crie um certificado autoassinado em um cofre de chaves.

    Olá use comandos do PowerShell a seguir:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Isso proporciona comando Olá entrada para o modelo do Azure Resource Manager hello.

    Para obter um exemplo de como toocreate um certificado autoassinado em um cofre de chaves, consulte [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Alterar o modelo do Gerenciador de recursos de saudação.

    Adicionar essa propriedade muito**virtualMachineProfile**, como parte da saudação recurso de conjunto de escala de máquina virtual:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Pode especificar um toouse do par de chaves de SSH para a autenticação de SSH com uma escala de máquina virtual Linux definida a partir de um modelo do Gerenciador de recursos?  

Sim. Olá API REST para **osProfile** é semelhante API REST de VM toohello padrão. 

Inclua **osProfile** em seu modelo:

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
Este bloco JSON é usado em [modelo de início rápido do hello 101-vm-chave SSH GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Olá perfil de sistema operacional também é usado em [grelayhost.json Olá GitHub rápida iniciar modelo](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Para obter mais informações, veja [Criar ou atualizar um conjunto de dimensionamento de máquinas virtuais](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Como remover certificados preteridos? 

tooremove preterido certificados, o certificado antigo do hello remover da lista de certificados de cofre hello. Deixe todos os certificados de saudação que você deseja tooremain em seu computador na lista de saudação. Isso não removerá o certificado de saudação de todas as suas VMs. Ele também não adicione Olá certificado toonew VMs que são criados no conjunto de escalas da máquina virtual hello. 

certificado de saudação tooremove de máquinas virtuais existentes, grave um script personalizado extensão toomanually remover Olá certificados do seu repositório de certificados.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Como inserir uma chave pública de SSH existente na camada SSH Olá máquina virtual escala conjunto durante o provisionamento? Desejo toostore Olá SSH públicos valores de chave no cofre de chaves do Azure e, em seguida, usá-los em meu modelo de Gerenciador de recursos.

Se você estiver fornecendo Olá VMs somente com uma chave SSH pública, chaves públicas do tooput Olá no cofre de chaves não é necessário. As chaves públicas não são secretas.
 
Você pode fornecer as chaves públicas SSH em texto sem formatação ao criar uma VM do Linux:

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
Nome do elemento linuxConfiguration | Obrigatório | Tipo | Descrição
--- | --- | --- | --- |  ---
ssh | Não | Coleção | Especifica a configuração de chave SSH Olá para um sistema operacional Linux
path | Sim | Cadeia de caracteres | Especifica o caminho de arquivo do Linux Olá onde as chaves de SSH hello ou certificado deve estar localizado
keyData | Sim | Cadeia de caracteres | Especifica uma chave pública SSH codificada em base64

Para obter um exemplo, consulte [modelo de início rápido do hello 101-vm-chave SSH GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Quando executar `Update-AzureRmVmss` depois da adição de mais de um certificado de saudação mesma chave cofre, vejo Olá a seguinte mensagem de erro:
 
>Update-AzureRmVmss: o segredo da lista contém repetidas instâncias de /subscriptions/<meu-id-assinatura>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, o que não é permitido.
 
Isso pode ocorrer se você tentar toore-adicionar Olá mesmo cofre em vez de usar um novo certificado do cofre para o Cofre de origem existente hello. Olá `Add-AzureRmVmssSecret` comando não funcionar corretamente se você estiver adicionando segredos adicionais.
 
tooadd mais segredos de saudação mesmo Cofre de chaves, atualização Olá $vmss.properties.osProfile.secrets[0].vaultCertificates lista.
 
Para Olá esperado a estrutura de entrada, consulte [criar ou atualizar uma máquina virtual configurada](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Localize segredo Olá Olá máquina virtual escala conjunto de objeto que está no cofre de chaves hello. Em seguida, adicione sua lista de toohello de referência (Olá URL e o nome de armazenamento secreto Olá) certificado associada Olá cofre.

> [!NOTE] 
> No momento, você não pode remover certificados de máquinas virtuais usando a API de conjunto de escala de máquina virtual hello.
>

Novas VMs não terá o certificado antigo hello. No entanto, as VMs que têm o certificado hello e que já foram implantado terão certificado antigo hello.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Push escala de máquinas virtuais toohello certificados definido sem fornecer a senha de hello, quando o certificado de saudação está no armazenamento secreto Olá?

Não é necessário senhas toohard código em scripts. Você pode recuperar dinamicamente senhas com permissões de saudação você usar o script de implantação toorun hello. Se você tiver um script que move um certificado do Cofre de chaves de armazenamento secreto hello, Olá armazenamento secreto `get certificate` comando também gera a senha de saudação do arquivo. pfx de saudação.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Como a propriedade de segredos de saudação do virtualMachineProfile.osProfile para uma escala de máquina virtual definir trabalho? Por que preciso quando houver toospecify Olá URI absoluto para um certificado usando a propriedade de certificateUrl Olá o valor de sourceVault Olá? 

Uma referência de certificado do Windows Remote Management (WinRM) deve estar presente no hello propriedade segredos de saudação do perfil de SO. 

Olá finalidade indicando o Cofre de origem Olá é políticas (ACL) da lista de controle de acesso de tooenforce que existem no modelo de serviço de nuvem do Azure do usuário. Se o Cofre de origem Olá não for especificado, os usuários que não têm permissões toodeploy ou acesso segredos tooa Cofre de chaves seria capaz de toothrough um provedor de recursos de computação (CRP). As ACLs existem até para os recursos que não existem.

Se você fornecer uma ID de Cofre de origem incorreto mas uma URL de Cofre de chave válido, um erro é relatado quando você sondar a operação de saudação.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Se adicionar tooan segredos existente conjunto de escalas da máquina virtual, são segredos Olá injetados em VMs existentes, ou apenas no novos? 

Os certificados são adicionados tooall suas VMs, preexistente até mesmo aquelas. Se a escala de máquina virtual definir propriedade de upgradePolicy está definido muito**manual**, certificado de saudação é adicionado toohello VM quando você executar uma atualização manual em Olá VM.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Onde coloco os certificados para as VMs do Linux?

toolearn como toodeploy certificados para VMs do Linux, consulte [implantar certificados tooVMs de um cofre de chaves gerenciados pelo cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Como adicionar um novo cofre certificado tooa novo objeto de certificado?

tooadd um cofre tooan existente segredo de certificado, consulte Olá PowerShell de exemplo a seguir. Use apenas um objeto de segredo.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Se você recriar a imagem de uma máquina virtual, o que acontece toocertificates?

Se você recriar a imagem de uma VM, os certificados serão excluídos. Refazer a imagem de disco do sistema operacional exclusões Olá todo. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>O que acontece se você excluir um certificado de chave de cofre Olá?

Se segredo Olá é excluído do Cofre de chaves Olá, e, em seguida, executar `stop deallocate` para todas as suas VMs e, em seguida, iniciá-los novamente, você encontrará uma falha. Falha de saudação ocorre porque Olá CRP precisa tooretrieve segredos de saudação do Cofre de chave hello, mas ele não pode. Nesse cenário, você pode excluir certificados de saudação do modelo de conjunto de escala de máquina virtual de saudação. 

componente de CRP Olá não mantém os segredos de cliente. Se você executar `stop deallocate` para todas as VMs no conjunto de escalas da máquina virtual hello, Olá será excluído. Nesse cenário, os segredos são recuperados do Cofre de chaves de saudação.

Você não encontrar esse problema ao expandir porque há uma cópia armazenada em cache de segredo Olá no Azure Service Fabric (no modelo de malha de único locatário Olá).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Por que tenho local exato do toospecify Olá Olá URL de certificado (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), conforme indicado na [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Olá documentação do Cofre de chaves do Azure informa que Olá que obter API de REST do segredo deve retornar a versão mais recente de saudação do segredo Olá se Olá versão não for especificada.
 
Método | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

Substitua {*secret-name*} com nome hello e substituir {*versão do segredo*} com a versão de saudação do segredo Olá deseja tooretrieve. a versão do segredo Olá pode ser excluída. Nesse caso, a versão atual do hello é recuperado.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Por que tem a versão de certificado Olá toospecify quando usar o Cofre de chaves?

finalidade Olá Olá versão Cofre de chaves requisito toospecify Olá certificado é toomake toohello usuário claro qual certificado será implantado em suas VMs.

Se você cria uma máquina virtual e, em seguida, atualize seu segredo no cofre de chaves Olá, Olá novo certificado não é baixado tooyour VMs. Mas suas VMs aparecem tooreference e novas VMs obtém novo segredo do hello. tooavoid isso, são necessária tooreference uma versão do segredo.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Minha equipe funciona com vários certificados são distribuídos toous como chaves públicas. cer. O que é Olá abordagem para implantar o conjunto de escalas da máquina virtual de tooa esses certificados recomendada?

conjunto de escala do virtual machine tooa do toodeploy. cer chaves públicas, você pode gerar um arquivo. pfx que contém somente arquivos. cer. toodo isso, use `X509ContentType = Pfx`. Por exemplo, carregar o arquivo. cer de saudação como um objeto x509Certificate2 em c# ou PowerShell e, em seguida, chame o método hello. 

Para obter mais informações, consulte [Método X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Não vejo uma opção para os usuários toopass em certificados como cadeias de caracteres base64. A maioria dos outros provedores de recursos tem essa opção.

tooemulate passando um certificado como uma cadeia de caracteres base64, você pode extrair hello mais recente URL de versão em um modelo do Gerenciador de recursos. Inclua Olá propriedade JSON em seu modelo do Gerenciador de recursos a seguir:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>É necessário toowrap certificados de objetos JSON em cofres chave?

Nos conjuntos de dimensionamento de máquinas virtuais, os certificados devem ser encapsulados nos objetos JSON. 

Também há suporte para tipo de conteúdo de saudação application/x-pkcs12. Para obter instruções sobre como usar application/x-pkcs12, consulte os [Certificados PFX no Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
Atualmente não temos suporte para os arquivos .cer. arquivos. cer de toouse, exportá-los em contêineres. pfx.



## <a name="compliance"></a>Conformidade

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Os conjuntos de dimensionamento de máquinas virtuais são compatíveis com o PCI?

Conjuntos de escala de máquinas virtuais são uma camada de API thin sobre Olá CRP. Ambos os componentes são parte da plataforma de computação Olá Olá árvore de serviço do Azure.

De uma perspectiva de conformidade, conjuntos de escala de máquinas virtuais são uma parte fundamental da plataforma de computação do Azure hello. Eles compartilham uma equipe, ferramentas, processos, metodologia de implantação, controles de segurança, just-in-time (JIT) compilação, monitoramento, alertas e assim por diante, com CRP Olá em si. Conjuntos de escala de máquinas virtuais são Payment Card Industry (PCI)-compatíveis porque faz parte de atestado de PCI dados segurança padrão (DSS) atual Olá Olá CRP.

Para obter mais informações, consulte [Olá Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Extensões

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Como excluo uma extensão do conjunto de dimensionamento de máquinas virtuais?

toodelete uma escala de máquina virtual definir a extensão de saudação do uso do PowerShell exemplo a seguir:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Você pode encontrar hello extensionName valor em `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Há um exemplo de modelo do conjunto de dimensionamento de máquinas virtuais que se integra com o Operations Management Suite?

Para uma escala de máquina virtual do conjunto de exemplo de modelo que se integra ao Operations Management Suite, consulte o segundo exemplo hello em [implantar um cluster do Azure Service Fabric e habilitar o monitoramento usando a análise de Log](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Extensões parecerem toorun em paralelo em conjuntos de escala de máquina virtual. Isso faz com que o meu toofail de extensão do script personalizado. O que fazer toofix isso?

toolearn sobre sequenciamento de extensão em conjuntos de escala de máquina virtual, consulte [sequenciamento de extensão em conjuntos de escala de máquina virtual do Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Como redefinir senha Olá para VMs em meu conjunto de escala de máquinas virtuais?

senha de saudação tooreset para VMs na escala de sua máquina virtual definido, usar extensões de acesso VM. 

Saudação de uso do PowerShell exemplo a seguir:

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Como adicionar uma extensão tooall VMs em meu conjunto de escala de máquinas virtuais?

Se a política de atualização for definida muito**automáticas**, reimplantação modelo Olá com novas propriedades de extensão Olá atualiza todas as máquinas virtuais.

Se a política de atualização for definida muito**manual**, primeiro atualize a extensão hello e, em seguida, atualizar manualmente todas as instâncias em suas VMs.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Se as extensões de saudação associadas a um conjunto de escala de máquina virtual existente forem atualizadas, existentes VMs afetadas? (Ou seja, será Olá VMs *não* modelo de conjunto de escala de máquina virtual do correspondência Olá?) Ou serão ignoradas? Quando uma máquina existente é recuperado de serviço ou imagem refeita, Olá scripts que estão configuradas atualmente no conjunto de escalas da máquina virtual Olá executado ou são scripts de saudação que foram configurados quando usado Olá que VM foi criada pela primeira vez?

Se a definição de extensão Olá na escala de máquinas virtuais Olá definido modelo é atualizado e Olá upgradePolicy está definida muito**automático**, ele atualiza Olá VMs. Se Olá upgradePolicy está definida muito**manual**, extensões são sinalizadas como não coincide com o modelo de saudação. 

Se uma VM existente é recuperado de serviço, ele aparecerá como uma reinicialização e extensões de saudação não são novamente. Se ela é criada, é como substituição de unidade Olá SO com a imagem de origem de saudação. Qualquer especialização de modelo mais recente hello, como extensões, são executados.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Como faço para ingressar em um domínio de tooan AD do Azure do conjunto de escala máquina virtual?

toojoin um máquina virtual escala conjunto tooan Azure Active Directory (AD do Azure) domínio, você pode definir uma extensão. 

toodefine uma extensão, use a propriedade de JsonADDomainExtension de saudação:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>Extensão de conjunto de escala minha máquina virtual está tentando tooinstall algo que requer uma reinicialização. Por exemplo, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"

Se sua extensão de conjunto de escala de máquina virtual está tentando tooinstall algo que requer uma reinicialização, você pode usar a extensão do hello Azure Automation configuração do estado desejado (DSC de automação). Se o sistema operacional de saudação for Windows Server 2012 R2, o Azure extrai na instalação do Windows Management Framework (WMF) 5.0 hello, reinicializações e, em seguida, continua com a configuração de saudação. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Como ativo o antimalware em meu conjunto de dimensionamento de máquinas virtuais?

tooturn em antimalware em sua escala de máquina virtual definido, use Olá PowerShell de exemplo a seguir:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Preciso de tooexecute um script personalizado que é hospedado em uma conta de armazenamento privado. Olá script é executado com êxito ao armazenamento de saudação é público, mas quando tento toouse uma assinatura de acesso compartilhado (SAS), ele falhará. Esta mensagem é exibida: "Parâmetros obrigatórios ausentes para uma Assinatura de Acesso Compartilhado válida". O link+SAS funcionam bem em meu navegador local.

tooexecute um script personalizado que é hospedado em uma conta de armazenamento privado, defina as configurações protegidas com chave de conta de armazenamento hello e nome. Para obter mais informações, consulte [Extensão de Script Personalizado para o Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Rede
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>É possível tooassign definida em uma escala de tooa do grupo de segurança de rede (NSG), para que ele aplicará tooall Olá NICs de VM no conjunto de Olá?

Sim. Um grupo de segurança de rede podem ser aplicado diretamente o conjunto de escala de tooa fazendo referência a ele na seção de networkInterfaceConfigurations Olá Olá de perfil de rede. Exemplo:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Como fazer uma permuta de VIP para conjuntos de escala de máquinas virtuais em Olá mesma assinatura e região mesmo?

Se você tiver duas VMs conjuntos de escala de máquina com o balanceador de carga do Azure front-ends e estão em Olá a mesma assinatura e região, você poderia desalocar os endereços IP públicos saudação de cada um deles e atribuir toohello outros. Consulte [Permuta de VIP: implantação azul-verde no Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) para ver um exemplo. Isso implica um atraso, embora como Olá recursos são alocados/desalocado no nível de rede de saudação. Uma opção mais rápida é toouse Azure Application Gateway com dois pools de back-end e uma regra de roteamento. Como alternativa, você pode hospedar o aplicativo no [serviço de Aplicativo do Azure](https://azure.microsoft.com/en-us/services/app-service/), que fornece suporte para a alternância rápida entre slots de preparo e de produção.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Como posso especificar um intervalo de toouse de endereços IP privado para alocação de endereço IP privada estática?

Os endereços IPs são selecionados em uma sub-rede que você especifica. 

método de alocação de saudação de endereços IP de conjunto de escala de máquina virtual é sempre "dinâmico", mas isso não significa que esses endereços IP podem alterar. Nesse caso, "dinâmico" significa apenas que você não especificar o endereço IP de saudação em uma solicitação PUT. Especifique definido por meio de sub-rede Olá Olá estático. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Como posso implantar uma máquina virtual escala conjunto tooan existente rede virtual do Azure? 

toodeploy uma escala de máquina virtual definir tooan existente da rede virtual do Azure, consulte [implantar uma máquina virtual escala conjunto tooan rede virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Como adicionar endereço IP de saudação do hello primeira VM em uma escala de máquina virtual definido toohello saída de um modelo?

endereço IP de saudação tooadd de saudação primeira VM em uma saída de toohello do conjunto de escala máquina virtual de um modelo, consulte [ARM: IPs privados do VMSS obter](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Posso usar conjuntos de escala com Rede Acelerada?

Sim. toouse acelerado por rede, defina enableAcceleratedNetworking tootrue na sua escala do conjunto de networkInterfaceConfigurations. Por exemplo
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Como posso configurar servidores DNS Olá usados por um conjunto de escala?

toocreate uma escala VM definida com uma configuração personalizada do DNS, adicione que uma escala de toohello dnsSettings JSON pacote definido networkInterfaceConfigurations seção. Exemplo:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Como configurar um conjunto de escala tooassign um tooeach de endereço IP público VM?

toocreate conjunto de uma escala VM que atribui um tooeach de endereço IP público VM, certifique-se de saudação API versão Olá Microsoft.Compute/virtualMAchineScaleSets recurso está 2017-03-30 e adicionar um _publicipaddressconfiguration_ pacote JSON o conjunto de escala de toohello ipConfigurations seção. Exemplo:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Pode configurar um toowork de conjunto de escala com vários Gateways de aplicativo?

Sim. Você pode adicionar Olá id de recurso para vários endereços de back-end de Application Gateway toohello pools _applicationGatewayBackendAddressPools_ lista Olá _ipConfigurations_ seção de seu conjunto de escala perfil de rede.

## <a name="scale"></a>Escala

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>No qual situação eu criaria um conjunto de dimensionamento de máquinas virtuais com menos de duas VMs?

Um motivo toocreate uma escala de máquina virtual definido com menos de duas VMs seriam definidas toouse Olá Elástico propriedades uma escala de máquina virtual. Por exemplo, você pode implantar um conjunto de escala de máquinas virtuais com zero toodefine VMs sua infraestrutura sem pagar VM que executa os custos. Em seguida, quando você estiver pronto toodeploy VMs, aumente hello "capacidade" da escala de máquina virtual Olá conjunto toohello produção instância contagem.

Outro motivo para criar um conjunto de dimensionamento de máquinas virtuais com menos de duas VMs é se você estiver menos preocupado com disponibilidade do que com o uso de um conjunto de disponibilidade com VMs separadas. Conjuntos de escala de máquinas virtuais oferecem um toowork de maneira com as unidades de computação não-diferenciado fungível. Essa uniformidade é um diferencial importante para os conjuntos de dimensionamento de máquinas virtuais versus os conjuntos de disponibilidade. Muitas cargas de trabalho sem estado não controlam as unidades individuais. Se a carga de trabalho Olá cair, reduzir a unidade de computação tooone e cresçam toomany quando a carga de trabalho Olá aumenta.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Como alterar o número de saudação de VMs em um conjunto de escala de máquinas virtuais?

número de saudação toochange de VMs em um conjunto de escala de máquina virtual, consulte [altere Olá contagem de instância de um conjunto de escala de máquina virtual](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Como defino alertas personalizados para quando determinados limites são atingidos?

Há alguma flexibilidade em como lidar com os alertas para os limites especificados. Por exemplo, você pode definir webhooks personalizados. Olá webhook exemplo a seguir é de um modelo do Gerenciador de recursos:

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

Neste exemplo, um alerta vai tooPagerduty.com quando um limite for atingido.



## <a name="patching-and-operations"></a>Aplicação de patch e operações

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Como fazer para criar um conjunto de dimensionamento em um grupo de recursos existente?

Criando conjuntos de escala em um recurso existente grupo ainda não é possível Olá portal do Azure, mas você pode especificar um grupo de recursos existente quando a implantação de uma escala definido de um modelo do Gerenciador de recursos do Azure. Também é possível especificar um grupo de recursos existente ao criar um conjunto de dimensionamento usando o Azure PowerShell ou a CLI.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Pode mover que uma escala de definir o grupo de recursos de tooanother?

Sim, você pode mover escala conjunto de recursos tooa nova assinatura ou grupo de recursos.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Como atualizar tooI minha escala de máquina virtual defina tooa nova imagem? Como gerencio os patches?

tooupdate sua escala de máquina virtual definido tooa nova imagem e toomanage a aplicação de patch, consulte [atualizar um conjunto de escala de máquinas virtuais](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Pode usar tooreset de operação de recriação de imagem Olá uma VM sem alterar a imagem de Olá? (Ou seja, deseja redefinir uma VM toofactory configurações em vez de tooa nova imagem.)

Sim, você pode usar tooreset de operação de recriação de imagem Olá uma VM sem alterar a imagem de saudação. No entanto, se a escala de máquina virtual definido faz referência a uma imagem de plataforma com `version = latest`, sua VM pode atualizar tooa imagem de sistema operacional posterior ao chamar `reimage`.

Para obter mais informações, consulte [Gerenciar todas as VMs em um conjunto de dimensionamento de máquinas virtuais](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Solucionar problemas

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Como ativo o diagnóstico de inicialização?

tooturn no diagnóstico de inicialização, primeiro, crie uma conta de armazenamento. Em seguida, colocar esse bloco JSON em seu conjunto de escala de máquinas virtuais **virtualMachineProfile**e atualizar o conjunto de escalas da máquina virtual hello:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Quando uma nova VM é criada, Olá InstanceView propriedade Olá VM mostra detalhes de saudação para captura de tela hello e assim por diante. Aqui está um exemplo:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Propriedades de máquina virtual

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Como obtenho informações de propriedade para cada VM sem fazer várias chamadas? Por exemplo, como seria obter domínio de falha de saudação do cada Olá 100 VMs em meu conjunto de escala de máquinas virtuais?

informações de propriedade tooget para cada VM sem fazer várias chamadas, você pode chamar `ListVMInstanceViews` fazendo uma API REST `GET` em Olá URI do recurso a seguir:

/subscriptions/<id_assinatura>/resourceGroups/<nome_grupo_recursos>/providers/Microsoft.Compute/virtualMachineScaleSets/<nome_conjunto_dimensionamento>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Pode, passar argumentos de extensão diferente toodifferent VMs em um conjunto de escala de máquinas virtuais?

Não, você não pode passar argumentos de extensão diferente toodifferent VMs em um conjunto de escala de máquinas virtuais. No entanto, as extensões podem agir com base em propriedades exclusivas de saudação do hello VM estão sendo executados em tal como em nome da máquina hello. Extensões também podem consultar metadados de instância no http://169.254.169.254 tooget obter mais informações sobre Olá VM.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Por que existem lacunas entre os nomes de máquina e as IDs da VM do conjunto de dimensionamento de máquinas virtuais? Por exemplo: 0, 1, 3...

Existem lacunas entre seus nomes de computador VM do conjunto de escala de máquina virtual e IDs de VM, porque o conjunto de escala de sua máquina virtual **overprovision** propriedade é definir o valor de padrão de toohello de **true**. Se o excesso de provisionamento está definido muito**true**, mais VMs que solicitado são criados. Então, as VMs extras são excluídas. Nesse caso, você obter implantação maior confiabilidade, mas à custa de saudação de contígua de nomenclatura e contíguos conversão de endereço de rede (NAT) de regras. 

Você pode definir essa propriedade muito**false**. Para os conjuntos de dimensionamento de máquinas virtuais pequenos, isso não afeta muito a confiabilidade da implantação.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Qual é a diferença Olá entre a exclusão de uma VM em um conjunto de escala de máquinas virtuais e desalocando Olá VM? Quando devo escolher um em detrimento de outros Olá?

Olá principal diferença entre a exclusão de uma VM em um conjunto de escala de máquinas virtuais e desalocando Olá VM é que `deallocate` não exclui Olá discos de rígidos virtuais (VHDs). Existem custos de armazenamento associados à execução de `stop deallocate`. Você pode usar um ou Olá outros para uma saudação motivos a seguir:

- Você deseja toostop pagar custos de computação, mas deseja que o estado do disco Olá tookeep de saudação VMs.
- Você deseja toostart um conjunto de VMs mais rapidamente do que você pode expandir um conjunto de escala de máquinas virtuais.
  - Cenário de toothis relacionados, você pode ter criado seu próprio mecanismo de dimensionamento automático e quiser uma escala de ponta a ponta mais rápida.
- Você tem um conjunto de dimensionamento de máquinas virtuais distribuído sem uniformidade entre os domínios de falha ou os domínios de atualização. Isso pode ser porque você excluiu seletivamente as VMs ou porque as VMs foram excluídas depois do excesso de provisionamento. Executando `stop deallocate` seguido `start` na máquina virtual de saudação escala definida uniformemente distribui Olá VMs em domínios de falha ou domínios de atualização.

