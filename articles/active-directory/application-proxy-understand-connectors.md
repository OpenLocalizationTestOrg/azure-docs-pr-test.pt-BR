---
title: conectores de Proxy de aplicativo aaaUnderstand AD do Azure | Microsoft Docs
description: "Abrange Olá Noções básicas sobre conectores de Proxy de aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Noções básicas sobre conectores de Proxy de Aplicativo Azure AD

Os conectores são o que torna o Proxy de Aplicativo Azure AD possível. Eles são toodeploy simple e fácil manter e super avançado. Este artigo aborda os conectores que são, como eles funcionam e algumas sugestões de como toooptimize sua implantação. 

## <a name="what-is-an-application-proxy-connector"></a>O que é um conector do Proxy de Aplicativo

Conectores são leves agentes que ficam no local e facilitam o serviço de Proxy de aplicativo de toohello Olá conexão de saída. Conectores devem ser instalados em um servidor Windows que tenha o aplicativo de back-end do access toohello. Você pode organizar os conectores em grupos de conector, a cada grupo de aplicativos de toospecific de tráfego de tratamento. Balanceamento de carga de conectores automaticamente e pode ajudar a toooptimize sua estrutura de rede. 

## <a name="requirements-and-deployment"></a>Requisitos e implantação

toodeploy Proxy de aplicativo com êxito, é necessário pelo menos um conector, mas recomendamos dois ou mais para maior capacidade de recuperação. Instale o conector de saudação em um Windows Server 2012 R2 ou uma máquina de 2016. conector de saudação precisa toocommunicate capaz de toobe com o serviço de Proxy de aplicativo hello, bem como aplicativos de locais de saudação que você publicar. 

