1. Enquanto a máquina virtual de toohello conectado com a área de trabalho remota, procure **do Configuration Manager**:

    ![Abrir SSCM](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. No SQL Server Configuration Manager, no painel de console hello, expanda **configuração de rede do SQL Server**.

1. No painel de console hello, clique em **protocolos para MSSQLSERVER** (Olá nome da instância padrão.) No painel de detalhes de saudação, clique com botão direito **TCP** e clique em **habilitar** se ele não ainda estiver habilitado.

    ![Habilitar TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. No painel de console hello, clique em **SQL Server Services**. No painel de detalhes de saudação, clique com botão direito  **do SQL Server (*nome de instância*) * * (instância padrão de saudação é **SQL Server (MSSQLSERVER)**) e, em seguida, clique em **reiniciar** , toostop e reinicie a instância de saudação do SQL Server.

    ![Reiniciar o Mecanismo de Banco de Dados](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Feche o SQL Server Configuration Manager.

Para obter mais informações sobre como habilitar protocolos para Olá mecanismo de banco de dados do SQL Server, consulte [habilitar ou desabilitar um protocolo de rede de servidor](http://msdn.microsoft.com/library/ms191294.aspx).
