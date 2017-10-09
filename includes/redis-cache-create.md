toocreate um cache, primeiro entrar toohello [portal do Azure](https://portal.azure.com)e clique em **novo** > **bancos de dados** > **deCacheRedis**.

> [!NOTE]
> Se você não tiver uma conta do Azure, poderá [Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) em poucos minutos.
> 
> 

![Novo cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Toocreating armazena em cache no portal do Azure de saudação Além disso, você também pode criar usando o Gerenciador de recursos de modelos, o PowerShell ou CLI do Azure.
> 
> * toocreate um cache usando o Gerenciador de recursos de modelos, consulte [criar um cache Redis usando um modelo](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate um cache usando o PowerShell do Azure, consulte [gerenciar Azure Redis Cache com o Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate um cache usando a CLI do Azure, consulte [como toocreate e gerenciar o Cache Redis do Azure usando hello Azure Interface de linha de comando (CLI do Azure)](../articles/redis-cache/cache-manage-cli.md).
> 
> 

Em Olá **novo Cache Redis** folha, especifique a configuração desejada Olá para o cache de saudação.

![Criar o cache](media/redis-cache-create/redis-cache-cache-create.png) 

* Em **nome Dns**, insira um toouse de nome exclusivo do cache para o ponto de extremidade do hello cache. nome do cache Olá deve ser uma cadeia de caracteres entre 1 e 63 caracteres e conter apenas números, letras e Olá `-` caracteres. Hello nome do cache não pode começar ou terminar com hello `-` caractere e consecutivos `-` caracteres não são válidos.
* Para **assinatura**, selecione Olá assinatura do Azure que você deseja toouse para o cache de saudação. Se sua conta tiver apenas uma assinatura, ele será selecionado automaticamente e Olá **assinatura** suspensa não será exibida.
* No **Grupo de recursos**, selecione ou crie um grupo de recursos para seu cache. Para obter mais informações, consulte [toomanage de grupos de recursos usando os recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Use **local** toospecify Olá localização geográfica em que o cache está hospedado. Para melhor desempenho de saudação, a Microsoft recomenda expressamente criar cache Olá Olá mesma região que o aplicativo de cliente de cache hello.
* Use **preço** tooselect Olá desejado tamanho do cache e recursos.
* **Redis cluster** permite que você toocreate caches maiores que 53 GB e tooshard dados em vários nós de Redis. Para obter mais informações, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Persistência de redis** oferece Olá capacidade toopersist tooan seu cache conta de armazenamento do Azure. Para obter instruções sobre como configurar persistência, consulte [como tooconfigure persistência para um Premium do Azure Redis Cache](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Rede virtual** oferece maior segurança e isolamento, restringindo o acesso tooyour cache tooonly esses clientes Olá especificado dentro de rede Virtual do Azure. Você pode usar todos os recursos de saudação do VNet, como sub-redes, políticas de controle de acesso e outros recursos toofurther restringem acesso tooRedis. Para obter mais informações, consulte [como suporte a tooconfigure rede Virtual para um Premium do Azure Redis Cache](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Por padrão, o acesso não SSL está desabilitado para novos caches. porta não SSL do hello tooenable, seleção **desbloquear a porta 6379 (não SSL criptografada)**.

Quando novas opções de cache Olá são configuradas, clique em **criar**. Pode levar alguns minutos para Olá cache toobe criado. status de saudação toocheck, você pode monitorar o progresso de Olá no quadro saudação inicial. Olá cache foi criado, o novo cache tem um **executando** status e está pronto para uso com [configurações padrão](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Cache criado](media/redis-cache-create/redis-cache-cache-created.png)

