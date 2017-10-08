---
title: "aaaCloud considerações sobre privacidade e segurança de descoberta do aplicativo | Microsoft Docs"
description: "Este tópico descreve a segurança hello e privacidade de considerações relacionadas tooCloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Considerações de privacidade e segurança no Cloud App Discovery
Microsoft é confirmada tooprotecting sua privacidade e segurança de dados, oferecendo softwares e serviços que ajudam a gerenciar segurança de saudação da sua organização.  
Reconhecemos que quando você entrega seus dados tooothers, essa confiança requer investimentos de engenharia de segurança rigorosa e experiência tooback-lo.
A Microsoft obedece toostrict conformidade e diretrizes de segurança de software seguro desenvolvimento do ciclo de vida práticas toooperating um serviço.  
Segurança e proteção de dados é uma prioridade principal da Microsoft.

Este tópico explica como os dados são coletados, processados e protegidos dentro do Cloud App Discovery do Active Directory do Azure

## <a name="overview"></a>Visão geral
Cloud App Discovery é um recurso do AD do Azure e é hospedado no Microsoft Azure.  
Agente de ponto de extremidade do Cloud App Discovery Olá é toocollect usados dados de descoberta de aplicativo gerenciado por TI máquinas.  
Olá dados coletados são enviados com segurança por um canal criptografado de toohello serviço do Azure AD Cloud App Discovery.  
Olá dados de descoberta de aplicativo de nuvem para uma organização, em seguida, é visível no hello portal do Azure. 

