## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Como toocreate uma VNet clássica usando a CLI do Azure
Você pode usar o hello CLI do Azure toomanage seus recursos do Azure de saudação de prompt de comando de qualquer computador que executa o Windows, Linux ou OSX. toocreate uma rede virtual usando Olá CLI do Azure, siga as etapas de saudação abaixo.

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../articles/cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **criar redes de rede do azure** comando toocreate uma rede virtual e uma sub-rede, conforme mostrado abaixo. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Saída esperada:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Nome da saudação VNet toobe criado. Para o nosso cenário, *TestVNet*
   * **-e (ou --address-space)**. Espaço de endereço da rede virtual. Para o nosso cenário, *192.168.0.0*
   * **-i (ou -cidr)**. Máscara de rede no formato CIDR. Para o nosso cenário, *16*.
   * **-n (ou --subnet-name**). Nome da sub-rede primeiro hello. Para o nosso cenário, *FrontEnd*.
   * **-p (ou --subnet-start-ip)**. Endereço IP inicial da sub-rede ou espaço de endereço da sub-rede. Em nosso cenário, *192.168.1.0*.
   * **-r (ou --subnet-cidr)**. Máscara de rede no formato CIDR para a sub-rede. Para o nosso cenário, *24*.
   * **-l (ou --location)**. Região do Azure onde Olá rede virtual será criado. Para o nosso cenário, *Central US*.
3. Executar Olá **sub-rede da rede virtual de rede do azure criar** comando toocreate uma sub-rede, conforme mostrado abaixo. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Aqui está a saída Olá esperado para o comando de saudação acima:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (ou --vnet-name**. Nome da saudação redes onde sub-rede Olá será criado. Para o nosso cenário, *TestVNet*.
   * **-n (or --name)**. Nome da nova subrede hello. Para o nosso cenário, *BackEnd*.
   * **-a (ou --address-prefix)**. Bloco CIDR da sub-rede. Para o nosso cenário, *192.168.2.0/24*.
4. Executar Olá **Mostrar de rede virtual de rede do azure** comando tooview propriedades Olá Olá nova rede virtual, conforme mostrado abaixo.
   
            azure network vnet show
   
    Aqui está a saída Olá esperado para o comando de saudação acima:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

