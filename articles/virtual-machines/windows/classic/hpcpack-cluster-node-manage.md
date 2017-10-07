---
title: "nós de computação de cluster de HPC Pack aaaManage | Microsoft Docs"
description: "Saiba mais sobre tooadd de ferramentas de script do PowerShell, remover, iniciar e parar nós de computação de cluster de HPC Pack 2012 R2 no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Gerenciar o número de saudação e a disponibilidade de nós de computação em um cluster de HPC Pack no Azure
Se você criou um cluster de HPC Pack 2012 R2 em VMs do Azure, convém maneiras tooeasily adicionar, remover, iniciar (provisionar) ou pare (desprovisione) algumas VMs do nó do cluster de computação. toodo essas tarefas, executar scripts do PowerShell do Azure que são instalados na VM do nó principal hello. Esses scripts ajudam a controlar o número de saudação e a disponibilidade de seus recursos de cluster de HPC Pack para que você pode controlar os custos.

> [!IMPORTANT] 
> Este artigo se aplica apenas tooHPC os clusters Pack 2012 R2 no Azure criados usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.
> Além disso, os scripts do PowerShell Olá descritos neste artigo não estão disponíveis no HPC Pack 2016.

## <a name="prerequisites"></a>Pré-requisitos
* **Cluster de HPC Pack 2012 R2 em VMs do Azure**: criar um cluster de HPC Pack 2012 R2 no modelo de implantação clássico hello. Por exemplo, você pode automatizar a implantação de saudação usando a imagem de VM do HPC Pack 2012 R2 Olá no hello Azure Marketplace e um script do PowerShell do Azure. Para obter informações e pré-requisitos, consulte [criar um Cluster de HPC com hello script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md).
  
    Após a implantação, localize Olá scripts de gerenciamento do nó em Olá % CCP\_pasta inicial % bin no nó de cabeçalho hello. Execute cada um dos scripts hello como um administrador.
* **Certificado de arquivo ou o gerenciamento de configurações de publicação no Azure**: necessário toodo Olá seguinte no nó de cabeçalho hello:
  
  * **Saudação de importação do Azure publica o arquivo de configurações**. toodo, Olá executar cmdlets do Azure PowerShell a seguir no nó de cabeçalho de saudação:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Configurar o certificado de gerenciamento do Azure Olá no nó de cabeçalho Olá**. Se você tiver um arquivo. cer de hello, importe-Olá de certificados currentuser\my e execute Olá cmdlet do PowerShell do Azure para seu ambiente do Azure (AzureCloud ou AzureChinaCloud) a seguir:
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Adicionar VMs de nó de computação
Adicionar nós de computação com hello **Add-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintaxe
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>parâmetros
* **ServiceName**: nome do serviço de nuvem Olá novas VMs do nó de computação são adicionados ao.
* **ImageName**: nome de imagem de VM do Azure, que pode ser obtido por meio de saudação portal clássico do Azure ou o cmdlet do PowerShell do Azure **Get-AzureVMImage**. imagem de Olá deve atender a saudação requisitos a seguir:
  
  1. Um sistema operacional Windows deve ser instalado.
  2. HPC Pack deve ser instalado na função de nó de computação hello.
  3. imagem de saudação deve ser uma imagem privada na categoria de usuário hello, não uma imagem de VM do Azure pública.
* **Quantidade**: número de toobe de VMs de nó de computação adicionado.
* **InstanceSize**: tamanho da saudação VMs do nó de computação.
* **DomainUserName**: nome de usuário de domínio, que é usado toojoin Olá novas VMs toohello domínio.
* **DomainUserPassword**: senha de usuário de domínio hello.
* **NodeNameSeries** (opcional): padrão de nomenclatura para Olá nós de computação. saudação de formato deve ser &lt; *raiz\_nome*&gt;&lt;*iniciar\_número*&gt;%. Por exemplo, MyCN % 10% significa uma série de saudação MyCN11 a partir de nomes de nó de computação. Se não for especificado, Olá script usa Olá configurado série de nomeação de nó no cluster HPC hello.

### <a name="example"></a>Exemplo
Olá exemplo a seguir adiciona nós de computação grandes tamanho 20 VMs no serviço de nuvem Olá *hpcservice1*, com base na imagem VM Olá *hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Remover VMs de nó de computação
Remover nós de computação com hello **remove-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintaxe
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>parâmetros
* **Nome**: nomes de toobe de nós de cluster removidos. Há suporte para caracteres curinga. nome do conjunto de parâmetro Hello é nome. Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.
* **Nó**: objeto HpcNode Olá para Olá nós toobe removido, que pode ser obtido por meio do cmdlet PowerShell HPC Olá [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nome do conjunto de parâmetro Hello é o nó. Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.
* **DeleteVHD** (opcional): configuração toodelete discos Olá associado Olá VMs que são removidos.
* **Forçar** (opcional): configuração tooforce nós HPC a ficarem offline antes de removê-los.
* **Confirmar** (opcional): solicitar confirmação antes de executar o comando hello.
* **WhatIf**: configuração toodescribe o que aconteceria se você executasse o comando Olá sem realmente executar comando de saudação.

### <a name="example"></a>Exemplo
Olá exemplo a seguir força nós offline Olá com nomes começando *HPCNode-CN -* e eles remove nós hello e os discos associados.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Iniciar VMs de nó de computação
Início de computação nós com hello **Start-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintaxe
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>parâmetros
* **Nome**: nomes de saudação toobe de nós de cluster é iniciado. Há suporte para caracteres curinga. nome do conjunto de parâmetro Hello é nome. Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.
* **Nó**-objeto HpcNode Olá para Olá nós toobe iniciado, que pode ser obtido por meio do cmdlet PowerShell HPC Olá [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nome do conjunto de parâmetro Hello é o nó. Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.

### <a name="example"></a>Exemplo
Olá exemplo a seguir inicia nós com nomes começando *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Interromper VMs de nó de computação
Parar nós de computação com hello **Stop-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintaxe
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>parâmetros
* **Nome**-nomes de saudação toobe de nós de cluster é interrompido. Há suporte para caracteres curinga. nome do conjunto de parâmetro Hello é nome. Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.
* **Nó**: objeto HpcNode Olá para Olá nós toobe interrompido, que pode ser obtido por meio do cmdlet PowerShell HPC Olá [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nome do conjunto de parâmetro Hello é o nó. Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.
* **Forçar** (opcional): configuração tooforce nós HPC a ficarem offline antes de interrompê-los.

### <a name="example"></a>Exemplo
Olá exemplo a seguir força nós offline com nomes começando *HPCNode-CN -* e, em seguida, interrompe Olá nós.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Próximas etapas
* tooautomatically aumentar ou reduzir nós de cluster de saudação de acordo com a carga de trabalho atual de trabalhos e tarefas no cluster Olá Olá, consulte [automaticamente ampliar ou reduzir os recursos de cluster de HPC Pack hello Azure acordo toohello cluster cargas de trabalho](hpcpack-cluster-node-autogrowshrink.md).