![Como o Cloud App Discovery funciona](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Olá seções a seguir seguem Olá fluxo de informações e descrevem como ele é protegido conforme avança da sua organização toohello Cloud App Discovery serviço e, finalmente, toohello Cloud App Discovery portal do.

## <a name="collecting-data-from-your-organization"></a>Coletando dados de sua organização
Em aplicativo de nuvem descoberta recurso tooget um panorama do ordem toouse Active Directory do Azure aplicativos Olá usados pelos funcionários da sua organização, você precisa toofirst implantar hello Azure AD Cloud App Discovery endpoint agent toomachines em sua organização.

Os administradores de locatário do Active Directory do Azure hello (ou seus representantes) podem baixar o pacote de instalação do agente de saudação do hello portal do Azure. Agente de saudação pode ser manualmente instalado ou instalado em vários computadores na organização hello usando o SCCM ou diretiva de grupo.

Para obter mais instruções sobre opções de implantação, consulte [Guia de implantação da política de grupo do Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Dados coletados pelo agente de saudação
informações de Olá descritas na lista de saudação abaixo são coletadas pelo agente de saudação quando uma conexão é feita tooa aplicativo Web. Olá informações são coletadas apenas para esses aplicativos administrador Olá configurou para descoberta.  
Você pode editar Olá lista de aplicativos de nuvem que Olá agent monitora a folha do Cloud App Discovery Olá no hello Microsoft [portal do Azure](https://portal.azure.com/), em **configurações**->**dados Coleção**->**lista de coleção de aplicativos**. Para obter mais detalhes, consulte [Introdução ao Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Categoria das informações**: informações do usuário  
**Descrição**:  
nome de usuário do Windows Hello do processo de saudação que fez a um aplicativo Web de destino toohello solicitação (por exemplo: domínio \ nomedeusuário), bem como Olá identificador de segurança do Windows (SID) do usuário hello.

**Categoria das Informações**: informações do processo  
**Descrição**:  
nome de saudação do processo de saudação que fez o aplicativo Web do hello solicitação toohello destino (por exemplo: "iexplore.exe")

**Categoria das Informações**: informações do computador  
**Descrição**:  
nome de NetBIOS de máquina Olá no qual Olá agente está instalado.

**Categoria das Informações**: informações de tráfego do aplicativo  
**Descrição**: 

Olá informações de conexão a seguir:

* origem da saudação (computador local) e endereços IP de destino e números de porta
* Olá endereço IP público de organização Olá por meio do qual Olá solicitação sai.
* tempo de saudação da solicitação de saudação
* volume de saudação do tráfego enviado e recebido
* versão IP Hello (4 ou 6)
* Somente para conexões TLS: nome do host de destino Olá da extensão do hello indicação de nome de servidor ou certificado de servidor de saudação.

Olá informações de HTTP a seguir:

* Método (GET, POST, etc.)
* Protocolo (HTTP/1.1, etc.)
* Cadeia de caracteres de agente do usuário
* Nome do host
* URI de destino (exceto a cadeia de caracteres de consulta)
* Informações de tipo de conteúdo
* Informações de referência de URL (exceto a cadeia de caracteres de consulta)

> [!NOTE]
> Olá informações de HTTP acima é coletada para todas as conexões não criptografadas.
> Para conexões TLS, essas informações só são capturadas quando a configuração de 'Inspeção profunda' hello está ativada no portal de saudação. configuração de saudação é 'ON' por padrão.
> Para obter mais detalhes, consulte abaixo, e [Introdução ao Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

Além disso toohello dados que o agente Olá coleta sobre a atividade de rede hello, ele também coletará informações anônimas sobre a configuração de hardware e software hello, relatórios de erros e informações sobre como o agente hello está sendo usado.


### <a name="how-hello-agent-works"></a>Como funciona o agente Olá
instalação do agente Olá inclui dois componentes:

* Um componente de modo de usuário
* Um componente de driver no modo kernel (driver da Plataforma para Filtros do Windows)

Quando o agente de saudação é instalado, ele armazena um certificado confiável do computador no computador de saudação que usa tooestablish uma conexão segura com o serviço do Cloud App Discovery hello.  
agente Olá recupera periodicamente configuração de política de saudação serviço Cloud App Discovery por essa conexão segura.  
política de saudação inclui informações sobre quais toomonitor de aplicativos de nuvem e se a atualização automática deve ser habilitada, entre outras coisas.

Como o tráfego da Web é enviado e recebido na máquina de saudação do Internet Explorer e no Chrome, agente do Cloud App Discovery Olá analisa o tráfego de saudação e extrai Olá metadados relevantes (consulte Olá **os dados coletados pelo agente Olá** seção acima).  
A cada minuto, o agente de saudação carrega Olá coletado metadados toohello serviço Cloud App Discovery por um canal criptografado.

Olá interseções de componente de driver Olá tráfego criptografado e entra no fluxo criptografado hello. Para obter mais detalhes no hello **interceptando dados de conexões criptografadas (inspeção profunda)** seção abaixo.

### <a name="respecting-user-privacy"></a>Respeitando a privacidade do usuário
Nosso objetivo é tooprovide administradores Olá ferramentas tooset Olá equilíbrio entre a óptica detalhada da privacidade de uso e de usuário do aplicativo conforme apropriado para sua organização. toothat final, fornecemos Olá botões na página de configurações de saudação do hello Portal a seguir:

* **Coleta de dados**: os administradores podem optar toospecify quais aplicativos ou categorias de aplicativo que quiserem tooget dados de descoberta.
* **Inspeção profunda**: os administradores podem escolher toospecify se agente Olá coleta tráfego HTTP para conexões SSL/TLS (também conhecido como **'Inspeção profunda'**). Mais informações sobre isso na próxima seção, Olá.
* **Opções de consentimento**: os administradores podem usar toochoose portal do Cloud App Discovery Olá se usuários toonotify Olá da coleta de dados pelo agente Olá, e se o usuário toorequire consentir antes do agente de saudação começará a coletar dados de usuário.

Olá Cloud App Discovery endpoint agent coleta apenas informações de saudação descritas Olá **os dados coletados pelo agente Olá** seção acima.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Interceptando dados de conexões criptografadas (inspeção profunda)
Como mencionado anteriormente, os administradores podem configurar dados de toomonitor agente saudação de conexões criptografadas ('inspeção profunda'). TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) é uma saudação protocolos mais comuns em uso no hello Internet hoje em dia. Ao criptografar a comunicação com o TLS, um cliente pode estabelecer um canal de comunicação segura e privada com um servidor web. TLS fornece uma proteção essencial para passar as credenciais de autenticação e evitar a divulgação de saudação de informações confidenciais.

Enquanto o hello ponta a ponta criptografados canal seguro fornecido por TLS permite importantes de segurança e proteção de privacidade, protocolo de saudação é geralmente seja explorado para fins mal-intencionados ou mal-intencionado. Muito dessa forma, na verdade, TLS geralmente é chamado tooas hello "firewall universal-bypass protocolo". raiz de saudação do problema de saudação é que a maioria dos firewalls comunicação TLS de tooinspect não é possível porque os dados da camada de aplicativo hello for criptografados com SSL. Sendo assim, os invasores frequentemente aproveitam usuário mal-intencionado cargas de tooa do toodeliver TLS confiante de que o mesmo hello mais inteligente camada de aplicativo firewalls são completamente oculta tooTLS e simplesmente devem retransmitir comunicação TLS entre hosts. Os usuários finais com frequência aproveite TLS toobypass os controles de acesso impostos por seus servidores de proxy, usá-lo tooconnect toopublic proxies e firewalls corporativos e de túnel protocolos TLS não através do firewall do hello caso contrário, pode ser bloqueado pela política.

Inspeção profunda permite Olá Cloud App Discovery agent tooact como um confiável man-in-the-middle. Quando é feita uma solicitação de cliente recurso protegido de tooaccess um HTTPS, o driver de agente de ponto de extremidade de Olá intercepta conexão hello e estabelece um novo tooretrieves de servidor de destino de toohello conexão seu certificado SSL em nome do cliente de saudação. Agente de Hello, em seguida, verifica se Olá certificado pode ser confiável (verificação de que ele não foi revogado e executar outras verificações de certificado), e se eles passam, hello agente de ponto de extremidade, em seguida, copia informações de saudação do certificado do servidor de saudação e cria seu próprio certificado do servidor – conhecido como um certificado de intercepção – usando essas informações. certificado de interceptação de saudação é assinado em dinamicamente pelo agente de ponto de extremidade de saudação com um certificado raiz, que é instalado no repositório de certificados confiáveis do Windows hello. Este certificado raiz autoassinado está marcado como não exportável e ACL tinha tooadministrators. É máquina de saudação deixe toonever pretendido no qual ele foi criado. Quando o aplicativo de cliente de saudação do usuário final recebe certificado de intercepção Olá, ele confiará-lo porque pode validar a cadeia de certificados Olá com êxito todos os certificados de raiz Olá maneira toohello. Esse processo, na maioria das vezes, é transparente para o usuário final com algumas advertências, conforme descrito abaixo.

Habilitando a inspeção profunda, Olá Cloud App Discovery Endpoint Agent pode descriptografar e inspecionar as comunicações de TLS criptografada, permitindo que o ruído de tooreduce serviço hello e fornecem informações sobre o uso de saudação de aplicativos na nuvem Olá criptografado.

#### <a name="a-word-of-caution"></a>Uma advertência
Antes de ativar a inspeção profunda, é altamente recomendável que você se comunicar sua intenção tooyour legal e departamentos de RH e obter o consentimento. Inspecionar a comunicação criptografada privada do usuário final pode ser um assunto confidencial, por motivos óbvios. Antes de um produção roll-out de inspeção profunda, certifique-se que segurança da sua empresa e políticas de uso aceitável tenham sido atualizadas tooindicate que comunicação criptografada será ser inspecionado. Notificação do usuário e a isenção de sites consideradas confidenciais (por exemplo, médicos e bancários sites) também podem ser necessários se você configurar o Cloud App Discovery toomonitor-los. Conforme mencionado acima, os administradores podem usar toochoose portal do Cloud App Discovery Olá se usuários toonotify Olá da coleta de dados pelo agente Olá, e se o usuário toorequire consentir antes do agente de saudação começará a coletar dados de usuário.

### <a name="known-issues-and-drawbacks"></a>Problemas conhecidos e desvantagens
Há alguns casos onde interceptação TLS pode afetar a experiência do usuário final hello:

* Os certificados de validação (EV) estendida renderizam barra de endereços de saudação do Olá web navegador verde tooact como uma indicação visual que você está visitando um site confiável. Inspeção de TLS não é possível duplicar EV no certificado Olá emite toohello cliente, para que sites que usam certificados EV funcione normalmente mas barra de endereços de saudação não exibirá em verde.  
* Fixando chave pública (também conhecido como certificado fixar) são projetados toohelp proteger os usuários contra ataques man-in-the-middle e autorizados autoridades de certificação. Quando o certificado de raiz de saudação para um site fixo não corresponde a uma saudação conhecida BOM da autoridade de certificação, o navegador Olá rejeita conexão Olá com um erro. Como a intercepção de TLS é, na verdade, um intermediário, essas conexões falharão.
* Se os usuários clicarem o ícone de cadeado Olá Olá navegador informações de endereço barra navegador tooinspect Olá site, eles não verão uma cadeia que termina em autoridade de certificação Olá usado certificado de site toosign hello, mas em vez disso, uma cadeia de certificados terminam com hello Windows repositório de certificados confiáveis.

ocorrências de saudação tooreduce desses problemas, podemos manter o controle de serviços de nuvem e aplicativos cliente conhecidos toouse estendidos validação ou a fixação de chave pública e instruem Olá Endpoint Agent tooavoid interceptando conexões afetados. Mesmo nesses casos, no entanto, você ainda receberá relatórios de uso de saudação desses aplicativos de nuvem e volume de saudação de dados que estão sendo transferidos, mas como não são profundas inspecionados, sem detalhes sobre como os aplicativos Olá foram usados estarão disponíveis.

## <a name="sending-data-toocloud-app-discovery"></a>Enviando dados tooCloud App Discovery
Depois de metadados foram coletados pelo agente Olá, ele é armazenado em cache na máquina de saudação para backup tooone minuto ou até Olá dados armazenados em cache atinjam um tamanho de 5MB. Em seguida, são compactado e enviado por uma conexão segura de toohello serviço Cloud App Discovery.

Se o agente de saudação toocommunicate não é possível com hello serviço Cloud App Discovery por algum motivo, hello coletados metadados são armazenados em um cache de arquivo local que só pode ser acessado por usuários com privilégios no computador de saudação (por exemplo, o grupo de administradores de saudação).  
agente Olá automaticamente tentativas tooresend Olá metadados armazenados até que ele tem foi recebido com êxito pelo serviço do Cloud App Discovery hello.

## <a name="receiving-hello-data-at-hello-service-end"></a>Recebendo dados Olá na extremidade de serviço Olá
agentes de saudação autenticam toohello Cloud App Discovery serviço usando o certificado de autenticação de cliente específico de máquina Olá mencionado acima e encaminha os dados por um canal criptografado.  
análise do serviço do Cloud App Discovery Olá pipeline processos metadados para cada cliente separadamente ao particionar logicamente por todos os estágios do pipeline de análise de saudação.
Olá analisados metadados unidades Olá vários relatórios no portal de saudação.

Olá metadados não processados e metadados Olá analisado são armazenados por backup too180 dias. Além disso, os clientes podem optar toocapture Olá analisado metadados em uma conta de armazenamento de BLOBs do Azure de sua escolha.
Isso é útil para análise offline de metadados, bem como maior retenção dos dados de saudação.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Acessando dados hello usando Olá portal do Azure
Em um esforço tookeep Olá metadados que coletados seguro, por padrão somente os administradores globais do locatário Olá tem acesso toohello Cloud App Discovery recurso no hello portal do Azure.  
No entanto, os administradores podem optar toodelegate esse acesso tooother usuários ou grupos.

> [!NOTE]
> Para obter mais detalhes, consulte [Introdução ao Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Qualquer usuário acessando Olá dados no portal Olá, deve ser licenciado com uma licença Azure AD Premium.

## <a name="additional-resources"></a>Recursos adicionais
* [Como descobrir aplicativos na nuvem não aprovados, usados em minha organização](active-directory-cloudappdiscovery-whatis.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

