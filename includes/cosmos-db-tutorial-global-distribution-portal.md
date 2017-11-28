
<span data-ttu-id="4c552-101">Você pode aprender distribuição global do BD Cosmos do Azure nesse vídeo do Azure Friday com Scott Hanselman e o gerente de engenharia chefe Karthik Raman.</span><span class="sxs-lookup"><span data-stu-id="4c552-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="4c552-102">Para obter mais informações sobre como a replicação de banco de dados global funciona no BD Cosmos, veja [Distribuir dados globalmente com o BD Cosmos](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="4c552-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="4c552-103"><a id="addregion"></a>Adicionar regiões de banco de dados globais usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4c552-103"><a id="addregion"></a>Add global database regions using the Azure Portal</span></span>
<span data-ttu-id="4c552-104">O BD Cosmos do Azure está disponível em todas as [regiões do Azure][azureregions] pelo mundo.</span><span class="sxs-lookup"><span data-stu-id="4c552-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="4c552-105">Após a seleção do nível de consistência padrão para sua conta de banco de dados, você pode associar uma ou mais regiões (dependendo da sua escolha do nível de consistência padrão e das necessidades de distribuição global).</span><span class="sxs-lookup"><span data-stu-id="4c552-105">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="4c552-106">No [Portal do Azure](https://portal.azure.com/), na barra esquerda, clique em **BD Cosmos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4c552-106">In the [Azure portal](https://portal.azure.com/), in the left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="4c552-107">Na folha **BD Cosmos do Azure**, escolha a conta do banco de dados a ser modificada.</span><span class="sxs-lookup"><span data-stu-id="4c552-107">In the **Azure Cosmos DB** blade, select the database account to modify.</span></span>
3. <span data-ttu-id="4c552-108">Na folha da conta, clique em **Replicar dados globalmente** no menu.</span><span class="sxs-lookup"><span data-stu-id="4c552-108">In the account blade, click **Replicate data globally** from the menu.</span></span>
4. <span data-ttu-id="4c552-109">Na folha **Replicar dados globalmente**, clicando nas regiões no mapa, selecione aquelas a serem adicionadas ou removidas e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4c552-109">In the **Replicate data globally** blade, select the regions to add or remove by clicking regions in the map, and then click **Save**.</span></span> <span data-ttu-id="4c552-110">Há um custo para adicionar regiões. Veja a [página de preços](https://azure.microsoft.com/pricing/details/documentdb/) ou o artigo [Distribuir dados globalmente com o DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="4c552-110">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Clicar nas regiões no mapa para adicioná-las ou removê-las][1]
    
<span data-ttu-id="4c552-112">Depois de adicionar uma segunda região, a opção **Failover Manual** é habilitada na folha **Replicar dados globalmente** no portal.</span><span class="sxs-lookup"><span data-stu-id="4c552-112">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data globally** blade in the portal.</span></span> <span data-ttu-id="4c552-113">Você pode usar essa opção para testar o processo de failover ou alterar a região de gravação principal.</span><span class="sxs-lookup"><span data-stu-id="4c552-113">You can use this option to test the failover process or change the primary write region.</span></span> <span data-ttu-id="4c552-114">Depois de adicionar uma terceira região, a opção **Prioridades de Failover** é habilitada na mesma folha para que você possa alterar a ordem de failover das leituras.</span><span class="sxs-lookup"><span data-stu-id="4c552-114">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="4c552-115">Selecionar regiões de bancos de dados globais</span><span class="sxs-lookup"><span data-stu-id="4c552-115">Selecting global database regions</span></span>
<span data-ttu-id="4c552-116">Há dois cenários comuns para configurar duas ou mais regiões:</span><span class="sxs-lookup"><span data-stu-id="4c552-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="4c552-117">Fornecimento de acesso a dados de baixa latência para os usuários finais, independentemente de onde estejam localizados em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="4c552-117">Delivering low-latency access to data to end users no matter where they are located around the globe</span></span>
2. <span data-ttu-id="4c552-118">Adição de resiliência regional para continuidade dos negócios e recuperação de desastre (BCDR)</span><span class="sxs-lookup"><span data-stu-id="4c552-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="4c552-119">Para oferecer baixa latência para os usuários finais, é recomendável implantar o aplicativo e adicionar o BD Cosmos do Azure nas regiões que correspondem a onde os usuários do aplicativo estão localizados.</span><span class="sxs-lookup"><span data-stu-id="4c552-119">For delivering low-latency to end-users, it is recommended to deploy both the application and add Azure Cosmos DB in the regions thats correspond to where the application's users are located.</span></span>

<span data-ttu-id="4c552-120">Para o BCDR, é recomendável adicionar regiões com base nos pares de regiões descritos no artigo [Continuidade dos negócios e recuperação de desastre (BCDR): Regiões Emparelhadas do Azure][bcdr].</span><span class="sxs-lookup"><span data-stu-id="4c552-120">For BCDR, it is recommended to add regions based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **Azure Cosmos DB** blade, select the database account to modify.
2. In the account blade, click **Replicate data globally** from the menu.
3. In the **Replicate data globally** blade, click **Manual Failover** from the top bar.
    ![Change the write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region to become the new write region, click the checkbox to confirm triggering a failover, and click OK
    ![Change the write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
