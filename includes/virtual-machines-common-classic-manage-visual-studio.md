Você pode criar máquinas virtuais no Azure usando o Gerenciador de Servidores no Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Criar uma máquina virtual do Azure no Gerenciador de Servidores
Embora você possa criar uma máquina virtual em Olá [Portal de gerenciamento](http://go.microsoft.com/fwlink/?LinkID=253103), você também pode criar uma máquina virtual no Azure usando comandos no Gerenciador de servidores. Máquinas virtuais podem ser usadas, por exemplo, tooprovide um front end por trás de um balanceamento de carga público ponto de extremidade comum.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate uma nova máquina virtual
1. No Gerenciador de servidores, abra Olá **Azure** nó e clique em **máquinas virtuais**.
2. No menu de contexto de saudação, clique em **criar Máquina Virtual**.
   
    Olá **criar uma nova máquina Virtual** assistente é exibido.
   
    ![Olá comando Criar Máquina Virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Em Olá **escolher uma assinatura** página, selecione uma assinatura toouse ao criar a máquina virtual de saudação e, em seguida, clique em **próximo**.
   
    Se você não tiver entrado no tooAzure, clique em **entrar** toosign no. Em seguida, selecione sua assinatura do Azure na caixa de listagem suspensa Olá se ela ainda não estiver selecionada.
4. Em Olá **selecionar uma imagem de máquina Virtual** , selecione um tipo de imagem em Olá **tipo de imagem** suspensa caixa de listagem e selecione um imagens da máquina virtual em Olá **nome da imagem** caixa de listagem. Quando terminar, clique em **Próximo**.
   
    ![Selecionar uma página de imagem de máquina virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Você pode escolher Olá seguintes tipos de imagem.
   
   * **Imagens públicas** lista imagens de máquinas virtuais de sistemas operacionais e software para servidores, como o Windows Server e SQL Server.
   * **Imagens MSDN** listas de imagens de máquinas virtuais de assinantes tooMSDN disponível do software, como o Visual Studio e o Microsoft Dynamics.
   * **Imagens privadas** lista imagens especializadas e generalizadas da máquina virtual que você criou.
     
     toolearn sobre especializadas e generalizadas máquinas virtuais, consulte [imagem VM](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Consulte [como tooCapture tooUse uma máquina Virtual do Windows como um modelo](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) para obter informações sobre como tooturn uma máquina virtual em um modelo que você pode usar tooquickly criar novas máquinas virtuais pré-configuradas.
     
     Você pode clicar em uma máquina virtual imagem nome toosee informações sobre Olá imagem Olá direita da página de saudação.
     
     > [!NOTE]
     > Não é possível adicionar toohello de imagens de máquina virtual **imagens públicas** ou **imagens MSDN** lista porque eles são somente leitura. Todas as máquinas virtuais que você criar são adicionadas toohello **imagens privadas** lista.
     > 
     > 
     
     Se for assinante do MSDN com uma assinatura do nível do Visual Studio, você poderá criar uma máquina virtual do Azure pré-criada que contém o Visual Studio, além de várias outras imagens. Para saber mais, confira [Create a Virtual Machine in Visual Studio by Using Images Visual Studio 2013 Gallery image for MSDN subscribers (Criar uma máquina virtual no Visual Studio usando imagens da galeria de imagens do Visual Studio 2013 para assinantes do MSDN)](http://visualstudio2013msdngalleryimage.azurewebsites.net) e [Assinaturas do MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs).|
5. Em Olá **configurações básicas de máquina Virtual** página, insira um nome de máquina e, em seguida, adicione especificações de saudação para a máquina virtual de hello, incluindo tamanho Olá e um nome de usuário e senha. Quando terminar, clique em **Próximo**.
   
    Você usará o nome do novo hello e senha toolog na máquina de saudação usando área de trabalho remota é um toowrite boa ideia-las para baixo caso você esqueça. Depois de criar uma máquina virtual do Azure no Visual Studio, você pode alterar seu tamanho e outras configurações de saudação [Portal de gerenciamento](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Se você escolher tamanhos maiores para a máquina virtual de hello, podem ser aplicadas taxas adicionais. Consulte [Detalhes de preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/) para obter mais informações.
   > 
   > 
6. Máquinas virtuais criadas no Visual Studio exigem um serviço de nuvem. Em Olá **as configurações de serviço de nuvem** página, selecione um serviço de nuvem para a máquina virtual de hello ou clique em **< criar novo... >** na lista suspensa de saudação se você ainda não tiver uma nuvem de serviço ou deseja toouse um novo um. Também é necessária uma conta de armazenamento, então escolha uma conta de armazenamento (ou criar uma nova conta de armazenamento) no hello **conta de armazenamento** caixa de listagem suspensa. Consulte [tooMicrosoft Introdução armazenamento do Azure](../articles/storage/common/storage-introduction.md) para obter mais informações.
7. Se você quiser toospecify uma rede virtual (que é opcional), selecione-o nas caixas de listagem de lista suspensa de rede Virtual e a sub-rede de saudação.
   
    Máquinas virtuais que são membros de um conjunto de disponibilidade são implantados toodifferent domínios de falha. Consulte [Rede Virtual do Azure](https://azure.microsoft.com/services/virtual-network/) para obter mais informações.
8. Se você quiser que sua máquina virtual toobelong tooan conjunto de disponibilidade (também opcional), selecione Olá **especificar um conjunto de disponibilidade** caixa de seleção e, em seguida, escolha um conjunto na caixa de listagem suspensa Olá de disponibilidade. Quando terminar, escolha Olá **próximo** botão.
   
    Adicionar a máquina virtual tooan conjunto de disponibilidade ajuda a seu aplicativo permanecer disponível durante falhas de rede, falhas de hardware de disco local e qualquer tempo de inatividade planejado. Você precisa Olá toouse [Portal de gerenciamento](http://go.microsoft.com/fwlink/?LinkID=253103) define toocreate as redes virtuais, sub-redes e disponibilidade. Consulte [gerenciar Olá disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) para obter mais informações.
9. Em Olá **pontos de extremidade** , especifique os pontos de extremidade públicos Olá que você deseja toousers disponíveis de sua máquina virtual. Por exemplo, você pode escolher tooenable HTTP (porta 80) além toohello área de trabalho remota e PowerShell pontos de extremidade, que são habilitados por padrão. tooadd um ponto de extremidade, escolha um na Olá **nome da porta** suspensa caixa de listagem e, em seguida, escolha Olá **adicionar** botão. tooremove um ponto de extremidade, escolha Olá vermelho **X** próximo nome toohello na lista de pontos de extremidade de saudação.
   
    ![página de pontos de extremidade Olá no Assistente de máquinas virtuais de saudação.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    pontos de extremidade de saudação que estão disponíveis dependem do serviço de nuvem Olá selecionado para sua máquina virtual. Consulte [Pontos de extremidade de serviço do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) para obter mais informações.
   
   > [!NOTE]
   > Habilitar pontos de extremidade públicos torna os serviços em seu toohello disponíveis da máquina virtual à internet. Ser tooinstall se e corretamente configurar pontos de extremidade de saudação e serviços em sua máquina virtual, como listas de controle de acesso de configuração (ACLs) para pontos de extremidade de saudação. Consulte [como pontos de extremidade de tooSet tooa Máquina Virtual](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) para obter mais informações.
   > 
   > 
10. Depois de terminar de configurar as configurações de máquina virtual hello, escolha Olá **criar** máquina virtual do botão toocreate hello.
    
     Enquanto o Azure cria uma máquina virtual de hello, Olá **o Log de atividades do Azure** mostra Olá progresso da operação de criação de máquina virtual de saudação.
    
     ![Log de atividades de máquina virtual - em andamento.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     informações de máquina virtual somente tooview, escolha Olá **máquinas virtuais** guia Olá **o Log de atividades do Azure**.
    
     ![Log de atividades de máquina virtual - concluído.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Se a operação de saudação for concluída com êxito, Olá nova máquina de virtual aparece sob Olá **máquinas virtuais** nó no Gerenciador de servidores. Você pode fazer logon nela clicando Olá **conectar usando a área de trabalho remota** atalho.
    
     ![Máquina virtual que aparece no Gerenciador de Servidores.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Gerenciar suas máquinas virtuais
Na página de configuração de máquina virtual hello, além de tooshutting para baixo, conectar, atualizar e adicionando toohello de pontos de verificação selecionada máquina virtual, você também pode exibir ou alterar as configurações de máquina virtual de saudação. Você pode:

* Alterar o tamanho da máquina virtual hello.
* O conjunto de disponibilidade de saudação selecione toouse com a máquina virtual de saudação.
* Adicionar, remover ou alterar as configurações de pontos de extremidade públicos.
* Adicionar, remover ou configurar as extensões de máquina virtual.
* Exibir informações sobre discos Olá associados à máquina virtual de saudação.

### <a name="view-or-change-virtual-machine-settings"></a>Exibir ou alterar as configurações de máquina virtual
1. No Gerenciador de servidores, escolha sua máquina virtual no hello **máquinas virtuais do Azure** nó.
2. No menu de atalho hello, escolha **configurar** tooview página de configuração de máquina virtual de saudação.
   
    ![página de configuração de máquina virtual do Azure Olá](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Exibir informações da máquina virtual hello ou alterá-la.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Salvar ou restaurar o status de saudação de sua máquina virtual
Como configurar sua máquina virtual e instalar o software nela, é tooregularly uma boa ideia salvar seu progresso com a criação de pontos de verificação de máquina virtual. Um ponto de verificação é um instantâneo ou uma imagem do estado atual de saudação de sua máquina virtual. Se algo de errado com a máquina virtual de hello, ou se desejar tooreconfigure Olá VM, você pode poupar tempo restaurando tooa estado de ponto de verificação anterior em vez de começar do zero.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate um ponto de verificação de máquina virtual
1. No Gerenciador de servidores, escolha sua máquina virtual no hello **máquinas virtuais do Azure** nó.
2. No menu de atalho hello, escolha **configurar** tooview página de configuração de máquina virtual de saudação.
3. Na página de configuração de saudação, escolha Olá **capturar imagem** botão.
   
    ![Botão de captura da página de configuração do Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Olá **capturar a máquina Virtual** caixa de diálogo é exibida.
   
    ![Caixa de diálogo de máquina virtual de captura do Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Fornece um rótulo de imagem e a descrição. Um rótulo padrão e uma descrição são fornecidos, mas você pode substituí-los pelo seu próprio rótulo se desejar.
5. Se você já tiver executado o Sysprep nesta máquina virtual, selecione Olá **executei o Sysprep na máquina virtual de saudação** caixa.
   
    O Sysprep é uma ferramenta que, entre outras coisas, remove dados específicos do sistema de versão de hello máquina virtual do Windows, fazendo de um modelo que outras pessoas possam usar. Consulte [como tooCapture tooUse uma máquina Virtual do Windows como um modelo](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) para obter mais informações. Faça backup Olá VM antes de executar o Sysprep.
6. Depois de terminar de configurar as configurações de captura hello, escolha Olá **capturar** ponto de verificação do botão toocreate hello.
   
    Enquanto o Azure cria um ponto de verificação hello, Olá **o Log de atividades do Azure** mostra Olá progresso da operação de saudação.
   
    ![Capturar um ponto de verificação de máquina virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Quando a operação de ponto de verificação de saudação for concluída, você verá ele no hello **o Log de atividades do Azure**.
   
    ![Operação de ponto de verificação foi concluída](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>pontos de verificação de máquina virtual toomanage
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>toorestore tooa uma máquina virtual estado salvo anteriormente
* Siga etapas Olá descritas em [passo a passo: executar nuvem restaura do Microsoft Azure máquinas virtuais usando o PowerShell - parte 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete um ponto de verificação
1. Vá toohello [Portal de gerenciamento](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Na página de configuração de máquina virtual hello, escolha Olá **imagens** guia na parte superior de saudação da página de saudação.
3. Escolha o ponto de verificação de saudação desejado toodelete e, em seguida, escolha Olá **excluir** botão final Olá Olá página.

## <a name="shut-down-your-virtual-machine"></a>Desligar a máquina virtual
1. No Gerenciador de servidores, escolha Olá máquina de virtual você deseja tooshut para baixo no hello **máquinas virtuais do Azure** nó.
2. No menu de atalho hello, escolha Olá **desligamento** comando, ou escolha **configurar** tooview Olá a página de configuração de máquina virtual e escolha Olá **desligamento**botão.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a criação de máquinas virtuais, consulte [criar uma máquina Virtual executando o Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [criar uma máquina virtual executando o Windows no portal de visualização do Azure Olá](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

