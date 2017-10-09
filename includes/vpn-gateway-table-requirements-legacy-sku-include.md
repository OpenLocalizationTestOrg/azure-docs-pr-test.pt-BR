Olá tabela listas Olá requisitos para gateways PolicyBased e RouteBased VPN a seguir. Esta tabela se aplica a saudação tooboth Gerenciador de recursos e modelos de implantação clássico. Para o modelo clássico Olá gateways VPN PolicyBased são Olá mesmo como gateways estáticos e gateways de rota são Olá mesmo como gateways dinâmicos.

|  | **Gateway Básico de VPN PolicyBased** | **Gateway Básico de VPN RouteBased** | **Gateway Padrão de VPN RouteBased** | **Gateway de Alto Desempenho de VPN RouteBased** |
| --- | --- | --- | --- | --- |
| **Conectividade site a site (S2S)** |Configuração de VPN PolicyBased |Configuração de VPN RouteBased |Configuração de VPN RouteBased |Configuração de VPN RouteBased |
| **Conectividade P2S (Ponto a Site**) |Sem suporte |Com suporte (pode coexistir com S2S) |Com suporte (pode coexistir com S2S) |Com suporte (pode coexistir com S2S) |
| **Método de autenticação** |Chave pré-compartilhada |Chave pré-compartilhada para conectividade S2S, Certificados para conectividade P2S |Chave pré-compartilhada para conectividade S2S, Certificados para conectividade P2S |Chave pré-compartilhada para conectividade S2S, Certificados para conectividade P2S |
| **Número máximo de conexões S2S** |1 |10 |10 |30 |
| **Número máximo de conexões P2S** |Sem suporte |128 |128 |128 |
| **Suporte ao roteamento ativo (BGP)** |Sem suporte |Sem suporte |Suportado |Suportado |