Para obter mais informações sobre os requisitos de rede Olá para o servidor de conector hello, consulte [Introdução ao Proxy de aplicativo e instalar um conector](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Manutenção 
Olá conectores e serviço Olá cuidam de todas as tarefas de alta disponibilidade de saudação. Eles podem ser adicionados ou removidos dinamicamente. Cada vez que uma nova solicitação chega é roteado tooone dos conectores Olá que está disponível no momento. Se um conector temporariamente não estiver disponível, ele não responder toothis tráfego.

conectores de saudação são sem monitoração de estado e não tem nenhum dado de configuração no computador de saudação. Olá apenas os dados que eles armazenam são configurações Olá para conectar-se o serviço hello e seu certificado de autenticação. Quando eles se conectam toohello serviço, eles pull todos os dados de configuração de saudação necessário e atualização-lo a cada dois minutos.

Conectores também sondagem Olá server toofind se há uma versão mais recente do conector de saudação. Se for encontrado, conectores Olá atualizam-se.

Você pode monitorar seus conectores da máquina Olá que eles estão em execução, usando Olá log de eventos e contadores de desempenho. Ou você pode exibir o status da página de Proxy de aplicativo de saudação do hello portal do Azure:

 ![Conectores do Proxy de Aplicativo Azure AD](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

Você não tem toomanually excluir os conectores que não foram utilizadas. Quando um conector é executado, ele permanece ativo, como ele se conecta toohello serviço. Os conectores não utilizados são marcados como _inativos_ e são removidos depois de 10 dias de inatividade. Se você quiser toouninstall um conector, desinstale, serviço de conector hello e o serviço do atualizador de saudação do servidor de saudação. Reinicie o serviço de saudação do computador toofully remover.

## <a name="automatic-updates"></a>Atualizações automáticas

O AD do Azure fornece atualizações automáticas para todos os conectores de saudação que você implanta. Como Olá serviço atualizador do conector de Proxy de aplicativo está em execução, os conectores são atualizadas automaticamente. Se você não vir Olá serviço atualizador do conector no servidor, você precisa muito[reinstalar seu conector](active-directory-application-proxy-enable.md) tooget todas as atualizações. 

Se você não quiser toowait para um conector de tooyour toocome atualização automática, você pode executar uma atualização manual. Vá toohello [página de download do conector](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) no servidor de saudação em que o conector está localizado e selecione **baixar**. Esse processo inicia uma atualização para o conector local hello. 

Para locatários com vários conectores, as atualizações automáticas Olá destino um conector de cada vez em cada grupo tooprevent o tempo de inatividade em seu ambiente. 

Poderá ocorrer tempo de inatividade quando o conector for atualizado se:  
- Você só tiver um conector. tooavoid esse tempo de inatividade e melhorar a alta disponibilidade, recomendamos que você instale um segundo conector e [criar um grupo de conector](active-directory-application-proxy-connectors-azure-portal.md).  
- Um conector estava no meio de saudação de uma transação quando atualização Olá começou. Embora a transação de saudação inicial for perdida, seu navegador automaticamente deve repetir a operação de hello ou você pode atualizar a página. Quando a solicitação de saudação é enviado novamente, o tráfego de Olá é roteado tooa conector de backup.

## <a name="creating-connector-groups"></a>Criando grupos de conector

Grupos de conector habilitar aplicativos específicos do tooserve tooassign conectores específicos. Você pode agrupar um número de conectores e, em seguida, atribua cada grupo de tooa de aplicativo. 

Grupos de conector tornam mais fácil toomanage grandes implantações. Eles também melhoram a latência para locatários que têm aplicativos hospedados em regiões diferentes, como você pode criar grupos de conector com base no local de aplicativos locais somente tooserve. 

toolearn mais sobre grupos de conector, consulte [publicar aplicativos em redes separadas e locais usando grupos de conector](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Rede e segurança

Conectores podem ser instalados em qualquer lugar na rede de saudação que lhes permite serviço de Proxy de aplicativo de toohello toosend solicitações. O importante é que o computador Olá que executam o conector Olá também tem acesso tooyour aplicativos. Você pode instalar conectores dentro de sua rede corporativa, ou em uma máquina virtual que é executado na nuvem hello. Os conectores podem ser executados em uma DMZ (zona desmilitarizada), mas não é necessário porque todo o tráfego é de saída e, portanto, sua rede fica segura.

Os conectores só enviam solicitações de saída. o tráfego de saída Olá enviado toohello serviço de Proxy de aplicativo e toohello aplicativos publicados. Você não tem tooopen portas de entrada porque o tráfego passa ambos os modos após o estabelecimento de uma sessão. Você não tiver tooset o balanceamento de carga entre os conectores de saudação ou configurar o acesso de entrada por meio de seus firewalls. 

Para saber mais sobre como configurar regras de firewall de saída, confira [Trabalhar com servidores proxy locais existentes](application-proxy-working-with-proxy-servers.md).

Saudação de uso [ferramenta de teste das portas conector do Azure AD aplicativo Proxy](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que seu conector possa acessar o serviço de Proxy de aplicativo hello. No mínimo, certifique-se de que que a região do hello centro dos EUA e Olá região mais próxima tooyou tenham todas as marcas de seleção verdes. Além disso, um número maior de marcas de seleção verdes significa maior resiliência. 

## <a name="performance-and-scalability"></a>Desempenho e escala

Escala para Olá serviço Proxy de aplicativo é transparente, mas a escala é um fator para conectores. Você precisa de tráfego de pico suficiente conectores toohandle toohave. No entanto, você não precisa tooconfigure balanceamento de carga porque todos os conectores dentro de um grupo de conector automaticamente o balanceamento de carga.

Desde que os conectores são sem monitoração de estado, eles não são afetados pelo número de saudação de usuários ou sessões. Em vez disso, eles respondem toohello o número de solicitações e seu tamanho de carga. Com o tráfego padrão da Web, um computador médio pode manipular milhares de solicitações por segundo. capacidade específica Olá depende de características do computador exata de saudação. 

desempenho do conector Olá é associado por CPU e de rede. Desempenho da CPU é necessária para criptografia SSL e descriptografia, enquanto a rede é importante tooget aplicativos de toohello de conectividade rápida e serviço on-line de saudação no Azure.

Por outro lado, a memória é uma questão menos significativa para os conectores. serviço on-line Olá cuida grande parte do processamento de saudação e todo o tráfego não autenticado. Tudo o que pode ser feito na nuvem Olá é feito na nuvem hello. 

Outro fator que afeta o desempenho é a qualidade de saudação da rede Olá entre conectores hello, incluindo: 

* **Olá serviço on-line**: conexões lentas ou alta latência toohello serviço de Proxy de aplicativo no desempenho do conector Olá influência do Azure. Para melhor desempenho de hello, conecte-se tooAzure sua organização com a rota expressa. Caso contrário, tem sua equipe da rede Certifique-se de que tooAzure conexões são tratadas mais eficiente possível. 
* **Olá aplicativos de back-end**: em alguns casos, há outros proxies entre conector hello e aplicativos de back-end de saudação que podem reduzir ou impedir conexões. tootroubleshoot neste cenário, abra um navegador do servidor de conector hello e tente o aplicativo de hello tooaccess. Se você executar conectores Olá no Azure, mas aplicativos Olá estão no local, a experiência de saudação pode não ser espera que seus usuários.
* **Olá controladores de domínio**: se os conectores Olá executam o SSO usando a delegação restrita de Kerberos, eles entre em contato com controladores de domínio de saudação antes do envio de back-end do hello solicitação toohello. conectores de saudação têm um cache de tíquetes Kerberos, mas em um ambiente de ocupado capacidade de resposta Olá Olá de controladores de domínio pode afetar o desempenho. Esse problema é mais comum em conectores executados no Azure, mas que se comunicam com os controladores de domínio locais. 

Para saber mais sobre como otimizar sua rede, confira [Considerações sobre a topologia de rede ao usar o Proxy de Aplicativo do Azure Active Directory](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Ingresso no domínio

Os conectores podem ser executados em um computador que não foi ingressado no domínio. No entanto, se você quiser single sign-on (SSO) tooapplications que usam a autenticação do Windows integrada (IWA), você precisa de um computador ingressado no domínio. Nesse caso, máquinas de conector Olá devem ser tooa ingressado no domínio que pode executar [Kerberos](https://web.mit.edu/kerberos) delegação restrita em nome dos usuários Olá para Olá publicado os aplicativos.

Conectores também podem ser unidas toodomains ou florestas que têm uma relação de confiança parcial, ou controladores de domínio somente tooread.

## <a name="connector-deployments-on-hardened-environments"></a>Implantações de conector em ambientes protegidos

Normalmente, a implantação do conector é simples e não exige nenhuma configuração especial. No entanto, há algumas condições exclusivas que devem ser consideradas:

* As organizações que limitam o tráfego de saída Olá devem [abrir as portas necessárias](active-directory-application-proxy-enable.md#open-your-ports).
* Máquinas compatíveis com FIPS podem ser necessária toochange tooallow sua configuração Olá toogenerate de processos do conector e armazenar um certificado.
* As organizações que bloqueiam seu ambiente com base em processos Olá Olá esse problema que solicitações de rede ter toomake se ambos os serviços do conector estão habilitados tooaccess todas as necessárias portas e IPs.
* Em alguns casos, saída proxies forward podem quebrar a autenticação de certificado bidirecional hello e causar Olá toofail de comunicação.

## <a name="connector-authentication"></a>Autenticação do conector

tooprovide um serviço seguro, conectores têm tooauthenticate para serviço hello e serviço Olá tem tooauthenticate para conector de saudação. Essa autenticação é feita usando certificados de cliente e servidor quando conectores Olá iniciam conexão hello. Esse administrador de saudação de maneira nome de usuário e senha não são armazenados no computador do conector de saudação.

certificados de saudação usados são específicos toohello serviço de Proxy de aplicativo. Elas são criadas durante o registro inicial hello e são automaticamente renovados pelos conectores Olá a cada dois meses. 

Se não estiver conectado a um conector de serviço toohello para vários meses, seus certificados pode estar desatualizado. Nesse caso, desinstale e reinstale o registro do hello conector tootrigger. Você pode executar Olá comandos do PowerShell a seguir:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Bastidores Olá

Conectores baseiam-se no Proxy de aplicativo do Windows Server Web, portanto, têm a maioria das Olá mesmas ferramentas de gerenciamento, incluindo os Logs de eventos do Windows

 ![Gerenciar logs de eventos com hello Visualizador de eventos](./media/application-proxy-understand-connectors/event-view-window.png)

e contadores de desempenho do Windows. 

 ![Adicionar contadores toohello conector com hello Monitor de desempenho](./media/application-proxy-understand-connectors/performance-monitor.png)

conectores de saudação têm admin e sessão logs. Olá administrador logs incluem seus erros e eventos importantes. logs de sessão Olá incluem todas as transações de saudação e seus detalhes de processamento. 

logs de saudação toosee, vá toohello Visualizador de eventos, abra Olá **exibição** menu e habilitar **Mostrar analítica e logs de depuração**. Em seguida, habilitá-las toostart coleta de eventos. Esses logs não aparecem no Proxy de aplicativo Web no Windows Server 2012 R2, como conectores Olá baseiam-se em uma versão mais recente.

Você pode examinar o estado de saudação do serviço de saudação na janela de serviços de saudação. conector de saudação consiste em dois serviços do Windows: conector real hello e updater hello. Os dois devem executar todo o tempo de saudação.

 ![Local dos Serviços do Azure AD](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Próximas etapas


* [Publicar aplicativos em redes e locais separados usando grupos de conectores](active-directory-application-proxy-connectors-azure-portal.md)
* [Trabalhar com servidores proxy locais existentes](application-proxy-working-with-proxy-servers.md)
* [Solucionar erros do conector e do Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)
* [Como instalar o toosilently Olá conector de Proxy de aplicativo do AD do Azure](active-directory-application-proxy-silent-installation.md)

