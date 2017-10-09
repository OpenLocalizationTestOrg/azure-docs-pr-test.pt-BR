## <a name="scenario"></a>Cenário
Uma VM com uma única NIC é a rede virtual tooa criado e conectado. Olá VM requer três diferentes *privada* IP endereços e dois *pública* endereços IP. endereços IP Hello recebem toohello as configurações de IP a seguir:

* **IPConfig-1:** atribui um endereço IP privado *estático* e um endereço IP público *estático*.
* **IPConfig-2:** atribui um endereço IP privado *estático* e um endereço IP público *estático*.
* **IPConfig-3:** atribui um endereço IP privado *estático* e nenhum endereço IP público.
  
    ![Vários endereços IP](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

as configurações de IP Hello são associado toohello NIC quando Olá NIC é criada e hello NIC é anexado toohello VM quando Olá VM é criada. tipos de saudação de endereços IP usados para o cenário de saudação são para fins ilustrativos. Você pode atribuir quaisquer tipos de atribuição e de endereço IP necessários.

> [!NOTE]
> Embora Olá etapas neste artigo atribui todos os tooa de configurações de IP NIC único, você também pode atribuir várias tooany de configurações de IP NIC em uma VM multi-NIC. toolearn como toocreate uma VM com várias NICs, ler Olá [criar uma VM com várias NICs](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) artigo.
