
<span data-ttu-id="76c5e-101">Você pode aprender distribuição global do BD Cosmos do Azure nesse vídeo do Azure Friday com Scott Hanselman e o gerente de engenharia chefe Karthik Raman.</span><span class="sxs-lookup"><span data-stu-id="76c5e-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="76c5e-102">Para obter mais informações sobre como a replicação de banco de dados global funciona no BD Cosmos, veja [Distribuir dados globalmente com o BD Cosmos](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="76c5e-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="76c5e-103"><a id="addregion"></a>Adicionar regiões globais do banco de dados usando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="76c5e-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="76c5e-104">O BD Cosmos do Azure está disponível em todas as [regiões do Azure][azureregions] pelo mundo.</span><span class="sxs-lookup"><span data-stu-id="76c5e-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="76c5e-105">Depois de selecionar o nível de consistência saudação padrão para sua conta de banco de dados, você pode associar uma ou mais regiões (dependendo de sua escolha de necessidades de distribuição global e nível de consistência padrão).</span><span class="sxs-lookup"><span data-stu-id="76c5e-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="76c5e-106">Em Olá [portal do Azure](https://portal.azure.com/), no hello barra à esquerda, clique em **o banco de dados do Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="76c5e-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="76c5e-107">Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá toomodify de conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76c5e-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="76c5e-108">Na folha de conta hello, clique em **replicar dados globalmente** menu hello.</span><span class="sxs-lookup"><span data-stu-id="76c5e-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="76c5e-109">Em Olá **replicar dados globalmente** folha, selecione Olá regiões tooadd ou remover clicando em áreas no mapa hello e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="76c5e-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="76c5e-110">Não há regiões de tooadding um custo, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/documentdb/) ou hello [distribuir dados globalmente com documentos](../articles/documentdb/documentdb-distribute-data-globally.md) artigo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="76c5e-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Clique em regiões Olá Olá mapa tooadd ou removê-los][1]
    
<span data-ttu-id="76c5e-112">Depois de adicionar uma segunda região, Olá **Failover Manual** opção é habilitada em Olá **replicar dados globalmente** folha no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c5e-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="76c5e-113">Você pode usar o processo de failover opção tootest hello ou alterar Olá gravação primária região.</span><span class="sxs-lookup"><span data-stu-id="76c5e-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="76c5e-114">Depois de adicionar uma região de terceira, Olá **Failover prioridades** opção está habilitada em Olá mesmo folha para que você pode alterar a ordem de failover Olá para leituras.</span><span class="sxs-lookup"><span data-stu-id="76c5e-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="76c5e-115">Selecionar regiões de bancos de dados globais</span><span class="sxs-lookup"><span data-stu-id="76c5e-115">Selecting global database regions</span></span>
<span data-ttu-id="76c5e-116">Há dois cenários comuns para configurar duas ou mais regiões:</span><span class="sxs-lookup"><span data-stu-id="76c5e-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="76c5e-117">Fornecer acesso de baixa latência toodata tooend usuários, independentemente de onde estejam localizados em todo o mundo de saudação</span><span class="sxs-lookup"><span data-stu-id="76c5e-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="76c5e-118">Adição de resiliência regional para continuidade dos negócios e recuperação de desastre (BCDR)</span><span class="sxs-lookup"><span data-stu-id="76c5e-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="76c5e-119">Para entregar baixa latência tooend-usuários, é recomendável toodeploy ambos Olá aplicativo e adicione o Azure Cosmos banco de dados em regiões de saudação que é correspondem a usuários do aplicativo do toowhere Olá estão localizados.</span><span class="sxs-lookup"><span data-stu-id="76c5e-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="76c5e-120">Para BCDR, é recomendável tooadd regiões com base nos pares de região Olá descritos em Olá [Business continuidade e recuperação de desastres (BCDR): regiões emparelhadas do Azure] [ bcdr] artigo.</span><span class="sxs-lookup"><span data-stu-id="76c5e-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
