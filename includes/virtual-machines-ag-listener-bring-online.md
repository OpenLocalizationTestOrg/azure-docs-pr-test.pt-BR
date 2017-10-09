1. <span data-ttu-id="2598b-101">No Gerenciador de Cluster de Failover, expanda **funções** e realce seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2598b-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="2598b-102">Em Olá **recursos** guia, clique o nome do ouvinte hello e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2598b-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="2598b-103">Clique em Olá **dependências** guia. Se vários recursos estiverem listados, verifique se os endereços IP hello tem ou não e dependências.</span><span class="sxs-lookup"><span data-stu-id="2598b-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="2598b-104">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2598b-104">Click **OK**.</span></span>

5. <span data-ttu-id="2598b-105">Clique no nome do ouvinte Olá e clique **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="2598b-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="2598b-106">Após a saudação ouvinte está online, em hello **recursos** guia, clique o grupo de disponibilidade hello e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2598b-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Configurar o recurso de grupo de disponibilidade Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="2598b-108">Crie uma dependência no recurso de nome de ouvinte hello (não nome de recursos de endereço Olá IP) e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="2598b-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Adicionar dependência no nome do ouvinte Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="2598b-110">Inicie o SQL Server Management Studio e conecte a réplica primária toohello.</span><span class="sxs-lookup"><span data-stu-id="2598b-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="2598b-111">Vá muito**alta disponibilidade AlwaysOn** > **grupos de disponibilidade** > **\<AvailabilityGroupName\>**   >  **Ouvintes do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="2598b-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="2598b-112">nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover deve ser exibido.</span><span class="sxs-lookup"><span data-stu-id="2598b-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="2598b-113">Clique no nome do ouvinte Olá e clique **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2598b-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="2598b-114">Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade Olá usando Olá $EndpointPort utilizado antes (neste tutorial, 1433 era o padrão de saudação) e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="2598b-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

