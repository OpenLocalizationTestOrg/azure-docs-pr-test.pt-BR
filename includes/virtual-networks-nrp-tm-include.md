## <a name="traffic-manager-profile"></a>Perfil de Gerenciador de Tráfego
O traffic manager e seus recursos de ponto de extremidade filho habilitar tooendpoints de roteamento de DNS no Azure e fora do Azure. Essa distribuição de tráfego é controlada por métodos de política de roteamento. Traffic manager também permite toobe de integridade do ponto de extremidade é monitorado e tráfego desviado adequadamente com base na integridade de saudação de um ponto de extremidade. 

| Propriedade | Descrição |
| --- | --- |
| **trafficRoutingMethod** |os valores possíveis são *Desempenho*, *Ponderado* e *Prioridade* |
| **dnsConfig** |FQDN para o perfil de saudação |
| **Protocolo** |protocolo de monitoramento, os valores possíveis são *HTTP* e *HTTPS* |
| **Porta** |porta de monitoramento |
| **Caminho** |caminho de monitoramento |
| **Pontos de extremidade** |contêiner para recursos de ponto de extremidade |

### <a name="endpoint"></a>Ponto de extremidade
Um ponto de extremidade é um recurso de filho de um perfil de Gerenciador de Tráfego. Representa um serviço ou tráfego de usuário de toowhich de ponto de extremidade da web é distribuído com base na política de saudação configurada no hello recurso de perfil do Traffic Manager. 

| Propriedade | Descrição |
| --- | --- |
| **Tipo** |Olá tipo de ponto de extremidade hello, os valores possíveis são *Azure ponto*, *ponto de extremidade externo*, e *aninhados ponto de extremidade* |
| **targetResourceId** |endereço IP público de um ponto de extremidade de serviço ou da Web. Isso pode ser um ponto de extremidade do Azure ou externo. |
| **Peso** |peso de ponto de extremidade usado no gerenciamento de tráfego. |
| **Prioridade** |prioridade de ponto de extremidade Olá toodefine usado uma ação de failover |

Exemplo do Gerenciador de Tráfego no formato Json: 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Recursos adicionais
Leia a [documentação da API REST para o Gerenciador de Tráfego](https://msdn.microsoft.com/library/azure/mt163664.aspx) para saber mais.

