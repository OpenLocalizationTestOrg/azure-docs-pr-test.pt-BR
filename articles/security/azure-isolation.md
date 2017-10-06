---
title: "aaaIsolation em Olá nuvem pública do Azure | Microsoft Docs"
description: "Saiba mais sobre os serviços que podem ser dimensionada para cima e automaticamente toomeet Olá às necessidades de seu aplicativo ou empresa e serviços de computação em nuvem que incluem uma ampla seleção de instâncias de computação."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Isolamento no hello nuvem pública do Azure
##  <a name="introduction"></a>Introdução
### <a name="overview"></a>Visão geral
tooassist atuais e potenciais clientes do Azure entender e utilizar Olá Olá de diversos recursos relacionados à segurança ao redor e disponíveis na plataforma Windows Azure, a Microsoft desenvolveu uma série de White Papers, visões gerais de segurança, as práticas recomendadas, e Listas de verificação.
Olá tópicos variam em termos de amplitude e profundidade e são atualizadas periodicamente. Este documento é parte da série, como resumido na seção de abstrato Olá a seguir.

### <a name="azure-platform"></a>Plataforma Azure
O Azure é uma plataforma de serviço de nuvem aberta e flexível que suporta Olá a seleção mais ampla de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos. Por exemplo, você pode:
- Executar contêineres do Linux com a integração com o Docker;
- Compilar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js; e
- Crie back-ends para dispositivos iOS, Android e Windows.

Microsoft Azure oferece suporte a saudação tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiarem.

Quando você construir ou migra ativos de TI para um provedor de serviços de nuvem pública, você depender de tooprotect de recursos da organização seus aplicativos e dados com hello controles hello e serviços oferecem toomanage segurança de saudação do seu baseado em nuvem ativos.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender às suas necessidades de segurança. Além disso, Azure fornece uma ampla gama de segurança configuráveis toocontrol de capacidade de opções e hello-los para que você possa personalizar requisitos exclusivos de saudação do toomeet de segurança de suas implantações. Este documento ajuda você a atender a esses requisitos.

### <a name="abstract"></a>Resumo

Microsoft Azure permite que você toorun aplicativos e máquinas virtuais (VMs) na infraestrutura física compartilhada. Um dos Olá motivações econômico principal toorunning aplicativos em um ambiente de nuvem é custo de saudação do hello capacidade toodistribute de recursos compartilhados entre vários clientes. Essa prática de multilocação aprimora a eficiência por meio da multiplexação de recursos entre diferentes clientes por custos baixos. Infelizmente, também apresenta riscos de saudação de compartilhar outros toorun de recursos de infraestrutura e servidores físicos seus aplicativos confidenciais e máquinas virtuais que podem pertencer tooan arbitrário e potencialmente mal-intencionado usuário.

Este artigo descreve como o Microsoft Azure fornece isolamento contra usuários mal-intencionados e não pode ser mal-intencionado e serve como um guia para desenvolver soluções de nuvem, oferecendo várias tooarchitects de opções de isolamento. Este white paper concentra-se na tecnologia de saudação da plataforma Windows Azure e controles de segurança do cliente e não tenta tooaddress SLAs, modelos e considerações de práticas recomendadas de DevOps de preços.

## <a name="tenant-level-isolation"></a>Isolamento no nível do locatário
Um dos principais benefícios de saudação de computação é o conceito de uma infraestrutura comum compartilhado entre vários clientes simultaneamente, à esquerda tooeconomies de escala de nuvem. Esse conceito é chamado de multilocação. A Microsoft trabalha continuamente tooensure arquitetura de multilocatário de saudação do Azure de nuvem da Microsoft oferece suporte a padrões de confidencialidade, segurança, privacidade, integridade e disponibilidade.

Em Olá habilitado para a nuvem no local de trabalho, um locatário pode ser definido como um cliente ou a organização que possui e gerencia uma instância específica do serviço em nuvem. Com a plataforma de identidade Olá fornecida pelo Microsoft Azure, um locatário é simplesmente uma instância dedicada do Active Directory do Azure (AD do Azure) que sua organização recebe e detém quando se inscreve em um serviço de nuvem da Microsoft.

Cada diretório do Azure AD é distinto e separado de outros diretórios do Azure AD. Assim como uma construção de escritório corporativo é um tooonly de ativo seguro específico sua organização, um diretório do AD do Azure também foi projetado toobe um ativo seguro para uso unicamente de sua organização. Olá arquitetura do AD do Azure isola cliente dados e informações de identidade de conglomerados. Isso significa que os usuários e administradores de um diretório do Azure AD não podem acessar acidentalmente ou maliciosamente dados em outro diretório.

