### <a name="record-names"></a>Nomes de registros

No DNS do Azure, os registros são especificados usando nomes relativos. Um *totalmente qualificado* nome de domínio (FQDN) inclui o nome da zona hello, enquanto um *relativo* nome não. Por exemplo, o nome de registro relativo de Olá www na zona de saudação 'contoso.com' fornece o nome de registro totalmente qualificado de saudação 'www.contoso.com'.

Um *ápice* é um registro DNS raiz hello (ou *ápice*) de uma zona DNS. Por exemplo, na zona DNS hello "contoso.com", um registro ápice também tem nome totalmente qualificado de saudação 'contoso.com' (isso às vezes é chamado um *naked* domínio).  Por convenção, Olá nome relativo ' @' é usado toorepresent registros ápice.

### <a name="record-types"></a>Tipos de registro

Cada registro DNS tem um nome e um tipo. Os registros são organizados em vários tipos de acordo com o toohello dados que eles contêm. tipo mais comum de saudação é um registro 'A', que mapeia um endereço IPv4 de tooan do nome. Outro tipo comum é um registro de 'MX', que mapeia um servidor de email de tooa do nome.

O DNS do Azure dá suporte a todos os tipos de registro DNS comuns: A, AAAA, CNAME, MX, NS, PTR, SOA, SRV e TXT. Observe que [registros SPF são representados usando registros TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Conjuntos de registros

Às vezes você precisa toocreate mais de um registro DNS com um determinado nome e tipo. Por exemplo, suponha que Olá 'www.contoso.com' web site hospedado em dois endereços IP. site Olá requer dois registros, um para cada endereço IP. Aqui está um exemplo de um conjunto de registros:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

O DNS do Azure gerencia todos os registros DNS usando *conjuntos de registros*. Um conjunto de registros (também conhecido como um *recurso* registrar conjunto) é Olá conjunto de registros DNS em uma zona com hello mesmo nome e são de saudação mesmo tipo. A maioria dos conjuntos de registros contém um único registro. No entanto, os exemplos como Olá acima, em que um conjunto de registros contém mais de um registro, não são incomuns.

Por exemplo, suponha que você já tiver criado um registro "www" na zona hello "contoso.com", apontando toohello IP endereços '134.170.185.46' (Olá primeiro registro acima).  toocreate Olá segundo registro você adicionaria que registram o registro existente toohello definido, em vez de criar um conjunto de registros adicional.

Olá SOA e tipos de registro CNAME são exceções. padrões DNS Olá não permitirem que vários registros com o mesmo nome para esses tipos de saudação, portanto, esses conjuntos de registros só podem conter um único registro.
