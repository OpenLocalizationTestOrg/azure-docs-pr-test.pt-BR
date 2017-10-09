Olá 2.0 do CLI do Azure permite que você toocreate e gerenciar seus recursos do Azure no Windows, Linux e macOS. Este artigo detalha algumas Olá toocreate de comandos mais comuns e gerenciar máquinas virtuais (VMs).

Este artigo requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli). Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Comandos básicos do Azure Resource Manager na CLI do Azure
Para obter mais ajuda com as opções e opções de linha de comando específico, você pode usar ajuda de comando online hello e opções digitando `az <command> <subcommand> --help`.

### <a name="create-vms"></a>Criar VMs
| Tarefa | Comandos da CLI do Azure |
| --- | --- |
| Criar um grupo de recursos | `az group create --name myResourceGroup --location eastus` |
| Criar uma VM do Linux | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| Criar uma VM do Windows | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a>Gerenciar o estado da VM
| Tarefa | Comandos da CLI do Azure |
| --- | --- |
| Iniciar uma VM | `az vm start --resource-group myResourceGroup --name myVM` |
| Parar uma VM | `az vm stop --resource-group myResourceGroup --name myVM` |
| Desalocar uma VM | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| Reiniciar uma VM | `az vm restart --resource-group myResourceGroup --name myVM` |
| Reimplantar uma VM | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| Excluir uma VM | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a>Obter informações sobre a VM
| Tarefa | Comandos da CLI do Azure |
| --- | --- |
| Listar VMs | `az vm list` |
| Obter informações sobre uma VM | `az vm show --resource-group myResourceGroup --name myVM` |
| Conferir o uso dos recursos de VM | `az vm list-usage --location eastus` |
| Conferir todos os tamanhos de VM disponíveis | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a>Discos e imagens
| Tarefa | Comandos da CLI do Azure |
| --- | --- |
| Adicionar um disco de dados tooa VM | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| Remover um disco de dados de uma VM | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| Redimensionar um disco | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| Instantâneo de um disco | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| Criar imagem de uma VM | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| Criar uma VM com base em uma imagem | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a>Próximas etapas
Para obter exemplos adicionais de comandos CLI hello, consulte Olá [criar e gerenciar máquinas virtuais Linux com hello CLI do Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.

