### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Abra as portas TCP no firewall do Windows hello para instância padrão Olá Olá mecanismo de banco de dados
1. Conecte a máquina virtual de toohello com área de trabalho remota. Para obter instruções detalhadas sobre como conectar toohello VM, consulte [abrir uma VM do SQL com a área de trabalho remota](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Depois de conectado, na tela de início do hello, digite **WF.msc**e em seguida, pressione ENTER.
   
    ![Saudação de iniciar o programa de Firewall](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. Em Olá **Firewall do Windows com segurança avançada**, no painel esquerdo de hello, com o botão direito **regras de entrada**e, em seguida, clique em **nova regra** no painel de ações de saudação.
   
    ![Nova Regra](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. Em Olá **novo Assistente de regra de entrada** caixa de diálogo **tipo de regra**, selecione **porta**e, em seguida, clique em **próximo**.
5. Em Olá **protocolo e portas** caixa de diálogo, usar saudação padrão **TCP**. Em Olá **portas locais específicas** caixa, então a saudação do tipo número de instância de saudação do hello mecanismo de banco de dados da porta (**1433** instância de padrão de saudação ou de sua escolha para a porta privada Olá na etapa de ponto de extremidade de saudação).
   
    ![Porta TCP 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Clique em **Avançar**.
7. Em Olá **ação** caixa de diálogo, selecione **Permitir conexão Olá**e, em seguida, clique em **próximo**.
   
    **Observação de segurança:** selecionando **Permitir conexão Olá se é seguro** pode fornecer segurança adicional. Selecione esta opção se você quiser tooconfigure opções de segurança adicional no seu ambiente.
   
    ![Permitir Conexões](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. Em Olá **perfil** caixa de diálogo, selecione **pública**, **privada**, e **domínio**. Em seguida, clique em **Próximo**.
   
    **Observação de segurança:** selecionando **pública** permitir acesso pela Olá da internet. Sempre que possível, selecione um perfil mais restritivo.
   
    ![Perfil Público](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. Em Olá **nome** caixa de diálogo, digite um nome e uma descrição para a regra e, em seguida, clique em **concluir**.
   
    ![Nome da Regra](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Abrir portas adicionais para outros componentes conforme necessário. Para obter mais informações, consulte [Configurando tooAllow de Firewall do Windows hello acesso ao SQL Server](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Configurar toolisten do SQL Server em Olá protocolo TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Configurar o SQL Server para autenticação de modo misto
Olá mecanismo de banco de dados do SQL Server não pode usar a autenticação do Windows sem um ambiente de domínio. tooconnect toohello o mecanismo de banco de dados de outro computador, configurar o SQL Server para a autenticação de modo misto. A autenticação de modo misto permite a Autenticação do SQL Server e a Autenticação do Windows.

> [!NOTE]
> A configuração da autenticação de modo misto pode não ser necessária se você tiver configurado uma Rede Virtual do Azure com um ambiente de domínio configurado.
> 
> 

1. Enquanto a máquina virtual de toohello conectado, na página inicial do hello, digite **SQL Server Management Studio** e clique em ícone de saudação selecionado.
   
    Olá primeira vez que você abra o Management Studio, é necessário criar o ambiente do hello usuários Management Studio. Isso pode demorar alguns instantes.
2. Management Studio apresenta Olá **conectar tooServer** caixa de diálogo. Em Olá **nome do servidor** caixa, digite o nome de saudação do hello máquina virtual tooconnect toohello mecanismo de banco de dados com hello Pesquisador de objetos (em vez do nome da máquina virtual Olá você também pode usar **(local)** ou um único período como Olá **nome do servidor**). Selecione **autenticação do Windows**e deixe  ***your_VM_name*\your_local_administrator** em Olá **nome de usuário** caixa. Clique em **Conectar**.
   
    ![Conecte-se tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. No SQL Server Management Studio Pesquisador de objetos, clique Olá nome da instância de saudação do SQL Server (nome da máquina virtual Olá) e, em seguida, clique em **propriedades**.
   
    ![Propriedades do servidor](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Em Olá **segurança** página em **autenticação de servidor**, selecione **modo de autenticação do Windows e SQL Server**e, em seguida, clique em **Okey** .
   
    ![Selecionar modo de autenticação](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Na caixa de diálogo do SQL Server Management Studio hello, clique em **Okey** tooacknowledge Olá requisito toorestart do SQL Server.
6. No Object Explorer, clique com o botão direito do mouse no seu servidor, e em seguida, clique em **Reiniciar**. (Se o SQL Server Agent estiver em execução, ele também deverá ser reinicializado.)
   
    ![Reiniciar](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Na caixa de diálogo do SQL Server Management Studio hello, clique em **Sim** tooagree que você deseja toorestart do SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Criar logons de autenticação do SQL Server
tooconnect toohello do mecanismo de banco de dados de outro computador, você deve criar pelo menos um logon de autenticação do SQL Server.

1. No SQL Server Management Studio Pesquisador de objetos, expanda a pasta de Olá Olá da instância do servidor no qual você deseja que o novo logon do toocreate hello.
2. Saudação de atalho **segurança** pasta, ponto muito**novo**e selecione **logon...** .
   
    ![Novo Logon](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. Em Olá **logon - novo** caixa de diálogo Olá **geral** página, insira o nome de saudação do novo usuário de saudação em Olá **nome de logon** caixa.
4. Selecione **Autenticação do SQL Server**.
5. Em Olá **senha** caixa, digite uma senha para Olá novo usuário. Digite essa senha novamente em Olá **Confirmar senha** caixa.
6. Selecione opções de imposição de senha Olá necessárias (**impor política de senha**, **impor expiração de senha**, e **usuário deve alterar a senha no próximo logon**). Se você estiver usando esse logon por conta própria, não é necessário toorequire uma alteração de senha no próximo logon. hello.
7. De saudação **banco de dados padrão** , selecione um banco de dados padrão para logon de saudação. **mestre** é saudação padrão para essa opção. Se você ainda não tiver criado um banco de dados de usuário, deixe essa definição muito**mestre**.
   
    ![Propriedades de Logon](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Se esse for o primeiro logon de saudação que você está criando, convém toodesignate esse logon como um administrador do SQL Server. Nesse caso, no hello **funções de servidor** página de seleção **sysadmin**.
   
   > [!NOTE]
   > Os membros da função de servidor fixa de sysadmin de Olá tem total controle sobre Olá mecanismo de banco de dados. Você deve restringir cuidadosamente a associação nessa função.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Clique em OK.

Para obter mais informações sobre logons do SQL Server, consulte [Criar um logon (a página pode estar em inglês)](http://msdn.microsoft.com/library/aa337562.aspx).

