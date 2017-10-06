---
title: "AAA \"conexões híbridas do serviço de aplicativo do Azure | Microsoft Docs\""
description: "Como toocreate e usar recursos de tooaccess de conexões híbridas em redes diferentes"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Conexões Híbridas do Serviço de Aplicativo do Azure #

## <a name="overview"></a>Visão geral ##

Conexões híbridas é um serviço no Azure, bem como um recurso de saudação do serviço de aplicativo do Azure.  Como um serviço tem uso e recursos além daqueles que serão utilizados na saudação do serviço de aplicativo do Azure.  toolearn mais sobre conexões híbridas e seu uso fora de saudação do serviço de aplicativo do Azure você pode iniciar aqui, [as conexões de retransmissão híbridas do Azure][HCService]

Dentro de saudação do serviço de aplicativo do Azure, conexões híbridas podem ser usado tooaccess recursos do aplicativo em outras redes. Ele fornece acesso a partir de seu ponto de extremidade de aplicativo do aplicativo tooan.  Ele não permite que um recurso alternativo tooaccess seu aplicativo.  Como usado no saudação do serviço de aplicativo, cada conexão híbrida correlaciona tooa combinação única de host e porta do TCP.  Isso significa que esse ponto de extremidade de conexão do hello híbrida pode ser em qualquer sistema operacional e qualquer aplicativo fornecido que está atingindo uma porta de escuta TCP. Conexões híbridas não souber ou importantes para o protocolo de aplicativo hello é ou o que você está acessando.  Ele simplesmente fornece acesso à rede.  


## <a name="how-it-works"></a>Como funciona ##
recurso de conexões híbridas Olá consiste em duas chamadas de saída tooService retransmissão de barramento.  Há uma conexão de uma biblioteca no host de saudação em que seu aplicativo está em execução no serviço de aplicativo hello e, em seguida, há uma conexão de retransmissão de barramento de tooService Olá Manager(HCM) de Conexão híbrida.  Olá HCM é um serviço de retransmissão que você implanta em Olá hospedagem de rede 

Por meio de saudação duas conexões ingressado no seu aplicativo tenha um tooa de túnel TCP fixa combinação de host: porta em hello outro lado da saudação HCM.  conexão Olá usa o protocolo TLS 1.2 para segurança e chaves SAS para autenticação/autorização.    

![][1]

Quando seu aplicativo faz uma solicitação DNS que corresponde a um ponto de extremidade de Conexão híbrida de configurar e tráfego TCP de saída Olá será redirecionado para baixo de conexão do hello híbrida.  

> [!NOTE]
> Isso significa que você deve tentar tooalways use um nome DNS para sua Conexão híbrida.  Alguns softwares cliente fazer uma pesquisa de DNS se o ponto de extremidade de saudação usa um endereço IP em vez disso.
>
>

Há dois tipos de conexões híbridas, conexões híbridas novo Olá que são oferecidos como um serviço de retransmissão do Azure e Olá as conexões híbridas BizTalk mais antigos.  Hello as conexões híbridas BizTalk mais antigos são chamados tooas as conexões híbridas clássico no portal de saudação.  Há mais informações posteriormente neste documento sobre elas.

### <a name="app-service-hybrid-connection-benefits"></a>Benefícios das conexões híbridas do Serviço de Aplicativo ###

Há inúmeras vantagens toohello híbrida conexões recurso incluindo

- Os aplicativos podem acessar serviços e sistemas locais com segurança
- Olá recurso não exige um ponto de extremidade acessível da internet
- é rápido e fácil tooset backup  
- combinação de host: porta única tooa que é um aspecto de segurança excelente corresponde a cada conexão híbrida
- normalmente não é necessário buracos firewall como conexões Olá são todas as saídas através das portas padrão da web
- porque o recurso Olá é o nível de rede que também significa que se trata de idioma desconhecido toohello usado pela sua tecnologia de aplicativo e hello usada pelo ponto de extremidade de saudação
- ele pode ser usado tooprovide acesso em várias redes de um único aplicativo 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Coisas que você não pode fazer com as Conexões Híbridas ###

Há algumas coisas que você não pode fazer com as conexões híbridas e elas incluem:

- montagem de unidade
- usar UDP
- acessar serviços baseados em TCP que usam portas dinâmicas como um Modo passivo de FTP ou Modo passivo estendido
- suporte a LDAP, já que isso às vezes requer UDP
- suporte ao Active Directory

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Adicionar e criar uma Conexão Híbrida em seu aplicativo ##

