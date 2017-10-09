

![Máquinas virtuais em um serviço de nuvem autônomo](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Se você colocar as máquinas virtuais em uma rede virtual, você pode decidir quantos serviços de nuvem que você deseja toouse para conjuntos de disponibilidade e balanceamento de carga. Além disso, você pode organizar as máquinas virtuais de saudação em sub-redes no hello mesma maneira que o local de rede e conecte-se Olá tooyour de rede virtual local rede. Aqui está um exemplo:

![Máquinas virtuais em uma rede virtual](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Redes virtuais são Olá recomendado maneira tooconnect as máquinas virtuais no Azure. Olá prática recomendada é tooconfigure cada camada do seu aplicativo em um serviço de nuvem separado. No entanto, talvez seja necessário toocombine algumas máquinas virtuais de diferentes níveis de aplicativos em Olá mesmo serviço tooremain no máximo Olá 200 dos serviços de nuvem por assinatura na nuvem. tooreview este e outros limites, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Conectar VMs em uma rede virtual
tooconnect as máquinas virtuais em uma rede virtual:

1. Criar rede virtual Olá no hello [portal do Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) e especifique 'implantação clássico'.
2. Criar conjunto de saudação de serviços em nuvem para sua implantação tooreflect seu design para conjuntos de disponibilidade e balanceamento de carga. No portal do Azure de Olá, clique em **Novo > computação > serviço de nuvem** para cada serviço de nuvem.

  Como preencher detalhes do serviço de nuvem hello, escolha Olá mesmo _grupo de recursos_ usado com a rede virtual hello.

3. toocreate virtual cada nova máquina, clique em **Novo > computação**, em seguida, selecione Olá imagem VM apropriada da saudação **aplicativos em destaque**.

  Na VM de saudação **Noções básicas de** folha, escolha Olá mesmo _grupo de recursos_ usado com a rede virtual hello.

  ![Folha Noções básicas da VM ao usar uma rede virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. Como preencher Olá VM **configurações**, escolha Olá correto _serviço de nuvem_ ou _rede virtual_ para Olá VM.

  Azure selecionará Olá outro item com base em sua seleção.

  ![Folha Configurações da VM ao usar uma rede virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Conectar VMs em um serviço de nuvem autônomo
tooconnect as máquinas virtuais em um serviço de nuvem autônomo:

1. Criar serviço de nuvem Olá no hello [portal do Azure](http://portal.azure.com). Clique em **Novo > Computação > Serviço de nuvem**. Ou, você pode criar serviço em nuvem para sua implantação hello quando você criar sua primeira máquina virtual.
2. Ao criar máquinas virtuais de saudação, escolha Olá mesmo grupo de recursos usado com o serviço de nuvem hello.

  ![Adicionar um serviço de nuvem existente do virtual machine tooan](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Como preencher detalhes VM hello, escolha o nome de saudação do serviço de nuvem criado na primeira etapa de saudação.

  ![Selecionar um serviço de nuvem para uma máquina virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
