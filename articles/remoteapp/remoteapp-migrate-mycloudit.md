---
title: "a cobrança do Azure RemoteApp Olá aaaChange | Microsoft Docs"
description: Saiba como toostop sendo cobrado Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Migrar do Azure RemoteApp tooMyCloudIT 

**Você usa atualmente o RemoteApp do Microsoft Azure?** : MyCloudIT criados em uma ferramenta automatizada toomigrate sua plataforma de gerenciamento do Azure RemoteApp (ARA) collection(s) toohello MyCloudIT enquanto continua toorun no Microsoft Azure.

**Tirar proveito do portal do Azure Resource Manager Olá**: migração concluída na plataforma de MyCloudIT Olá permite que o novo portal de Gerenciador de recursos do Azure do acesso instantâneo tooAzure. Este portal contém todos os novos recursos de saudação e inovações oferecidos pelo Microsoft Azure, incluindo acesso tooVirtual máquina tamanhos tooensure sua implantação é criada toosupport necessidades de saudação do seu negócio.

**Testar a solução certa de saudação de tooensure paralelo para suas necessidades**: ferramenta de migração do hello MyCloudIT é compilada tooinitiate processo de migração de saudação e teste paralelo enquanto os usuários ARA atuais continuam toouse ARA.  Os usuários permanecerão no ARA até que a migração e o teste sejam concluídos.  ferramenta de migração de saudação é compilada coleção de ARA toohandle Olá típica.  Se você acha que tenha um cenário exclusivo, não padrão, entre em contato conosco em [ sales@conexlink.com ](mailto:sales@conexlink.com) para que possa fornecer tooassist um plano personalizada com a migração.

**Recursos de área de trabalho como um serviço**: Observe que MyCloudIT não só oferece recursos de RemoteApp Olá estiver acostumado a, mas nós também oferecemos a área de trabalho-como-um-serviço completo recursos para Olá mesmo custo por mês sem qualquer usuário mínimo requisitos.

## <a name="what-we-will-do-for-you"></a>O que faremos por você

MyCloudIT automatiza a migração de saudação do seu modelo do RemoteApp do Azure do portal clássico do Azure de saudação do toohello sua assinatura do Azure Gerenciador de recursos de Portal da sua assinatura com nossa ferramenta de migração automatizada.  

> [!NOTE]
> Hello Azure RemoteApp modelo deve permanecer no hello mesma região do Azure que sua implantação original do Azure RemoteApp.  Se você precisar regiões do Azure toochange ou assinaturas do Azure durante a migração de hello, entre em contato conosco para obter orientação adicional em [ sales@conexlink.com ](mailto:sales@conexlink.com).

Leia a seguir para informações detalhadas sobre o processo de migração de saudação automatizada com hello MyCloudIT ferramenta de migração:

