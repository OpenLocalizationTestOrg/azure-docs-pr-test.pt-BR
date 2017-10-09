Uma zona DNS é usado toohost Olá registros DNS para um domínio específico. toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio. Cada registro DNS para seu domínio é criado dentro dessa zona DNS.

Por exemplo, domínio Olá 'contoso.com' pode conter vários registros DNS, como mail.contoso.com (para um servidor de email) e www.contoso.com (para um site da web).

Ao criar uma zona DNS no DNS do Azure:

* nome de saudação da zona Olá deve ser exclusivo dentro do grupo de recursos de saudação e zona de saudação não deve existir. Olá, caso contrário, haverá falha na operação.
* saudação de mesmo nome da zona pode ser reutilizado em outro grupo de recursos ou uma assinatura do Azure diferente.
* Onde várias zonas compartilham hello mesmo nome, cada instância é atribuída endereços de servidor de nome diferente. Apenas um conjunto de endereços pode ser configurado com o registrador de nome de domínio de saudação.

> [!NOTE]
> Você não possuem tooown um nome de domínio toocreate uma zona DNS com esse nome de domínio DNS do Azure. No entanto, é necessário servidores de nome tooown Olá domínio tooconfigure Olá DNS do Azure como Olá servidores de nome correto para nome de domínio Olá registrador de nomes de domínio hello.
> 
> Para obter mais informações, consulte [delegar tooAzure um domínio DNS](../articles/dns/dns-domain-delegation.md).
