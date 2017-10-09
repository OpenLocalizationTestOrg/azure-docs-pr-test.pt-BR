## <a name="nic"></a>NIC
Um recurso de placa de interface de rede fornece conectividade tooan existente sub-rede em um recurso de rede virtual. Embora você possa criar uma NIC como um objeto autônomo, você precisa tooassociate-tooanother objeto tooactually fornecer conectividade. Uma NIC pode ser usado tooconnect tooa uma subrede VM, um endereço IP público ou um balanceador de carga.  

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **virtualMachine** |Saudação VM NIC está associada. |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |Endereço MAC para Olá NIC |qualquer valor entre 4 e 30 |
| **networkSecurityGroup** |NSG associado toohello NIC |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Configurações de DNS para Olá NIC |veja [PIP](#Public-IP-address) |

Uma placa de Interface de rede ou NIC, representa uma interface de rede que pode ser associado tooa VM (máquina virtual). Uma VM pode ter uma ou mais NICs.

![NICs em uma única VM](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>Configurações de IP
NICs têm um objeto filho chamado **ipConfigurations** contendo Olá propriedades a seguir:

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **subnet** |Olá sub-rede NIC está conectado ao. |/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |Endereço IP para Olá NIC na sub-rede Olá |10.0.0.8 |
| **privateIPAllocationMethod** |Método de alocação de IP |Dinâmico ou estático |
| **enableIPForwarding** |Se Olá NIC pode ser usado para roteamento |true ou false |
| **primary** |Se Olá NIC é Olá NIC primário para Olá VM |true ou false |
| **publicIPAddress** |PIP associado Olá NIC |consulte [Configurações DNS](#DNS-settings) |
| **loadBalancerBackendAddressPools** |Faça a saudação de pools de endereço final que NIC está associada | |
| **loadBalancerInboundNatRules** |NIC está associada a saudação de regras carga balanceador NAT de entrada | |

Endereço IP de público exemplo, no formato JSON:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Recursos adicionais
* Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) para as NICs.

