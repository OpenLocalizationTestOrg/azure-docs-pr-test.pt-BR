1. Entrar toohello [portal clássico do Azure](http://manage.windowsazure.com).  
2. Na barra de comandos de saudação na parte inferior da saudação da janela de saudação, clique em **novo**.
3. Em **Computação**, clique em **Máquina Virtual** e em **Da Galeria**.
   
    ![Criar uma Nova Máquina Virtual][Image1]
4. Em Olá **SUSE** grupo, selecione uma imagem de máquina virtual OpenSUSE e clique em Olá seta toocontinue.
5. Em Olá primeiro **configuração de máquina Virtual** página:
   
   * Digite um **Nome da máquina virtual**, como "testlinuxvm". Olá nome deve conter entre 3 e 15 caracteres, pode conter apenas letras, números e hifens e deve começar com uma letra e terminar com uma letra ou um número.
   * Verifique se Olá **camada** e escolher um **tamanho**. camada de saudação determina tamanhos de saudação, que você pode escolher. Olá tamanho afeta Olá custo de usá-lo, bem como as opções de configuração, como quantos discos de dados, você pode anexar. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Digite um **novo nome de usuário**, ou aceite o padrão de saudação **azureuser**. Esse nome é adicionado toohello Sudoers arquivo da lista.
   * Decidir qual tipo de **autenticação** toouse. Para obter diretrizes gerais de senha, consulte [Senhas fortes](http://msdn.microsoft.com/library/ms161962.aspx).
6. Em Olá próximo **configuração de máquina Virtual** página:
   
   * Usar saudação padrão **criar um novo serviço de nuvem**.
   * Em Olá **nome DNS** , digite um toouse de nome DNS exclusivo como parte do endereço de saudação, como "testlinuxvm".
   * Em Olá **afinidade região/grupo/Rede Virtual** , selecione uma região onde esta imagem virtual será hospedada.
   * Em **pontos de extremidade**, mantenha o ponto de extremidade SSH hello. Você pode adicionar outros agora, ou adicionar, alterar ou excluí-los após a criação da máquina virtual de saudação.
     
     > [!NOTE]
     > Se você quiser que uma máquina virtual de toouse uma rede virtual, você **deve** especificar a rede virtual hello quando você criar a máquina virtual de saudação. Você não pode adicionar uma rede virtual de tooa de máquina virtual depois de criar a máquina virtual de saudação. Para saber mais, confira [Visão geral da rede virtual](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. Em Olá última **configuração de máquina Virtual** , manter as configurações padrão de saudação e, em seguida, em Olá toofinish de marca de seleção.

portal Hello lista Olá nova máquina virtual em **máquinas virtuais**. Enquanto o status de saudação será relatado como **(provisionamento)**, máquina virtual de hello está sendo configurada. Quando o status da saudação é relatado como **executando**, você pode mover toohello próxima etapa.

## <a name="connect-toohello-virtual-machine"></a>Conecte-se toohello Máquina Virtual
Você usará o SSH ou PuTTY tooconnect toohello máquina virtual, dependendo do sistema operacional de saudação no computador Olá de que você se conectará:

* Em um computador executando o Linux, use SSH. No prompt de comando hello, digite:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Digite a senha do usuário hello.
* Em um computador executando o Windows, use PuTTY. Se você não tiver instalado, baixe-o da saudação [página de Download do PuTTY][PuTTYDownload].
  
    Salvar **putty.exe** tooa diretório no seu computador. Abra um prompt de comando, navegue toothat pasta e executar **putty.exe**.
  
    Digite o nome de host de saudação, como "testlinuxvm.cloudapp.net" e digite "22" hello **porta**.
  
    ![Tela PuTTY][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Atualizar Olá Máquina Virtual (opcional)
1. Depois que você está conectado toohello virtual machine, opcionalmente, você pode instalar patches e atualizações do sistema. atualização de saudação toorun, tipo:
   
    `$ sudo zypper update`
2. Selecione **Software**, em seguida, **atualização on-line** atualizações disponíveis toolist. Selecione **aceitar** toostart Olá instalação e aplicar todos os patches disponíveis novo (exceto Olá aqueles opcionais).
3. Após a instalação ser concluída, selecione **Concluir**.  O sistema agora estiver toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
