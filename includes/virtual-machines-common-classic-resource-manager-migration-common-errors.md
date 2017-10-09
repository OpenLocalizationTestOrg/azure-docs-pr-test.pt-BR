# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Erros comuns durante clássico tooAzure migração do Gerenciador de recursos
Catálogos neste artigo Olá erros mais comuns e atenuantes durante a migração de saudação de recursos de IaaS de pilha de Gerenciador de recursos do Azure de toohello de modelo de implantação clássico do Azure.

## <a name="list-of-errors"></a>Lista de erros
| Cadeia de caracteres de erro | Redução |
| --- | --- |
| Erro interno do servidor |Em alguns casos, isso é um erro transitório desaparece com uma nova tentativa. Se ele persistir toopersist, [entre em contato com o suporte do Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) necessária investigação dos logs de plataforma. <br><br> **Observação:** depois que o incidente Olá é controlado pela equipe de suporte de hello, não tente qualquer redução automática como isso pode ter consequências não intencionais no seu ambiente. |
| Não há suporte para migração para implantação {nome_da_implantação} em {nome_do_serviço_hospedado} HostedService porque é uma implantação de PaaS (Web/Trabalho). |Isso ocorre quando uma implantação contém uma função de trabalho/Web. Como só há suporte para máquinas virtuais para a migração, remova Olá web/função de trabalho de implantação de saudação e tente novamente a migração. |
| Falha na implantação do modelo {nome_do_ modelo}. CorrelationId={guid} |Olá back-end do serviço de migração, usamos recursos do Azure Resource Manager modelos toocreate na pilha do hello Azure Resource Manager. Como os modelos são idempotentes, geralmente você poderá repetir com segurança Olá tooget de operação de migração após esse erro. Se o erro continuar toopersist, [entre em contato com o suporte do Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) e conceder a eles Olá CorrelationId. <br><br> **Observação:** depois que o incidente Olá é controlado pela equipe de suporte de hello, não tente qualquer redução automática como isso pode ter consequências não intencionais no seu ambiente. |
| rede virtual de Olá {virtual-network-name} ' não existe. |Isso pode acontecer se você criou Olá rede Virtual no novo portal do Azure de saudação. nome de rede Virtual real Olá segue o padrão de hello "grupo * <VNET name>" |
| A VM {nome_da_VM} no HostedService {nome_do_serviço_hospedado} contém a Extensão {nome_da_extensão} para a qual não há suporte no Azure Resource Manager. É recomendável toouninstall do hello VM antes de continuar com a migração. |Extensões XML como a BGInfo 1. * não têm suporte no Azure Resource Manager. Portanto, essas extensões não podem ser migradas. Se essas extensões são esquerdo Olá instalado na VM, eles são automaticamente desinstalados antes de concluir a migração de saudação. |
| A VM {nome_da_VM} no serviço hospedado {nome_do_serviço_hospedado} contém a Extensão VMSnapshot/VMSnapshotLinux, que atualmente não tem suporte para Migração. Desinstale-a da saudação VM e adicioná-lo novamente usando o Gerenciador de recursos do Azure depois Olá migração é concluída |Esse é o cenário de saudação onde a máquina virtual de saudação está configurada para Backup do Azure. Como no momento, esse é um cenário sem suporte, siga solução Olá https://aka.ms/vmbackupmigration |
| VM {vm-name} no HostedService {hospedado-service-name} contém extensão {extensão-name} cujo Status não está sendo informado de saudação VM. Portanto, esta VM não pode ser migrada. Certifique-se de que Olá status da extensão está sendo relatado ou desinstalar a extensão de saudação do hello VM e tente novamente a migração. <br><br> A VM {nome_da_VM} no serviço hospedado {nome_do_serviço_hospedado} contém a Extensão {nome_da_extensão} relatando o status do manipulador: {status_do_manipulador}. Portanto, a saudação VM não pode ser migrada. Verifique se o status de manipulador de extensão hello está sendo relatado é {status manipulador} ou desinstale-a da saudação VM e tente novamente a migração. <br><br> Agente de VM de VM {vm-name} no HostedService {hospedado-service-name} está relatando Olá status geral do agente como não estando pronta. Portanto, Olá VM pode não ser migrada, se ele tem uma extensão de migrada. Certifique-se de que o agente de VM hello está relatando status geral do agente como pronto. Consulte toohttps://aka.ms/classiciaasmigrationfaqs. |O agente convidado do Azure e extensões de VM necessário saída internet acesso toohello VM armazenamento conta toopopulate seu status. Causas comuns de falha de status incluem <li> um grupo de segurança de rede que bloqueia o acesso de saída toohello internet <li> Se Olá VNET tem conectividade DNS e servidores DNS local será perdido <br><br> Se você continuar toosee um status sem suporte, é possível desinstalar Olá extensões tooskip essa verificação e continuar com a migração. |
| Não há suporte para migração para implantação {nome_da_implantação} no serviço hospedado {nome_do_serviço_hospedado} porque ele tem vários conjuntos de disponibilidade. |Atualmente, apenas os serviços hospedados com um ou nenhum conjunto de disponibilidade podem ser migrados. toowork alternativa para esse problema, mova Olá adicional conjuntos de disponibilidade e serviço hospedado de máquinas virtuais nesses conjuntos de disponibilidade tooa diferentes. |
| Não há suporte para migração para implantação {deployment-name} no HostedService {hospedado--nome do serviço porque ela contém VMs que não fazem parte do conjunto de disponibilidade de saudação embora Olá HostedService contém um. |solução alternativa de saudação para este cenário é tooeither move todas as máquinas virtuais de saudação em uma único disponibilidade definir ou remover todas as máquinas virtuais de saudação que conjunto de disponibilidade no serviço hospedado de saudação. |
| Conta de armazenamento/HostedService/Virtual rede {virtual-network-name} está no processo de saudação do que está sendo migrado e, portanto, não pode ser alterada |Esse erro ocorre quando hello "Preparação" a operação de migração foi concluída no recurso hello e uma operação que criam um recurso de toohello de alteração é disparada. Devido a bloqueio Olá no plano de gerenciamento de saudação após a operação de "Preparação", qualquer recurso de toohello alterações estão bloqueados. plano de gerenciamento de saudação toounlock, você pode executar hello "Confirmação" migração operação toocomplete migração ou hello "Cancelar" migração operação tooroll volta hello "Preparação" operação. |
| A migração não é permitida para o serviço hospedado {nome_do_serviço_hospedado} porque ele tem a VM {nome_da_vm} no estado: RoleStateUnknown. A migração é permitida apenas quando Olá VM estiver em um dos seguintes Olá estados - em execução, parado, interrompido desalocado. |Olá VM pode estar sofrendo por meio de uma transição de estado, que geralmente acontece quando durante uma operação de atualização em Olá HostedService como uma reinicialização, a instalação da extensão etc. É recomendável para Olá toocomplete de operação de atualização em Olá HostedService antes de tentar a migração. |
| Implantação {deployment-name} no HostedService {hospedado-service-name} contém uma VM {vm-name} com o disco de dados {dados-disco-name} cujo tamanho {size-of-the-vhd-blob-backing-the-data-disk} bytes de blob físico não coincide com Olá {de tamanho lógico de disco de dados da VM size-of-the-data-Disk-specified-in-the-VM-API} bytes. Migração continuará sem especificar um tamanho de disco de dados Olá para Olá VM do Azure Resource Manager. | Esse erro ocorre se o tamanho do blob do VHD Olá sem atualizar o tamanho de saudação no modelo de VM API hello. As etapas de atenuação detalhadas estão descritas [abaixo](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| Ocorreu uma exceção de armazenamento ao validar o disco de dados {nome do disco de dados} com link de mídia {Uri do disco de dados} para VM {nome da VM} no Serviço de Nuvem {nome do Serviço de Nuvem}. Verifique se que esse link de mídia Olá VHD está acessível para esta máquina virtual | Esse erro pode ocorrer se discos Olá Olá VM tenha sido excluída ou não está acessível mais. Certifique-se de que discos Olá Olá VM existe.|
| A VM {vm-name} em HostedService {cloud-service-name} contém o Disco com MediaLink {vhd-uri} que tem o nome do blob {vhd-blob-name}, que não é suportado no Azure Resource Manager. | Esse erro ocorre quando o nome de saudação do blob Olá tem um "/" no, o que não tem suporte no provedor de recursos de computação no momento. |
| Migração não é permitida para implantação no HostedService {cloud-service-name} de {deployment-name}, pois não está no escopo regional hello. Consulte toohttp://aka.ms/regionalscope para mover este escopo de tooregional de implantação. | Em 2014, o Azure anunciou que recursos de rede serão movidos de um escopo de tooregional de escopo de nível de cluster. Consulte [http://aka.ms/regionalscope] para obter mais detalhes (http://aka.ms/regionalscope). Esse erro ocorre quando a implantação de saudação que está sendo migrada não teve uma operação de atualização, que move automaticamente escopo regional tooa. Solução alternativa recomendada é tooeither adicionar um ponto de extremidade tooa VM ou dados de um disco toohello VM e, em seguida, tente novamente a migração. <br> Consulte [como tooset pontos de extremidade em uma máquina virtual do Windows clássica no Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) ou [anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico Olá](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Atenuação detalhada

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>VM com o disco de dados cujo físico bytes de tamanho de blob não corresponde bytes de tamanho lógico de disco de dados da VM hello.

Isso acontece quando hello tamanho lógico do disco de dados pode obter fora de sincronia com o tamanho de blob VHD real hello. Isso pode ser facilmente verificado usando Olá comandos a seguir:

#### <a name="verifying-hello-issue"></a>Verificando o problema de saudação

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Reduzindo o problema de saudação

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Mover uma assinatura diferente do VM tooa após a conclusão da migração

Depois de concluir o processo de migração de saudação, talvez você queira assinatura de tooanother toomove Olá VM. No entanto, se você tiver um segredo/certificado em Olá Mover VM que faz referência a um recurso de Cofre de chaves, hello não é suportado atualmente. Olá instruções abaixo permitem tooworkaround problema de saudação. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
