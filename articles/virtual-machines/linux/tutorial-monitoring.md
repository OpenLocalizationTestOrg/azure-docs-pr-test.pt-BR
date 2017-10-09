---
title: "máquinas virtuais do aaaMonitor Linux no Azure | Microsoft Docs"
description: "Saiba como toomonitor de inicialização de diagnóstico e métricas de desempenho em uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Como toomonitor uma máquina virtual do Linux no Azure

tooensure que suas máquinas virtuais (VMs) no Azure estão sendo executados corretamente, você pode examinar o diagnóstico de inicialização e métricas de desempenho. Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Habilitar o diagnóstico de inicialização em Olá VM
> * Exibir diagnóstico de inicialização
> * Exibir métricas de host
> * Habilitar a extensão de diagnóstico em Olá VM
> * Exibir métricas de VM
> * Criar alertas com base nas métricas de diagnóstico
> * Configurar monitoramento avançado


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>Criar VM

toosee diagnósticos e métricas em ação, você precisa de uma VM. Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupMonitor* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Agora, crie uma VM com [az vm create](https://docs.microsoft.com/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Habilitar o diagnóstico de inicialização

Como inicializar as VMs do Linux, extensão de diagnóstico de inicialização de saudação captura a saída de inicialização e os armazena no armazenamento do Azure. Esses dados podem ser usados tootroubleshoot problemas de inicialização VM. O diagnóstico de inicialização não é habilitado automaticamente quando você criar uma VM do Linux usando Olá CLI do Azure.

Antes de habilitar o diagnóstico de inicialização, uma conta de armazenamento precisa toobe criado para armazenar logs de inicialização. As contas de armazenamento devem ter um nome exclusivo globalmente, com três a 24 caracteres e conter apenas números e letras minúsculas. Criar uma conta de armazenamento com hello [criar conta de armazenamento az](/cli/azure/storage/account#create) comando. Neste exemplo, uma cadeia de caracteres aleatória é toocreate usado um nome de conta de armazenamento exclusivo. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Ao habilitar o diagnóstico de inicialização, o contêiner de armazenamento de blob do hello URI toohello é necessária. Olá consultas a seguir comando Olá tooreturn da conta de armazenamento esse URI. Olá valor URI é armazenado em uma variável nomes *bloburi*, que é usada na próxima etapa do hello.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Agora, habilite o diagnóstico de inicialização com [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Olá `--storage` valor é blob Olá URI coletado na etapa anterior hello.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Exibir diagnóstico de inicialização

Quando o diagnóstico de inicialização está habilitado, cada vez que você parar e iniciar Olá VM, o processo de inicialização hello serão gravadas informações sobre tooa arquivo de log. Neste exemplo, primeiro desalocar Olá VM com hello [az vm desalocar](/cli/azure/vm#deallocate) comando da seguinte maneira:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Iniciar agora Olá VM com hello [início de vm az]( /cli/azure/vm#stop) comando da seguinte maneira:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Você pode obter dados de diagnóstico de inicialização Olá para *myVM* com hello [az vm diagnóstico de inicialização get-inicialização-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comando da seguinte maneira:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Exibir métricas de host

Uma VM do Linux tem um host dedicado no Azure com o qual ela interage. Métricas são automaticamente coletadas para o host de saudação e podem ser exibidas no portal do Azure de saudação da seguinte maneira:

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroupMonitor**e, em seguida, selecione **myVM** na lista de recursos de saudação.
1. toosee como VM do host hello está sendo executado, clique em **métricas** na folha VM hello, em seguida, selecione qualquer uma das Olá *[Host]* métricas em **métricas disponíveis**.

    ![Exibir métricas de host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Instalar extensão de diagnóstico

> [!IMPORTANT]
> Este documento descreve a versão 2.3 Olá extensão de diagnóstico do Linux, que foi preterido. A versão 2.3 será suportada até 30 de junho de 2018.
>
> A versão 3.0 do hello extensão de diagnóstico do Linux pode ser habilitada em vez disso. Para obter mais informações, consulte [Olá documentação](./diagnostic-extension.md).

métricas de host básica Olá estão disponíveis, mas toosee mais granular e métricas de VM específico, você tooneed tooinstall Olá diagnóstico do Azure extensão no hello VM. Olá extensão de diagnóstico do Azure permite o monitoramento adicional e toobe de dados de diagnóstico recuperados da saudação VM. Você pode exibir essas métricas de desempenho e criar alertas com base em como Olá VM executa. extensão de diagnóstico Olá é instalado por meio de saudação portal do Azure da seguinte maneira:

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
1. Clique em **Configurações de diagnóstico**. lista de saudação mostra que *diagnósticos de inicialização* já estão habilitados na seção anterior hello. Clique em caixa de seleção Olá *métricas básicas*.
1. Em Olá *conta de armazenamento* seção, procurar Olá selecione tooand *mydiagdata [1234]* conta criada na seção anterior hello.
1. Clique em Olá **salvar** botão.

    ![Exibir métricas de diagnóstico](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Exibir métricas de VM

Você pode exibir as métricas VM Olá no hello mesma maneira que você exibiu métricas VM do host hello:

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
1. toosee como Olá VM for executada, clique em **métricas** Olá folha de VM e, em seguida, selecione qualquer uma das métricas de diagnóstico de saudação em **métricas disponíveis**.

    ![Exibir métricas de VM](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Criar alertas

Você pode criar alertas com base em métricas de desempenho específicas. Alertas podem ser usado toonotify quando uso médio da CPU excede um determinado limite ou espaço em disco livre disponível cai abaixo de um determinado valor, por exemplo. Alertas são exibidos no portal do Azure de saudação ou podem ser enviados por email. Você também pode disparar runbooks de automação do Azure ou aplicativos do Azure lógica tooalerts de resposta que está sendo gerado.

Olá, exemplo a seguir cria um alerta para o uso médio da CPU.

1. No portal do Azure de Olá, clique em **grupos de recursos**, selecione **myResourceGroup**e, em seguida, selecione **myVM** na lista de recursos de saudação.
2. Clique em **regras de alerta** na folha VM hello, em seguida, clique em **adicionar alerta métrica** na parte superior de saudação da folha de alertas de saudação.
4. Forneça um **Nome** para o alerta, como *myAlertRule*
5. tootrigger um alerta quando a porcentagem de CPU exceder 1.0 por cinco minutos, deixe Olá todos os outros padrões selecionados.
6. Opcionalmente, marque a caixa da saudação *proprietários, Contribuidores e leitores de Email* toosend notificação por email. ação de padrão de saudação é toopresent uma notificação no portal de saudação.
7. Clique em Olá **Okey** botão.


## <a name="advanced-monitoring"></a>Monitoramento avançado 

Você pode fazer um monitoramento mais avançado da sua VM usando o [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Caso ainda não tenha feito isso, você pode se inscrever para uma [avaliação gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) do Operations Management Suite.

Quando você tiver acesso toohello OMS portal, você pode encontrar o identificador de chave e o espaço de trabalho do espaço de trabalho Olá na folha de configurações de saudação. Substitua < chave do espaço de trabalho > e < id do espaço de trabalho > com valores de saudação para do seu OMS espaço de trabalho e, em seguida, você pode usar **conjunto de extensão de vm az** tooadd Olá OMS extensão toohello VM:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

Na folha de pesquisa de Log de saudação do portal do OMS hello, você deve ver *myVM* como o mostrado na figura abaixo de saudação:

![Folha do OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você configurou e revisou VMs com a Central de Segurança do Azure. Você aprendeu como:

> [!div class="checklist"]
> * Habilitar o diagnóstico de inicialização em Olá VM
> * Exibir diagnóstico de inicialização
> * Exibir métricas de host
> * Habilitar a extensão de diagnóstico em Olá VM
> * Exibir métricas de VM
> * Criar alertas com base nas métricas de diagnóstico
> * Configurar monitoramento avançado

Avançar toohello toolearn próximo de tutorial sobre o Centro de segurança do Azure.

> [!div class="nextstepaction"]
> [Gerenciar a segurança da VM](./tutorial-azure-security.md)