
Você pode aprender distribuição global do BD Cosmos do Azure nesse vídeo do Azure Friday com Scott Hanselman e o gerente de engenharia chefe Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Para obter mais informações sobre como a replicação de banco de dados global funciona no BD Cosmos, veja [Distribuir dados globalmente com o BD Cosmos](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Adicionar regiões globais do banco de dados usando Olá Portal do Azure
O BD Cosmos do Azure está disponível em todas as [regiões do Azure][azureregions] pelo mundo. Depois de selecionar o nível de consistência saudação padrão para sua conta de banco de dados, você pode associar uma ou mais regiões (dependendo de sua escolha de necessidades de distribuição global e nível de consistência padrão).

1. Em Olá [portal do Azure](https://portal.azure.com/), no hello barra à esquerda, clique em **o banco de dados do Azure Cosmos**.
2. Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá toomodify de conta de banco de dados.
3. Na folha de conta hello, clique em **replicar dados globalmente** menu hello.
4. Em Olá **replicar dados globalmente** folha, selecione Olá regiões tooadd ou remover clicando em áreas no mapa hello e, em seguida, clique em **salvar**. Não há regiões de tooadding um custo, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/documentdb/) ou hello [distribuir dados globalmente com documentos](../articles/documentdb/documentdb-distribute-data-globally.md) artigo para obter mais informações.
   
    ![Clique em regiões Olá Olá mapa tooadd ou removê-los][1]
    
Depois de adicionar uma segunda região, Olá **Failover Manual** opção é habilitada em Olá **replicar dados globalmente** folha no portal de saudação. Você pode usar o processo de failover opção tootest hello ou alterar Olá gravação primária região. Depois de adicionar uma região de terceira, Olá **Failover prioridades** opção está habilitada em Olá mesmo folha para que você pode alterar a ordem de failover Olá para leituras.  

### <a name="selecting-global-database-regions"></a>Selecionar regiões de bancos de dados globais
Há dois cenários comuns para configurar duas ou mais regiões:

1. Fornecer acesso de baixa latência toodata tooend usuários, independentemente de onde estejam localizados em todo o mundo de saudação
2. Adição de resiliência regional para continuidade dos negócios e recuperação de desastre (BCDR)

Para entregar baixa latência tooend-usuários, é recomendável toodeploy ambos Olá aplicativo e adicione o Azure Cosmos banco de dados em regiões de saudação que é correspondem a usuários do aplicativo do toowhere Olá estão localizados.

Para BCDR, é recomendável tooadd regiões com base nos pares de região Olá descritos em Olá [Business continuidade e recuperação de desastres (BCDR): regiões emparelhadas do Azure] [ bcdr] artigo.

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