### <a name="azure-tenancy"></a>Locação do Azure
Aluguel do Azure (assinatura do Azure) refere-se a relação de "cliente/cobrança" tooa e uma única [locatário](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) na [Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). O isolamento no nível do locatário no Microsoft Azure é obtido usando o Azure Active Directory e [controles com base em função](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) oferecidos por ele. Cada assinatura do Azure está associada com um diretório do Azure Active Directory (AD).

Usuários, grupos e aplicativos do diretório podem gerenciar recursos no hello assinatura do Azure. Você pode atribuir esses direitos de acesso usando Olá portal do Azure, as ferramentas de linha de comando do Azure e APIs de gerenciamento do Azure. Um locatário do Azure AD é logicamente isolado usando limites de segurança, para que nenhum cliente possa acessar ou comprometer colocatários, de forma maliciosa ou acidental. O Azure AD é executado em servidores "bare metal" isolados em um segmento de rede segregado, onde a filtragem de pacotes no nível do host e o Firewall do Windows bloqueiam o tráfego e conexões indesejadas.

- Toodata de acesso no AD do Azure exige autenticação do usuário por meio de um [serviço de token de segurança (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Obter informações sobre a existência do usuário hello, estado habilitado e função são usadas por toodetermine de sistema de autorização de saudação se locatário de destino em toohello Olá acesso solicitado está autorizado para este usuário nesta sessão.

![Locação do Azure](./media/azure-isolation/azure-isolation-fig1.png)


- Os locatários são contêineres discretos, e não há nenhuma relação entre eles.

- Não há acesso entre os locatários, a menos que o administrador de locatários o conceda por meio de federação ou do provisionamento de contas de usuários de outros locatários.

- Acesso físico tooservers que compõem o serviço de saudação do AD do Azure e sistemas de acesso direto tooAzure do AD do back-end, é restrito.

- Os usuários do AD do Azure não têm nenhum acesso toophysical ativos ou locais e, portanto, não é possível para toobypass-los Olá RBAC política verificações lógicas indicadas a seguir.

Para as necessidades de diagnóstico e manutenção, um modelo operacional que emprega um sistema de elevação de privilégio just-in-time é exigido e usado. Azure AD Privileged Identity Management (PIM) apresenta o conceito de saudação do administrador qualificados. [Administradores elegíveis](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) devem ser usuários que precisam de acesso privilegiado às vezes, mas não todos os dias. função Hello está inativa até que o usuário Olá precisa de acesso, em seguida, eles concluir um processo de ativação e se tornar um administrador ativo para uma quantidade predeterminada de tempo.

![Gerenciamento de identidades com privilégios do AD do Azure](./media/azure-isolation/azure-isolation-fig2.png)

Active Directory do Azure hospeda cada locatário em seu próprio contêiner protegido, com tooand políticas e permissões no contêiner de saudação exclusivamente de propriedade e gerenciados por locatário hello.

conceito de saudação de contêineres de locatário é profundamente inata no serviço de diretório de saudação em todas as camadas, de portais todos Olá armazenamento de toopersistent de forma.

Mesmo quando os metadados de vários locatários do Active Directory do Azure são armazenados em Olá mesmo físico em disco, não há nenhuma relação entre contêineres Olá diferente que é definido pelo serviço de diretório hello, que por sua vez é determinado pelo administrador de locatários hello.

### <a name="azure-role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função) do Azure
[Controle de acesso do Azure baseado em função (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) ajuda você tooshare vários componentes disponíveis dentro de uma assinatura do Azure, fornecendo gerenciamento de acesso refinado para o Azure. RBAC do Azure permite que você toosegregate tarefas dentro de sua organização e conceder acesso com base em que os usuários precisam tooperform seus trabalhos. Em vez de dar a todos permissões irrestritas na assinatura ou recursos do Azure, você pode permitir apenas certas ações.

RBAC do Azure tem três funções básicas que se aplicam a tipos de recurso de tooall:

- **Proprietário** tem acesso completo tooall recursos incluindo Olá toodelegate direito acesso tooothers.

- **Colaborador** pode criar e gerenciar todos os tipos de recursos do Azure, mas não é possível conceder acesso tooothers.

- **leitor** pode exibir os recursos existentes do Azure.

![Controle de acesso baseado em função do Azure](./media/azure-isolation/azure-isolation-fig3.png)

rest Olá das funções de RBAC hello Azure permitir o gerenciamento de recursos do Azure específicos. Por exemplo, hello função Colaborador da máquina Virtual permite Olá toocreate de usuário e gerenciar máquinas virtuais. Ele não oferece a eles acesso toohello rede Virtual do Azure ou sub-rede Olá Olá máquina virtual se conecta ao.

[Funções internas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) listar Olá funções disponíveis no Azure. Especifica operações hello e escopo de cada função interna concede toousers. Se você estiver procurando toodefine suas próprias funções para controlar ainda mais, consulte como toobuild [funções personalizadas no Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Entre os outros recursos para o Azure Active Directory estão:
- O AD do Azure permite que os aplicativos de tooSaaS SSO, independentemente de onde eles estão hospedados. Alguns aplicativos são federados com o AD do Azure e outros usam SSO com senha. Os aplicativos federados também podem dar suporte ao provisionamento do usuário e ao [armazenamento de senha no cofre](https://www.techopedia.com/definition/31415/password-vault).

- Acesso toodata em [armazenamento do Azure](https://azure.microsoft.com/services/storage/) é controlado através da autenticação. Cada conta de armazenamento tem uma chave primária ([chave da conta de armazenamento](https://docs.microsoft.com/azure/storage/storage-create-storage-account), ou SAK) e uma chave de segredo secundária (assinatura de acesso compartilhado hello, ou SAS).

- O Azure AD fornece identidade como um serviço de federação usando [Serviços de Federação do Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), sincronização e replicação com diretórios locais.

- [Autenticação multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) é o serviço de autenticação multifator Olá que exige que os usuários tooverify entradas usando um aplicativo móvel, chamada telefônica ou mensagem de texto. Ele pode ser usado com recursos do AD do Azure toohelp local seguro com o servidor de autenticação multifator do Azure Olá e também com diretórios usando Olá SDK e aplicativos personalizados.

- [Serviços de domínio do AD do Azure](https://azure.microsoft.com/services/active-directory-ds/) permite você entrar no domínio de Active Directory tooan máquinas virtuais do Azure sem implantar controladores de domínio. Você pode entrar em máquinas virtuais de toothese com suas credenciais corporativas do Active Directory e administrar computadores que ingressaram no domínio virtual com linhas de base de segurança de tooenforce política de grupo em todas as suas máquinas virtuais do Azure.

- [B2C de diretório ativo do Azure](https://azure.microsoft.com/services/active-directory-b2c/) fornece um serviço de gerenciamento de identidade global altamente disponíveis para aplicativos voltados para o consumidor que pode ser dimensionado toohundreds de milhões de identidades. Ele pode ser integrado a plataformas móveis e da Web. Seus consumidores podem entrar tooall seus aplicativos por meio de experiências personalizáveis com suas contas sociais existentes ou criando credenciais.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Isolamento dos administradores da Microsoft e exclusão de dados
Microsoft usa medidas forte tooprotect seus dados contra acesso não autorizado ou uso por pessoas não autorizadas. Esses controles e processos operacionais com suporte de saudação [termos de serviços Online](http://aka.ms/Online-Services-Terms), que oferecem contratuais compromissos que controlam acesso tooyour dados.

-   Os engenheiros da Microsoft não tem dados de tooyour de acesso padrão na nuvem hello. Em vez disso, eles recebem acesso sob supervisão de gerenciamento, apenas quando é necessário. Esse acesso é cuidadosamente controlado e registrado em log, sendo revogado assim que não é mais necessário.

-   Microsoft pode contratar outros serviços tooprovide limitado de empresas em seu nome. Subcontratados podem acessar os serviços de saudação do cliente dados toodeliver somente para os quais, contratamos-los tooprovide, e elas estão proibidas de usá-lo para qualquer outra finalidade. Além disso, eles são associados ao contrato toomaintain Olá confidencialidade de informações de nossos clientes.

Serviços comerciais com certificações auditados como ISO/IEC 27001 regularmente verificados pela Microsoft e credenciado auditoria empresas que executam tooattest de auditorias de exemplo que o acesso, apenas para fins comerciais legítima. Você pode acessar os dados de seus clientes a qualquer momento e por qualquer motivo.

Se você excluir todos os dados, o Microsoft Azure exclui dados hello, incluindo quaisquer cópias em cache ou de backup. Para serviços em escopo, que a exclusão ocorrerá dentro de 90 dias após o término de Olá Olá do período de retenção. (Em escopo serviços são definidos na seção de termos de processamento de dados de saudação do nosso [termos de serviços Online](http://aka.ms/Online-Services-Terms).)

Se uma unidade de disco usada para armazenamento sofrer uma falha de hardware, com segurança é [apagados ou destruído](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) antes Microsoft retorna toohello fabricante para reparo ou substituição. Olá dados na unidade de saudação são substituídos tooensure que Olá dados não pode ser recuperado por qualquer meio.

## <a name="compute-isolation"></a>Isolamento de computação
O Microsoft Azure fornece vários serviços computação em nuvem que incluem uma ampla seleção de instâncias de computação e serviços que podem ser dimensionada para cima e automaticamente toomeet Olá às necessidades de seu aplicativo ou enterprise. Esses instância de computação e o serviço de oferecem isolamento de dados de toosecure vários níveis sem sacrificar a saudação flexibilidade na configuração que os clientes exigem.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Isolamento de sistema operacional raiz e Hyper-V entre a VM raiz e as VMs convidadas
A plataforma de computação do Azure tem base na virtualização da máquina — ou seja, todo o código do cliente é executado em uma máquina virtual Hyper-V. Em cada nó do Azure (ou ponto de extremidade de rede), há um hipervisor que é executado diretamente sobre o hardware de saudação e divide um nó em um número variável de convidado (máquinas virtuais).


![Isolamento de sistema operacional raiz e Hyper-V entre a VM raiz e as VMs convidadas](./media/azure-isolation/azure-isolation-fig4.jpg)


Cada nó também tem uma VM raiz especial, que é executado Olá SO de Host. Um limite crítico é o isolamento de saudação de raiz de saudação VM de convidado Olá VMs e convidado Olá VMs umas das outras, gerenciadas pelo hipervisor hello e sistema operacional de raiz de saudação. emparelhamento de hipervisor/sistema operacional de raiz Olá aproveita décadas da Microsoft de experiência de segurança do sistema operacional e aprendizado mais recente do Microsoft Hyper-V, tooprovide forte isolamento de VMs convidadas.

Olá plataforma Windows Azure usa um ambiente virtualizado. Instâncias de usuário funcionam como máquinas virtuais autônomas que não têm o servidor do acesso tooa host físico, e esse isolamento é imposto usando níveis de privilégio (anel-0/anel-3) do processador físico.

Anel 0 é hello mais privilegiada e 3 é hello menos. sistema operacional convidado de saudação é executado em um anel de menor privilégio 1 e aplicativos executados em hello 3 de anel com menos privilégios. Essa virtualização dos recursos físicos leva tooa clara separação entre o sistema operacional convidado e do hipervisor, resultando na separação de segurança adicional entre hello dois.

Hello Azure hipervisor age como um micro-kernel e passa todas as solicitações de acesso de hardware do host de toohello de máquinas virtuais de convidados para processamento usando uma interface de memória compartilhada chamada VMBus. Isso impede que os usuários obtenham o sistema de toohello de acesso de leitura/gravação/execução bruto e reduz o risco de saudação do compartilhamento de recursos do sistema.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Algoritmo avançado de posicionamento da VM e proteção contra ataques de canal lateral
Qualquer ataque entre VM envolve duas etapas: colocar uma VM controlado adversário em Olá mesmo host como uma vítima Olá VMs e, em seguida, serem violados Olá tooeither de limites de isolamento roubar informações confidenciais vítima ou afetar o desempenho para ganância ou vandalismo. O Microsoft Azure fornece proteção nas duas etapas usando um algoritmo avançado de posicionamento de VM e proteção contra todos os ataques de canal lateral conhecidos, incluindo VMs vizinhas barulhentas.

### <a name="hello-azure-fabric-controller"></a>Olá controlador de malha do Azure
Olá controlador de malha do Azure é responsável pela alocação de recursos de infraestrutura tootenant cargas de trabalho e gerencia a comunicação unidirecional de máquinas de toovirtual Olá host. algoritmo de colocação Olá VM do controlador de malha do Azure Olá é sofisticado e praticamente impossível toopredict como nível de host físico.

![Olá controlador de malha do Azure](./media/azure-isolation/azure-isolation-fig5.png)

Olá hipervisor do Azure impõe a memória e separação do processo entre máquinas virtuais e o roteamento seguro de locatários de tooguest SO de tráfego de rede. Isso elimina a possibilidade de ataques de canal lateral no nível da VM.

No Azure, a raiz de saudação VM é especial: ele é executado em um sistema operacional protegido chamado raiz Olá sistema operacional que hospeda um agente de malha (FA). FAs são usados em agentes convidados toomanage ativar (GA) em sistemas operacionais de convidado em máquinas virtuais do cliente. Os FAs também gerenciam nós de armazenamento.

coleção de hipervisor do Azure, Hello raiz SO/FA e cliente VMs/gás consiste em um nó de computação. Os FAs são gerenciados por um controlador de malha (FC), que existe fora dos nós de computação e de armazenamento (clusters de computação e de armazenamento são gerenciados por FCs separados). Se um cliente atualiza o arquivo de configuração do seu aplicativo enquanto ele está em execução, Olá FC se comunica com hello FA, que então contata o gás, qual notificar o aplicativo hello de alteração de configuração de saudação. No caso de saudação de uma falha de hardware, Olá FC será automaticamente encontrar componentes de hardware disponíveis e reinicie Olá VM.

![Controlador de malha do Azure](./media/azure-isolation/azure-isolation-fig6.jpg)

Comunicação do agente de tooan controlador de malha é unidirecional. Agente de saudação implementa um serviço protegido por SSL que responde apenas toorequests do controlador de saudação. Ele não pode iniciar o controlador de toohello de conexões ou outros nós internos privilegiados. Olá FC trata todas as respostas como se fossem não confiáveis.


![Controlador de malha](./media/azure-isolation/azure-isolation-fig7.png)

Isolamento estende da saudação VM raiz de VMs convidadas e Olá VMs convidadas uns dos outros. Os nós de computação também são isolados dos nós de armazenamento para aumentar a proteção.


Olá hipervisor e sistema operacional do host Olá fornecem o pacote de rede - filtros toohelp assegurar que máquinas de virtuais não confiáveis não pode gerar tráfego falsificado ou receber tráfego não endereçado toothem, pontos de extremidade de infraestrutura do tráfego direto tooprotected ou enviar/receber tráfego de difusão inadequado.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>As regras adicionais configuradas pelo agente de controlador de malha tooIsolate VM
Por padrão, todo o tráfego é bloqueado quando uma máquina virtual é criada, e, em seguida, o agente de controlador de malha Olá configura Olá pacote filtro tooadd regras e exceções tooallow autorizado tráfego.

Há duas categorias de regras que são programadas:

-   **Configuração de máquina ou regras de infraestrutura**: por padrão, toda a comunicação é bloqueada. Há é exceções tooallow toosend uma máquina virtual e receber o tráfego DHCP e DNS. Máquinas virtuais também pode enviar tráfego toohello "público" da internet e enviar tráfego tooother máquinas virtuais em Olá mesma rede Virtual do Azure e Olá o servidor de ativação do sistema operacional. lista de saudação das máquinas virtuais permitido destinos de saída não inclui sub-redes do roteador do Azure, gerenciamento do Azure e outras propriedades de Microsoft.

-   **Arquivo de configuração de função:** define Olá entrada controle listas de acesso (ACLs) com base no modelo de serviço do locatário hello.

### <a name="vlan-isolation"></a>Isolamento de VLAN
Há três VLANs em cada cluster:

![Isolamento de VLAN](./media/azure-isolation/azure-isolation-fig8.jpg)


-   Olá, VLAN principal – interconexões nós de cliente não confiável

-   Olá FC VLAN – contém FCs confiável e sistemas de suporte

-   Olá dispositivo VLAN – contém redes confiáveis e outros dispositivos de infraestrutura

A comunicação é permitida do hello FC VLAN toohello VLAN principal, mas não pode ser iniciado do hello toohello principal da VLAN FC VLAN. Comunicação também é bloqueada de dispositivo de toohello VLAN principal do hello VLAN. Isso garante que o mesmo que um nó que executa o código de cliente estiver comprometido, não é possível ataque nós Olá FC ou dispositivo VLANs.

## <a name="storage-isolation"></a>Isolamento de armazenamento
### <a name="logical-isolation-between-compute-and-storage"></a>Isolamento lógico entre computação e armazenamento
Como parte de seu design fundamental, o Microsoft Azure separa a computação baseada em VM do armazenamento. Essa separação permite computação e armazenamento tooscale independentemente, tornando mais fácil tooprovide multilocação e isolamento.

Portanto, é executado de armazenamento do Azure no hardware separado com nenhum tooAzure de conectividade de rede de computação exceto logicamente. [Isso](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) significa que, quando um disco virtual é criado, o espaço em disco não é alocado totalmente. Em vez disso, é criada uma tabela que mapeia endereços em Olá tooareas de disco virtual no disco físico hello e essa tabela é inicialmente vazia. **Olá primeira vez que um cliente grava dados no disco virtual de Olá, seja alocado espaço em disco físico hello e tooit um ponteiro é colocado na tabela de saudação.**
### <a name="isolation-using-storage-access-control"></a>Isolamento usando o Controle de acesso de armazenamento
**O Controle de acesso no Armazenamento do Azure** tem um modelo de controle de acesso simples. Cada assinatura do Azure pode criar uma ou mais Contas de armazenamento. Cada conta de armazenamento tem uma única chave secreta que é usado toocontrol acesso tooall dados nessa conta de armazenamento.

![Isolamento usando o Controle de acesso de armazenamento](./media/azure-isolation/azure-isolation-fig9.png)

**Acessar dados de armazenamento tooAzure (incluindo as tabelas)** pode ser controlado por meio de um [SAS (assinatura de acesso compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) token, que concede acesso de escopo. Olá SAS é criado por meio de um modelo de consulta (URL) assinado com hello [SAK (chave de conta de armazenamento)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Que [assinado URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) tooanother processo (isto é, delegado), que pode, em seguida, preencha os detalhes de Olá de consulta hello e fazer a solicitação Olá Olá do serviço de armazenamento pode ser fornecido. Uma SAS permite que você toogrant acesso com base no tempo tooclients sem revelar a chave secreta da conta de armazenamento hello.

Olá SAS significa que podemos pode conceder que permissões, tooobjects em nossa conta de armazenamento para um determinado período de tempo e com um conjunto de permissões especificado de limitadas a um cliente. Podemos pode conceder essas permissões limitados sem a necessidade de tooshare suas chaves de acesso da conta.

### <a name="ip-level-storage-isolation"></a>Isolamento de armazenamento no nível do IP
Você pode habilitar o firewall e definir um intervalo de endereços IP para seus clientes confiáveis. Com um intervalo de endereços IP, somente os clientes que têm um endereço IP dentro do intervalo de saudação definido podem se conectar muito[armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-security-guide).

Dados de armazenamento IP podem ser protegidos contra usuários não autorizados por meio de um mecanismo de rede que é usado tooallocate um túnel dedicado ou dedicado de armazenamento de tooIP de tráfego.

### <a name="encryption"></a>Criptografia
Azure oferece os seguintes tipos de dados de tooprotect de criptografia:
-   Criptografia em trânsito

-   Criptografia em repouso

#### <a name="encryption-in-transit"></a>Criptografia em trânsito
A criptografia em trânsito é um mecanismo de proteção de dados quando eles são transmitidos entre redes. Com o Armazenamento do Azure, você pode proteger dados usando:

-   [Criptografia de nível de transporte](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), como HTTPS ao transferir dados dentro ou fora do Armazenamento do Azure.

-   [Criptografia na transmissão](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), como a criptografia SMB 3.0 para compartilhamentos de Arquivo do Azure.

-   [Criptografia do lado do cliente](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), dados de saudação tooencrypt antes que sejam transferidos em dados de saudação do armazenamento e toodecrypt depois que ela é transferida do armazenamento.

#### <a name="encryption-at-rest"></a>Criptografia em repouso
Para muitas organizações, a [criptografia de dados em repouso](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) é uma etapa obrigatória no sentido de garantir a soberania, a privacidade e a conformidade dos dados. Há três recursos do Azure que fornecem criptografia de dados que estão “em repouso”:

-   [Criptografia do serviço de armazenamento](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) permite que o serviço de armazenamento de saudação criptografa automaticamente os dados quando escrever tooAzure armazenamento de toorequest.

-   [Criptografia do lado do cliente](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) também fornece o recurso de saudação de criptografia em repouso.

-   [Criptografia de disco do Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) permite que você tooencrypt Olá OS discos e dados usados por uma máquina virtual IaaS.

#### <a name="azure-disk-encryption"></a>Azure Disk Encryption
O [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) para VMs (Máquinas Virtuais) o ajuda a atender aos requisitos de conformidade e segurança organizacionais criptografando os discos de VM (incluindo discos de dados e de inicialização) com chaves e políticas controladas no [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Olá solução de criptografia de disco para o Windows é baseado no [Microsoft BitLocker Drive Encryption](https://technet.microsoft.com/library/cc732774.aspx), e Olá Linux solução se baseia em [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

solução de saudação dá suporte à saudação os seguintes cenários para VMs de IaaS quando eles estão habilitados no Microsoft Azure:
-   Integração com o Cofre da Chave do Azure

-   VMs da camada Standard: VMs IaaS das séries A, D, DS, G, GS e assim por diante

-   Como habilitar a criptografia em VMs IaaS Windows e Linux

-   Como desabilitar a criptografia em unidades do sistema operacional e de dados para VMs IaaS do Windows

-   Como desabilitar a criptografia em unidades de dados para VMs IaaS do Linux

-   Ativando a criptografia em VMs IaaS que estão executando o sistema operacional cliente Windows

-   Como habilitar a criptografia em volumes com caminhos de montagem

-   Habilitação da criptografia em VMs do Linux que estão configuradas com distribuição de discos (RAID) usando o [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Como habilitar a criptografia em VMs do Linux usando [LVM (Gerenciador de Volume Lógico)](https://msdn.microsoft.com/library/windows/desktop/bb540532) para discos de dados

-   Ativando a criptografia em VMs do Windows que são configurados usando espaços de armazenamento

-   Há suporte para todas as regiões públicas do Azure

solução de saudação não oferece suporte a saudação tecnologia versão hello, recursos e cenários a seguir:

-   VMs IaaS da camada Básica

-   Como desabilitar a criptografia em unidades do sistema operacional para VMs IaaS do Linux

-   VMs de IaaS que são criadas usando o método de criação de VM clássico Olá

-   Integração com o Serviço de Gerenciamento de Chaves no local

-   Arquivos do Azure (sistema de arquivos compartilhados), NFS (Network File System), volumes dinâmicos e VMs do Windows configuradas com Sistemas RAID baseados em software

## <a name="sql-azure-database-isolation"></a>Isolamento do Banco de Dados SQL Azure
Banco de dados SQL é um serviço de banco de dados relacional na nuvem da Microsoft hello com base no mecanismo de Microsoft SQL Server do hello líder do mercado e capaz de lidar com cargas de trabalho de missão crítica. O Banco de Dados SQL oferece isolamento previsível de dados no nível da conta, com base na geografia/região e na rede, tudo com administração quase zero.

### <a name="sql-azure-application-model"></a>Modelo de aplicativo do SQL Azure

[O Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) é um serviço de banco de dados relacional baseado em nuvem compilado com tecnologias do SQL Server. Ele fornece um serviço de banco de dados multilocatário altamente disponível e escalonável hospedado pela Microsoft na nuvem.

Da perspectiva do aplicativo do SQL Azure fornece Olá hierarquia a seguir: cada nível tem um-para-muitos contenção de níveis abaixo.

![Modelo de aplicativo do SQL Azure](./media/azure-isolation/azure-isolation-fig10.png)

Olá conta e assinatura são gerenciamento e a cobrança de tooassociate de conceitos de plataforma Microsoft Azure.

Servidores e bancos de dados lógicos são conceitos específicos do SQL Azure e são gerenciados usando o SQL Azure, pelas interfaces do OData e do TSQL ou por meio do Portal do SQL Azure, que é integrado ao Portal do Azure.

Os servidores do SQL Azure não são instâncias físicas ou de VM, em vez disso, são coleções de bancos de dados que compartilham políticas de gerenciamento e segurança, armazenadas no chamado banco de dados de "mestre lógico".

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Os bancos de dados mestres lógicos incluem:

-   Logons do SQL Server usada tooconnect toohello server

-   Regras de firewall

Cobrança e relacionados à utilização de informações para bancos de dados do SQL Azure de saudação mesmo servidor lógico não estão garantidas toobe em Olá mesma instância física em cluster do SQL Azure, em vez disso, aplicativos devem fornecer nome de banco de dados de destino Olá ao se conectar.

Da perspectiva do cliente, um servidor lógico é criado em uma região geográfica gráfica enquanto criação real de saudação do servidor de saudação ocorre em um dos clusters de saudação na região de saudação.

### <a name="isolation-through-network-topology"></a>Isolamento por meio da topologia de rede

Quando um servidor lógico é criado e seu nome DNS é registrado, o nome DNS de saudação pontos toohello chamado endereço "Gateway VIP" no Centro de dados específicos de saudação em que o servidor de saudação foi colocado.

Atrás Olá VIP (endereço IP virtual), temos uma coleção de serviços de gateway sem monitoração de estado. Em geral, os gateways são envolvidos quando há a necessidade de coordenação entre várias fontes de dados (banco de dados mestre, banco de dados do usuário etc.). Serviços de gateway implementam seguinte hello:
-   **Proxy de conexão de TDS.** Isso inclui localizando o banco de dados de usuário no cluster de back-end de saudação, Implementando a sequência de logon de saudação e encaminhamento de volta e Olá TDS pacotes toohello back-end.

-   **Gerenciamento do banco de dados.** Isso inclui a implementação de uma coleção de operações de banco de dados CREATE/ALTER/DROP de toodo fluxos de trabalho. operações de banco de dados de saudação podem ser chamadas por rastreiem pacotes TDS ou explícita APIs OData.

-   Operações de logon/usuário CREATE/ALTER/DROP

-   Operações de gerenciamento de servidor lógico por meio da API do OData

![Isolamento por meio da topologia de rede](./media/azure-isolation/azure-isolation-fig12.png)

camada Olá atrás de gateways de saudação é chamada de "back-end". Isso é onde todos os dados de saudação são armazenados de maneira altamente disponível. Cada parte de dados é tal toobelong tooa "partição de" ou "unidade de failover," cada um pelo menos três réplicas. Réplicas são armazenadas e replicadas pelo mecanismo do SQL Server e gerenciadas por um sistema geralmente chamado de failover tooas "malha".

Em geral, sistema back-end de saudação não se comunicam sistemas tooother saída como uma precaução de segurança. Isso é reservado toohello sistemas na camada de front-end (gateway) de saudação. máquinas de camada de gateway Olá privilégios limitados na superfície de ataque do hello máquinas de back-end toominimize hello como um mecanismo de defesa em profundidade.

### <a name="isolation-by-machine-function-and-access"></a>Isolamento por função e acesso do computador
O SQL Azure é composto por serviços em execução nas funções de máquina diferentes. O SQL Azure é dividido em "back-end" banco de dados de nuvem "front-end" (Gateway/ambientes e gerenciamento), a princípio geral Olá de entrada de tráfego somente back-end e não-out. ambiente de front-end Olá pode se comunicar toohello fora do mundo de outros serviços e em geral, tenha somente permissões limitadas no back-end de saudação (suficiente toocall Olá pontos de entrada-necessidades tooinvoke).

## <a name="networking-isolation"></a>Isolamento de rede
A implantação do Azure têm vários níveis de isolamento de rede. Olá diagrama a seguir mostra várias camadas do Azure fornece toocustomers de isolamento de rede. Essas camadas são nativo em Olá plataforma do Azure e recursos definidos pelo cliente. Entrada de saudação à Internet, DDoS Azure fornece isolamento contra ataques em grande escala no Azure. Olá próxima camada de isolamento é definido pelo cliente endereços IP públicos (pontos de extremidade), que são usado toodetermine tráfego que pode passar por rede virtual do hello nuvem serviço toohello. O isolamento de rede virtual Nativa do Azure garante o isolamento completo de todas as outras redes e garante que o tráfego flua somente através de métodos e caminhos configurados pelo usuário. Esses caminhos e os métodos são próxima camada hello, onde os NSGs, UDR e dispositivos de rede virtual podem ser toocreate usado isolamento limites tooprotect Olá implantações de aplicativos em rede Olá protegido.

![Isolamento de rede](./media/azure-isolation/azure-isolation-fig13.png)

**Isolamento de tráfego:** um [rede virtual](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) é o limite de isolamento de tráfego Olá em Olá plataforma Windows Azure. Máquinas virtuais (VMs) em uma rede virtual não pode se comunicar diretamente tooVMs em uma rede virtual diferente, mesmo se as duas redes virtuais são criadas por Olá mesmo cliente. Isolamento é uma propriedade vital que garante que as VMs e as comunicações do cliente permaneçam privadas em uma rede virtual.

[Subrede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) oferece uma camada adicional de isolamento na rede virtual com base no intervalo de IPs. Endereços IP na rede virtual hello, você pode dividir uma rede virtual em várias sub-redes para a organização e segurança. VMs e PaaS função instâncias implantadas toosubnets (igual ou diferente) dentro de uma rede virtual podem se comunicar uns com os outros sem qualquer configuração adicional. Você também pode configurar [o grupo de segurança de rede (NSGs)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow ou negar a instância VM de tooa de tráfego de rede com base em regras configuradas na lista de controle de acesso (ACL) do NSG. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um NSG está associado uma sub-rede, regras de ACL de saudação se aplicam a instâncias de VM Olá tooall nessa sub-rede.

## <a name="next-steps"></a>Próximas etapas

- [Opções de isolamento de rede para computadores em redes virtuais do Windows Azure](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Isso inclui Olá clássico front-end e back-end cenário em que máquinas em uma rede de back-end específico ou uma sub-rede podem permitir apenas determinados clientes ou outros computadores tooconnect tooa ponto de extremidade específico com base em uma lista branca de endereços IP.

- [Isolamento de computação](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

O Microsoft Azure fornece um serviços computação vários baseado em nuvem que incluem uma ampla seleção de instâncias de computação e serviços que podem ser dimensionada para cima e automaticamente toomeet Olá às necessidades de seu aplicativo ou enterprise.

- [Isolamento de armazenamento](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

O Microsoft Azure separa a computação baseada em VM do cliente do armazenamento. Essa separação permite computação e armazenamento tooscale independentemente, tornando mais fácil tooprovide multilocação e isolamento. Portanto, é executado de armazenamento do Azure no hardware separado com nenhum tooAzure de conectividade de rede de computação exceto logicamente. Todas as solicitações são executadas via HTTP ou HTTPS com base na escolha do cliente.

