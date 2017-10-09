## <a name="overview"></a>Visão geral
Quando você cria uma nova máquina virtual (VM) em um grupo de recursos ao implantar uma imagem de [Azure Marketplace](https://azure.microsoft.com/marketplace/), unidade de sistema operacional saudação padrão será de 127 GB. Mesmo que é possível tooadd dados discos toohello VM (dependendo de quantos dos Olá SKU que você escolheu) e Além disso é recomendado tooinstall aplicativos e cargas de trabalho intensivas nesses discos adendo da CPU, muitas vezes, os clientes precisam tooexpand Olá SO unidade toosupport determinados cenários, como a seguir:

1. Suporte a aplicativos herdados que instalam componentes na unidade do sistema operacional.
2. Migração de um PC físico ou máquina virtual local com uma unidade do sistema operacional maior.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico. Este artigo aborda usando o modelo do Gerenciador de recursos de saudação. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.
> 
> 

## <a name="resize-hello-os-drive"></a>Redimensionar a unidade Olá SO
Neste artigo é vai realizar tarefa de saudação do redimensionamento unidade Olá SO usando módulos de Gerenciador de recursos de [Azure Powershell](/powershell/azureps-cmdlets-docs). Abra o ISE do Powershell ou a janela do Powershell no modo de administrador e execute as etapas de saudação abaixo:

1. Tooyour entrar no Microsoft Azure da conta no modo de gerenciamento de recursos e selecione sua assinatura da seguinte maneira:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Defina o nome do grupo de recursos e o nome da VM como se segue:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Obter uma referência tooyour VM da seguinte maneira:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Pare Olá VM antes de redimensionar o disco de saudação da seguinte maneira:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. E aqui vai momento Olá que você estava esperando! Definir tamanho de saudação do valor do hello OS disco toohello desejado e atualizar Olá VM da seguinte maneira:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > Olá novo tamanho deve ser maior que o tamanho de disco existente hello. Olá máximo permitido é de 1023 GB.
   > 
   > 
6. Olá atualização VM pode levar alguns segundos. Depois que o comando Olá conclui a execução, reinicie Olá VM da seguinte maneira:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

É isso. Agora RDP em Olá VM, abra o gerenciamento do computador (ou o gerenciamento de disco) e expanda a unidade hello usando Olá espaço recentemente alocado.

## <a name="summary"></a>Resumo
Neste artigo, usamos o Azure Resource Manager módulos do Powershell tooexpand Olá unidade do sistema operacional de uma máquina virtual IaaS. Reproduzida abaixo é o script completo a saudação para referência:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Próximas etapas
Embora neste artigo, nos concentramos principalmente nos expandir disco Olá SO da VM de saudação, hello desenvolvido script também pode ser usado para expandir Olá dados discos anexados toohello VM alterando uma única linha de código. Por exemplo, tooexpand Olá primeiramente os dados anexado toohello VM de disco, substitua Olá ```OSDisk``` objeto do ```StorageProfile``` com ```DataDisks``` de matriz e usar um índice numérico de tooobtain um disco de dados anexados referência toofirst, conforme mostrado abaixo:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Da mesma forma, você pode fazer referência a outros dados discos anexados toohello VM, usando um índice, como mostrado acima ou Olá ```Name``` Olá disco conforme ilustrado abaixo:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Se você quiser toofind out como tooattach discos tooan VM do Azure Resource Manager, verifique isso [artigo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

