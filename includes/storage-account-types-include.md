Existem dois tipos de contas de armazenamento:

### <a name="general-purpose-storage-accounts"></a>Contas de armazenamento de uso geral
Um oferece de conta de armazenamento de uso geral acesso tooAzure serviços de armazenamento, como tabelas, filas, arquivos, Blobs e Azure discos da máquina virtual em uma única conta. Esse tipo de conta de armazenamento tem dois níveis de desempenho:

* Um nível de desempenho de armazenamento padrão que permite que você toostore tabelas, filas, arquivos, Blobs e Azure discos da máquina virtual.
* Um nível de desempenho de armazenamento premium, que atualmente suporta apenas discos de máquina virtual do Azure. Confira [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](../articles/storage/common/storage-premium-storage.md) para ter uma visão geral detalhada do Armazenamento Premium.

### <a name="blob-storage-accounts"></a>Contas de armazenamento de Blobs
Uma conta de Armazenamento de Blobs é uma conta de armazenamento especializada para armazenar dados não estruturados como blobs (objetos) no Armazenamento do Azure. Contas de armazenamento de blob são contas de armazenamento de uso geral existentes tooyour semelhantes e compartilham todos Olá ótima durabilidade, disponibilidade, escalabilidade e desempenho recursos que você usa atualmente incluindo 100% de consistência de API para blobs de bloco e blobs de acréscimo. Para aplicativos que exigem apenas o armazenamento de blobs em bloco ou acréscimo, recomendamos o uso de contas de Armazenamento de Blobs.

> [!NOTE]
> As contas de armazenamento de blobs oferecem suporte apenas aos blobs de bloco e aos blobs de acréscimo, e não aos blobs de página.
> 
> 

Contas de armazenamento de blob expõem Olá **camada de acesso** atributo que pode ser especificado durante a criação da conta e modificado posteriormente, conforme necessário. Há dois tipos de camadas de acesso que podem ser especificados com base em seu padrão de acesso a dados:

* Um **acesso** nível de acesso que indica que objetos Olá na conta de armazenamento Olá serão acessados com mais frequência. Isso permite que você toostore dados a um custo menor de acesso.
* Um **moderado** nível de acesso que indica que objetos Olá na conta de armazenamento hello serão acessados com menos frequência. Isso permite que você toostore dados em um menor custo de armazenamento de dados.

Se houver uma alteração no padrão de uso de saudação de seus dados, você também pode alternar entre esses níveis de acesso a qualquer momento. Camada de acesso de saudação alteração pode resultar em encargos adicionais. Confira [Preços e cobrança para contas de Armazenamento de Blobs](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) para obter mais detalhes.

Para saber mais sobre contas de Armazenamento de Blobs, confira [Armazenamento de Blobs do Azure: camadas estática e dinâmica](../articles/storage/blobs/storage-blob-storage-tiers.md).

Antes de criar uma conta de armazenamento, você deve ter uma assinatura do Azure, que é um plano que oferece acesso tooa variedade de serviços do Azure. Você pode começar com o Azure com uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/). Depois que você decidir toopurchase um plano de assinatura, você pode escolher entre uma variedade de [opções de compra](https://azure.microsoft.com/pricing/purchase-options/). Se for um [assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), você obterá créditos mensais gratuitos que podem se usados com os serviços do Azure, incluindo o Armazenamento do Azure. Consulte [Preços do Armazenamento do Azure ](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre preço por volume.

toolearn como toocreate uma conta de armazenamento, consulte [criar uma conta de armazenamento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) para obter mais detalhes. Você pode criar até too200 exclusivamente nomeada contas de armazenamento com uma única assinatura. Consulte [Escalabilidade e Metas de Desempenho do Armazenamento do Azure](../articles/storage/common/storage-scalability-targets.md) para obter detalhes sobre os limites da conta de armazenamento.

