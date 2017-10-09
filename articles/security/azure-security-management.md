---
title: "segurança do gerenciamento remoto de aaaEnhance no Azure | Microsoft Docs"
description: "Este artigo discute medidas para melhorar a segurança do gerenciamento remoto durante a administração dos ambientes do Microsoft Azure, incluindo serviços de nuvem, Máquinas Virtuais e aplicativos personalizados."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Gerenciamento de segurança no Azure
Os assinantes do Azure podem gerenciar ambientes de nuvem de vários dispositivos, incluindo estações de trabalho, computadores de desenvolvedores e até mesmo dispositivos de usuário final com privilégios que têm permissões de tarefas específicas. Em alguns casos, as funções administrativas são executadas por meio de consoles baseado na web como Olá [portal do Azure](https://azure.microsoft.com/features/azure-portal/). Em outros casos, pode haver tooAzure conexões diretas de sistemas locais através de redes virtuais privadas (VPNs), os serviços de Terminal, protocolos de cliente de aplicativo ou (programaticamente) Olá API de gerenciamento de serviço do Azure (SMAPI). Além disso, os pontos de extremidade do cliente podem ser unidos ao domínio ou isolados e não gerenciados, como tablets ou smartphones.

Embora vários recursos de gerenciamento e acesso fornecem um conjunto avançado de opções, essa variação pode adicionar implantação de nuvem tooa risco significativo. Pode ser difícil toomanage, controlar e auditar as ações administrativas. Essa variação também pode introduzir ameaças de segurança por meio de acesso irregular tooclient os pontos de extremidade que são usados para gerenciar os serviços de nuvem. O uso de estações de trabalho pessoais ou gerais para desenvolvimento e gerenciamento de infraestrutura abre vetores de ameaça imprevisíveis, como navegação na Web (por exemplo, ataques do tipo "watering hole") ou email (por exemplo, engenharia social e phishing).

![][1]

Olá potencial para ataques aumenta nesse tipo de ambiente porque ele é um desafio tooconstruct as políticas de segurança e mecanismos tooappropriately gerenciar acesso tooAzure interfaces (como SMAPI) amplamente diversos pontos de extremidade de.

### <a name="remote-management-threats"></a>Ameaças de gerenciamento remoto
Os invasores geralmente tentam acessar a toogain privilegiado comprometer credenciais de conta (por exemplo, por meio de força bruta da senha, phishing e coleta de credencial) ou enganar os usuários na execução de código prejudicial (por exemplo, de sites mal-intencionados com downloads drive-by ou dos anexos de email prejudiciais). Em um ambiente de nuvem remotamente gerenciada, conta violações podem levar tooan maior risco tooanywhere vencimento, o acesso a qualquer momento.

Mesmo com controles rígidos em contas de administrador primário, contas de usuário de nível inferior podem ser fracos tooexploit usado em uma estratégia de segurança. Falta de treinamento de segurança apropriadas também pode levar toobreaches por meio de divulgação acidental ou exposição das informações de conta.

Quando uma estação de trabalho de usuário também é usada para tarefas administrativas, ela pode ser comprometida em vários pontos diferentes. Se um usuário está navegando Olá web, usando ferramentas de terceiros 3º e código-fonte aberto ou abrindo um arquivo de documento prejudiciais que contém um cavalo de Troia.

Em geral, mais ataques direcionados que resultam em violações de dados pode ser rastreados toobrowser explorações, plug-ins (por exemplo, Flash, PDF, Java) e lança phishing (email) em computadores desktop. Esses computadores podem ter nível administrativo ou tooaccess permissões de nível de serviço ao vivo de servidores ou dispositivos para operações quando usado para desenvolvimento ou gerenciamento de outros ativos de rede.

### <a name="operational-security-fundamentals"></a>Conceitos básicos de segurança operacional
Para mais segura e operações de gerenciamento, você pode minimizar a superfície de ataque do cliente, reduzindo o número de saudação de possíveis pontos de entrada. Isso pode ser feito por meio de princípios de segurança: "separação de tarefas" e "diferenciação de ambientes".

Isole funções confidenciais de uma outra toodecrease Olá probabilidade de que um erro em um nível leva tooa violação em outro. Exemplos:

* Tarefas administrativas não devem ser combinadas com atividades que podem causar o comprometimento de tooa (por exemplo, contra malware no email do administrador que infecta, em seguida, um servidor de infraestrutura).
* Uma estação de trabalho usada para operações de alta sensibilidade não deve ser Olá mesmo sistema usado para fins de alto risco, como navegação Olá da Internet.

Reduza a superfície de ataque do sistema Olá Removendo softwares desnecessários. Exemplo:

* Padrão administrativo, suporte ou estação de trabalho de desenvolvimento não deve exigir a instalação de um cliente de email ou outros aplicativos de produtividade se o objetivo principal do dispositivo Olá é toomanage serviços de nuvem.

Sistemas de cliente que têm tooinfrastructure de acesso de administrador componentes devem estar sujeitos toohello mais rígido política possíveis tooreduce os riscos de segurança. Exemplos:

* Políticas de segurança podem incluir configurações de política de grupo que negam o acesso de Internet aberto do dispositivo hello e o uso de uma configuração de firewall restritivas.
* Use VPNs com o IPsec (protocolo IPsec), caso seja necessário acesso direto.
* Configure domínios separados do Active Directory de gerenciamento e de desenvolvimento.
* Isole e filtre o tráfego de rede de estações de trabalho de gerenciamento.
* Use software antimalware.
* Implementar o risco de saudação tooreduce autenticação multifator de credenciais roubadas.

Consolidar recursos de acesso e eliminar pontos de extremidade não gerenciados também simplifica as tarefas de gerenciamento.

### <a name="providing-security-for-azure-remote-management"></a>Fornecer segurança para o gerenciamento remoto do Azure
O Azure fornece segurança Administradores de tooaid mecanismos que gerenciam serviços de nuvem do Azure e máquinas virtuais. Esses mecanismos incluem:

* Autenticação e [controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md).
* Monitoramento, registro em log e auditoria.
* Certificados e comunicações criptografadas.
* Um portal de gerenciamento da Web.
* Filtragem de pacotes de rede.

Com a configuração de segurança do cliente e implantação de datacenter de um gateway de gerenciamento, é dados e possíveis toorestrict e monitor administrador toocloud aplicativos do access.

> [!NOTE]
> Determinadas recomendações neste artigo podem resultar em maior uso de recursos de computação, rede ou dados e podem aumentar os custos de licença ou assinatura.
>
>

## <a name="hardened-workstation-for-management"></a>Estação de trabalho protegida para gerenciamento
meta de saudação de proteção de uma estação de trabalho é tooeliminate todos os mas funções mais críticas Olá necessário toooperate, tornando a superfície de ataque potencial Olá tão pequenas quanto possível. Proteção de sistema inclui reduzindo o número de saudação de serviços e aplicativos, limitando a execução do aplicativo, restringindo tooonly de acesso de rede, o que é necessário, instalados e mantendo sempre sistema Olá toodate. Além disso, o uso de uma estação de trabalho protegida para o gerenciamento segrega as ferramentas administrativas e as atividades de outras tarefas de usuário final.

Em um ambiente de empresa local, você pode limitar a superfície de ataque de saudação de sua infraestrutura física por meio de redes de gerenciamento dedicado, salas de servidores que têm acesso de cartão e estações de trabalho que são executados em áreas protegidas da rede hello. Em uma nuvem ou híbrida modelo de TI, seja cuidadoso sobre serviços seguros de gerenciamento pode ser mais complexa devido à falta de saudação de recursos de tooIT acesso físico. A implementação de soluções de proteção requer configuração cuidadosa do software, processos voltados para a segurança e regras abrangentes.

Usando um espaço de software minimizado com menos privilégios em uma estação de trabalho bloqueada para o gerenciamento de nuvem — e para o desenvolvimento de aplicativos — pode reduzir o risco de saudação de incidentes de segurança padronizando ambientes remotos de gerenciamento e desenvolvimento hello. Uma configuração de proteção da estação de trabalho pode ajudar a evitar o comprometimento de saudação de contas que são recursos de nuvem crítico toomanage usado por vários caminhos comuns usados por malware e explorações de fechamento. Especificamente, você pode usar [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) e toocontrol de tecnologia Hyper-V e isolar o comportamento do sistema cliente e reduzir as ameaças, incluindo email ou navegação na Internet.

Em uma estação de trabalho de proteção, administrador de saudação é executado em uma conta de usuário padrão (que bloqueia a execução de nível administrativo) e aplicativos associados são controlados por uma lista de permissões. elementos básicos de saudação de uma estação de trabalho de proteção são os seguintes:

* Verificação e patches ativos. Implantar o software antimalware, executar varreduras regulares de vulnerabilidade e atualizar todas as estações de trabalho por meio da atualização de segurança mais recente da saudação de maneira oportuna.
* Funcionalidade limitada. Desinstalar todos os aplicativos que não são necessários e desabilitar serviços desnecessários (inicialização).
* Proteção de rede. Use o Firewall do Windows regras tooallow somente os endereços IP válidos, portas e gerenciamento de tooAzure relacionados de URLs. Certifique-se de estação de trabalho toohello conexões remotas de entrada também são bloqueados.
* Restrição de execução. Permitir que apenas um conjunto de arquivos executáveis predefinidos que são necessários para gerenciamento toorun (chamado tooas "negação padrão"). Por padrão, os usuários devem ser permissão negados toorun qualquer programa, a menos que ele seja explicitamente definido em hello lista de permissões.
* Menor privilégio. Usuários da estação de trabalho de gerenciamento não devem ter privilégios administrativos no computador local de saudação em si. Dessa forma, não podem alterar configuração de saudação do sistema ou arquivos do sistema Olá, intencionalmente ou não.

Você pode impor isso usando [objetos de diretiva de grupo](https://www.microsoft.com/download/details.aspx?id=2612) (GPOs) em serviços de domínio Active Directory (AD DS) e aplicá-las por meio de suas contas de gerenciamento de tooall de domínio de gerenciamento (local).

### <a name="managing-services-applications-and-data"></a>Gerenciamento de serviços, aplicativos e dados
Configuração de serviços de nuvem do Azure é executada por meio de saudação portal do Azure ou SMAPI, por meio da interface de linha de comando do Windows PowerShell hello ou um aplicativo personalizado que aproveita essas interfaces RESTful. Os serviços que usam esses mecanismos incluem o Azure AD (Azure Active Directory), o Armazenamento do Azure, os Sites do Azure e a Rede Virtual do Azure, entre outros.

Os aplicativos implantados para máquina virtual é fornecer suas próprias ferramentas de cliente e interfaces, conforme necessário, como Olá Microsoft Management Console (MMC), um console de gerenciamento da empresa (como o Microsoft System Center ou do Windows Intune) ou outro gerenciamento aplicativo – Microsoft SQL Server Management Studio, por exemplo. Essas ferramentas geralmente residem em uma rede de cliente ou ambiente empresarial. Elas podem depender de protocolos de rede específicos, como o protocolo RDP, que exigem conexões diretas com estado. Algumas podem ter interfaces habilitadas para a web que não devem ser abertas publicado ou acessível por meio de saudação à Internet.

Você pode restringir o acesso tooinfrastructure e plataforma de gerenciamento de serviços no Azure usando [autenticação multifator](../multi-factor-authentication/multi-factor-authentication.md), [certificados de gerenciamento x. 509](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)e as regras de firewall. Olá portal do Azure e SMAPI requerem segurança de camada de transporte (TLS). No entanto, serviços e aplicativos que você implanta no Azure requerem tootake medidas de proteção que são apropriadas com base em seu aplicativo. Esses mecanismos muitas vezes podem ser habilitados mais facilmente por meio de uma configuração de estação de trabalho protegida padronizada.

### <a name="management-gateway"></a>Gateway de gerenciamento
toocentralize todos os administrativa acessar e simplificar o monitoramento e registro em log, você pode implantar um dedicado [Gateway de área de trabalho remota](https://technet.microsoft.com/library/dd560672) server (Gateway RD) em seu local de rede, conectado tooyour ambiente do Azure.

Um Gateway de Área de Trabalho Remota é um serviço de proxy RDP com base em políticas que impõe requisitos de segurança. Implementar o Gateway de Área de Trabalho Remota junto com o NAP (Proteção de Acesso à Rede) do Windows Server ajuda a garantir que somente os clientes que atendam a critérios de integridade de segurança específicos estabelecidos pelos GPOs (Objetos de Política de Grupo) do AD DS (Serviços de Domínio do Active Directory) possam se conectar. Além disso:

* Provisionar um [certificado de gerenciamento do Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx) em Olá Gateway de área de trabalho remota para que ele seja host somente de saudação permitido tooaccess Olá portal do Azure.
* Unir Olá Gateway RD toohello mesmo [domínio de gerenciamento](http://technet.microsoft.com/library/bb727085.aspx) como Olá estações de trabalho do administrador. Isso é necessário quando você estiver usando uma VPN IPsec de site a site ou rota expressa em um domínio que tenha uma relação de confiança unidirecional de tooAzure AD, ou se você está associando credenciais entre suas instalações instância do AD DS e AD do Azure.
* Configurar um [diretiva de autorização de conexão de cliente](http://technet.microsoft.com/library/cc753324.aspx) toolet Olá Gateway de área de trabalho remota Verifique se o nome da máquina cliente Olá é válido (ingressados no domínio) e tooaccess permitidos Olá portal do Azure.
* Use o IPsec para [VPN Azure](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther proteger tráfego de gerenciamento de interceptação e token roubo ou considere um link isolado da Internet por meio de [rota expressa do Azure](https://azure.microsoft.com/documentation/services/expressroute/).
* Habilite a autenticação multifator (via [Autenticação Multifator do Azure](../multi-factor-authentication/multi-factor-authentication.md)) ou a autenticação de cartão inteligente para administradores que fazem logon por meio do Gateway de Área de Trabalho Remota.
* Configurar fonte [restrições de endereço IP](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) ou [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) no número de hello Azure toominimize de pontos de extremidade de gerenciamento permitidos.

## <a name="security-guidelines"></a>Diretrizes de segurança
Em geral, ajudando a estações de trabalho de administrador toosecure para uso com a nuvem de saudação é semelhante práticas toohello usadas para qualquer estação de trabalho local — por exemplo, minimizado compilação e permissões restritivas. Alguns aspectos exclusivos de gerenciamento de nuvem são mais parecido tooremote ou gerenciamento corporativo de fora da banda. Isso inclui uso hello e auditoria de credenciais, a segurança aprimorada de acesso remoto e a detecção de ameaças e resposta.

### <a name="authentication"></a>Autenticação
Você pode usar endereços IP de origem do logon do Azure restrições tooconstrain para acessar ferramentas administrativas e solicitações de acesso de auditoria. toohelp Azure identificar gerenciamento clientes (estações de trabalho e/ou aplicativos), você pode configurar o SMAPI (por meio de ferramentas de cliente desenvolvido como cmdlets do Windows PowerShell) e toobe de certificados de gerenciamento de cliente Olá toorequire portal do Azure instalado, além de tooSSL certificados. Também recomendamos que o acesso de administrador exija a autenticação multifator.

Alguns aplicativos ou serviços que você implanta no Azure podem ter seus próprios mecanismos de autenticação para acesso do administrador e do usuário final, enquanto outros aproveitam plenamente o Azure AD. Dependendo se você está associando as credenciais por meio de serviços de Federação do Active Directory (AD FS), usando a sincronização de diretório ou manutenção de contas de usuário apenas na saudação de nuvem, usando [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (parte do O Azure AD Premium) ajuda você a gerenciar os ciclos de vida de identidade entre recursos hello.

### <a name="connectivity"></a>Conectividade
Vários mecanismos está disponíveis toohelp tooyour de conexões de cliente seguro redes virtuais do Azure. Dois desses mecanismos, [VPN site a site](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) e [VPN ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S), habilitar o uso de saudação do setor de IPsec padrão (S2S) ou hello [Secure Socket Tunneling Protocol](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) para criptografia e de túnel. Quando o Azure está se conectando o gerenciamento de serviços do Azure toopublic voltados como Olá portal do Azure, o Azure requer HTTPS Hypertext Transfer Protocol Secure ().

Uma estação de trabalho robusto autônoma que não se conectam tooAzure através de um Gateway de área de trabalho remota deve usar Olá baseada em SSTP ponto a site VPN toocreate Olá conexão inicial toohello rede Virtual do Azure e, em seguida, estabelecer tooindividual de conexão de RDP virtual máquinas de com encapsulamento VPN hello.

### <a name="management-auditing-vs-policy-enforcement"></a>Auditoria de gerenciamento versus imposição de políticas
Normalmente, há duas abordagens para ajudar a processos de gerenciamento de toosecure: aplicação de políticas de auditoria. A adoção de ambas fornece controles abrangentes, mas talvez não seja possível em todas as situações. Além disso, cada abordagem tem diferentes níveis de risco, o custo e o esforço associados ao gerenciamento de segurança, principalmente quando se trata toohello nível de confiança colocada em pessoas e arquiteturas de sistema.

Monitoramento, log e auditoria fornecem uma base para acompanhamento e Noções básicas sobre atividades administrativas, mas não pode ser sempre viável tooaudit todas as ações em Concluir detalhes devido toohello quantidade de dados gerados. A auditoria de eficácia Olá das políticas de gerenciamento de saudação é uma prática recomendada, no entanto.

A imposição de políticas que inclui controles de acesso estritos utiliza mecanismos programáticos que podem controlar as ações do administrador e ajuda a garantir que todas as medidas de proteção possíveis sejam usadas. O log fornece verificação de imposição, no registro de tooa de adição de quem fez o quê, de onde e quando. Registro em log também permite que você tooaudit e crosscheck informações sobre como os administradores seguir políticas e fornece evidência de atividades

## <a name="client-configuration"></a>Configuração do cliente
Recomendamos três configurações principais para uma estação de trabalho protegida. diferenciais maiores de saudação entre eles são custo, facilidade de uso e acessibilidade, mantendo um perfil de segurança semelhante em todas as opções. Olá, a tabela a seguir fornece uma análise curta da saudação tooeach de benefícios e riscos. (Observe que "computador corporativo" refere-se tooa desktop PC configuração padrão que deve ser implantada para todos os usuários do domínio, independentemente de funções).

| Configuração | Benefícios | Contras |
| --- | --- | --- |
| Estação de trabalho protegida autônoma |Estação de trabalho rigidamente controlada |custo mais alto para áreas de trabalho dedicadas |
| - | Risco reduzido de explorações de aplicativos |Maior esforço de gerenciamento |
| - | Clara separação de funções | - |
| Computador corporativo como máquina virtual |Menor custo de hardware | - |
| - | Segregação de funções e aplicativos | - |
| Windows toogo com criptografia de unidade de disco BitLocker |Compatibilidade com a maioria dos computadores |Acompanhamento de ativos |
| - | Economia e portabilidade | - |
| - | Ambiente de gerenciamento isolado |- |

É importante que hello protegida de estação de trabalho é host hello e hello convidado sem nada entre hello hospeda hardware hello e de sistema operacional. (Também conhecido como "segura origem") seguir hello "princípio de origem limpo" significa que hospedam Olá que deve ser hello mais protegido. Caso contrário, hello protegido workstation (convidado) é um assunto tooattacks no sistema Olá no qual ele está hospedado.

Você pode separar mais funções administrativas por meio de imagens do sistema dedicado para cada estação de trabalho de proteção que têm somente as ferramentas de saudação e as permissões necessárias para gerenciar selecione Azure aplicativos e na nuvem, com GPOs de DS AD locais específicos de saudação tarefas necessárias.

Para ambientes de TI que não têm nenhuma infraestrutura local (por exemplo, nenhum acesso tooa AD DS locais da instância para os GPOs porque todos os servidores na nuvem Olá), um serviço, como [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) pode simplificar a implantação e manutenção configurações da estação de trabalho.

### <a name="stand-alone-hardened-workstation-for-management"></a>Estação de trabalho protegida autônoma para gerenciamento
Com uma estação de trabalho autônoma protegida, os administradores têm um computador ou laptop que usam para tarefas administrativas e outro computador ou laptop separado para tarefas não administrativas. Uma estação de trabalho dedicada toomanaging os serviços do Azure não é necessário para outros aplicativos instalados. Além disso, o uso de estações de trabalho que dão suporte a [TPM](https://technet.microsoft.com/library/cc766159) (Trusted Platform Module) ou outra tecnologia de criptografia de nível de hardware semelhante auxilia na autenticação de dispositivos e na prevenção de certos ataques. TPM pode também suporte à proteção de volume completo da unidade de sistema hello usando [criptografia de unidade de disco BitLocker](https://technet.microsoft.com/library/cc732774.aspx).

Cenário de estação de trabalho autônoma protegido hello (mostrada abaixo), a instância local saudação do Firewall do Windows (ou um firewall não Microsoft cliente) é tooblock configurado conexões, como RDP de entrada. Olá administrador faça em toohello estação de trabalho robusto e iniciar uma sessão RDP que se conecta tooAzure depois de estabelecer uma VPN se conectar com uma rede Virtual do Azure, mas não é possível fazer logon tooa corporativos PC e usar RDP tooconnect toohello protegidos de estação de trabalho em si.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>Computador corporativo como máquina virtual
Em casos em que uma estação de trabalho robusto autônoma separada é custo Olá proibitivo ou inconveniente, estação de trabalho de proteção pode hospedar um tarefas não administrativas de tooperform de máquina virtual.

![][3]

tooavoid vários riscos de segurança que podem surgir do uso de uma estação de trabalho para gerenciamento de sistemas e outras tarefas de trabalho diário, você pode implantar um toohello de máquina virtual do Hyper-V do Windows protegido estação de trabalho. Esta máquina virtual pode ser usada como Olá PC corporativo. ambiente de PC corporativo Olá pode permanecer isolado Olá Host, o que reduz sua superfície de ataque e remove as atividades diárias do usuário da saudação (como email) da coexistindo com confidenciais tarefas administrativas.

máquina de virtual PC corporativa Olá é executado em um espaço e fornece aplicativos de usuário. host Olá permanece "fonte normal" e impõe políticas de rede restrita no sistema operacional de raiz hello (por exemplo, bloqueio acesso para RDP da máquina virtual de saudação).

### <a name="windows-toogo"></a>TooGo do Windows
Outro toorequiring alternativo uma estação de trabalho de proteção autônoma é toouse uma [tooGo Windows](https://technet.microsoft.com/library/hh831833.aspx) unidade, um recurso que oferece suporte a um recurso de inicialização USB do lado do cliente. TooGo do Windows permite que a imagem do sistema isolado usuários tooboot um computador compatível tooan em execução de uma unidade flash USB criptografada. Ele fornece controles adicionais para pontos de extremidade de administração remota como imagem Olá pode ser totalmente gerenciada por uma equipe de TI corporativa, com as políticas de segurança estrita, uma compilação mínima do sistema operacional, e suporte a TPM.

Figura Olá abaixo, imagem portátil Olá é um sistema de domínio que é tooAzure somente tooconnect pré-configurados, requer a autenticação multifator e bloqueia todo o tráfego de gerenciamento não. Se um usuário é inicializada hello mesmo imagem corporativa do PC toohello padrão e tentativas de acessar o Gateway de área de trabalho remota para as ferramentas de gerenciamento do Azure, a sessão de saudação é bloqueada. TooGo do Windows se torna o sistema de operacional de nível raiz de saudação e nenhum camadas adicionais são necessária (host de sistema operacional, hipervisor, máquina virtual) que pode ser mais vulneráveis ataques de toooutside.

![][4]

É importante toonote que unidades flash USB são perdidas mais facilmente de um computador desktop médio. Uso do BitLocker tooencrypt Olá todo o volume, junto com uma senha forte, torna menos provável que um invasor pode usar a imagem da unidade Olá para fins mal-intencionados. Além disso, se Olá unidade flash USB for perdida, revogando e [emitir um novo certificado de gerenciamento](https://technet.microsoft.com/library/hh831574.aspx) junto com uma senha rápida redefinição pode reduzir a exposição. Logs de auditoria administrativas residam dentro do Azure, não no cliente hello, reduzindo ainda mais a perda de dados.

## <a name="best-practices"></a>Práticas recomendadas
Considere Olá diretrizes adicionais a seguir ao gerenciar aplicativos e dados no Azure.

### <a name="dos-and-donts"></a>Recomendações
Não suponha que, como uma estação de trabalho foi bloqueada que outros requisitos comuns de segurança não é necessário toobe atendido. risco potencial de saudação é maior devido a níveis de acesso com privilégios elevados que geralmente possuem contas de administrador. Exemplos de riscos e suas práticas de seguras alternativas são mostrados na tabela de saudação abaixo.

| Errado | Certo |
| --- | --- |
| Não envie por email credenciais para acesso de administrador ou outros segredos (por exemplo, certificados de gerenciamento ou SSL) |Mantenha a confidencialidade fornecendo nomes de contas e senhas por voz (mas não os armazenando na caixa postal), execute uma instalação remota de certificados de cliente/servidor (por meio de uma sessão criptografada), baixe de um compartilhamento de rede protegido ou distribua manualmente por meio de mídia removível. |
| - | Gerencie os ciclos de vida de certificado de gerenciamento. |
| Não armazene senhas de contas não criptografadas ou sem hash no armazenamento de aplicativos (como em planilhas, sites do SharePoint ou compartilhamentos de arquivos). |Estabelecer políticas de proteção de sistema e princípios de gerenciamento de segurança e aplicá-las tooyour ambiente de desenvolvimento. |
| - | Use [aprimorada 5.5 Kit de ferramentas de experiência de atenuação](https://technet.microsoft.com/security/jj653751) fixação de certificado regras sites SSL/TLS em tooAzure tooensure acesso adequado. |
| Não compartilhe contas e senhas entre administradores nem reutilize senhas em várias contas de usuário ou serviços, particularmente para mídia social ou outras atividades não administrativas. |Criar um toomanage de conta Microsoft dedicado a sua assinatura do Azure — uma conta que não é usada para email pessoal. |
| Não envie arquivos de configuração por email. |Os perfis e arquivos de configuração devem ser instalados de uma fonte confiável (por exemplo, uma unidade flash USB criptografada), não por meio de um mecanismo que possa ser facilmente comprometido, como email. |
| Não use senhas de logon fracas ou simples. |Imponha políticas de senha forte, ciclos de expiração (alteração no primeiro uso), tempos limite de console e bloqueios de conta automáticos. Use um sistema de gerenciamento de senha de cliente com a autenticação multifator para acesso ao cofre de senhas. |
| Não expõem toohello de portas de gerenciamento da Internet. |Bloqueio de portas do Azure e o acesso de gerenciamento de toorestrict de endereços IP. Para obter mais informações, consulte Olá [segurança de rede do Azure](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) white paper. |
| - | Use firewalls, VPNs e NAP para todas as conexões de gerenciamento. |

## <a name="azure-operations"></a>Operações do Azure
Na operação do Azure da Microsoft, os engenheiros de operações e a equipe de suporte que acessam os sistemas de produção do Azure usam [computadores de estações de trabalho protegidos com VMs](#stand-alone-hardened-workstation-for-management) provisionados neles para acesso à rede corporativa interna e aos aplicativos (como email, intranet etc.). Todos os computadores de estação de trabalho de gerenciamento têm TPMs, unidade de inicialização do host de saudação é criptografada com BitLocker e são unidas tooa especiais unidade organizacional (UO) no domínio corporativo do principal da Microsoft.

A proteção do sistema é imposta pela Política de Grupo, com a atualização de software centralizada. Para auditar e análise, logs de eventos (por exemplo, segurança e o AppLocker) são coletados de estações de trabalho de gerenciamento e salvo local central tooa.

Além disso, dedicadas salto caixas na rede da Microsoft que exigem autenticação de dois fatores são rede de produção do tooAzure tooconnect usado.

## <a name="azure-security-checklist"></a>Lista de verificação de segurança do Azure
Minimizar o número de saudação de tarefas que os administradores podem executar em uma estação de trabalho de proteção ajuda a minimizar a superfície de ataque de saudação em seu ambiente de desenvolvimento e gerenciamento. Saudação de uso toohelp tecnologias a seguir proteger sua estação de trabalho de proteção:

* Proteção do IE. Olá navegador Internet Explorer (ou qualquer navegador da web, para essa finalidade) é um ponto de entrada de chave para o código perigoso devido interações de amplo tooits com servidores externos. Examine suas políticas de cliente e imponha a execução no modo protegido, desabilitando complementos e downloads de arquivos e usando a filtragem do [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx). Verifique se os avisos de segurança são exibidos. Tire proveito das zonas da Internet e crie uma lista de sites confiáveis para os quais você configurou proteção razoável. Bloqueie todos os outros sites e código no navegador, como ActiveX e Java.
* Usuário standard. Executando como um usuário padrão apresenta várias vantagens, Olá maior do que é que o roubo de credenciais de administrador por meio de malware se torna mais difícil. Além disso, uma conta de usuário padrão não tem privilégios elevados no sistema de operacional de raiz hello e muitas opções de configuração e as APIs estão bloqueados por padrão.
* AppLocker. Você pode usar [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict Olá programas e scripts que os usuários podem executar. Você pode executar o AppLocker no modo de auditoria ou de imposição. Por padrão, o AppLocker tem uma regra de permissão que permite que os usuários que têm um toorun de token de administrador todo o código no cliente de saudação. Essa regra existe tooprevent administradores bloqueiem seu próprio limite e aplica-se somente os tokens de tooelevated. Confira também Integridade do código como parte da [segurança principal](http://technet.microsoft.com/library/dd348705.aspx) do Windows Server.
* Assinatura de código. A assinatura de código de todas as ferramentas e scripts usados pelos administradores fornece um mecanismo gerenciável para implantar políticas de bloqueio de aplicativos. Hashes não são dimensionados com o código de toohello mudanças rápidas e caminhos de arquivos não fornecem um nível alto de segurança. Você deve combinar as regras do AppLocker com um PowerShell [política de execução](http://technet.microsoft.com/library/ee176961.aspx) que só permite que o código assinado específico e scripts toobe [executado](http://technet.microsoft.com/library/hh849812.aspx).
* Política de Grupo. Criar uma política administrativa global que é aplicada tooany domínio estação de trabalho que é usada para gerenciamento (e bloquear o acesso de todos os outros), e toouser contas autenticadas nessas estações de trabalho.
* Provisionamento com segurança avançada. Proteja sua imagem de estação de trabalho de proteção de linha de base toohelp proteção contra violação. Use medidas de segurança, como criptografia e isolamento toostore imagens, máquinas virtuais e scripts e restringir o acesso (talvez o processo de usar um auditável check-em/check-out).
* Aplicação de patches. Manter uma compilação consistente (ou ter imagens separadas para o desenvolvimento, operações e outras tarefas administrativas), verificar se há alterações malware rotineiramente, lembre-Olá criados toodate e ativar apenas computadores quando eles forem necessários.
* Criptografia. Verifique se as estações de trabalho tem um TPM toomore ativa com segurança [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) e o BitLocker. Se você estiver usando o Windows tooGo, use somente chaves USB criptografadas com BitLocker.
* Governança. Use o AD DS GPOs toocontrol Windows todos os administradores Olá interfaces, como compartilhamento de arquivos. Inclua as estações de trabalho de gerenciamento em processos de auditoria, monitoramento e registro em log. Acompanhe todo o acesso e uso de administradores e desenvolvedores.

## <a name="summary"></a>Resumo
O uso de uma configuração de estação de trabalho protegida para administrar os serviços de nuvem, as Máquinas Virtuais e os aplicativos do Azure pode ajudá-lo a evitar vários riscos e ameaças que podem ocorrer deviso ao gerenciamento remoto da infraestrutura de TI crítica. Azure e Windows fornecer mecanismos que você pode empregar toohelp Proteja e controlam o comportamento do cliente, autenticação e comunicações.

## <a name="next-steps"></a>Próximas etapas
Olá, recursos a seguir estão disponível tooprovide obter mais informações gerais sobre o Azure e serviços da Microsoft, em adição toospecific itens referenciados neste documento relacionados:

* [Protegendo o acesso privilegiado](https://technet.microsoft.com/library/mt631194.aspx) – obter detalhes técnicos Olá Projetando e criando uma estação de trabalho administrativa segura para o gerenciamento do Azure
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) - Saiba mais sobre os recursos de plataforma do Azure que proteger a saudação malha do Azure e Olá cargas de trabalho em execução em que o Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) – onde podem ser relatadas vulnerabilidades de segurança da Microsoft, incluindo problemas com o Azure, ou por meio de email muito[secure@microsoft.com](mailto:secure@microsoft.com)
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – acompanhe toodate em hello mais recente na segurança do Azure

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