Conexões híbridas podem ser criadas por meio do portal aplicativo hello ou no portal de serviço de Conexão híbrida hello.  É altamente recomendável que você use Olá toocreate portal de aplicativo hello conexões híbridas desejar toouse com seu aplicativo.  toocreate uma Conexão híbrida vá toohello [portal do Azure] [ portal] e vá para hello da interface do usuário para seu aplicativo.  Selecione **Rede > Configurar seus pontos de extremidade de conexão híbrida**.  Aqui você pode ver conexões híbridas Olá configurados com seu aplicativo  

![][2]

tooadd uma nova Conexão híbrida, clique em Adicionar Conexão de híbrida.  saudação de interface do usuário que abre a lista conexões híbridas Olá que você criou.  tooadd uma ou mais delas tooyour aplicativo, clique em Olá que você deseja e pressione **adicionar selecionada conexão híbrida**.  

![][3]

Se você quiser toocreate uma Conexão híbrida novo, clique em **criar nova conexão de híbrida**.  Aqui você especifica o: 

- nome do ponto de extremidade
- nome do host do ponto de extremidade
- porta do ponto de extremidade
- namespace de barramento de serviço que você deseja toouse

![][4]

Cada conexão híbrida é o namespace do barramento de serviço tooa associado e cada namespace do barramento de serviço está em uma região do Azure.  É importante tootry e usar um serviço de namespace de barramento Olá mesma região do seu aplicativo, latência de rede induzido tooavoid.

Se você quiser tooremove sua conexão híbrida do seu aplicativo, clique com o botão direito nele e selecione **Disconnect**.  

Depois que uma conexão híbrida é adicionada tooyour web app, você pode ver detalhes sobre ele, simplesmente clicando nele.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Conexões Híbridas e Planos de Serviço de Aplicativo ##

Olá híbrida apenas conexões estabelecidas que agora você pode fazer são do hello novo híbrida.  Eles só estão disponíveis em SKUs de preço Básico, Standard, Premium e Isolado.  Há limites vinculados toohello preços do plano.  

| Plano de Preços | Número de conexões híbridas utilizáveis no plano de saudação |
|----|----|
| Basic | 5 |
| Standard | 25 |
| Premium | 200 |
| Isolado | 200 |

Como há restrições plano do serviço de aplicativo, também há UI Olá plano de serviço aplicativo que mostra quantas conexões híbridas estão sendo usadas e por quais aplicativos.  

![][6]

Assim como com a exibição do aplicativo hello, você pode ver detalhes sobre a conexão híbrida clicando nele.  Nas propriedades de saudação mostradas aqui, você pode ver todas as informações de saudação você tinha no modo de exibição de aplicativo hello, mas também pode ver quantos outros aplicativos no hello mesmo plano de serviço de aplicativo estão usando essa conexão híbrida.

![][7]

Embora não haja um limite no número de saudação de pontos de extremidade de conexão híbrida que podem ser usados em um plano de serviço de aplicativo, cada conexão híbrida usado pode ser usado em qualquer número de aplicativos no plano de serviço desse aplicativo.  Isso é toosay se eu tivesse 1 conexão híbrida usados em 5 aplicativos separados no meu plano de serviço de aplicativo, que é ainda apenas 1 conexão de híbrida.

Não há conexões de toohybrid um custo adicional além somente ser usados em Basic, Standard, Premium ou SKU isolado.  Para obter detalhes sobre preços de conexão híbrida, veja aqui: [Preços do Barramento de Serviço][sbpricing].

## <a name="hybrid-connection-manager"></a>Gerenciador de Conexão Híbrida ##

Para toowork de conexões híbrida é necessário um agente de retransmissão na rede de saudação que hospeda o ponto de extremidade de conexão híbrida.  Olá Gerenciador de Conexão híbrida (HCM) é chamado de que o agente de retransmissão.  Essa ferramenta pode ser baixada do hello **rede > configurar seus pontos de extremidade de conexão híbrida** a interface do usuário disponível no seu aplicativo hello [portal do Azure][portal].  

Essa ferramenta é executada no Windows Server 2008 R2 e versões posteriores do Windows.  Depois de instalado, Olá HCM é executado como um serviço.  Esse serviço se conecta a retransmissão de barramento de serviço tooAzure com base em pontos de extremidade de saudação configurado.  conexões de saudação do hello HCM são tooports saída 80 e 443.    

Olá HCM tem uma interface de usuário tooconfigure-lo.  Após Olá que HCM está instalado, você pode abrir a saudação da interface do usuário executando Olá HybridConnectionManagerUi.exe que se encontra no diretório de instalação do Gerenciador de Conexão híbrida hello.  Ela também pode ser facilmente acessada no Windows 10 digitando *Interface do usuário do Gerenciador de Conexões Híbridas* na caixa de pesquisa.  

Quando Olá HCM UI é iniciada, primeiro Olá você consulte é uma tabela que lista todas as conexões híbridas Olá configurados com esta instância do hello HCM.  Se você quiser toomake as alterações, você precisará tooauthenticate com o Azure. 

