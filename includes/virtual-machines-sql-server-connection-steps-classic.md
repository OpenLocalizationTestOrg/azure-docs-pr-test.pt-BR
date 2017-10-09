### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Determinar nome DNS de saudação da máquina virtual de saudação
tooconnect toohello do mecanismo de banco de dados do SQL Server de outro computador, você deve saber Olá sistema de nome de domínio (DNS) nome da máquina virtual de saudação. (Isso é Olá nome hello internet usa tooidentify Olá máquina virtual. Você pode usar o endereço IP hello, mas o endereço IP hello pode mudar quando o Azure move recursos de redundância ou manutenção. nome DNS de saudação será estável porque ele pode ser redirecionado tooa novo endereço IP.)  

1. Olá Portal do Azure (ou da etapa anterior Olá), selecione **máquinas virtuais (clássicas)**.
2. Selecione sua VM do SQL.
3. Em Olá **Máquina Virtual** folha, Olá cópia **nome DNS** para a máquina virtual de saudação.
   
    ![Nome DNS](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Conectar toohello mecanismo de banco de dados de outro computador
1. Em um computador conectado toohello internet, abra o SQL Server Management Studio.
2. Em Olá **conectar tooServer** ou **conectar tooDatabase mecanismo** caixa de diálogo Olá **nome do servidor** , digite o nome DNS de saudação da máquina virtual de saudação (determinada na Olá tarefa anterior) e um número de porta do ponto de extremidade público no formato de saudação do *DNSName, portnumber* como **mysqlvm.cloudapp.net,57500**.
   
    ![Conectar-se usando SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Se você não lembrar o número da porta do ponto de extremidade público Olá criado anteriormente, você pode encontrar no hello **pontos de extremidade** área da saudação **Máquina Virtual** folha.
   
    ![Porta pública](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. Em Olá **autenticação** selecione **autenticação do SQL Server**.
4. Em Olá **Login** caixa, digite o nome de saudação de um logon que você criou em uma tarefa anterior.
5. Em Olá **senha** caixa, digite a senha de saudação do logon de saudação que você cria em uma tarefa anterior.
6. Clique em **Conectar**.

