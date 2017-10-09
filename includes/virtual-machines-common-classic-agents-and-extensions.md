

As Extensões de VM podem ajudá-lo a:

* Modificar os recursos de segurança e identidade, como redefinir os valores de conta e usar antimalware
* Iniciar, parar ou configurar o monitoramento e o diagnóstico
* Redefinir ou instalar os recursos de conectividade, como RDP e SSH
* Diagnosticar, monitorar e gerenciar suas VMs

Há muitos outros recursos. Novos recursos de extensão de VM são lançados regularmente. Este artigo descreve hello Azure VM agentes para Windows e Linux, e como dar suporte a funcionalidade de extensão de VM. Para ver uma lista de Extensões de VM por categoria de recurso, veja [Extensões de VM e recursos do Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Agentes de VM do Azure para Windows e Linux
Olá agente de máquinas virtuais do Azure (agente de VM) é um processo seguro e leve que instala, configura e remove extensões VM em instâncias de máquinas virtuais do Azure. Olá agente de VM atua como o serviço de controle de local seguro Olá para VMs do Azure. extensões de Olá Olá cargas de agente fornecem tooincrease recursos específicos a produtividade usando a instância de saudação.

Existem dois agentes de VM do Azure, um para máquinas virtuais do Windows e outro para VMs do Linux.

Se você quiser um toouse de instância de máquina virtual em uma ou mais extensões VM, a instância de saudação deve ter um agente de VM instalado. Uma imagem de máquina virtual criada usando hello portal do Azure e uma imagem de saudação **Marketplace** automaticamente instala um agente de VM no processo de criação de saudação. Se uma instância de máquina virtual não possui um agente de VM, você pode instalar Olá agente de VM após a criação da instância de máquina virtual de saudação. Ou, você pode instalar o agente de saudação em uma imagem VM personalizada carregada.

> [!IMPORTANT]
> Esses Agentes de VM são serviços muito leves que permitem a administração segura de instâncias de máquina virtual. Pode haver casos em que você não quer Olá agente de VM. Nesse caso, ter VMs toocreate-se de que não têm Olá agente de VM instalado usando Olá CLI do Azure ou o PowerShell. Embora Olá agente de VM possa ser fisicamente removido, o comportamento de saudação de extensões de VM na instância de saudação é indefinido. Como resultado, não há suporte para a remoção de um Agente de VM instalado.
>

Olá agente da VM está habilitada no hello situações a seguir:

* Quando você cria uma instância de uma VM usando Olá portal do Azure e selecionar uma imagem de saudação **Marketplace**,
* Quando você cria uma instância de uma VM usando Olá [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) ou hello [New-AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet. Você pode criar uma máquina virtual sem um agente de VM adicionando Olá **– DisableGuestAgent** parâmetro toohello [Add-AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet,

* Quando você manualmente baixar e instalar Olá agente de VM em uma instância VM existente e definir Olá **ProvisionGuestAgent** valor muito**true**. Você pode usar essa técnica para agentes Windows e Linux usando um comando do PowerShell ou uma chamada REST. (Se você não definir Olá **ProvisionGuestAgent** valor após a instalação manual Olá agente de VM, adição de saudação do hello agente de VM não é detectado corretamente.) Olá mostra exemplo de código a seguir como toodo esse usando o PowerShell onde hello `$svc` e `$name` já foram determinados argumentos:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Quando você cria uma imagem de VM que inclui um Agente de VM instalado. Após a imagem de saudação com hello agente de VM existe, você pode carregar tooAzure essa imagem. Para uma VM do Windows, baixe Olá [arquivo. msi de agente de VM do Windows](http://go.microsoft.com/fwlink/?LinkID=394789) e instalar Olá agente de VM. Para uma VM do Linux, instale Olá agente de VM do repositório do GitHub Olá localizado em <https://github.com/Azure/WALinuxAgent>. Para obter mais informações sobre como tooinstall Olá agente de VM no Linux, consulte Olá [guia do usuário do agente do Azure Linux VM](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Em PaaS, hello agente VM é chamado **WindowsAzureGuestAgent**e está sempre disponível na Web e as VMs de função de trabalho. (Para obter mais informações, consulte [arquitetura de funções do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) Olá agente de VM para VMs de função agora pode adicionar serviço de nuvem extensões toohello VMs Olá mesma maneira que faz para máquinas virtuais persistentes. Olá maior diferença entre as extensões de VM em VMs de função e VMs persistentes é Olá extensões VM são adicionadas. Com VMs de função, as extensões são adicionadas primeiro toohello serviço de nuvem, em seguida, toohello implantações nesse serviço de nuvem.
>
> Use o [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) toolist cmdlet todas as extensões VM de função disponíveis.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>Localizar, adicionar, atualizar e remover extensões de VM
Para obter detalhes sobre essas tarefas, veja [Adicionar, encontrar, atualizar e remover Extensões de VM do Azure](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