1. ferramenta de migração de saudação examina a subscrição atual para todas as implantações ARA existentes.  
2. Selecione um ARA coleção toomigrate por vez.  Caso você tenha várias coleções, execute nossa ferramenta várias vezes.
3. Você tem Olá opção toocopy Olá discos de perfil de usuário (UDP) tooyour nova implantação para que possa recuperar dados herdados, ou mapear manualmente UPDs toohello nova implantação. Se você escolher toocopy seu UPDs, vamos salvar UPDs hello e incluir um arquivo de texto que mapeia o nome hello UPD nome tooeach dos usuários.  Olá UPDs será compartilhamento tooa copiados no servidor RDSMGMT Olá `F:\Shares\LegacyUPD` e será exposta por meio do compartilhamento de saudação `\\RDSmgmt\LegacyUPD`. 
4. A migração não exigirá nenhum tempo de inatividade para a implantação atual do ARA.  Porém, se as alterações forem feitas toohello UPDs (de ARA) após a cópia Olá, essas alterações não aparecerá em UPDs Olá armazenados no portal do Azure Resource Manager hello. 
5. Se você tiver VMs adicionais como controladores de domínio e servidores de arquivos em sua rede Virtual do Azure clássico será estabelecemos entre sua rede Virtual do clássico do Azure existente de emparelhamento VNet e hello nova rede Virtual criamos para você, em Olá novo recurso do Azure Gerenciador de Portal.
6. Nossa solução automatizada só estabelecerá entre sua rede Virtual do clássico do Azure existente de emparelhamento VNet e Olá nova rede Virtual se sua implantação ARA existente é uma implantação híbrida; ou seja, você estiver autenticando com Windows Server Active Directory controlador de domínio em Olá existente clássico de rede Virtual. Se não estabelecemos para sua coleção de emparelhamento VNet, mas você precisa de emparelhamento VNet, entre em contato conosco como [ sales@conexlink.com ](mailto:sales@conexlink.com) e será tooconfigure feliz emparelhamento de rede virtual sem nenhum custo adicional.
7. Nossa solução automatizada garantirá a configuração de DNS do Azure é atualizada com hello nova rede Virtual configurações tooensure nova implantação pode se conectar a tooyour existentes de controlador de domínio no hello VNet clássico.
8. Nossa solução automatizada irá garantir que não há nenhum conflito de endereço IP como podemos criar essa nova rede Virtual e estabelecer Olá emparelhamento de rede virtual para implantações que possuem um Windows Server Active Directory Server existente.
9. Se você estiver usando apenas o AD do Azure para autenticação, MyCloudIT criará um novo domínio Windows Server Active Directory e use o Azure AD Connect toosynchronize usuários entre instância do AD do Azure existente hello e hello que novo domínio Windows Server Active Directory criado por MyCloudIT.
10. Se você estiver usando um usuário do domínio do Active Directory para Windows Server tooauthenticate ARA, nossa solução automatizada conectará seu novo tooyour de implantação MyCloudIT existentes do controlador de domínio de diretório ativo do Windows Server por meio do emparelhamento de rede virtual.
11. Se você estiver usando o Azure Active Directory Domain Services para autenticação, poderemos migrá-lo, mas contate nossa equipe para que possamos criar um plano de migração personalizado para você.  Envie um email muito[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Depois de migrados Olá coleção toobe é confirmado, aguarde e observe enquanto nossa solução automatizada migra sua coleção ARA e os discos de perfil de usuário (opcional) toohello nova aplicativos remotos MyCloudIT controlada por solução.
13. Após a conclusão da implantação hello, podemos novamente publicará Olá mesmos aplicativos que foram publicados no ARA e após a implantação, você será capaz de toopublish outros aplicativos.

## <a name="post-migration-benefits"></a>Benefícios pós-migração

1. Fornecemos o console de gerenciamento de saudação que permite que você toomanage Olá ciclo de vida completo de sua implantação de aplicativos remotos.
2. Você será capaz de toomanage seu Virtual máquinas de nosso portal.  Inicie/pare e redimensione VMs individuais, se necessário.
3. console de gerenciamento de saudação fornece Olá toocreate de capacidade e gerenciar usuários / grupos de nosso portal de gerenciamento.
4. console de gerenciamento de saudação fornece Olá capacidade toosynchronize aos usuários toocreate do Office 365 uma mesma experiência de logon.
5. Olá, console de gerenciamento fornece Olá capacidade toocreate Remote App adicionais e coleções de área de trabalho sem os custos de usuário duplicado ou os requisitos mínimos do usuário. 
6. console de gerenciamento de saudação fornece a capacidade de saudação toopublish novos aplicativos de aplicativos remotos.
7. console de gerenciamento de saudação fornece inicialização de Olá Olá capacidade tooschedule e desligamento da sua implantação de aplicativos remotos se você precisar apenas da sua solução durante o horário específico.
8. console de gerenciamento de saudação fornece instalação de Olá Olá capacidade tooautomate e configuração do agente de Backup do Azure Olá que fornece um histórico de retenção de documentos para dados do cliente.
9. console de gerenciamento de saudação fornece métricas de tooperformance de acesso da sua implantação.  Isso proporciona Olá capacidade tooidentify possíveis gargalos de desempenho sem instalar as ferramentas de gerenciamento de desempenho adicionais.
10. Se você tiver vários hosts de sessão, você será automaticamente tooenable capaz de dimensionamento de forma que só sessão Olá hosts que precisam toobe em execução estão em execução.
11. MyCloudIT fornece o servidor de gateway do access toohello RDWeb por meio de um nome de domínio MyCloudIT.  Nós também fornecemos Olá capacidade toore mapa Olá URL tooa URL personalizada para o usuário final de identidade visual.

## <a name="prerequisites-for-migration"></a>Pré-requisitos da migração

1. Você deve ter acesso toohello assinatura do Azure que hospeda sua solução atual do Azure RemoteApp.
2. Você deve conceder permissões nosso portais dentro de sua assinatura toomigrate seu modelo e toocreate / modificar sua nova implantação MyCloudIT.
3. Observe que devido a limitação de tooa no RemoteApp do Azure, cada coleção só pode ser migrada três vezes.  Se você precisar de mais de três vezes toomigrate uma coleção, você pode aumentar a contagem de exportação de tooincrease de tooAzure um tíquete, ou entre em contato conosco e nós ajudará a contagem de exportação de Olá Olá ARA solicitação tooincrease.

## <a name="mycloudit-billing"></a>Cobrança do MyCloudIT

Consulte [MyCloudIT preços para soluções de RemoteApp](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) para obter informações sobre como toopredict e gerenciar os custos gerais do Azure.

Se você ainda tiver dúvidas, entre em contato conosco em [ sales@conexlink.com ](mailto:sales@conexlink.com) ou assista o vídeo de demonstração completo Olá [ferramenta de migração do Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

