### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Configurar um rótulo de DNS para o endereço IP público de Olá

tooconnect toohello o mecanismo de banco de dados do SQL Server de saudação à Internet, considere a criação de um rótulo de DNS para seu endereço IP público. Você pode se conectar por endereço IP, mas Olá rótulo DNS cria um registro que é mais fácil tooidentify e resumos Olá subjacente endereço IP público.

> [!NOTE]
> Rótulos de DNS não são necessários se o plano tooonly conectar toohello do SQL Server da instância em Olá mesmo rede Virtual ou apenas localmente.

toocreate um rótulo de DNS, primeiro selecione **máquinas virtuais** no portal de saudação. Selecione seu toobring VM do SQL Server, suas propriedades.

1. Na visão geral de máquina virtual hello, selecione seu **endereço IP público**.

    ![endereço ip público](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. Nas propriedades de saudação de seu endereço IP público, expanda **configuração**.

1. Insira um nome para o rótulo de DNS. Esse nome é um registro que podem ser usados tooconnect tooyour VM do SQL Server por nome em vez de por endereço IP diretamente.

1. Clique em Olá **salvar** botão.

    ![rótulo de dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Conectar toohello mecanismo de banco de dados de outro computador

1. Em um computador conectado toohello internet, abra SQL Server Management Studio (SSMS). Se você não tiver o SQL Server Management Studio, poderá baixá-lo [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. Em Olá **conectar tooServer** ou **conectar tooDatabase mecanismo** caixa de diálogo, editar Olá **nome do servidor** valor. Insira o endereço IP de saudação ou nome DNS completo da máquina virtual de saudação (determinado na tarefa anterior Olá). Você também pode adicionar uma vírgula e fornecer a porta TCP do SQL Server. Por exemplo: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. Em Olá **autenticação** selecione **autenticação do SQL Server**.

1. Em Olá **Login** caixa, digite o nome de saudação de um logon SQL válido.

1. Em Olá **senha** caixa, digite a senha de logon Olá Olá.

1. Clique em **Conectar**.

    ![conexão ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)