## <a name="route-tables"></a>Tabelas de rotas
Recursos de tabela de rota contém rotas usadas toodefine como fluxos de tráfego dentro de sua infraestrutura do Azure. Você pode usar toosend de rotas (UDR) definidos pelo usuário em todo o tráfego de um determinada sub-rede tooa dispositivo virtual, como um sistema de detecção firewall ou invasão (IDS). Você pode associar um toosubnets da tabela de rota. 

Tabelas de rotas contêm Olá propriedades a seguir.

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **routes** |Coleção de usuário definida rotas na tabela de rotas Olá |veja [rotas definidas pelo usuário](#User-defined-routes) |
| **sub-redes** |Coleção de tabela de rotas Olá sub-redes é aplicada muito|veja [sub-redes](#Subnets) |

### <a name="user-defined-routes"></a>rotas definidas pelo usuário
Você pode criar toospecify UDRs onde o tráfego deve ser enviado, com base em seu endereço de destino. Você pode pensar em uma rota como definição de gateway padrão de saudação com base no endereço de destino de saudação de um pacote de rede.

UDRs contêm Olá propriedades a seguir. 

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **addressPrefix** |Prefixo de endereço ou endereço IP completo para o destino de saudação |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Tipo de dispositivo Olá tráfego será enviado muito|Dispositivo Virtual, Gateway de VPN, Internet |
| **nextHopIpAddress** |Endereço IP do próximo salto de saudação |192.168.1.4 |

Exemplo de tabela de rotas no formato JSON:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Recursos adicionais
* Obtenha mais informações sobre [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).
* Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) para tabelas de rotas.
* Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) para o usuário definido rotas (UDRs).

