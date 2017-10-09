## <a name="network-security-group"></a>Grupo de Segurança de Rede
Um recurso NSG permite a criação de saudação do limite de segurança para cargas de trabalho, com a implementação de permissão e negação de regras. Essas regras podem ser aplicadas tooa VM, uma NIC ou uma sub-rede.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **sub-redes** |Lista de ids de subrede Olá NSG é aplicada ao. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Lista de regras de segurança que compõem a saudação NSG |Veja [Regra de segurança](#Security-rule) abaixo |
| **defaultSecurityRules** |Lista de regras de segurança padrão presentes em cada NSG |Veja [Regras de segurança padrão](#Default-security-rules) abaixo |

* **Regra de segurança** - um NSG um pode ter várias regras de segurança definidas. Cada regra pode permitir ou negar diferentes tipos de tráfego.

### <a name="security-rule"></a>Regra de segurança
Uma regra de segurança é um recurso filho de um NSG que contém as propriedades de saudação abaixo.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **description** |Descrição para a regra de saudação |Permitir tráfego de entrada para todas as VMs na sub-rede X |
| **protocol** |Toomatch de protocolo para a regra de saudação |TCP, UDP ou * |
| **sourcePortRange** |Origem toomatch de intervalo de porta para a regra de saudação |80, 100-200, * |
| **destinationPortRange** |Toomatch de intervalo de porta de destino para a regra de saudação |80, 100-200, * |
| **sourceAddressPrefix** |Toomatch de prefixo de endereço de origem para regra de saudação |10.10.10.1, 10.10.10.0/24, Rede Virtual |
| **destinationAddressPrefix** |Toomatch de prefixo de endereço de destino para a regra de saudação |10.10.10.1, 10.10.10.0/24, Rede Virtual |
| **direction** |Direção do tráfego toomatch para regra de saudação |entrada ou saída |
| **prioridade** |Prioridade de regra de saudação. As regras são verificadas em ordem de prioridade, e depois que uma regra é aplicada, nenhuma outra regra é testada quanto à correspondência. |10, 100, 65000 |
| **access** |Tipo de acesso tooapply se corresponder a regra de saudação |permitir ou negar |

Exemplo de NSG no formato JSON:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Regras de segurança padrão

Regras de segurança padrão têm Olá mesmas propriedades disponíveis nas regras de segurança. Elas existem tooprovide a conectividade básica entre os recursos que têm toothem NSGs aplicados. Certifique-se de que você sabe quais [regras de segurança padrão](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existem.

### <a name="additional-resources"></a>Recursos adicionais
* Obtenha mais informações sobre [NSGs](../articles/virtual-network/virtual-networks-nsg.md).
* Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) para NSGs.
* Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) para regras de segurança.
