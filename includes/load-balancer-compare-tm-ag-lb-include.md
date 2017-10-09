## <a name="load-balancer-differences"></a>Diferenças do balanceador de carga

Há diferentes opções toodistribute o tráfego usando o Microsoft Azure. Essas opções funcionam de forma diferente uma da outra, com conjuntos diferentes de recursos e permitindo cenários diferentes. Cada uma pode ser usada isoladamente ou em combinação.

* **O balanceador de carga do Azure** funciona na camada de transporte da saudação (camada 4 na pilha de referência de rede Olá OSI). Ele fornece o nível da rede de distribuição do tráfego em instâncias de um aplicativo em execução no hello mesmo data center do Azure.
* **Application Gateway** funciona na camada de aplicativo hello (camada 7 na pilha de referência de rede Olá OSI). Ele atua como um serviço de proxy reverso, encerrando a conexão de cliente hello e encaminhamento de solicitações de pontos de extremidade tooback-end.
* **Gerenciador de tráfego** funciona no nível DNS de saudação.  Ele usa DNS respostas toodirect do usuário final tráfego tooglobally distribuída pontos de extremidade. Clientes, em seguida, conecte-se pontos de extremidade toothose diretamente.

Olá, a tabela a seguir resume os recursos de saudação oferecidos por cada serviço:

| O Barramento de | Azure Load Balancer | Gateway de Aplicativo | Gerenciador de Tráfego |
| --- | --- | --- | --- |
| Tecnologia |Nível de transporte (Camada 4) |Nível de aplicativo (Camada 7) |Nível de DNS |
| Protocolos de aplicativo com suporte |Qualquer |HTTP, HTTPS e WebSockets |Qualquer um (um ponto de extremidade HTTP é exigido para monitoramento do ponto de extremidade) |
| Pontos de extremidade |VMs do Azure e instâncias de função dos Serviços de Nuvem |Qualquer endereço IP interno do Azure, endereço IP de internet pública, VM do Azure ou Serviço de Nuvem do Azure |VMs do Azure, Serviços de Nuvem, Aplicativos Web do Azure e pontos de extremidade externos |
| Suporte à rede virtual |Pode ser usado para aplicativos voltados para a Internet e internos (rede virtual) |Pode ser usado para aplicativos voltados para a Internet e internos (rede virtual) |Suporte apenas para aplicativos voltados para a Internet |
| Monitoramento do ponto de extremidade |Tem suporte por meio de investigações |Tem suporte por meio de investigações |Tem suporte por meio de HTTP/HTTPS GET |

Azure balanceador de carga e tooendpoints de tráfego de rede do Application Gateway rota, mas eles têm toohandle de tráfego de toowhich de cenários de uso diferentes. Olá tabela a seguir ajuda a diferença de saudação Noções básicas sobre entre balanceadores de carga dois hello:

| Tipo | Azure Load Balancer | Gateway de Aplicativo |
| --- | --- | --- |
| Protocolos |UDP/TCP |HTTP, HTTPS e WebSockets |
| Reserva de IP |Suportado |Sem suporte |
| Modo de balanceamento de carga |5 tuplas (IP de origem, porta de origem, IP de destino, porta de destino, tipo de protocolo) |Round Robin<br>Roteamento com base na URL |
| Modo de balanceamento de carga (IP de origem/sessões complexas) |Duas tuplas (IP de origem e IP de destino), 3 tuplas (IP de origem, IP de destino e porta). Pode ser dimensionado para cima ou para baixo com base no número de saudação de máquinas virtuais |Afinidade baseada em cookie<br>Roteamento com base na URL |
| Investigações de integridade |Padrão: intervalo de investigação - 15 segundos. Retirada da rotação: 2 falhas contínuas. Oferece suporte a investigações definidas pelo usuário |Intervalo de investigação ociosa de 30 segundos. Retirado após 5 falhas consecutivas do tráfego ativo ou uma única falha de investigação no modo ocioso. Oferece suporte a investigações definidas pelo usuário |
| Descarregamento de SSL |Sem suporte |Suportado |
| Roteamento baseado em URL | Sem suporte | Suportado|
| Política SSL | Sem suporte | Suportado|
