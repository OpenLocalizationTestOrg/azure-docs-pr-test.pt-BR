Quando você criar um gateway de rede virtual, é necessário que você deseja toouse SKU do gateway de saudação do toospecify. Selecione Olá SKUs que atendem suas necessidades com base nos tipos de saudação de SLAs, taxas de transferência, recursos e cargas de trabalho.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Produção *versus* Cargas de Trabalho de Desenvolvimento e Teste

Devido a diferenças de toohello nos SLAs e conjuntos de recursos, é recomendável seguir SKUs para a produção de hello *versus* desenvolvimento de teste:

| **Carga de trabalho**                       | **SKUs**               |
| ---                                | ---                    |
| **Produção, cargas de trabalho críticas** | VpnGw1, VpnGw2, VpnGw3 |
| **Teste de desenvolvimento ou prova de conceito**   | Basic                  |
|                                    |                        |

Se você estiver usando Olá antigo SKUs, recomendações de SKU de produção de hello são padrão e SKUs de alto desempenho. Para obter informações sobre Olá antigos SKUs, consulte [SKUs de Gateway (SKUs herdados)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Conjuntos de recursos do SKU de gateway

Olá novo gateway SKUs simplificar Olá conjuntos de recursos oferecidos em gateways hello:

| **SKU**| **Recursos**|
| ---    | ---         |
|**Básico**   | **VPN baseada em rota**: 10 túneis com P2S<br><br>**VPN baseada em políticas:** (IKEv1): 1 túnel; sem P2S|
| **VpnGw1, VpnGw2 e VpnGw3** | **VPN com base em rota**: backup túneis too30 (*), P2S, BGP, política de IPsec/IKE ativo-ativo e personalizada, coexistência VPN/rota expressa |
|        |             |

(*) Você pode configurar tooconnect "PolicyBasedTrafficSelectors" um baseadas em rota VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple local firewall baseado em política de dispositivos. Consulte também[toomultiple de gateways de VPN conectar dispositivos VPN baseado em políticas usando o PowerShell local](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter detalhes.

###  <a name="resize"></a>Redimensionamento de SKUs de gateway

1. Você pode redimensionar entre as SKUs VpnGw1, VpnGw2 e VpnGw3.
2. Ao trabalhar com o gateway de antigo Olá SKUs, você pode redimensionar entre Basic, Standard e SKUs de alto desempenho.
2. Você **não é possível** redimensionar de SKUs Basic/Standard/HighPerformance toohello SKUs do novo VpnGw2/VpnGw1/VpnGw3. Em vez disso, você deve [migrar](#migrate) toohello SKUs de novo.

###  <a name="migrate"></a>Migrando do antigo toohello de SKUs SKUs novo

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
