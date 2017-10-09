## <a name="public-ip-address"></a>Endereço IP público
Um recurso de endereço IP público fornece um endereço IP para Internet dinâmico ou reservado. Embora você possa criar um endereço IP público como um objeto autônomo, você precisa tooassociate-tooanother objeto tooactually usar endereço hello. Você pode associar um balanceador de carga do tooa de endereço IP público, o gateway de aplicativo ou uma NIC tooprovide Internet acessar toothose os recursos.  

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **publicIPAllocationMethod** |Define se o endereço IP de saudação é *estático* ou *dinâmico*. |estático, dinâmico |
| **idleTimeoutInMinutes** |Define o limite de tempo ocioso hello, com um valor padrão de 4 minutos. Se não há mais pacotes para uma determinada sessão for recebida dentro desse período, a sessão de saudação é encerrada. |qualquer valor entre 4 e 30 |
| **ipAddress** |Endereço IP atribuído tooobject. Essa é uma propriedade somente leitura. |104.42.233.77 |

### <a name="dns-settings"></a>Configurações DNS
Endereços IP públicos tem um objeto filho chamado **dnsSettings** contendo Olá propriedades a seguir:

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **domainNameLabel** |Host nomeado usado para resolução de nomes. |www, ftp, vm1 |
| **fqdn** |Nome totalmente qualificado para o IP público hello. |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Nome de domínio totalmente qualificado que resolve o endereço IP de toohello e está registrado no DNS como um registro PTR. |www.contoso.com. |

Endereço IP de público exemplo, no formato JSON:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Recursos adicionais
* Obtenha mais informações sobre [endereços IP públicos](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Saiba mais sobre [endereços IP públicos em nível de instância](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) endereços IP públicos.

