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
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="0f17b-103">Perguntas frequentes sobre os conjuntos de dimensionamento de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="0f17b-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="0f17b-104">Obtenha respostas define toofrequently perguntas frequentes sobre a escala de máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="0f17b-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="0f17b-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="0f17b-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="0f17b-106">Quais são as práticas recomendadas para o Dimensionamento Automático do Azure?</span><span class="sxs-lookup"><span data-stu-id="0f17b-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="0f17b-107">Para obter as práticas recomendadas para o Dimensionamento Automático, consulte as [Práticas recomendadas para o dimensionamento automático das máquinas virtuais](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="0f17b-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="0f17b-108">Onde localizar os nomes de métrica para o dimensionamento automático usando as métricas baseadas em host?</span><span class="sxs-lookup"><span data-stu-id="0f17b-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="0f17b-109">Para ver os nomes de métrica para o dimensionamento automático que usa as medidas baseadas em host, consulte o [Suporte para as métricas com o Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="0f17b-110">Há exemplos de dimensionamento automático baseado em um tópico de Azure Service Bus e comprimento da fila?</span><span class="sxs-lookup"><span data-stu-id="0f17b-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="0f17b-111">Sim.</span><span class="sxs-lookup"><span data-stu-id="0f17b-111">Yes.</span></span> <span data-ttu-id="0f17b-112">Para obter exemplos de dimensionamento automático baseado em um tópico de Azure Service Bus e comprimento de fila, consulte as [Métricas comuns do dimensionamento automático do Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="0f17b-113">Para uma fila do barramento de serviço, use Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="0f17b-114">Para uma fila de armazenamento, use Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="0f17b-115">Substitua os valores de exemplo pelos URIs (Uniform Resource Identifier) do recurso.</span><span class="sxs-lookup"><span data-stu-id="0f17b-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="0f17b-116">Devo dimensionar automaticamente usando as métricas baseadas em host ou uma extensão de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="0f17b-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="0f17b-117">Você pode criar uma configuração de AutoEscala em um métricas de nível de host VM toouse ou métricas de baseado no sistema operacional convidado.</span><span class="sxs-lookup"><span data-stu-id="0f17b-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="0f17b-118">Para obter uma lista das métricas com suporte, consulte [Métricas comuns de dimensionamento automático do Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="0f17b-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="0f17b-119">Para obter um exemplo completo dos conjuntos de dimensionamento de máquinas virtuais, consulte a [Configuração avançada do dimensionamento automático usando modelos do Resource Manager para os conjuntos de dimensionamento de máquinas virtuais](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="0f17b-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="0f17b-120">exemplo Hello usa a métrica de CPU de nível de host hello e uma métrica de contagem de mensagem.</span><span class="sxs-lookup"><span data-stu-id="0f17b-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-121">Como defino as regras de alerta em um conjunto de dimensionamento de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-122">Você pode criar alertas nas métricas dos conjuntos de dimensionamento de máquinas virtuais via PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f17b-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="0f17b-123">Para obter mais informações, consulte [Exemplos de início rápido do PowerShell do Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) e [Exemplos de início rápido da CLI de plataforma cruzada do Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="0f17b-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="0f17b-124">Olá TargetResourceId do conjunto de escalas da máquina virtual Olá tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0f17b-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="0f17b-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="0f17b-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="0f17b-126">Você pode escolher qualquer contador de desempenho da VM como tooset métrica Olá um alerta para.</span><span class="sxs-lookup"><span data-stu-id="0f17b-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="0f17b-127">Para obter mais informações, consulte [métricas do sistema operacional convidado para VMs com base no Gerenciador de recursos do Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [métricas do sistema operacional convidado para VMs do Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) em Olá [métricas comuns de dimensionamento automático do Monitor do Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artigo.</span><span class="sxs-lookup"><span data-stu-id="0f17b-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="0f17b-128">Como configuro o dimensionamento automático em um conjunto de dimensionamento de máquinas virtuais usando o PowerShell?</span><span class="sxs-lookup"><span data-stu-id="0f17b-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="0f17b-129">tooset o dimensionamento automático em uma escala de máquina virtual definido usando o PowerShell, consulte Olá postagem de blog [como tooadd AutoEscala tooan escala de máquina virtual do Azure definir](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="0f17b-130">Certificados</span><span class="sxs-lookup"><span data-stu-id="0f17b-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="0f17b-131">Como enviar com segurança o toohello um certificado VM?</span><span class="sxs-lookup"><span data-stu-id="0f17b-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="0f17b-132">Como provisionar o um toorun de conjunto de escala de máquina virtual um site onde hello SSL para o site de saudação é fornecido com segurança de uma configuração de certificado?</span><span class="sxs-lookup"><span data-stu-id="0f17b-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="0f17b-133">(operação de rotação de certificado comum Olá poderia ser quase Olá mesmo que uma operação de atualização de configuração.) Você tem um exemplo de como toodo isso?</span><span class="sxs-lookup"><span data-stu-id="0f17b-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="0f17b-134">toosecurely enviar um toohello certificado VM, você pode instalar um certificado de cliente diretamente em um repositório de certificados do Windows do Cofre de chaves do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="0f17b-135">Use Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-135">Use hello following JSON:</span></span>

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

<span data-ttu-id="0f17b-136">código Olá compatível com Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="0f17b-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="0f17b-137">Para obter mais informações, veja [Criar ou atualizar um conjunto de dimensionamento de máquinas virtuais](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f17b-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="0f17b-138">Exemplo de Certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="0f17b-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="0f17b-139">Crie um certificado autoassinado em um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="0f17b-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="0f17b-140">Olá use comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="0f17b-141">Isso proporciona comando Olá entrada para o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="0f17b-142">Para obter um exemplo de como toocreate um certificado autoassinado em um cofre de chaves, consulte [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="0f17b-143">Alterar o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="0f17b-144">Adicionar essa propriedade muito**virtualMachineProfile**, como parte da saudação recurso de conjunto de escala de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="0f17b-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="0f17b-145">Pode especificar um toouse do par de chaves de SSH para a autenticação de SSH com uma escala de máquina virtual Linux definida a partir de um modelo do Gerenciador de recursos?</span><span class="sxs-lookup"><span data-stu-id="0f17b-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="0f17b-146">Sim.</span><span class="sxs-lookup"><span data-stu-id="0f17b-146">Yes.</span></span> <span data-ttu-id="0f17b-147">Olá API REST para **osProfile** é semelhante API REST de VM toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="0f17b-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="0f17b-148">Inclua **osProfile** em seu modelo:</span><span class="sxs-lookup"><span data-stu-id="0f17b-148">Include **osProfile** in your template:</span></span>

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
 
<span data-ttu-id="0f17b-149">Este bloco JSON é usado em [modelo de início rápido do hello 101-vm-chave SSH GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="0f17b-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="0f17b-150">Olá perfil de sistema operacional também é usado em [grelayhost.json Olá GitHub rápida iniciar modelo](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="0f17b-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="0f17b-151">Para obter mais informações, veja [Criar ou atualizar um conjunto de dimensionamento de máquinas virtuais](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="0f17b-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="0f17b-152">Como remover certificados preteridos?</span><span class="sxs-lookup"><span data-stu-id="0f17b-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="0f17b-153">tooremove preterido certificados, o certificado antigo do hello remover da lista de certificados de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="0f17b-154">Deixe todos os certificados de saudação que você deseja tooremain em seu computador na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="0f17b-155">Isso não removerá o certificado de saudação de todas as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="0f17b-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="0f17b-156">Ele também não adicione Olá certificado toonew VMs que são criados no conjunto de escalas da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="0f17b-157">certificado de saudação tooremove de máquinas virtuais existentes, grave um script personalizado extensão toomanually remover Olá certificados do seu repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="0f17b-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="0f17b-158">Como inserir uma chave pública de SSH existente na camada SSH Olá máquina virtual escala conjunto durante o provisionamento?</span><span class="sxs-lookup"><span data-stu-id="0f17b-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="0f17b-159">Desejo toostore Olá SSH públicos valores de chave no cofre de chaves do Azure e, em seguida, usá-los em meu modelo de Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f17b-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="0f17b-160">Se você estiver fornecendo Olá VMs somente com uma chave SSH pública, chaves públicas do tooput Olá no cofre de chaves não é necessário.</span><span class="sxs-lookup"><span data-stu-id="0f17b-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="0f17b-161">As chaves públicas não são secretas.</span><span class="sxs-lookup"><span data-stu-id="0f17b-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="0f17b-162">Você pode fornecer as chaves públicas SSH em texto sem formatação ao criar uma VM do Linux:</span><span class="sxs-lookup"><span data-stu-id="0f17b-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

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
 
<span data-ttu-id="0f17b-163">Nome do elemento linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="0f17b-163">linuxConfiguration element name</span></span> | <span data-ttu-id="0f17b-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0f17b-164">Required</span></span> | <span data-ttu-id="0f17b-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f17b-165">Type</span></span> | <span data-ttu-id="0f17b-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f17b-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="0f17b-167">ssh</span><span class="sxs-lookup"><span data-stu-id="0f17b-167">ssh</span></span> | <span data-ttu-id="0f17b-168">Não</span><span class="sxs-lookup"><span data-stu-id="0f17b-168">No</span></span> | <span data-ttu-id="0f17b-169">Coleção</span><span class="sxs-lookup"><span data-stu-id="0f17b-169">Collection</span></span> | <span data-ttu-id="0f17b-170">Especifica a configuração de chave SSH Olá para um sistema operacional Linux</span><span class="sxs-lookup"><span data-stu-id="0f17b-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="0f17b-171">path</span><span class="sxs-lookup"><span data-stu-id="0f17b-171">path</span></span> | <span data-ttu-id="0f17b-172">Sim</span><span class="sxs-lookup"><span data-stu-id="0f17b-172">Yes</span></span> | <span data-ttu-id="0f17b-173">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f17b-173">String</span></span> | <span data-ttu-id="0f17b-174">Especifica o caminho de arquivo do Linux Olá onde as chaves de SSH hello ou certificado deve estar localizado</span><span class="sxs-lookup"><span data-stu-id="0f17b-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="0f17b-175">keyData</span><span class="sxs-lookup"><span data-stu-id="0f17b-175">keyData</span></span> | <span data-ttu-id="0f17b-176">Sim</span><span class="sxs-lookup"><span data-stu-id="0f17b-176">Yes</span></span> | <span data-ttu-id="0f17b-177">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f17b-177">String</span></span> | <span data-ttu-id="0f17b-178">Especifica uma chave pública SSH codificada em base64</span><span class="sxs-lookup"><span data-stu-id="0f17b-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="0f17b-179">Para obter um exemplo, consulte [modelo de início rápido do hello 101-vm-chave SSH GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="0f17b-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="0f17b-180">Quando executar `Update-AzureRmVmss` depois da adição de mais de um certificado de saudação mesma chave cofre, vejo Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0f17b-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="0f17b-181">Update-AzureRmVmss: o segredo da lista contém repetidas instâncias de /subscriptions/<meu-id-assinatura>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, o que não é permitido.</span><span class="sxs-lookup"><span data-stu-id="0f17b-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="0f17b-182">Isso pode ocorrer se você tentar toore-adicionar Olá mesmo cofre em vez de usar um novo certificado do cofre para o Cofre de origem existente hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="0f17b-183">Olá `Add-AzureRmVmssSecret` comando não funcionar corretamente se você estiver adicionando segredos adicionais.</span><span class="sxs-lookup"><span data-stu-id="0f17b-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="0f17b-184">tooadd mais segredos de saudação mesmo Cofre de chaves, atualização Olá $vmss.properties.osProfile.secrets[0].vaultCertificates lista.</span><span class="sxs-lookup"><span data-stu-id="0f17b-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="0f17b-185">Para Olá esperado a estrutura de entrada, consulte [criar ou atualizar uma máquina virtual configurada](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f17b-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="0f17b-186">Localize segredo Olá Olá máquina virtual escala conjunto de objeto que está no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="0f17b-187">Em seguida, adicione sua lista de toohello de referência (Olá URL e o nome de armazenamento secreto Olá) certificado associada Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="0f17b-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="0f17b-188">No momento, você não pode remover certificados de máquinas virtuais usando a API de conjunto de escala de máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="0f17b-189">Novas VMs não terá o certificado antigo hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="0f17b-190">No entanto, as VMs que têm o certificado hello e que já foram implantado terão certificado antigo hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="0f17b-191">Push escala de máquinas virtuais toohello certificados definido sem fornecer a senha de hello, quando o certificado de saudação está no armazenamento secreto Olá?</span><span class="sxs-lookup"><span data-stu-id="0f17b-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="0f17b-192">Não é necessário senhas toohard código em scripts.</span><span class="sxs-lookup"><span data-stu-id="0f17b-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="0f17b-193">Você pode recuperar dinamicamente senhas com permissões de saudação você usar o script de implantação toorun hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="0f17b-194">Se você tiver um script que move um certificado do Cofre de chaves de armazenamento secreto hello, Olá armazenamento secreto `get certificate` comando também gera a senha de saudação do arquivo. pfx de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="0f17b-195">Como a propriedade de segredos de saudação do virtualMachineProfile.osProfile para uma escala de máquina virtual definir trabalho?</span><span class="sxs-lookup"><span data-stu-id="0f17b-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="0f17b-196">Por que preciso quando houver toospecify Olá URI absoluto para um certificado usando a propriedade de certificateUrl Olá o valor de sourceVault Olá?</span><span class="sxs-lookup"><span data-stu-id="0f17b-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="0f17b-197">Uma referência de certificado do Windows Remote Management (WinRM) deve estar presente no hello propriedade segredos de saudação do perfil de SO.</span><span class="sxs-lookup"><span data-stu-id="0f17b-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="0f17b-198">Olá finalidade indicando o Cofre de origem Olá é políticas (ACL) da lista de controle de acesso de tooenforce que existem no modelo de serviço de nuvem do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="0f17b-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="0f17b-199">Se o Cofre de origem Olá não for especificado, os usuários que não têm permissões toodeploy ou acesso segredos tooa Cofre de chaves seria capaz de toothrough um provedor de recursos de computação (CRP).</span><span class="sxs-lookup"><span data-stu-id="0f17b-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="0f17b-200">As ACLs existem até para os recursos que não existem.</span><span class="sxs-lookup"><span data-stu-id="0f17b-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="0f17b-201">Se você fornecer uma ID de Cofre de origem incorreto mas uma URL de Cofre de chave válido, um erro é relatado quando você sondar a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="0f17b-202">Se adicionar tooan segredos existente conjunto de escalas da máquina virtual, são segredos Olá injetados em VMs existentes, ou apenas no novos?</span><span class="sxs-lookup"><span data-stu-id="0f17b-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="0f17b-203">Os certificados são adicionados tooall suas VMs, preexistente até mesmo aquelas.</span><span class="sxs-lookup"><span data-stu-id="0f17b-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="0f17b-204">Se a escala de máquina virtual definir propriedade de upgradePolicy está definido muito**manual**, certificado de saudação é adicionado toohello VM quando você executar uma atualização manual em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0f17b-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="0f17b-205">Onde coloco os certificados para as VMs do Linux?</span><span class="sxs-lookup"><span data-stu-id="0f17b-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="0f17b-206">toolearn como toodeploy certificados para VMs do Linux, consulte [implantar certificados tooVMs de um cofre de chaves gerenciados pelo cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="0f17b-207">Como adicionar um novo cofre certificado tooa novo objeto de certificado?</span><span class="sxs-lookup"><span data-stu-id="0f17b-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="0f17b-208">tooadd um cofre tooan existente segredo de certificado, consulte Olá PowerShell de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0f17b-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="0f17b-209">Use apenas um objeto de segredo.</span><span class="sxs-lookup"><span data-stu-id="0f17b-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="0f17b-210">Se você recriar a imagem de uma máquina virtual, o que acontece toocertificates?</span><span class="sxs-lookup"><span data-stu-id="0f17b-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="0f17b-211">Se você recriar a imagem de uma VM, os certificados serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="0f17b-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="0f17b-212">Refazer a imagem de disco do sistema operacional exclusões Olá todo.</span><span class="sxs-lookup"><span data-stu-id="0f17b-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="0f17b-213">O que acontece se você excluir um certificado de chave de cofre Olá?</span><span class="sxs-lookup"><span data-stu-id="0f17b-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="0f17b-214">Se segredo Olá é excluído do Cofre de chaves Olá, e, em seguida, executar `stop deallocate` para todas as suas VMs e, em seguida, iniciá-los novamente, você encontrará uma falha.</span><span class="sxs-lookup"><span data-stu-id="0f17b-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="0f17b-215">Falha de saudação ocorre porque Olá CRP precisa tooretrieve segredos de saudação do Cofre de chave hello, mas ele não pode.</span><span class="sxs-lookup"><span data-stu-id="0f17b-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="0f17b-216">Nesse cenário, você pode excluir certificados de saudação do modelo de conjunto de escala de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="0f17b-217">componente de CRP Olá não mantém os segredos de cliente.</span><span class="sxs-lookup"><span data-stu-id="0f17b-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="0f17b-218">Se você executar `stop deallocate` para todas as VMs no conjunto de escalas da máquina virtual hello, Olá será excluído.</span><span class="sxs-lookup"><span data-stu-id="0f17b-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="0f17b-219">Nesse cenário, os segredos são recuperados do Cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="0f17b-220">Você não encontrar esse problema ao expandir porque há uma cópia armazenada em cache de segredo Olá no Azure Service Fabric (no modelo de malha de único locatário Olá).</span><span class="sxs-lookup"><span data-stu-id="0f17b-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="0f17b-221">Por que tenho local exato do toospecify Olá Olá URL de certificado (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), conforme indicado na [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="0f17b-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="0f17b-222">Olá documentação do Cofre de chaves do Azure informa que Olá que obter API de REST do segredo deve retornar a versão mais recente de saudação do segredo Olá se Olá versão não for especificada.</span><span class="sxs-lookup"><span data-stu-id="0f17b-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="0f17b-223">Método</span><span class="sxs-lookup"><span data-stu-id="0f17b-223">Method</span></span> | <span data-ttu-id="0f17b-224">URL</span><span class="sxs-lookup"><span data-stu-id="0f17b-224">URL</span></span>
--- | ---
<span data-ttu-id="0f17b-225">GET</span><span class="sxs-lookup"><span data-stu-id="0f17b-225">GET</span></span> | <span data-ttu-id="0f17b-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="0f17b-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="0f17b-227">Substitua {*secret-name*} com nome hello e substituir {*versão do segredo*} com a versão de saudação do segredo Olá deseja tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="0f17b-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="0f17b-228">a versão do segredo Olá pode ser excluída.</span><span class="sxs-lookup"><span data-stu-id="0f17b-228">hello secret version might be excluded.</span></span> <span data-ttu-id="0f17b-229">Nesse caso, a versão atual do hello é recuperado.</span><span class="sxs-lookup"><span data-stu-id="0f17b-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="0f17b-230">Por que tem a versão de certificado Olá toospecify quando usar o Cofre de chaves?</span><span class="sxs-lookup"><span data-stu-id="0f17b-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="0f17b-231">finalidade Olá Olá versão Cofre de chaves requisito toospecify Olá certificado é toomake toohello usuário claro qual certificado será implantado em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="0f17b-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="0f17b-232">Se você cria uma máquina virtual e, em seguida, atualize seu segredo no cofre de chaves Olá, Olá novo certificado não é baixado tooyour VMs.</span><span class="sxs-lookup"><span data-stu-id="0f17b-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="0f17b-233">Mas suas VMs aparecem tooreference e novas VMs obtém novo segredo do hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="0f17b-234">tooavoid isso, são necessária tooreference uma versão do segredo.</span><span class="sxs-lookup"><span data-stu-id="0f17b-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-235">Minha equipe funciona com vários certificados são distribuídos toous como chaves públicas. cer.</span><span class="sxs-lookup"><span data-stu-id="0f17b-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="0f17b-236">O que é Olá abordagem para implantar o conjunto de escalas da máquina virtual de tooa esses certificados recomendada?</span><span class="sxs-lookup"><span data-stu-id="0f17b-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-237">conjunto de escala do virtual machine tooa do toodeploy. cer chaves públicas, você pode gerar um arquivo. pfx que contém somente arquivos. cer.</span><span class="sxs-lookup"><span data-stu-id="0f17b-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="0f17b-238">toodo isso, use `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="0f17b-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="0f17b-239">Por exemplo, carregar o arquivo. cer de saudação como um objeto x509Certificate2 em c# ou PowerShell e, em seguida, chame o método hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="0f17b-240">Para obter mais informações, consulte [Método X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0f17b-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="0f17b-241">Não vejo uma opção para os usuários toopass em certificados como cadeias de caracteres base64.</span><span class="sxs-lookup"><span data-stu-id="0f17b-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="0f17b-242">A maioria dos outros provedores de recursos tem essa opção.</span><span class="sxs-lookup"><span data-stu-id="0f17b-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="0f17b-243">tooemulate passando um certificado como uma cadeia de caracteres base64, você pode extrair hello mais recente URL de versão em um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f17b-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="0f17b-244">Inclua Olá propriedade JSON em seu modelo do Gerenciador de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="0f17b-245">É necessário toowrap certificados de objetos JSON em cofres chave?</span><span class="sxs-lookup"><span data-stu-id="0f17b-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="0f17b-246">Nos conjuntos de dimensionamento de máquinas virtuais, os certificados devem ser encapsulados nos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="0f17b-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="0f17b-247">Também há suporte para tipo de conteúdo de saudação application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="0f17b-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="0f17b-248">Para obter instruções sobre como usar application/x-pkcs12, consulte os [Certificados PFX no Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="0f17b-249">Atualmente não temos suporte para os arquivos .cer.</span><span class="sxs-lookup"><span data-stu-id="0f17b-249">We currently do not support .cer files.</span></span> <span data-ttu-id="0f17b-250">arquivos. cer de toouse, exportá-los em contêineres. pfx.</span><span class="sxs-lookup"><span data-stu-id="0f17b-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="0f17b-251">Conformidade</span><span class="sxs-lookup"><span data-stu-id="0f17b-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="0f17b-252">Os conjuntos de dimensionamento de máquinas virtuais são compatíveis com o PCI?</span><span class="sxs-lookup"><span data-stu-id="0f17b-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="0f17b-253">Conjuntos de escala de máquinas virtuais são uma camada de API thin sobre Olá CRP.</span><span class="sxs-lookup"><span data-stu-id="0f17b-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="0f17b-254">Ambos os componentes são parte da plataforma de computação Olá Olá árvore de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f17b-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="0f17b-255">De uma perspectiva de conformidade, conjuntos de escala de máquinas virtuais são uma parte fundamental da plataforma de computação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="0f17b-256">Eles compartilham uma equipe, ferramentas, processos, metodologia de implantação, controles de segurança, just-in-time (JIT) compilação, monitoramento, alertas e assim por diante, com CRP Olá em si.</span><span class="sxs-lookup"><span data-stu-id="0f17b-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="0f17b-257">Conjuntos de escala de máquinas virtuais são Payment Card Industry (PCI)-compatíveis porque faz parte de atestado de PCI dados segurança padrão (DSS) atual Olá Olá CRP.</span><span class="sxs-lookup"><span data-stu-id="0f17b-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="0f17b-258">Para obter mais informações, consulte [Olá Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="0f17b-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="0f17b-259">Extensões</span><span class="sxs-lookup"><span data-stu-id="0f17b-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="0f17b-260">Como excluo uma extensão do conjunto de dimensionamento de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="0f17b-261">toodelete uma escala de máquina virtual definir a extensão de saudação do uso do PowerShell exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="0f17b-262">Você pode encontrar hello extensionName valor em `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="0f17b-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="0f17b-263">Há um exemplo de modelo do conjunto de dimensionamento de máquinas virtuais que se integra com o Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="0f17b-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="0f17b-264">Para uma escala de máquina virtual do conjunto de exemplo de modelo que se integra ao Operations Management Suite, consulte o segundo exemplo hello em [implantar um cluster do Azure Service Fabric e habilitar o monitoramento usando a análise de Log](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="0f17b-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="0f17b-265">Extensões parecerem toorun em paralelo em conjuntos de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f17b-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="0f17b-266">Isso faz com que o meu toofail de extensão do script personalizado.</span><span class="sxs-lookup"><span data-stu-id="0f17b-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="0f17b-267">O que fazer toofix isso?</span><span class="sxs-lookup"><span data-stu-id="0f17b-267">What can I do toofix this?</span></span>

<span data-ttu-id="0f17b-268">toolearn sobre sequenciamento de extensão em conjuntos de escala de máquina virtual, consulte [sequenciamento de extensão em conjuntos de escala de máquina virtual do Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-269">Como redefinir senha Olá para VMs em meu conjunto de escala de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-270">senha de saudação tooreset para VMs na escala de sua máquina virtual definido, usar extensões de acesso VM.</span><span class="sxs-lookup"><span data-stu-id="0f17b-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="0f17b-271">Saudação de uso do PowerShell exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-271">Use hello following PowerShell example:</span></span>

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-272">Como adicionar uma extensão tooall VMs em meu conjunto de escala de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-273">Se a política de atualização for definida muito**automáticas**, reimplantação modelo Olá com novas propriedades de extensão Olá atualiza todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0f17b-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="0f17b-274">Se a política de atualização for definida muito**manual**, primeiro atualize a extensão hello e, em seguida, atualizar manualmente todas as instâncias em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="0f17b-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="0f17b-275">Se as extensões de saudação associadas a um conjunto de escala de máquina virtual existente forem atualizadas, existentes VMs afetadas?</span><span class="sxs-lookup"><span data-stu-id="0f17b-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="0f17b-276">(Ou seja, será Olá VMs *não* modelo de conjunto de escala de máquina virtual do correspondência Olá?) Ou serão ignoradas?</span><span class="sxs-lookup"><span data-stu-id="0f17b-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="0f17b-277">Quando uma máquina existente é recuperado de serviço ou imagem refeita, Olá scripts que estão configuradas atualmente no conjunto de escalas da máquina virtual Olá executado ou são scripts de saudação que foram configurados quando usado Olá que VM foi criada pela primeira vez?</span><span class="sxs-lookup"><span data-stu-id="0f17b-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="0f17b-278">Se a definição de extensão Olá na escala de máquinas virtuais Olá definido modelo é atualizado e Olá upgradePolicy está definida muito**automático**, ele atualiza Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="0f17b-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="0f17b-279">Se Olá upgradePolicy está definida muito**manual**, extensões são sinalizadas como não coincide com o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="0f17b-280">Se uma VM existente é recuperado de serviço, ele aparecerá como uma reinicialização e extensões de saudação não são novamente.</span><span class="sxs-lookup"><span data-stu-id="0f17b-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="0f17b-281">Se ela é criada, é como substituição de unidade Olá SO com a imagem de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="0f17b-282">Qualquer especialização de modelo mais recente hello, como extensões, são executados.</span><span class="sxs-lookup"><span data-stu-id="0f17b-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="0f17b-283">Como faço para ingressar em um domínio de tooan AD do Azure do conjunto de escala máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="0f17b-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="0f17b-284">toojoin um máquina virtual escala conjunto tooan Azure Active Directory (AD do Azure) domínio, você pode definir uma extensão.</span><span class="sxs-lookup"><span data-stu-id="0f17b-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="0f17b-285">toodefine uma extensão, use a propriedade de JsonADDomainExtension de saudação:</span><span class="sxs-lookup"><span data-stu-id="0f17b-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="0f17b-286">Extensão de conjunto de escala minha máquina virtual está tentando tooinstall algo que requer uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="0f17b-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="0f17b-287">Por exemplo, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="0f17b-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="0f17b-288">Se sua extensão de conjunto de escala de máquina virtual está tentando tooinstall algo que requer uma reinicialização, você pode usar a extensão do hello Azure Automation configuração do estado desejado (DSC de automação).</span><span class="sxs-lookup"><span data-stu-id="0f17b-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="0f17b-289">Se o sistema operacional de saudação for Windows Server 2012 R2, o Azure extrai na instalação do Windows Management Framework (WMF) 5.0 hello, reinicializações e, em seguida, continua com a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-290">Como ativo o antimalware em meu conjunto de dimensionamento de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-291">tooturn em antimalware em sua escala de máquina virtual definido, use Olá PowerShell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

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

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="0f17b-292">Preciso de tooexecute um script personalizado que é hospedado em uma conta de armazenamento privado.</span><span class="sxs-lookup"><span data-stu-id="0f17b-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="0f17b-293">Olá script é executado com êxito ao armazenamento de saudação é público, mas quando tento toouse uma assinatura de acesso compartilhado (SAS), ele falhará.</span><span class="sxs-lookup"><span data-stu-id="0f17b-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="0f17b-294">Esta mensagem é exibida: "Parâmetros obrigatórios ausentes para uma Assinatura de Acesso Compartilhado válida".</span><span class="sxs-lookup"><span data-stu-id="0f17b-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="0f17b-295">O link+SAS funcionam bem em meu navegador local.</span><span class="sxs-lookup"><span data-stu-id="0f17b-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="0f17b-296">tooexecute um script personalizado que é hospedado em uma conta de armazenamento privado, defina as configurações protegidas com chave de conta de armazenamento hello e nome.</span><span class="sxs-lookup"><span data-stu-id="0f17b-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="0f17b-297">Para obter mais informações, consulte [Extensão de Script Personalizado para o Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="0f17b-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="0f17b-298">Rede</span><span class="sxs-lookup"><span data-stu-id="0f17b-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="0f17b-299">É possível tooassign definida em uma escala de tooa do grupo de segurança de rede (NSG), para que ele aplicará tooall Olá NICs de VM no conjunto de Olá?</span><span class="sxs-lookup"><span data-stu-id="0f17b-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="0f17b-300">Sim.</span><span class="sxs-lookup"><span data-stu-id="0f17b-300">Yes.</span></span> <span data-ttu-id="0f17b-301">Um grupo de segurança de rede podem ser aplicado diretamente o conjunto de escala de tooa fazendo referência a ele na seção de networkInterfaceConfigurations Olá Olá de perfil de rede.</span><span class="sxs-lookup"><span data-stu-id="0f17b-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="0f17b-302">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0f17b-302">Example:</span></span>

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="0f17b-303">Como fazer uma permuta de VIP para conjuntos de escala de máquinas virtuais em Olá mesma assinatura e região mesmo?</span><span class="sxs-lookup"><span data-stu-id="0f17b-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="0f17b-304">Se você tiver duas VMs conjuntos de escala de máquina com o balanceador de carga do Azure front-ends e estão em Olá a mesma assinatura e região, você poderia desalocar os endereços IP públicos saudação de cada um deles e atribuir toohello outros.</span><span class="sxs-lookup"><span data-stu-id="0f17b-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="0f17b-305">Consulte [Permuta de VIP: implantação azul-verde no Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) para ver um exemplo.</span><span class="sxs-lookup"><span data-stu-id="0f17b-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="0f17b-306">Isso implica um atraso, embora como Olá recursos são alocados/desalocado no nível de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="0f17b-307">Uma opção mais rápida é toouse Azure Application Gateway com dois pools de back-end e uma regra de roteamento.</span><span class="sxs-lookup"><span data-stu-id="0f17b-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="0f17b-308">Como alternativa, você pode hospedar o aplicativo no [serviço de Aplicativo do Azure](https://azure.microsoft.com/en-us/services/app-service/), que fornece suporte para a alternância rápida entre slots de preparo e de produção.</span><span class="sxs-lookup"><span data-stu-id="0f17b-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="0f17b-309">Como posso especificar um intervalo de toouse de endereços IP privado para alocação de endereço IP privada estática?</span><span class="sxs-lookup"><span data-stu-id="0f17b-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="0f17b-310">Os endereços IPs são selecionados em uma sub-rede que você especifica.</span><span class="sxs-lookup"><span data-stu-id="0f17b-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="0f17b-311">método de alocação de saudação de endereços IP de conjunto de escala de máquina virtual é sempre "dinâmico", mas isso não significa que esses endereços IP podem alterar.</span><span class="sxs-lookup"><span data-stu-id="0f17b-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="0f17b-312">Nesse caso, "dinâmico" significa apenas que você não especificar o endereço IP de saudação em uma solicitação PUT.</span><span class="sxs-lookup"><span data-stu-id="0f17b-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="0f17b-313">Especifique definido por meio de sub-rede Olá Olá estático.</span><span class="sxs-lookup"><span data-stu-id="0f17b-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="0f17b-314">Como posso implantar uma máquina virtual escala conjunto tooan existente rede virtual do Azure?</span><span class="sxs-lookup"><span data-stu-id="0f17b-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="0f17b-315">toodeploy uma escala de máquina virtual definir tooan existente da rede virtual do Azure, consulte [implantar uma máquina virtual escala conjunto tooan rede virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="0f17b-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="0f17b-316">Como adicionar endereço IP de saudação do hello primeira VM em uma escala de máquina virtual definido toohello saída de um modelo?</span><span class="sxs-lookup"><span data-stu-id="0f17b-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="0f17b-317">endereço IP de saudação tooadd de saudação primeira VM em uma saída de toohello do conjunto de escala máquina virtual de um modelo, consulte [ARM: IPs privados do VMSS obter](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="0f17b-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="0f17b-318">Posso usar conjuntos de escala com Rede Acelerada?</span><span class="sxs-lookup"><span data-stu-id="0f17b-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="0f17b-319">Sim.</span><span class="sxs-lookup"><span data-stu-id="0f17b-319">Yes.</span></span> <span data-ttu-id="0f17b-320">toouse acelerado por rede, defina enableAcceleratedNetworking tootrue na sua escala do conjunto de networkInterfaceConfigurations.</span><span class="sxs-lookup"><span data-stu-id="0f17b-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="0f17b-321">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="0f17b-321">E.g.</span></span>
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="0f17b-322">Como posso configurar servidores DNS Olá usados por um conjunto de escala?</span><span class="sxs-lookup"><span data-stu-id="0f17b-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="0f17b-323">toocreate uma escala VM definida com uma configuração personalizada do DNS, adicione que uma escala de toohello dnsSettings JSON pacote definido networkInterfaceConfigurations seção.</span><span class="sxs-lookup"><span data-stu-id="0f17b-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="0f17b-324">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0f17b-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="0f17b-325">Como configurar um conjunto de escala tooassign um tooeach de endereço IP público VM?</span><span class="sxs-lookup"><span data-stu-id="0f17b-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="0f17b-326">toocreate conjunto de uma escala VM que atribui um tooeach de endereço IP público VM, certifique-se de saudação API versão Olá Microsoft.Compute/virtualMAchineScaleSets recurso está 2017-03-30 e adicionar um _publicipaddressconfiguration_ pacote JSON o conjunto de escala de toohello ipConfigurations seção.</span><span class="sxs-lookup"><span data-stu-id="0f17b-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="0f17b-327">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0f17b-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="0f17b-328">Pode configurar um toowork de conjunto de escala com vários Gateways de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="0f17b-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="0f17b-329">Sim.</span><span class="sxs-lookup"><span data-stu-id="0f17b-329">Yes.</span></span> <span data-ttu-id="0f17b-330">Você pode adicionar Olá id de recurso para vários endereços de back-end de Application Gateway toohello pools _applicationGatewayBackendAddressPools_ lista Olá _ipConfigurations_ seção de seu conjunto de escala perfil de rede.</span><span class="sxs-lookup"><span data-stu-id="0f17b-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="0f17b-331">Escala</span><span class="sxs-lookup"><span data-stu-id="0f17b-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="0f17b-332">No qual situação eu criaria um conjunto de dimensionamento de máquinas virtuais com menos de duas VMs?</span><span class="sxs-lookup"><span data-stu-id="0f17b-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="0f17b-333">Um motivo toocreate uma escala de máquina virtual definido com menos de duas VMs seriam definidas toouse Olá Elástico propriedades uma escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f17b-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="0f17b-334">Por exemplo, você pode implantar um conjunto de escala de máquinas virtuais com zero toodefine VMs sua infraestrutura sem pagar VM que executa os custos.</span><span class="sxs-lookup"><span data-stu-id="0f17b-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="0f17b-335">Em seguida, quando você estiver pronto toodeploy VMs, aumente hello "capacidade" da escala de máquina virtual Olá conjunto toohello produção instância contagem.</span><span class="sxs-lookup"><span data-stu-id="0f17b-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="0f17b-336">Outro motivo para criar um conjunto de dimensionamento de máquinas virtuais com menos de duas VMs é se você estiver menos preocupado com disponibilidade do que com o uso de um conjunto de disponibilidade com VMs separadas.</span><span class="sxs-lookup"><span data-stu-id="0f17b-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="0f17b-337">Conjuntos de escala de máquinas virtuais oferecem um toowork de maneira com as unidades de computação não-diferenciado fungível.</span><span class="sxs-lookup"><span data-stu-id="0f17b-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="0f17b-338">Essa uniformidade é um diferencial importante para os conjuntos de dimensionamento de máquinas virtuais versus os conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0f17b-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="0f17b-339">Muitas cargas de trabalho sem estado não controlam as unidades individuais.</span><span class="sxs-lookup"><span data-stu-id="0f17b-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="0f17b-340">Se a carga de trabalho Olá cair, reduzir a unidade de computação tooone e cresçam toomany quando a carga de trabalho Olá aumenta.</span><span class="sxs-lookup"><span data-stu-id="0f17b-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-341">Como alterar o número de saudação de VMs em um conjunto de escala de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-342">número de saudação toochange de VMs em um conjunto de escala de máquina virtual, consulte [altere Olá contagem de instância de um conjunto de escala de máquina virtual](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="0f17b-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="0f17b-343">Como defino alertas personalizados para quando determinados limites são atingidos?</span><span class="sxs-lookup"><span data-stu-id="0f17b-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="0f17b-344">Há alguma flexibilidade em como lidar com os alertas para os limites especificados.</span><span class="sxs-lookup"><span data-stu-id="0f17b-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="0f17b-345">Por exemplo, você pode definir webhooks personalizados.</span><span class="sxs-lookup"><span data-stu-id="0f17b-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="0f17b-346">Olá webhook exemplo a seguir é de um modelo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="0f17b-346">hello following webhook example is from a Resource Manager template:</span></span>

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

<span data-ttu-id="0f17b-347">Neste exemplo, um alerta vai tooPagerduty.com quando um limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="0f17b-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="0f17b-348">Aplicação de patch e operações</span><span class="sxs-lookup"><span data-stu-id="0f17b-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="0f17b-349">Como fazer para criar um conjunto de dimensionamento em um grupo de recursos existente?</span><span class="sxs-lookup"><span data-stu-id="0f17b-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="0f17b-350">Criando conjuntos de escala em um recurso existente grupo ainda não é possível Olá portal do Azure, mas você pode especificar um grupo de recursos existente quando a implantação de uma escala definido de um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f17b-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="0f17b-351">Também é possível especificar um grupo de recursos existente ao criar um conjunto de dimensionamento usando o Azure PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="0f17b-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="0f17b-352">Pode mover que uma escala de definir o grupo de recursos de tooanother?</span><span class="sxs-lookup"><span data-stu-id="0f17b-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="0f17b-353">Sim, você pode mover escala conjunto de recursos tooa nova assinatura ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f17b-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="0f17b-354">Como atualizar tooI minha escala de máquina virtual defina tooa nova imagem?</span><span class="sxs-lookup"><span data-stu-id="0f17b-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="0f17b-355">Como gerencio os patches?</span><span class="sxs-lookup"><span data-stu-id="0f17b-355">How do I manage patching?</span></span>

<span data-ttu-id="0f17b-356">tooupdate sua escala de máquina virtual definido tooa nova imagem e toomanage a aplicação de patch, consulte [atualizar um conjunto de escala de máquinas virtuais](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="0f17b-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="0f17b-357">Pode usar tooreset de operação de recriação de imagem Olá uma VM sem alterar a imagem de Olá?</span><span class="sxs-lookup"><span data-stu-id="0f17b-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="0f17b-358">(Ou seja, deseja redefinir uma VM toofactory configurações em vez de tooa nova imagem.)</span><span class="sxs-lookup"><span data-stu-id="0f17b-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="0f17b-359">Sim, você pode usar tooreset de operação de recriação de imagem Olá uma VM sem alterar a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="0f17b-360">No entanto, se a escala de máquina virtual definido faz referência a uma imagem de plataforma com `version = latest`, sua VM pode atualizar tooa imagem de sistema operacional posterior ao chamar `reimage`.</span><span class="sxs-lookup"><span data-stu-id="0f17b-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="0f17b-361">Para obter mais informações, consulte [Gerenciar todas as VMs em um conjunto de dimensionamento de máquinas virtuais](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="0f17b-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="0f17b-362">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="0f17b-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="0f17b-363">Como ativo o diagnóstico de inicialização?</span><span class="sxs-lookup"><span data-stu-id="0f17b-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="0f17b-364">tooturn no diagnóstico de inicialização, primeiro, crie uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f17b-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="0f17b-365">Em seguida, colocar esse bloco JSON em seu conjunto de escala de máquinas virtuais **virtualMachineProfile**e atualizar o conjunto de escalas da máquina virtual hello:</span><span class="sxs-lookup"><span data-stu-id="0f17b-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="0f17b-366">Quando uma nova VM é criada, Olá InstanceView propriedade Olá VM mostra detalhes de saudação para captura de tela hello e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0f17b-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="0f17b-367">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="0f17b-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="0f17b-368">Propriedades de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0f17b-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-369">Como obtenho informações de propriedade para cada VM sem fazer várias chamadas?</span><span class="sxs-lookup"><span data-stu-id="0f17b-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="0f17b-370">Por exemplo, como seria obter domínio de falha de saudação do cada Olá 100 VMs em meu conjunto de escala de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-371">informações de propriedade tooget para cada VM sem fazer várias chamadas, você pode chamar `ListVMInstanceViews` fazendo uma API REST `GET` em Olá URI do recurso a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="0f17b-372">/subscriptions/<id_assinatura>/resourceGroups/<nome_grupo_recursos>/providers/Microsoft.Compute/virtualMachineScaleSets/<nome_conjunto_dimensionamento>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="0f17b-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="0f17b-373">Pode, passar argumentos de extensão diferente toodifferent VMs em um conjunto de escala de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="0f17b-374">Não, você não pode passar argumentos de extensão diferente toodifferent VMs em um conjunto de escala de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0f17b-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="0f17b-375">No entanto, as extensões podem agir com base em propriedades exclusivas de saudação do hello VM estão sendo executados em tal como em nome da máquina hello.</span><span class="sxs-lookup"><span data-stu-id="0f17b-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="0f17b-376">Extensões também podem consultar metadados de instância no http://169.254.169.254 tooget obter mais informações sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0f17b-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="0f17b-377">Por que existem lacunas entre os nomes de máquina e as IDs da VM do conjunto de dimensionamento de máquinas virtuais?</span><span class="sxs-lookup"><span data-stu-id="0f17b-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="0f17b-378">Por exemplo: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="0f17b-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="0f17b-379">Existem lacunas entre seus nomes de computador VM do conjunto de escala de máquina virtual e IDs de VM, porque o conjunto de escala de sua máquina virtual **overprovision** propriedade é definir o valor de padrão de toohello de **true**.</span><span class="sxs-lookup"><span data-stu-id="0f17b-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="0f17b-380">Se o excesso de provisionamento está definido muito**true**, mais VMs que solicitado são criados.</span><span class="sxs-lookup"><span data-stu-id="0f17b-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="0f17b-381">Então, as VMs extras são excluídas.</span><span class="sxs-lookup"><span data-stu-id="0f17b-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="0f17b-382">Nesse caso, você obter implantação maior confiabilidade, mas à custa de saudação de contígua de nomenclatura e contíguos conversão de endereço de rede (NAT) de regras.</span><span class="sxs-lookup"><span data-stu-id="0f17b-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="0f17b-383">Você pode definir essa propriedade muito**false**.</span><span class="sxs-lookup"><span data-stu-id="0f17b-383">You can set this property too**false**.</span></span> <span data-ttu-id="0f17b-384">Para os conjuntos de dimensionamento de máquinas virtuais pequenos, isso não afeta muito a confiabilidade da implantação.</span><span class="sxs-lookup"><span data-stu-id="0f17b-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="0f17b-385">Qual é a diferença Olá entre a exclusão de uma VM em um conjunto de escala de máquinas virtuais e desalocando Olá VM?</span><span class="sxs-lookup"><span data-stu-id="0f17b-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="0f17b-386">Quando devo escolher um em detrimento de outros Olá?</span><span class="sxs-lookup"><span data-stu-id="0f17b-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="0f17b-387">Olá principal diferença entre a exclusão de uma VM em um conjunto de escala de máquinas virtuais e desalocando Olá VM é que `deallocate` não exclui Olá discos de rígidos virtuais (VHDs).</span><span class="sxs-lookup"><span data-stu-id="0f17b-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="0f17b-388">Existem custos de armazenamento associados à execução de `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="0f17b-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="0f17b-389">Você pode usar um ou Olá outros para uma saudação motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f17b-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="0f17b-390">Você deseja toostop pagar custos de computação, mas deseja que o estado do disco Olá tookeep de saudação VMs.</span><span class="sxs-lookup"><span data-stu-id="0f17b-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="0f17b-391">Você deseja toostart um conjunto de VMs mais rapidamente do que você pode expandir um conjunto de escala de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0f17b-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="0f17b-392">Cenário de toothis relacionados, você pode ter criado seu próprio mecanismo de dimensionamento automático e quiser uma escala de ponta a ponta mais rápida.</span><span class="sxs-lookup"><span data-stu-id="0f17b-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="0f17b-393">Você tem um conjunto de dimensionamento de máquinas virtuais distribuído sem uniformidade entre os domínios de falha ou os domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="0f17b-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="0f17b-394">Isso pode ser porque você excluiu seletivamente as VMs ou porque as VMs foram excluídas depois do excesso de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0f17b-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="0f17b-395">Executando `stop deallocate` seguido `start` na máquina virtual de saudação escala definida uniformemente distribui Olá VMs em domínios de falha ou domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="0f17b-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

