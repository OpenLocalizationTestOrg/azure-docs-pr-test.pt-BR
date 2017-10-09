Nesta etapa, você deve testar ouvinte do grupo de disponibilidade de saudação usando um aplicativo cliente que está em execução no hello mesma rede.

Conectividade de cliente tem Olá requisitos a seguir:

* Ouvinte de toohello de conexões de cliente deve vir de máquinas que residem em um serviço de nuvem diferente Olá um hosts Olá sempre em réplicas de disponibilidade.
* Se Olá sempre em réplicas estiverem em sub-redes diferentes, os clientes deverão especificar *MultisubnetFailover = True* na cadeia de caracteres de conexão de saudação. Isso resulta de condição em paralelo conexão tentativas tooreplicas em Olá várias sub-redes. Observe que esse cenário inclui uma implantação de grupo de disponibilidade do AlwaysOn entre regiões.

Um exemplo é tooconnect toohello ouvinte uma saudação VMs em Olá mesma rede virtual do Azure (mas não um que hospeda uma réplica). Uma maneira fácil de toocomplete este teste é o ouvinte do grupo de disponibilidade do SQL Server Management Studio toohello tootry tooconnect. Outro método simple é toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), da seguinte maneira:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Se for Olá EndpointPort valor *1433*, não é necessário toospecify na chamada de saudação. Olá chamada anterior também pressupõe máquina cliente Olá é toohello ingressado no mesmo domínio e o chamador Olá recebeu permissões no banco de dados de saudação usando a autenticação do Windows.
> 
> 

Quando você testar o ouvinte Olá, ser toofail certeza sobre toomake de grupo de disponibilidade de saudação se que os clientes podem se conectar a toohello ouvinte entre failovers.

