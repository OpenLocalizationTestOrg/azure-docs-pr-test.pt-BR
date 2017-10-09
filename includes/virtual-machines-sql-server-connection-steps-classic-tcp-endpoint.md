### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Criar um ponto de extremidade TCP para a máquina virtual de saudação
Em ordem tooaccess do SQL Server da saudação internet, uma máquina virtual de saudação deve ter toolisten um ponto de extremidade para comunicação TCP de entrada. Essa etapa de configuração do Azure, direciona a entrada TCP porta tráfego tooa pela porta TCP que é a máquina virtual de toohello acessível.

> [!NOTE]
> Se você estiver se conectando dentro Olá mesmo serviço ou de rede virtual na nuvem, você não tem toocreate um ponto de extremidade publicamente acessível. Nesse caso, você pode continuar toohello próxima etapa. Para obter mais informações, consulte [Cenários de conexão](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. No Portal do Azure do hello, selecione **máquinas virtuais (clássicas)**.
2. Em seguida, selecione a máquina virtual do SQL Server.
3. Selecione **pontos de extremidade**e, em seguida, clique em Olá **adicionar** botão na parte superior de saudação da folha de pontos de extremidade de saudação.
   
    ![Etapas do Portal para Criação de Pontos de Extremidade](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. Em Olá **Adicionar ponto de extremidade** folha, forneça um **nome** como SQLEndpoint.
5. Selecione **TCP** para Olá **protocolo**.
6. Para **Porta pública**, especifique um número de porta, como **57500**.
7. Para **porta privada**, especifique a porta de escuta do SQL Server, cujo padrão é muito**1433**.
8. Clique em **Okey** o ponto de extremidade do toocreate hello.

