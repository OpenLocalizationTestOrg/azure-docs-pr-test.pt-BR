
Se o problema do Azure não é abordado neste artigo, visite Olá [fóruns do Azure no MSDN e o estouro de pilha](https://azure.microsoft.com/support/forums/). Você pode lançar seu problema nesses fóruns ou too@AzureSupport no Twitter. Além disso, você pode emitir uma solicitação de suporte do Azure, selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="general-troubleshooting-steps"></a>Etapas gerais de solução de problemas
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Solucionar problemas de falhas de alocação comuns no modelo de implantação clássico Olá
Essas etapas podem ajudar a resolver diversas falhas de alocação em máquinas virtuais:

* Redimensione Olá VM tooa tamanho diferente de VM.<br>
    Clique em **Procurar tudo** > **Máquinas virtuais (clássicas)** > sua máquina virtual > **Configurações** > **Tamanho**. Para obter etapas detalhadas, consulte [redimensionar a máquina virtual de saudação](https://msdn.microsoft.com/library/dn168976.aspx).
* Excluir todas as VMs do serviço de nuvem hello e crie novamente as VMs.<br>
    Clique em **Procurar tudo** > **Máquinas virtuais (clássicas)** > sua máquina virtual > **Excluir**. Em seguida, clique em **Novo** > **Computação** > [imagem de máquina virtual].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Solucionar problemas de falhas de alocação comuns no modelo de implantação do Azure Resource Manager Olá
Essas etapas podem ajudar a resolver diversas falhas de alocação em máquinas virtuais:

* Parar (desalocar) todas as VMs em Olá disponibilidade mesmo definido e reinicie cada um deles.<br>
    toostop: clique em **grupos de recursos** > seu grupo de recursos > **recursos** > seu conjunto de disponibilidade > **máquinas virtuais** > sua máquina virtual >  **Parar**.
  
    Depois de interromper todas as VMs, selecione Olá primeira máquina virtual e clique em **iniciar**.

## <a name="background-information"></a>Informações básicas
### <a name="how-allocation-works"></a>Como funciona a alocação
servidores de saudação em datacenters do Azure são particionadas em clusters. Normalmente, uma solicitação de alocação é tentada em vários clusters, mas é possível que determinadas restrições da solicitação de alocação Olá force Olá plataforma Windows Azure tooattempt Olá solicitação apenas um cluster. Neste artigo, vamos nos referir toothis como "fixado tooa cluster". O diagrama 1 abaixo mostra o caso de saudação de uma alocação de normal é tentada em vários clusters. Diagrama 2 mostra o caso de saudação de uma alocação que foi fixado tooCluster 2 porque esse é onde Olá existente conjunto CS_1 de serviço de nuvem ou disponibilidade está hospedado.
![Diagrama de alocação](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Motivos das falhas de alocação
Quando uma solicitação de alocação é fixado tooa cluster, há uma possibilidade maior de falhar toofind liberar recursos, pois o pool de recursos disponíveis de saudação for menor. Além disso, se sua solicitação de alocação está fixado tooa cluster, mas tipo de saudação do recurso solicitado não é suportado por cluster, a solicitação falhará mesmo que o cluster Olá tem liberar recursos. Diagrama de 3 abaixo ilustra o caso de Olá onde uma alocação fixada falha porque cluster do candidato apenas Olá não tem recursos gratuitos. Diagrama 4 ilustra caso Olá onde uma alocação fixada falha porque não dá suporte a cluster de candidato apenas Olá Olá solicitado tamanho da VM, mesmo que o cluster Olá tem liberar recursos.

![Falha na alocação fixada](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Detalhadas solucionar problemas de cenários de falha de alocação específica de etapas no modelo de implantação clássico Olá
Aqui estão os cenários comuns de alocação que causam um toobe de solicitação de alocação fixada. Vamos nos aprofundar em cada cenário posteriormente neste artigo.

* Redimensionar uma VM ou adicionar VMs ou função instâncias tooan serviço em nuvem existente
* Reiniciar VMs parcialmente paradas (desalocadas)
* Reiniciar VMs totalmente paradas (desalocadas)
* Implantações de preparo/produção (apenas plataforma como serviço)
* Grupo de afinidades (proximidade de serviço/VM)
* Rede virtual com base em grupo de afinidade

Quando você receber um erro de alocação, consulte se qualquer um dos cenários de saudação descritos aplicar tooyour erro. Use o erro de alocação Olá retornado pelo cenário correspondente de Olá Olá de tooidentify plataforma Windows Azure. Se a solicitação é fixada, remova alguns Olá fixação restrições tooopen seus clusters toomore de solicitação, aumentando a probabilidade de saudação de êxito de alocação.

Em geral, como Olá erro não indica "hello solicitado não há suporte para o tamanho da VM", você pode sempre tentar novamente mais tarde, como recursos suficientes podem ter sido liberado no hello cluster tooaccommodate sua solicitação. Se o problema de saudação que Olá solicitada não há suporte para o tamanho da VM, tente um tamanho VM diferente. Caso contrário, Olá única opção é tooremove Olá fixação de restrição.

Dois cenários comuns de falha são grupos de tooaffinity relacionados. Em Olá anterior, um grupo de afinidade foi usado tooprovide proximidade tooVMs/serviço instâncias ou foi usada tooenable Olá criação de uma rede virtual. Com a introdução de saudação de redes virtuais regionais, grupos de afinidade não são mais necessário toocreate uma rede virtual. Com a redução de saudação de latência de rede na infraestrutura do Azure, grupos de afinidade de toouse Olá recomendação para a proximidade VM/serviço foi alterado.

O diagrama abaixo de 5 apresenta taxonomia Olá dos cenários de alocação da saudação (fixados).
![Taxonomia de alocação fixada](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> Erro de saudação listado em cada cenário de alocação é uma forma abreviada. Consulte toohello [pesquisa de cadeia de caracteres de erro](#Error string lookup) para cadeias de caracteres de erro detalhadas.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Cenário de alocação: redimensionar uma VM ou adicionar VMs ou função de instâncias de serviço de nuvem existente tooan
**Erro**

Upgrade_VMSizeNotSupported ou GeneralError

**Causa de fixação de cluster**

A solicitação tooresize uma VM ou adicionar uma VM ou um serviço de nuvem existente do função instância tooan tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem existente hello. Criar um novo serviço de nuvem permite Olá plataforma Windows Azure toofind outro cluster que tem recursos gratuitos ou dá suporte ao tamanho da VM Olá que você solicitou.

**Solução alternativa**

Se o erro de saudação Upgrade_VMSizeNotSupported *, tente um tamanho VM diferente. Se usando um tamanho diferente de VM não é uma opção, mas se for aceitável toouse um endereço IP virtual (VIP), diferente de criar um novo toohost de serviço de nuvem Olá nova VM e adicionar Olá nova nuvem serviço toohello rede virtual regional onde hello VMs existentes estão em execução. Se seu serviço de nuvem existente não usar uma rede virtual regional, você pode ainda criar uma nova rede virtual para o novo serviço de nuvem hello e, em seguida, conecte-se a [rede virtual toohello nova rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Saiba mais sobre as [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Se o erro de saudação é GeneralError *, é provável que o tipo de saudação do recurso (por exemplo, um determinado tamanho VM) é suportado por cluster hello, mas Olá cluster não tem recursos gratuitos no momento da saudação. Toohello semelhante acima cenário, adicionar recursos de computação Olá desejado durante a criação de um novo serviço de nuvem (Observe que o novo serviço de nuvem Olá tem toouse um VIP diferente) e usar uma rede virtual regional tooconnect seus serviços de nuvem.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Cenário de alocação: reiniciar VMs parcialmente paradas (desalocadas)
**Erro**

GeneralError*

**Causa de fixação de cluster**

A desalocação parcial significa que você parou (desalocou) uma ou mais, mas não todas, VMs no serviço de nuvem. Quando você parar (desalocar) uma VM, Olá associado recursos são liberados. A renicialização da VM parada (desalocada) é, portanto, uma nova solicitação de alocação. Reiniciando VMs em um serviço de nuvem parcialmente desalocado é equivalente tooadding VMs tooan serviço de nuvem existente. solicitação de alocação Olá tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem existente hello. Criando um serviço de nuvem diferentes permite Olá plataforma Windows Azure toofind outro cluster que tem um recurso gratuito ou dá suporte ao tamanho da VM Olá que você solicitou.

**Solução alternativa**

Se for aceitável toouse um VIP diferente, exclua Olá parado (desalocadas) VMs (mas manter Olá associado discos) e adicionar Olá VMs através de um serviço de nuvem diferente. Use uma rede virtual regional tooconnect seus serviços de nuvem:

* Se seu serviço de nuvem existente usa uma rede virtual regional, basta adicionar nova toohello de serviço de nuvem Olá mesma rede virtual.
* Se seu serviço de nuvem existente não usa uma rede virtual regional, crie uma nova rede virtual para o novo serviço de nuvem Olá e, em seguida, [conectar sua rede virtual toohello nova rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Saiba mais sobre as [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Cenário de alocação: reiniciar VMs totalmente paradas (desalocadas)
**Erro**

GeneralError*

**Causa de fixação de cluster**

A desalocação total significa que você parou (desalocou) todas as VMs de um serviço de nuvem. Olá toorestart de solicitações de alocação essas VMs tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem hello. Criar um novo serviço de nuvem permite Olá plataforma Windows Azure toofind outro cluster que tem recursos gratuitos ou dá suporte ao tamanho da VM Olá que você solicitou.

**Solução alternativa**

Se for aceitável toouse um VIP diferente, excluir Olá original parado (desalocadas) VMs (mas manter Olá associado discos) e excluir o serviço de nuvem correspondente hello (computação de saudação associada recursos já foram liberados quando você parada (desalocada) Olá VMs). Crie um novo Olá de tooadd de serviço de nuvem VMs novamente.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Cenário de alocação: implantações de preparo/produção (apenas plataforma como serviço)
**Erro**

New_General* ou New_VMSizeNotSupported*

**Causa de fixação de cluster**

saudação de preparo de implantação e a implantação de produção de hello de um serviço de nuvem é hospedada em hello mesmo cluster. Quando você adicionar implantação segundo hello, solicitação de alocação correspondente Olá será tentada no Olá Olá mesmo cluster que hospeda a primeira implantação.

**Solução alternativa**

Excluir implantação hello e o serviço de nuvem original hello e reimplante o serviço de nuvem hello. Esta ação pode ir para primeira implantação de saudação em um cluster que tem suficiente toofit liberar recursos ambas as implantações ou em um cluster que oferece suporte a tamanhos de VM Olá que você solicitou.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Cenário de alocação: grupo de afinidades (proximidade de serviço/VM)
**Erro**

New_General* ou New_VMSizeNotSupported*

**Causa de fixação de cluster**

Qualquer recurso de computação é o grupo de afinidade atribuído tooan ligado tooone cluster. Novas solicitações de recursos de computação no grupo de afinidade são tentadas na Olá mesmo cluster que hospedam os recursos existentes de saudação. Isso é verdadeiro se o hello novos recursos são criados por meio de um novo serviço de nuvem ou um serviço de nuvem existente.

**Solução alternativa**

Se um grupo de afinidades não for necessário, não use o grupo de afinidades ou agrupe os recursos de computação em vários grupos de afinidades.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Cenário de alocação: rede virtual com base em grupo de afinidades
**Erro**

New_General* ou New_VMSizeNotSupported*

**Causa de fixação de cluster**

Antes de redes virtuais regionais foram introduzidas, era necessário tooassociate uma rede virtual com um grupo de afinidade. Como resultado, os recursos de computação colocados em um grupo de afinidade são associados por Olá mesmas restrições, conforme descrito em hello "cenário de alocação: grupo de afinidade (proximidade VM/serviço)" seção acima. recursos de computação de saudação são cluster tooone associado.

**Solução alternativa**

Se você não precisar de um grupo de afinidade, criar uma nova rede virtual regional para Olá novos recursos que você está adicionando, e, em seguida, [conectar sua rede virtual toohello nova rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Saiba mais sobre as [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Como alternativa, você pode [migrar sua rede de virtual baseado em grupos de afinidade de rede virtual tooa regionais](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)e, em seguida, adicionar recursos de saudação desejado novamente.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Cenários de falha de alocação específica de etapas no modelo de implantação do Azure Resource Manager Olá de solução de problemas detalhada
Aqui estão os cenários comuns de alocação que causam um toobe de solicitação de alocação fixada. Vamos nos aprofundar em cada cenário posteriormente neste artigo.

* Redimensionar uma VM ou adicionar VMs ou função instâncias tooan serviço em nuvem existente
* Reiniciar VMs parcialmente paradas (desalocadas)
* Reiniciar VMs totalmente paradas (desalocadas)

Quando você receber um erro de alocação, consulte se qualquer um dos cenários de saudação descritos aplicar tooyour erro. Use o erro de alocação Olá retornado pelo cenário correspondente de Olá Olá de tooidentify plataforma Windows Azure. Se sua solicitação for cluster existente tooan fixados, remova alguns Olá fixação restrições tooopen seus clusters toomore de solicitação, aumentando a probabilidade de saudação de êxito de alocação.

Em geral, como Olá erro não indica "hello solicitado não há suporte para o tamanho da VM", você pode sempre tentar novamente mais tarde, como recursos suficientes podem ter sido liberado no hello cluster tooaccommodate sua solicitação. Se o problema de saudação que Olá solicitada não há suporte para o tamanho da VM, consulte abaixo para soluções alternativas.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Cenário de alocação: redimensionar uma VM ou adicionar VMs tooan conjunto de disponibilidade existente
**Erro**

Upgrade_VMSizeNotSupported* ou GeneralError*

**Causa de fixação de cluster**

A solicitação tooresize uma VM ou adicionar um tooan VM existente do conjunto de disponibilidade tem toobe tentado no cluster original de saudação que hospeda o conjunto de disponibilidade existente hello. Criando um novo conjunto de disponibilidade permite Olá plataforma Windows Azure toofind outro cluster que tem recursos gratuitos ou dá suporte ao tamanho da VM Olá que você solicitou.

**Solução alternativa**

Se o erro de saudação Upgrade_VMSizeNotSupported *, tente um tamanho VM diferente. Se não for uma opção de usar um tamanho diferente de VM, interrompa todas as VMs no conjunto de disponibilidade de saudação. Você pode alterar o tamanho de saudação de máquina virtual Olá alocará Olá tooa o cluster da VM que oferece suporte a saudação desejado tamanho da VM.

Se o erro de saudação é GeneralError *, é provável que o tipo de saudação do recurso (por exemplo, um determinado tamanho VM) é suportado por cluster hello, mas Olá cluster não tem recursos gratuitos no momento da saudação. Se Olá VM pode ser parte de um conjunto de disponibilidade diferente, crie uma nova VM em um conjunto de disponibilidade diferente (em Olá mesma região). Essa nova VM pode ser adicionado toohello mesma rede virtual.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Cenário de alocação: reiniciar VMs parcialmente paradas (desalocadas)
**Erro**

GeneralError*

**Causa de fixação de cluster**

A desalocação parcial significa que você parou (desalocou) uma ou mais, mas não todas, VMs em um conjunto de disponibilidade. Quando você parar (desalocar) uma VM, Olá associado recursos são liberados. A renicialização da VM parada (desalocada) é, portanto, uma nova solicitação de alocação. Reiniciando VMs em um conjunto de disponibilidade parcialmente desalocado é equivalente tooadding VMs tooan grupo de disponibilidade definida. solicitação de alocação Olá tem toobe tentado no cluster original de saudação que hospeda o conjunto de disponibilidade existente hello.

**Solução alternativa**

Pare todas as VMs em disponibilidade Olá definida antes de reiniciar Olá primeiro. Isso garante que uma nova tentativa de alocação seja executada e que um novo cluster com capacidade disponível possa ser selecionado.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Cenário de alocação: reiniciar a parada total (desalocada)
**Erro**

GeneralError*

**Causa de fixação de cluster**

A desalocação total significa que você parou (desalocou) todas as VMs em um conjunto de disponibilidade. solicitação de alocação Olá toorestart essas VMs serão direcionada a todos os clusters que suportam Olá tamanho desejado.

**Solução alternativa**

Selecione um novo tooallocate de tamanho VM. Se isso não funcionar, tente novamente mais tarde.

## <a name="error-string-lookup"></a>Pesquisa de cadeia de caracteres de erro
**New_VMSizeNotSupported***

"hello VM tamanho (ou combinação de tamanhos de VM) necessário para essa implantação não pode ser provisionada devido a restrições de solicitação toodeployment. Se possível, tente relaxar as restrições, como associações de rede virtual, implantação de serviço tooa hospedado sem nenhuma outra implantação nele e tooa a afinidade de outro grupo ou sem grupo de afinidade ou tente implantar tooa uma região diferente. "

**New_General***

"Falha na alocação; não é possível toosatisfy restrições na solicitação. Olá, nova implantação de serviço solicitada é grupo de afinidade tooan associadas, tem como alvo uma rede virtual ou há uma implantação existente sob esse serviço hospedado. Qualquer uma dessas condições restringe toospecific de implantação novo hello Azure recursos. Tente novamente mais tarde ou tente reduzir o tamanho da VM hello ou número de instâncias de função. Como alternativa, se possível, remova restrições mencionados acima hello ou tente implantar tooa uma região diferente."

**Upgrade_VMSizeNotSupported***

"Implantação de saudação tooupgrade não é possível. Olá solicitado tamanho da VM XXX pode não estar disponível em recursos Olá suporte à implantação existente do hello. Tente novamente mais tarde, tente com um tamanho de VM diferente ou com um número de instâncias de função menor, ou crie uma implantação em um serviço hospedado vazio com um novo grupo de afinidades ou sem nenhuma associação com grupo de afinidades."

**GeneralError***

"o servidor de saudação encontrou um erro interno. Tente novamente a solicitação de Olá". Ou "Falha tooproduce uma alocação de serviço Olá".

