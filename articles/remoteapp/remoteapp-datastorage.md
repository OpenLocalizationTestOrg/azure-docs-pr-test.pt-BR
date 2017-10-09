---
title: aaaNever armazenar dados confidenciais em imagens personalizadas para o Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as diretrizes de saudação para armazenar dados em imagens personalizadas no Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Nunca armazene dados confidenciais em imagens personalizadas
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Ao hospedar seu próprio aplicativo no Azure RemoteApp, Olá primeira etapa é toocreate uma imagem personalizada. Usamos que instâncias VM toocreate imagem personalizada que servem tooyour usuários de seus aplicativos. imagem personalizada Olá deve conter apenas aplicativos e dados nunca confidenciais que podem ser perdidos, como bancos de dados SQL, arquivos de pessoal ou arquivos de dados especiais como QuickBooks da empresa. Todos os dados confidenciais devem residir tooAzure externo RemoteApp em um servidor de arquivos, outra VM do Azure, ou no SQL Azure. imagem de saudação deve apenas aplicativo de saudação host que conecta-se a fonte de dados toohello e apresenta os dados de saudação. Releia os [Requisitos para as imagens do Azure RemoteApp](remoteapp-imagereqs.md) para obter mais informações. 

toounderstand por que você não deve armazenar dados confidenciais, você precisa toounderstand como funciona o Azure RemoteApp. Quando uma coleção é criada ou atualizada, em segundo plano do hello vários clones ou cópias de imagem de saudação são criadas. Todas essas instâncias VM são réplicas exatas de imagem personalizada do hello; Quando os usuários iniciar aplicativos estiverem conectado tooone dessas instâncias de VM. Mas hello mesma instância não é garantida e não deve importar porque eles são não persistente. Olá instâncias VM aplicativos de hospedagem Olá não são persistentes e podem ser destruído ou excluído com base, por exemplo, durante a atualização da coleção. 

Depois de coleção Olá é provisionada e os usuários iniciam o toohello conectar máquinas virtuais, dados de usuário são persistentes e protegido porque ele é salvo em um armazenamento separado dentro de um VHD que chamamos um [disco de perfil de usuário (UDP)](remoteapp-upd.md), que é o perfil de usuário Olá c:\Users\<userprofile >. Quando um aplicativo é iniciado, Olá UPD é montado e tratada como um perfil de usuário local pelo sistema operacional de saudação. Leia mais sobre como o [Azure RemoteApp salva configurações e dados de usuário](remoteapp-upd.md).

Dados de exemplo não devem residir na imagem de saudação:

* Dados compartilhados para usuários tooaccess
* Banco de dados SQL ou banco de dados do QuickBooks
* Quaisquer dados em D:\

Dados de exemplo que podem residir em saudação padrão perfil toobe copiado para UPD cada usuários:

* Arquivos de configuração por usuário
* Scripts que os usuários precisariam que fossem preservados no seu UPD

Pontos principais:

* Nunca armazene dados confidenciais que podem ser perdidos na imagem de saudação ao criar uma imagem personalizada.
* Dados confidenciais sempre deve residir em um servidor de arquivos separado, separe a VM do Azure, na nuvem hello e instâncias de VM externo sempre toohello hospedar seus aplicativos no Azure RemoteApp. 
* Dados de usuário é salvo e persistir no disco de perfil de usuário de saudação (UDP)

