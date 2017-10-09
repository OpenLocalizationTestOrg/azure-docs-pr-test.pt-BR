Se sua máquina virtual (VM) no Azure encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas. Um exemplo comum seria uma atualização de aplicativo com falha que impede a inicialização com êxito do hello VM. Este artigo descreve como toouse tooconnect portal do Azure seu toofix VM do disco rígido virtual tooanother quaisquer erros e, em seguida, crie novamente sua VM original.

## <a name="recovery-process-overview"></a>Visão geral do processo de recuperação
Olá Solucionando problemas do processo é o seguinte:

1. Excluir Olá VM que está encontrando problemas, mas manter os discos rígidos virtuais hello.
2. Anexar e monte tooanother de disco rígido virtual Olá VM para solução de problemas.
3. Conecte-se toohello VM de solução de problemas. Editar arquivos ou execute ferramentas toofix erros em Olá original do disco rígido virtual.
4. Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.
5. Crie uma VM usando Olá original do disco rígido virtual.

## <a name="delete-hello-original-vm"></a>Excluir Olá VM original
Discos rígidos virtuais e VMs são dois recursos distintos no Azure. Um disco rígido virtual é onde o sistema de operacional hello, aplicativos e configurações são armazenadas. Olá VM é os metadados que define Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC). Cada disco rígido virtual obtém uma concessão atribuída quando o disco está anexado tooa VM. Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída. concessão de saudação continua tooassociate Olá OS disco tooa VM mesmo quando a VM está em um estado parado e desalocado.

Olá primeiro toorecovering de etapa sua VM é toodelete Olá VM próprio recurso. Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento. Após Olá que VM é excluída, você pode anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação. 

1. Entrar toohello [portal do Azure](https://portal.azure.com). 
2. No menu de saudação no lado esquerdo da saudação, clique em **máquinas virtuais (clássicas)**.
3. Selecione Olá VM com problema hello, clique **discos**e, em seguida, identificar o nome da saudação de saudação do disco rígido virtual. 
4. Selecione Olá sistema operacional do disco rígido virtual e verificar Olá **local** tooidentify conta de armazenamento de saudação que contém o disco rígido virtual. Em Olá exemplo a seguir, Olá cadeia de caracteres imediatamente antes ". n e t" é o nome de conta de armazenamento hello.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![imagem de saudação sobre o local da VM](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Olá VM e, em seguida, selecione **excluir**. Certifique-se de que discos Olá não são selecionados quando você excluir Olá VM.
6. Crie uma nova VM de recuperação. Essa VM deve estar no hello mesmo região e grupo de recursos (serviço de nuvem) como o problema de saudação VM.
7. Selecione a VM de recuperação hello e, em seguida, selecione **discos** > **anexar existente**.
8. tooselect o disco rígido virtual existente, clique em **arquivo VHD**:

    ![Procurar VHD existente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Selecione a conta de armazenamento hello > contêiner VHD > Olá disco rígido virtual, clique em Olá **selecione** botão tooconfirm sua escolha.

    ![Selecionar o VHD existente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Com o VHD selecionado agora, selecione **Okey** tooattach Olá disco rígido virtual existente.
11. Depois de alguns segundos, Olá **discos** painel para sua VM exibirá o disco rígido virtual existente conectado como um disco de dados:

    ![Disco rígido virtual existente anexado como um disco de dados](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Corrigir problemas em Olá original do disco rígido virtual
Quando a saudação existente do disco rígido virtual estiver montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário. Depois que você resolveu problemas hello, continue com hello etapas a seguir.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Desmonte e desanexar Olá original do disco rígido virtual
Depois que os erros são resolvidos, desmonte e desanexar Olá disco rígido virtual existente de sua solução de problemas de VM. Você não pode usar o disco rígido virtual, junto com qualquer outra VM até que a concessão de saudação que anexa toohello do disco rígido virtual Olá VM de solução de problemas é liberado.  

1. Entrar toohello [portal do Azure](https://portal.azure.com). 
2. No menu de saudação no lado esquerdo do hello, selecione **máquinas virtuais (clássicas)**.
3. Localize a VM de recuperação hello. Selecione os discos, disco de saudação com o botão direito e, em seguida, selecione **desanexar**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Criar uma máquina virtual do disco rígido original de saudação

toocreate uma VM do seu disco rígido virtual original, use [portal clássico do Azure](https://manage.windowsazure.com).

1. Entre no [portal clássico do Azure](https://manage.windowsazure.com).
2. Na parte inferior de saudação do portal hello, selecione **novo** > **de computação** > **Máquina Virtual** > **da Galeria** .
3. Em Olá **escolha uma imagem** seção, selecione **meus discos**, e, em seguida, selecione Olá disco rígido virtual original. Verifique as informações de local de saudação. Isso é região Olá onde Olá VM deve ser implantado. Selecione o botão Avançar hello.
4. Em Olá **configuração de máquina Virtual** seção, digite o nome da VM hello e selecione um tamanho para Olá VM.
