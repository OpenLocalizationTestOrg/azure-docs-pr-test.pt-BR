1. No Gerenciador de Cluster de Failover, expanda **funções** e realce seu grupo de disponibilidade.  

2. Em Olá **recursos** guia, clique o nome do ouvinte hello e, em seguida, clique em **propriedades**.

3. Clique em Olá **dependências** guia. Se vários recursos estiverem listados, verifique se os endereços IP hello tem ou não e dependências.  

4. Clique em **OK**.

5. Clique no nome do ouvinte Olá e clique **colocar Online**.

6. Após a saudação ouvinte está online, em hello **recursos** guia, clique o grupo de disponibilidade hello e, em seguida, clique em **propriedades**.
   
    ![Configurar o recurso de grupo de disponibilidade Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Crie uma dependência no recurso de nome de ouvinte hello (não nome de recursos de endereço Olá IP) e, em seguida, clique em **Okey**.
   
    ![Adicionar dependência no nome do ouvinte Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Inicie o SQL Server Management Studio e conecte a réplica primária toohello.

9. Vá muito**alta disponibilidade AlwaysOn** > **grupos de disponibilidade** > **\<AvailabilityGroupName\>**   >  **Ouvintes do grupo de disponibilidade**.  
    nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover deve ser exibido.

10. Clique no nome do ouvinte Olá e clique **propriedades**.

11. Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade Olá usando Olá $EndpointPort utilizado antes (neste tutorial, 1433 era o padrão de saudação) e, em seguida, clique em **Okey**.