tooadd uma ou mais conexões híbridas tooyour HCM:

1. Iniciar Olá HCM UI
1. Clique em configurar outra conexão híbrida ![][8]

1. Entre com sua conta do Azure
1. Escolha uma subscrição
1. Clique em conexões híbridas de saudação deseja que este toorelay HCM![][9]

1. Clique em Salvar

Neste ponto, você verá as conexões híbridas Olá adicionado.  Também pode clicar em Olá configurado híbrida conexão e ver os detalhes sobre a conexão de saudação.

![][10]

Para que seu HCM toobe toosupport capaz de saudação conexões híbridas, que é configurado, ele precisa:

- TooAzure de acesso TCP por portas 80 e 443
- Ponto de extremidade de TCP acesso toohello híbrida conexão
- capacidade toodo DNS aparência no-break no host do ponto de extremidade de Olá Olá namespace de barramento de serviço do azure

Olá HCM aceita novas conexões híbridas, bem como conexões de híbrida do BizTalk mais antigas hello.

### <a name="redundancy"></a>Redundância ###

Cada HCM pode dar suporte a várias conexões híbridas.  Além disso, qualquer determinada conexão híbrida pode ter suporte de vários HCMs.  comportamento padrão de saudação é tooround tráfego robin Olá configurado HCMs para determinado ponto de extremidade.  Se desejar alta disponibilidade nas conexões híbridas da rede, basta instanciar vários HCMs em computadores separados. 

### <a name="manually-adding-a-hybrid-connection"></a>Adicionar uma conexão híbrida manualmente ###

Se desejar que alguém fora da sua assinatura toohost uma instância HCM para uma conexão híbrida determinado, você pode compartilhar com eles Olá a cadeia de caracteres de conexão de gateway para a conexão do hello híbrida.  Você pode ver isso nas propriedades de saudação de uma conexão híbrida na Olá [portal do Azure][portal]. toouse cadeia de caracteres, clique em Olá **configurar manualmente** botão no hello HCM e cole na cadeia de caracteres de conexão de gateway hello.


## <a name="troubleshooting"></a>Solucionar problemas ##

Quando a conexão híbrida é configurado com um aplicativo em execução e há pelo menos um HCM que tenha essa conexão híbrida configurado, Olá status indicará **conectado** no portal de saudação.  Se ele não indicar **conectado** significa que o seu aplicativo está inativo ou não é possível conectar seu HCM out tooAzure na porta 80 ou 443.  

motivo principal Olá para que os clientes não podem se conectar a tootheir de ponto de extremidade é porque o ponto de extremidade de saudação foi especificado usando um endereço IP em vez de um nome DNS.  Se seu aplicativo não é possível alcançar o ponto de extremidade de saudação desejado e você usou um endereço IP, alterne toousing um nome DNS válido no host Olá onde hello HCM está em execução.  Toocheck outras coisas são que Olá nome DNS seja resolvido corretamente no host de saudação onde hello HCM está em execução e se há conectividade de host Olá onde hello HCM está sendo executado o ponto de extremidade de conexão de híbrida toohello.  

É uma ferramenta de saudação do serviço de aplicativo que pode ser chamado do console de saudação chamado tcpping.  Essa ferramenta pode informar se você tiver o ponto de extremidade TCP de tooa acesso, mas não informa se você tiver o ponto de extremidade da conexão híbrida acesso tooa.  Quando usados no console de saudação em relação a um ponto de extremidade de conexão híbrida, um ping com êxito apenas informará que você tenha uma conexão híbrida configurado para o aplicativo que usa essa combinação de host: porta.  

## <a name="biztalk-hybrid-connections"></a>Conexões Híbridas do BizTalk ##

capacidade de conexões híbridas de BizTalk antiga Olá foi fechada off toofurther criações de Conexão de híbrida do BizTalk.  Você pode continuar usando o BizTalk preexistentes as conexões híbridas com seus aplicativos, mas deve migrar toohello novo serviço.  Entre Olá benefícios em novo serviço Olá pela versão do BizTalk Olá são:

- nenhuma conta adicional do BizTalk é necessária
- O TLS é 1.2 em vez do 1.0, o qual é usado nas Conexões Híbridas do BizTalk
- A comunicação é por portas 80 e 443 usando um tooreach do nome DNS do Azure, em vez de endereços IP e uma variedade de outros outras portas.  

tooadd um aplicativo do BizTalk híbrida conexão tooyour, vá tooyour aplicativo hello [portal do Azure] [ portal] e clique em **rede > configurar seus pontos de extremidade de conexão híbrida**.  Na tabela de conexões do hello clássico híbrida clique **Adicionar conexão híbrida clássico**.  Daqui em diante, você verá uma lista das conexões híbridas do BizTalk.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

