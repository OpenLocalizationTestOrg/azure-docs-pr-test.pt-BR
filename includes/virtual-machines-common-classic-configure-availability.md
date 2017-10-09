


Os conjuntos de disponibilidade ajudam a manter as máquinas virtuais disponíveis em caso de tempo de inatividade (por exemplo, durante a manutenção). Colocação de dois ou mais máquinas virtuais configuradas de forma semelhante em um conjunto de disponibilidade cria Olá redundância necessário toomaintain disponibilidade de aplicativos de saudação ou serviços que sua máquina virtual é executada. Para obter detalhes sobre como isso funciona, consulte [gerenciar Olá disponibilidade das máquinas virtuais][Manage hello availability of virtual machines].

É um toouse de prática recomendada conjuntos de disponibilidade e balanceamento de carga de pontos de extremidade toohelp Certifique-se de que o aplicativo estará sempre disponível e funcionando com eficiência. Para obter detalhes sobre os pontos de extremidade com balanceamento de carga, consulte [Balanceamento de carga para os serviços de infraestrutura do Azure][Load balancing for Azure infrastructure services].

Você pode adicionar máquinas virtuais clássicas a um conjunto de disponibilidade usando uma das duas opções:

* [Opção 1: Criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo][Option 1: Create a virtual machine and an availability set at hello same time]. Em seguida, adicione o novo toohello de máquinas virtuais definido quando você criar essas máquinas virtuais.
* [Opção 2: Adicionar um conjunto de disponibilidade de tooan de máquina virtual existente][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> No modelo clássico Olá Olá máquinas virtuais que você deseja tooput no mesmo conjunto de disponibilidade deve pertencer toohello mesmo serviço de nuvem.
> 
> 

## <a id="createset"></a>Opção 1: criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo
Você pode usar o portal do Azure hello ou do Azure PowerShell comandos toodo isso.

Olá toouse portal do Azure:

1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com).
2. No menu de hub hello, clique em **+ novo**e, em seguida, clique em **Máquina Virtual**.
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Selecione a imagem de máquina virtual do Marketplace Olá desejar toouse. Você pode escolher toocreate uma máquina virtual Linux ou Windows.
4. Olá selecionada a máquina virtual, verifique se esse modelo de implantação hello está definido muito**clássico** e, em seguida, clique em **criar**
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Insira um nome da máquina virtual, nome de usuário e senha (para computadores Windows) ou a chave pública SSH (para computadores Linux). 
6. Escolha o tamanho da VM hello e, em seguida, clique em **selecione** toocontinue.
7. Escolha **configuração opcional > conjunto de disponibilidade**e selecione o conjunto de disponibilidade Olá desejar tooadd Olá máquina virtual.
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Analise suas definições de configuração. Quando tiver concluído, clique em **Criar**.
9. Enquanto o Azure cria sua máquina virtual, você pode acompanhar o progresso de saudação em **máquinas virtuais** no menu de hub hello.

toouse do Azure PowerShell comandos toocreate uma máquina virtual do Azure e adicioná-lo tooa conjunto de disponibilidade novo ou existente, consulte [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Opção 2: adicionar um conjunto de disponibilidade de tooan de máquina virtual existente
Em Olá portal do Azure, você pode adicionar tooan existente de máquinas virtuais clássicas existente conjunto de disponibilidade ou criar um novo para eles. (Lembre-se de que as máquinas virtuais Olá Olá mesmo conjunto de disponibilidade deve pertencer toohello mesmo serviço de nuvem.) etapas de saudação são quase Olá mesmo. Com o Azure PowerShell, você pode adicionar conjunto de disponibilidade existente do hello máquina virtual tooan.

1. Se você ainda não tiver feito isso, entre no toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **máquinas virtuais (clássicas)**.
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Na lista de saudação de máquinas virtuais, selecione o nome de Olá da máquina virtual de saudação que você deseja que o conjunto de toohello tooadd.
4. Escolha **conjunto de disponibilidade** da máquina virtual de saudação **configurações**.
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Selecione conjunto de disponibilidade Olá que desejar tooadd Olá máquina virtual. máquina virtual de saudação deve pertencer toohello mesmo serviço em nuvem como um conjunto de disponibilidade de saudação.
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Clique em **Salvar**.

toouse comandos do PowerShell do Azure, abra uma sessão do PowerShell do Azure de nível de administrador e execute Olá comando a seguir. Espaços reservados de saudação (como &lt;VmCloudServiceName&gt;), substituir tudo entre aspas hello, incluindo hello < e > caracteres, com hello corrigir nomes.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> Olá VM pode ter toofinish toobe reiniciado adicioná-lo toohello conjunto de disponibilidade.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

