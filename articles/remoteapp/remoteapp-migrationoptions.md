---
title: "aaaOptions para a migração do Azure RemoteApp | Microsoft Docs"
description: "Saiba mais sobre opções de saudação para migrar do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Opções de migração fora do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.


Se você interrompeu a usar o Azure RemoteApp devido a saudação [anúncio de desativação](https://go.microsoft.com/fwlink/?linkid=821148) ou como terminar sua avaliação, é necessário toomigrate do serviço de aplicativo do Azure RemoteApp tooanother. Há duas abordagens diferentes para a migração: uma implantação autogerenciada (geralmente chamada de IaaS [infraestrutura como serviço]) ou uma oferta totalmente gerenciada (geralmente chamada de PaaS/SaaS [plataforma como serviço ou software como serviço]). 

O IaaS de autoatendimento é uma implantação do tipo faça você mesmo que é gerenciada, operada e de sua propriedade, implantada diretamente em VMs (máquinas virtuais) ou sistemas físicos. Em outros Olá terminar uma totalmente gerenciado PaaS/oferta de SaaS é mais como o Azure RemoteApp - um parceiro fornece uma camada de serviço sobre uma solução de comunicação remota que manipula operacionais e manutenção, enquanto você, como cliente Olá, fazer alguns gerenciamento de aplicativos e de imagem.

[Exibir hello Azure RemoteApp webinars nas opções de migração](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou continue lendo para obter mais informações (incluindo exemplos de saudação diferente opções de hospedagem).

## <a name="self-managed-iaas-solutions"></a>Soluções (IaaS) autogerenciadas
### <a name="rds-on-iaas"></a>**RDS em IaaS**
Você pode implantar uma implantação de Serviços de Área de Trabalho Remota (no Windows Server) com base em sessão nativa usando o RemoteApp ou áreas de trabalho locais ou em um ambiente hospedado (como em VMs do Azure). Os RDS em implantações de IaaS são melhores para os clientes já familiarizados com eles e que já têm experiência técnica com implantações de RDS. 

> [!NOTE]
> Você precisa com Software Assurance (SA) de licenciamento por Volume para toouse de licenças de acesso de cliente RDS essa opção de implantação.

A implantação dos RDS na VMs do Azure é mais fácil do que nunca quando você usa modelos de aplicação de patch e de implantação (leia uma [visão geral](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e [obtenha-as](https://aka.ms/rdautomation)). Você pode obter Olá mesmo recursos de dimensionamento Elásticos com recursos de modelo de implantação clássico do Azure (não recursos de modelo de recurso do Azure) dentro do Azure RemoteApp usando Olá [script de escala automática](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), embora não haja mais configurações e personalizações. Quando você implanta RDS em VMs do Azure, o suporte é fornecido por meio de [suporte do Azure](https://azure.microsoft.com/support/plans/), Olá mesmo profissionais de suporte que o suporte para você com o Azure RemoteApp. Você pode obter estimativas de custo com base no seu uso existente entrando em contato com [suporte do Azure](https://azure.microsoft.com/support/plans/), ou você pode executar cálculos usando um breve toobe liberado Calculadora de preços.  Além disso, com as VMs da série N (atualmente na visualização privada) você pode adicionar vGPU - saber mais sobre como adicionar vGPU e sobre como muito[utilizem as melhorias de RDS no Windows Server 2016](https://myignite.microsoft.com/videos/2794) em nossa sessão Ignite.   

Temos guias passo a passo de implantação para [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist com sua implantação. Check-out Olá [blog de área de trabalho remota](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para notícias mais recentes hello.

### <a name="citrix-on-iaas"></a>**Citrix no IaaS**
Uma implantação de Citrix nativa de XenApp ou XenDesktop com base em sessão pode ser implantada localmente ou em um ambiente hospedado (como em VMs do Azure). 

Check-out de guia de implantação passo a passo do hello [Citrix XA 7.6 no Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), para obter mais informações. Leia mais sobre [Citrix no Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), incluindo uma calculadora de preços. Você também pode encontrar um [Citrix contato](http://citrix.com/English/contact/index.asp) toodiscuss suas opções de com.

## <a name="fully-managed-paassaas-offerings"></a>Ofertas (PaaS/SaaS) totalmente gerenciadas

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (lançado em abril de 2017)
Disponível no hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials é o novo serviço de virtualização de aplicativo hello, combinando power hello e flexibilidade de Olá plataforma de nuvem Citrix com hello simples e prescritivas, e fácil de consumir a visão do Microsoft Azure RemoteApp. 

Os clientes existentes do Azure RemoteApp podem [registrar-se para uma avaliação gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Observação: somente o encargo de serviço do usuário do Citrix é gratuito, os custos de computação e armazenamento do Azure ainda se aplicam

Saiba Mais:
- [Migrar do Azure RemoteApp tooCitrix XenApp Essentials](remoteapp-migrate-citrix.md)
- [Citrix e Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Apresentação do Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix Cloud XenApp Service e XenDesktop Service 

[Serviço de nuvem XenApp do Citrix e XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) é a melhor solução Olá para entrega de saudação de aplicativos e desktops, além de gerenciamento avançado e recursos de monitoramento. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (nome da plataforma: MyCloudIT)
[MyCloudIT](https://mycloudit.com) é uma plataforma de automação para toosimplify de empresas IT, otimizar e dimensionar migração hello e Olá de entrega de áreas de trabalho remotas, aplicativos remotos e infraestrutura de nuvem do Microsoft Azure. 

plataforma de MyCloudIT Olá reduz o tempo de implantação em 95%, o custo em 30% do Azure e move a infra-estrutura de TI do seu cliente para nuvem Olá em questão de alguns pressionamentos de tecla. Parceiros agora podem gerenciar os clientes de um painel global, os usuários finais de serviço em torno de Olá, mundo como nunca antes e aumentar as receitas sem adicionar uma sobrecarga adicional ou amplo treinamento do Azure.  

> Localização primária: Dallas, Texas, EUA
> 
> Região de operação: em todo o mundo
> 
> Status de parceiro: [ouro](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Provedor de Serviços Microsoft Cloud: sim
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos
> 
> Soluções de migração do Azure RemoteApp: sim, [saiba mais](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, vice-presidente de desenvolvimento de negócios
> 
> Telefone: 972-218-0741
>   
> Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Frame

As organizações de TI na empresa e governamentais, provedores de serviços gerenciados e principais fornecedores de software escolha quadro toocreate e gerenciar seus espaços de trabalho seguros, definida pelo software na nuvem hello. Em organizações de pequeno toolarge quadro torna extremamente fácil toolet usuários acessar aplicativos do Windows em qualquer navegador em qualquer dispositivo. Hello plataforma quadro inclui tudo o que um administrador necessidades toodeploy aplicativos da nuvem Olá incluindo hello infraestrutura do Azure e licenças RDS (trazer a sua conta do Azure e licenças é opcional). 

Saiba sobre o [Frame no Azure](https://www.fra.me/ara). 

> Localização primária: San Mateo, CA, EUA
>
> Região de operação: em todo o mundo
>
> Parceiro da Microsoft: Sim
> 
> Telefone: 1-480-269-4668

### <a name="awingu"></a>Awingu
O Awingu fornece uma solução de espaço de trabalho online simples que executa aplicativos herdados, SaaS e documentos em um navegador com html5. Disponibilizando, dessa forma, os aplicativos com segurança em qualquer tipo de dispositivo. Para serviços SaaS, há uma ampla variedade de opções de logon único disponível. Também é possível integrar profundamente diversos sistemas de arquivos (nuvem) ao seu espaço de trabalho. Mobilidade toofull Avançar, avançados de trabalho online do Awingu dará a segurança ideal com controles granulares (por exemplo, baixando/carregar), uso completo auditoria, multi-Factor Authentication (por exemplo, o Azure MFA), gravação da sessão e muito mais. Desde a configuração inicial, o Awingu habilita o compartilhamento de documentos e aplicativos para colaboração otimizada e segura.
A solução do Awingu é uma API livre multilocatário e com diversos AD. Ele é usado por pequenas e grandes empresas, provedores de serviços de nuvem e [ISVs](http://www.isv2saas.com). Esses clientes apreciam especialmente Olá fácil de usar, fácil de instalar e de baixo custo total de propriedade.

É Awingu tudo em um [disponíveis no hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) com 2 usuários simultâneos internos. Licenças adicionais estão disponíveis por meio de uma [ampla gama de distribuidores e revendedores](http://www.awingu.com/reseller).

Saiba mais sobre [Awingu em como tooAzure alternativo RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Localização primária: Bélgica
> 
> Regiões de operação: EMEA, América do Norte e Brasil
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos 
> 
> **Global**:
> 
> Arnaud Marlière, CMO
> 
> Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Telefone: +1 646 583 3025
> 
> **EC da Bélgica**:
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> Email: [info@awingu.com](mailto:info@awingu.com) 
> 
> Telefone: +32 9 296 40 11
> 
> **EUA**:
> 
> 7 floor, Ave 1177 de saudação Américas,
> 
> New York, NY 10036
> 
> Email: [info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Provedor de serviços hospedados da Microsoft
Parceiros de hospedagem geralmente oferecem totalmente gerenciado hospedado área de trabalho do Windows hello de serviço de aplicativo, que pode incluir o gerenciamento de recursos do Azure, sistemas operacionais, aplicativos e assistência técnica usando o parceiro de saudação do contratos de licenciamento por com a Microsoft e outros fornecedores de software juntamente com sendo um contrato de licença de provedor de serviços tooallow revenda de licença de acesso de assinante (SAL). Olá informações a seguir fornecem detalhes e informações de contato para alguns hosters Olá especializadas em ajudar os clientes com a migração do Azure RemoteApp. Check-out [lista atual de saudação de provedores de serviços hospedados](http://aka.ms/rdsonazurecertified) que concluiu Olá RDS no caminho e avaliação de aprendizado de IaaS.  

### <a name="citrix-service-provider-program"></a>Programa Citrix Service Provider
Olá Citrix programa do provedor de serviço facilita para serviço provedores toodeliver Olá manter a simplicidade da nuvem virtual computação tooSMBs, oferecendo a eles serviços Olá desejarem em um modelo fácil e flexível. Provedores de serviço do Citrix aumentar seus negócios Microsoft SPLA e expandir seus investimentos na plataforma RDS com qualquer dispositivo, acesso em qualquer lugar, hello mais amplo suporte a aplicativos, uma experiência avançada, aumentar a segurança e maior escalabilidade. Por sua vez, provedores Citrix atraem mais assinantes, aumentam a satisfação do cliente e reduzem seus custos operacionais. [Saiba mais](http://www.citrix.com/products/service-providers.html) ou [encontre um parceiro](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) especializada em fornecer soluções de área de trabalho hospedadas, entrega de área de trabalho inteira e os aplicativos ISV experiências criadas no Microsoft tooa global cliente da tecnologia de base do Azure e seus datacenters.

> Localização primária: Londres, Reino Unido; Cingapura; Houston, Texas
> 
> Região de operação: em todo o mundo
> 
> Status de parceiro: ouro
> 
> Provedor de Serviços Microsoft Cloud: sim
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos
> 
> Soluções de migração do Azure RemoteApp: sim, [saiba mais](http://www.acuutech.com/ara-migration/)
> 
> **Reino Unido**:
>   
> 5/6 York House, Road Langston,
>   
> Loughton, Essex IG10 3TQ
>   
> Telefone: +44 (0) 20 8502 2155
> 
> **Cingapura**:
>   
> 100 Cecil Street, #09-02, 
>   
> Olá mundo, Cingapura 069532
> 
> Telefone: +65 6709 4933
>   
> **América do Norte**:
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, Texas 77098
>   
> Telefone: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) especializada em ISVs transição toohello nuvem e ISV' procurando toooptimize suas configurações atuais de nuvem. O ASPEX oferece uma ampla variedade de serviços gerenciados, DeVOps e serviços de consultoria.  

> Localização primária: Antuérpia, Bélgica
> 
> Região de operação: Europa Ocidental
> 
> Status de parceiro: [prata](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Provedor de Serviços Microsoft Cloud: sim
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos
> 
> Soluções de migração do Azure RemoteApp: sim, [saiba mais](https://www.aspex.be/en/azure-remote-apps)
> 
> Telefone: +3232202198
> 
> Email: [info@aspex.be](mailto:info@aspex.be)
> 
> Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) ajuda as empresas, governos locais, corpos de não-governamentais e instituições de saúde com sua jornada até uma maneira inteligente de trabalho no hello Microsoft Cloud. Ser seguros e produtivos em qualquer lugar, com qualquer dispositivo e com baixo custo de TI. Caase.com é uma verdadeira especialista em Microsoft Office365, Azure, Enterprise Mobility and Security e Windows. Com nossa consultoria, serviços de migração, programas de adoção, treinamento, gerenciamento e suporte, o Caase.com cria uma plataforma segura e otimizada para colaboração para fornecedores, parceiros e funcionários de clientes.
Caase.com é mastermind Olá Olá espaço de trabalho remota do Azure (local de trabalho móvel) e Olá espaço de trabalho Digital (Social Intranet). Ambas as soluções – realizadas com a adoção – são a base de saudação que garante que usuários Olá dessas soluções experiência mais agradável, bem-sucedida e eficiente de Olá seu toohello rota Microsoft Cloud.
Tradução holandesa e um filme de apoio aqui: http://caase.com/over-ons/

> Região de operação: com base nos Países Baixos, com alcance global
> 
> Status de parceiro: [ouro](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Provedor de Serviços Microsoft Cloud: sim
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos
> 
> Soluções de migração do Azure RemoteApp: sim, [saiba mais](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Países Baixos:
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Telefone: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio para o Azure](http://getnerdio.com/nfa/) é uma plataforma de automação de TI que entrega ridiculamente simples de provisionamento, gerenciamento e a otimização completas dos ambientes de TI em Olá nuvem da Microsoft. Prepare áreas de trabalho virtuais, aplicativos remotos e servidores em apenas duas horas. Administrar o ambiente Olá três cliques ou menos com o Portal de administração de Nerdio. Use o dimensionamento automático inteligente e salve 40% de too60 em recursos de IaaS do Azure.

> Localização primária: região de operação de Chicago, Illinois: Status do parceiro em todo o mundo: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Provedor de Serviços do Microsoft Cloud: Sim
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos
> 
> Soluções de migração do Azure RemoteApp: sim
> 
> 
> Av. Lincoln, 8001
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> EUA
> 
> (844) 4NERDIO ext. 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
O [SaaSplaza](http://www.saasplaza.com/) oferece um portfólio completo do Microsoft Dynamics (NAV, AX, GP, SL, CRM) em nuvem privada e pública (Azure).

> Localização primária: Países Baixos
> 
> Região de operação: em todo o mundo
> 
> Status de parceiro: [ouro](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Provedor de Serviços Microsoft Cloud: sim
> 
> Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos
> 
> **EMEA**:
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> Olá países baixos
> 
> Telefone: +31 20 547 8060 
> 
>  **Américas**:
> 
> 171 Saxony Road, Suite 105
> 
> Encinitas, CA 92024
> 
> San Diego
> 
> Estados Unidos
> 
> Telefone: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil Street
>    
> \#11-08, Olá octógono
> 
> Cingapura 069534
> 
> Cingapura
>   
> Telefone – Cingapura: +65 6222 6591
> 
> Telefone – Austrália: +61 2 8310 5568 
>    
> Telefone – Nova Zelândia: +64 4 488 0321
> 
## <a name="need-more-help"></a>Precisa de mais ajuda?
Ainda precisa de ajuda escolhendo ou tem mais perguntas? Use um dos Olá métodos tooget ajuda a seguir. 

1. Envie-nos um email para [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
2. Entre em contato com o [Suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Comece abrindo um [caso de Suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Ligue para nós. [Encontre um número de vendas local](https://azure.microsoft.com/overview/sales-number/).

