Antes de usar o hello CLI do Azure com o Gerenciador de recursos toodeploy comandos e modelos do Azure recursos e cargas de trabalho usando grupos de recursos, você precisará de uma conta com o Azure. Se você não tiver uma conta, você pode obter uma [avaliação gratuita do Azure aqui](https://azure.microsoft.com/pricing/free-trial/).

Se você ainda não instalou hello CLI do Azure e assinatura tooyour conectados, consulte [instalação Olá CLI do Azure](../articles/cli-install-nodejs.md) definir modo de saudação muito`arm` com `azure config mode arm`e conecte-se tooAzure com hello `azure login` comando.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- CLI do Azure 10 – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](../articles/virtual-machines/linux/cli-manage.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Comandos básicos do Azure Resource Manager na CLI do Azure
Este artigo aborda comandos básicos, você deseja toouse com toomanage CLI do Azure e interaja com seus recursos (principalmente VMs) de sua assinatura do Azure.  Para obter mais ajuda com as opções e opções de linha de comando específico, você pode usar ajuda de comando online hello e opções digitando `azure <command> <subcommand> --help` ou `azure help <command> <subcommand>`.

> [!NOTE]
> Esses exemplos não incluem operações baseadas em modelo que geralmente são recomendadas para implantações de VM no Gerenciador de Recursos. Para obter informações, consulte [Olá Use CLI do Azure com o Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) e [implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e Olá CLI do Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Tarefa | Gerenciador de Recursos |
| --- | --- | --- |
| Criar hello VM mais básico |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Obter Olá `image-urn` de saudação `azure vm image list` comando. Confira [este artigo](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter exemplos.) |
| Criar uma VM do Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Criar uma VM do Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Listar VMs |`azure  vm list [options]` |
| Obter informações sobre uma VM |`azure  vm show [options] <resource_group> <name>` |
| Iniciar uma VM |`azure vm start [options] <resource_group> <name>` |
| Parar uma VM |`azure vm stop [options] <resource_group> <name>` |
| Desalocar uma VM |`azure vm deallocate [options] <resource-group> <name>` |
| Reiniciar uma VM |`azure vm restart [options] <resource_group> <name>` |
| Excluir uma VM |`azure vm delete [options] <resource_group> <name>` |
| Capturar uma VM |`azure vm capture [options] <resource_group> <name>` |
| Criar uma VM por meio de uma imagem do usuário |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Criar uma VM por meio de um disco especializado |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Adicionar um disco de dados tooa VM |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Remover um disco de dados de uma VM |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Adicionar um tooa genérico extensão VM |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Adicionar extensão de acesso da máquina virtual tooa VM |`azure vm reset-access [options] <resource-group> <name>` |
| Adicionar extensão de Docker tooa VM |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Remover uma extensão de VM |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Conferir o uso dos recursos de VM |`azure vm list-usage [options] <location>` |
| Conferir todos os tamanhos de VM disponíveis |`azure vm sizes [options]` |

## <a name="next-steps"></a>Próximas etapas
* Para obter exemplos adicionais de comandos CLI Olá ultrapassando básicas de gerenciamento de VM, consulte [hello usando a CLI do Azure com o Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).
