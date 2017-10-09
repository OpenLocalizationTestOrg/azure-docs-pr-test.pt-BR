
Cada ponto de extremidade tem uma *porta pública* e uma *porta privada*:

* porta pública Olá é usada pelo Olá toolisten de Balanceador de carga do Azure para entrada tráfego toohello máquina virtual a partir da Internet de saudação.
* porta privada Olá é usada pelo Olá toolisten de máquina virtual para a entrada de tráfego, normalmente destinado tooan aplicativo ou serviço em execução na máquina virtual de saudação.

Valores padrão para Olá protocolo IP e portas TCP ou UDP para protocolos de rede conhecidos são fornecidas quando você cria pontos de extremidade com hello portal do Azure. Para pontos de extremidade personalizados, você precisará toospecify Olá correto protocolo IP (TCP ou UDP) e as portas públicas e privadas hello. tráfego de entrada toodistribute aleatoriamente entre várias máquinas virtuais, você precisará toocreate um conjunto com balanceamento de carga consiste em vários pontos de extremidade.

Depois de criar um ponto de extremidade, você pode usar um regras de toodefine ACL (lista) de controle de acesso que permitem ou negam o tráfego de entrada hello toohello a porta pública do ponto de extremidade de saudação com base em seu endereço IP de origem. No entanto, se a máquina virtual de saudação estiver em uma rede virtual do Azure, você deve usar grupos de segurança de rede. Para obter detalhes, veja [Sobre os grupos de segurança de rede](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> A configuração de firewall para máquinas virtuais do Azure é feita automaticamente para as portas associadas com pontos de extremidade de conectividade remota que o Azure configura automaticamente. Para portas especificadas para todos os outros pontos de extremidade, nenhuma configuração é feita automaticamente a toohello firewall da máquina virtual de saudação. Quando você cria um ponto de extremidade da máquina virtual de saudação, você precisará tooensure que Olá firewall da máquina virtual de saudação também permite que o tráfego de saudação do protocolo de saudação e de configuração de ponto de extremidade de toohello correspondente porta privada. tooconfigure Olá firewall, consulte a documentação hello ou a Ajuda online para o sistema operacional de saudação em execução na máquina virtual de saudação.
>
>

## <a name="create-an-endpoint"></a>Criar um ponto de extremidade
1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **máquinas virtuais**e clique em nome de saudação da máquina virtual de saudação que você deseja tooconfigure.
3. Clique em **pontos de extremidade** em Olá **configurações** grupo. Olá **pontos de extremidade** página lista todos os pontos de saudação atual para a máquina virtual de saudação. (Este exemplo é uma VM do Windows. Uma VM do Linux por padrão mostrará um ponto de extremidade para SSH.)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Pontos de extremidade](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Na barra de comandos Olá acima as entradas de ponto de extremidade de saudação, clique em **adicionar**.
5. Em Olá **Adicionar ponto de extremidade** página, digite um nome para o ponto de extremidade de saudação em **nome**.
6. Em **Protocolo**, escolha **TCP** ou **UDP**.
7. Em **porta pública**, digite Olá número da porta para tráfego de entrada de saudação de saudação à Internet. Em **porta privada**, digite Olá número da porta na qual Olá máquina virtual está escutando. O número de porta pode ser diferente. Certifique-se de que Olá firewall na máquina virtual de saudação foi configurado tooallow Olá tráfego toohello protocolo correspondente (na etapa 6) e porta privada.
10. Clique em **OK**.

novo ponto de extremidade de saudação será listado na Olá **pontos de extremidade** página.

![Criação de ponto de extremidade com êxito](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Gerenciar Olá ACL em um ponto de extremidade
conjunto de saudação toodefine de computadores que podem enviar o tráfego, Olá ACL em um ponto de extremidade pode restringir o tráfego com base no endereço IP de origem. Siga estas etapas tooadd, modificar ou remover uma ACL em um ponto de extremidade.

> [!NOTE]
> Se o ponto de extremidade de saudação é parte de um conjunto com balanceamento de carga, qualquer alteração feita toohello ACL em um ponto de extremidade são aplicadas tooall pontos de extremidade no conjunto de saudação.
>
>

Se a máquina virtual de saudação estiver em uma rede virtual do Azure, recomendamos grupos de segurança de rede em vez de ACLs. Para obter detalhes, veja [Sobre os grupos de segurança de rede](../articles/virtual-network/virtual-networks-nsg.md).

1. Se você ainda não fez isso, entre no toohello portal do Azure.
2. Clique em **máquinas virtuais**e clique em nome de saudação da máquina virtual de saudação que você deseja tooconfigure.
3. Clique em **Pontos de Extremidade**. Na lista de saudação, selecione o ponto de extremidade Olá apropriado. a lista ACL de saudação é final Olá Olá página.

   ![Detalhes específicos de ACL](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Use linhas em Olá lista tooadd, excluir ou editar regras para uma ACL e alterar sua ordem. Olá **sub-rede remota** valor é um intervalo de endereços IP para o tráfego de entrada de saudação da Internet que Olá toopermit de usos do balanceador de carga do Azure ou negar o tráfego de saudação com base em seu endereço IP de origem. Ser-se de intervalo de endereços IP de toospecify de saudação no formato CIDR, também conhecido como formato de prefixo de endereço. Um exemplo é `10.1.0.0/8`.

 ![Nova entrada ACL](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


Você pode usar regras tooallow somente do tráfego de computadores específicos correspondente tooyour computadores no tráfego de Internet ou toodeny Olá em intervalos de endereço específico, conhecido.

Olá regras são avaliadas na ordem começando com a primeira regra de saudação e terminando com a regra de saudação do último. Isso significa que as regras devem ser ordenadas de menos restritivo toomost restritiva. Para obter exemplos e saber mais, veja [O que é uma Lista de Controle de Acesso de rede](../articles/virtual-network/virtual-networks-acl.md).
