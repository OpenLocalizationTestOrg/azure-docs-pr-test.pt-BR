---
title: "aaaLearn sobre Olá versões mais recentes do sistema operacional de convidado do Azure | Microsoft Docs"
description: "Olá notícias mais recentes de versão e compatibilidade do SDK para o sistema operacional convidado de serviços de nuvem do Azure."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Matriz de compatibilidade de versões de SOs Convidados e do SDK do Azure
Fornece informações atualizadas sobre Olá que versões do sistema operacional de convidado do mais recente do Azure para serviços de nuvem. Essas informações ajudam a planejar seu caminho de atualização antes que um SO convidado seja desabilitado. Se você configurar sua funções toouse *automático* atualizações do sistema operacional convidado conforme descrito em [configurações de atualização do sistema operacional de convidado do Azure][Azure Guest OS Update Settings], não é essencial ler esta página.

> [!IMPORTANT]
> Esta página se aplica a tooCloud funções dos serviços web e de trabalho, que são executados em um sistema operacional convidado. Ele faz **não aplicar** tooIaaS máquinas virtuais.
>
>


> [!NOTE]
> Olá RSS Feed recentemente foi preterido. Fique atento a atualizações em um novo feed em breve!
>
>

Certeza sobre quais Olá é de sistema operacional convidado ou hello como o sistema operacional convidado versões trabalho? Leia [esta](#how-it-works) seção.

## <a name="news-updates"></a>Notícias atualizadas

###### <a name="august-24-2017"></a>**24 de agosto de 2017**
O SO convidado de agosto foi lançado.

###### <a name="august-3-2017"></a>**3 de agosto de 2017**
O SO convidado de julho foi lançado.

###### <a name="july-19-2017"></a>**19 de julho de 2017**
A distribuição do SO convidado de julho começa em 19 de julho e está projetada para ser lançada em 8 de agosto.

###### <a name="july-7-2017"></a>**7 de julho de 2017**
O SO convidado de junho foi lançado.

###### <a name="june-16-2017"></a>**16 de junho de 2017**
A distribuição do SO convidado de junho começa dia 16 de junho e está projetada para ser lançada em 11 de julho.

###### <a name="june-5-2017"></a>**5 de junho de 2017**
Talvez o SO convidado tenha sido lançado.

###### <a name="may-17-2017"></a>**17 de maio de 2017**
Devido a erro de segurança tooa, podemos estiver desabilitando Olá após dezembro de 2016 e de janeiro de 2017 versões do sistema operacional que não têm Olá [corrigir] do portal de saudação: WA-convidado-OS-5.4_201612-01, WA-convidado-OS-4.39_201612-01, WA-convidado-OS-3.46_ 201612-01, WA-GUEST-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**12 de maio de 2017**
A distribuição do SO convidado de maio começa dia 12 de maio e está projetada para ser lançada em 13 de junho.

###### <a name="april-18-2017"></a>**18 de abril de 2017**
A distribuição do SO convidado de abril começa dia 18 de abril e está projetada para ser lançada em 9 de maio.

###### <a name="april-10-2017"></a>**10 de abril de 2017**
A distribuição do SO convidado de março começou em 14 de março de 2017, sendo lançada em 10 de abril de 2017.

###### <a name="january-10-2017"></a>**10 de janeiro de 2017**
saudação de sistema operacional convidado contém correções que afetam somente a família de sistemas operacionais 2 (Windows 2008 Server R2). Lançamos, portanto, somente a imagem de saudação OS família 2 (WA-GUEST-OS-2.59_201701-01) deste mês. Para todas as outras famílias de sistema operacional, Olá SO dezembro (201612 - 01) permanece hello mais recente.


## <a name="releases"></a>Lançamentos
## <a name="family-5-releases"></a>Versões da Família 5
**Windows Server, 2016**

.NET Framework instalado: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> Datas com um * são toochange de assunto.
>
> Olá senha RDP para 5 de família do sistema operacional deve ter um mínimo de 10 caracteres.
>

| Cadeia de caracteres de configuração | Data do lançamento | Data da desabilitação | Data de validade |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |24 de agosto de 2017 |Post 5.12 |TBD |
| WA-GUEST-OS-5.9_201707-01 |3 de agosto de 2017 |Post 5.11 |TBD |
| WA-GUEST-OS-5.8_201706-01 |7 de julho de 2017 |Post 5.10 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |5 de junho de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |9 de maio de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |10 de abril de 2017 |7 de julho de 2017 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |10 de janeiro de 2017 |5 de junho de 2017|TBD |
|~~WA-GUEST-OS-5.3_201611-01~~ |14 de dezembro de 2016 |9 de maio de 2017 |TBD |
|~~WA-GUEST-OS-5.2_201610-02~~ |1º de novembro de 2016 |10 de abril de 2017 |TBD |

## <a name="family-4-releases"></a>Versões da Família 4
**Windows Server 2012 R2**

É compatível com .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Datas com um * são toochange de assunto
>
>

| Cadeia de caracteres de configuração | Data do lançamento | Data da desabilitação | Data de validade |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |24 de agosto de 2017 |Post 4.47 |TBD |
| WA-GUEST-OS-4.44_201707-01 |3 de agosto de 2017 |Post 4.46 |TBD |
| WA-GUEST-OS-4.43_201706-01 |7 de julho de 2017 |Post 4.45 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |5 de junho de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |9 de maio de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |10 de abril de 2017 |7 de julho de 2017 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |10 de janeiro de 2017 |5 de junho de 2017 |TBD |
|~~WA-GUEST-OS-4.38_201611-01~~ |14 de dezembro de 2016 |9 de maio de 2017 |TBD |
|~~WA-GUEST-OS-4.37_201610-02~~ |16 de novembro de 2016 |10 de abril de 2017 |TBD |
|~~WA-GUEST-OS-4.36_201609-01~~ |13 de outubro de 2016 |14 de janeiro de 2017 |TBD |
|~~WA-GUEST-OS-4.35_201608-01~~ |13 de setembro de 2016 |16 de dezembro de 2016 |TBD |
|~~WA-GUEST-OS-4.34_201607-01~~ |8 de agosto de 2016 |13 de novembro de 2016 |TBD |


## <a name="family-3-releases"></a>Versões da Família 3
**Windows Server 2012**

É compatível com .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Datas com um * são toochange de assunto
>
>

| Cadeia de caracteres de configuração | Data do lançamento | Data da desabilitação | Data de validade |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |24 de agosto de 2017 |Post 3.54 |TBD |
| WA-GUEST-OS-3.51_201707-01 |3 de agosto de 2017 |Post 3.53 |TBD |
| WA-GUEST-OS-3.50_201706-01 |7 de julho de 2017 |Post 3.52 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |5 de junho de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |9 de maio de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |10 de abril de 2017 |7 de julho de 2017 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |10 de janeiro de 2017 |5 de junho de 2017 |TBD |
|~~WA-GUEST-OS-3.45_201611-01~~ |14 de dezembro de 2016 |9 de maio de 2017 |TBD |
|~~WA-GUEST-OS-3.44_201610-02~~ |16 de novembro de 2016 |1º de maio de 2017 |TBD |
|~~WA-GUEST-OS-3.43_201609-01~~ |13 de outubro de 2016 |14 de janeiro de 2017 |TBD |
|~~WA-GUEST-OS-3.42_201608-01~~ |13 de setembro de 2016 |16 de dezembro de 2016 |TBD |
|~~WA-GUEST-OS-3.41_201607-01~~ |8 de agosto de 2016 |13 de novembro de 2016 |TBD |


## <a name="family-2-releases"></a>Versões da Família 2
**Windows Server 2008 R2 SP1**

Dá suporte a .NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Datas com um * são toochange de assunto
>
>

| Cadeia de caracteres de configuração | Data do lançamento | Data da desabilitação | Data de validade |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |24 de agosto de 2017 |Post 2.67 |TBD |
| WA-GUEST-OS-2.64_201707-01 |3 de agosto de 2017 |Post 2.66 |TBD |
| WA-GUEST-OS-2.63_201706-01 |7 de julho de 2017 |Post 2.65 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |5 de junho de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |9 de maio de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |10 de abril de 2017 |7 de julho de 2017 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |10 de janeiro de 2017 |5 de junho de 2017 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |10 de janeiro de 2017 |9 de maio de 2017|TBD |
|~~WA-GUEST-OS-2.57_201611-01~~ |14 de dezembro de 2016 |10 de abril de 2017 |TBD |
|~~WA-GUEST-OS-2.56_201610-02~~ |16 de novembro de 2016 |10 de fevereiro de 2017 |TBD |
|~~WA-GUEST-OS-2.55_201609-01~~ |13 de outubro de 2016 |14 de janeiro de 2017 |TBD |
|~~WA-GUEST-OS-2.54_201608-01~~ |13 de setembro de 2016 |16 de dezembro de 2016 |TBD |
|~~WA-GUEST-OS-2.53_201607-01~~ |8 de agosto de 2016 |13 de novembro de 2016 |TBD |



## <a name="msrc-patch-updates"></a>Atualizações de patch do MSRC
Olá lista de patches que são incluídas com cada versão de sistema operacional convidado mensal está disponível [aqui][patches].

## <a name="sdk-support"></a>Suporte a SDK
Olá, embora [política de desativação de saudação do SDK do Azure] [ retire policy sdk] indica que somente versões acima 2.2 são suportados e específico famílias do SO convidado permitem toouse versões anteriores. Você sempre deve usar o hello mais recente com suporte a SDK.

| Família do SO convidado | Versões compatíveis do SDK |
| --- | --- |
| 5 |Versão 2.9.5.1+ |
| 4 |Versão 2.1+ |
| 3 |Versão 1.8+ |
| 2 |Versão 1.3+ |
| 1 |Versão 1.0+ |

## <a name="guest-os-release-information"></a>Informações de versão do SO convidado
Há três datas importantes tooGuest OS libera: **versão** data, **desabilitado** data, e **validade** Data. Um sistema operacional convidado é considerado disponível quando ele estiver em Olá Portal e pode ser selecionado como destino Olá sistema operacional convidado. Quando um sistema operacional convidado atinge Olá **desabilitado** data, ele será removido do Azure. No entanto, qualquer Serviço de Nuvem direcionado àquele SO convidado ainda funcionará normalmente.

janela Olá entre hello **desabilitado** data e hello **validade** data fornece uma transição de tooeasily de buffer de tooone em um sistema operacional convidado mais recente. Se você estiver usando *automáticas* como o sistema operacional convidado, você sempre será na versão mais recente do hello e você não tiver tooworry sobre ele expirar.

Olá quando **validade** data passa, qualquer serviço de nuvem usar ainda que o sistema operacional convidado será interrompido, excluído ou forçado tooupgrade. Você pode ler mais sobre a política de desativação Olá [aqui][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Família do SO convidado, explicação de versão
famílias de sistema operacional convidado Olá são baseadas em versões do Microsoft Windows Server. saudação de sistema operacional convidado é sistema operacional subjacente Olá que os serviços de nuvem do Azure é executado em. Cada SO convidado tem uma família, uma versão e um número de lançamento.

* **Guest OS family**  
  Uma versão do sistema operacional Windows Server na qual o SO Convidado se baseia. Por exemplo, a *família 3* baseia-se no Windows Server 2012.
* **Versão do SO Convidado**  
  Imagem específica tooa família do SO convidado mais relevantes [Microsoft Security Response Center (MSRC)] [ msrc] patches que estão disponíveis em Olá data Olá nova versão do SO convidado é produzida. Nem todos os patches estarão necessariamente incluídos.

    Os números começam em 0 e são incrementados em 1 cada vez que um novo conjunto de atualizações é adicionado. Os zeros à direita são mostrados apenas se forem importantes. Ou seja, a versão 2.10 é uma versão diferente e muito posterior à versão 2.1.
* **Versão do SO convidado**  
  Um relançamento de uma versão do SO Convidado. Um relançamento ocorre quando a Microsoft encontra, durante os testes, problemas que exigem alterações. Olá versão mais recente sempre substitui qualquer anterior libera, público ou não. Olá portal do Azure só permitirá que os usuários a versão mais recente do toopick Olá para uma determinada versão. Implantações em execução em uma versão anterior geralmente não são atualizadas à força dependendo da gravidade de saudação do bug hello.

O exemplo hello abaixo, 2 é uma família de saudação, 12 é a versão de hello e "rel2" é a versão de saudação.

**Versão de SO convidado** - 2.12 rel2

**Cadeia de caracteres de configuração para essa versão** - WA-GUEST-OS-2.12_201208-02

cadeia de caracteres de configuração de saudação para um sistema operacional convidado tem essas mesmas informações inseridas nela, junto com uma data mostrando quais patches MSRC foram considerados para essa versão. Neste exemplo, os patches do MSRC produzidos para Windows Server 2008 R2 backup tooand incluindo agosto de 2012 foram considerados para inclusão. Apenas os patches que se aplicam especificamente a versão toothat do Windows Server são incluídos. Por exemplo, se um patch do MSRC se aplicar tooMicrosoft Office, ele não será incluído porque esse produto não faz parte da imagem base do Windows Server hello.

## <a name="guest-os-system-update-process"></a>Processo de atualização de sistema do SO convidado
Esta página contém informações sobre as próximas versões do SO convidado. Os clientes indicaram que desejam tooknow quando uma versão ocorrerá porque suas funções de serviço de nuvem reinicializarão se estiverem definidos atualização muito "automática". Versões do SO convidado normalmente ocorrem pelo menos cinco (5) dias após hello MSRC versão de atualização que ocorre em Olá segunda terça-feira de cada mês. Novas versões incluem todos os Olá relevantes patches do MSRC para cada família de sistema operacional convidado.

O Microsoft Azure está constantemente lançando atualizações. saudação de sistema operacional convidado é apenas uma atualização no pipeline de saudação. Uma versão pode ser afetada por muitos fatores muito numerosos toolist aqui. Além disso, o Azure é executado em literalmente centenas de milhares de computadores. Isso significa que é impossível toogive uma data e hora exatas quando sua função será reinicializada. Estamos trabalhando em um plano toolimit ou programar as reinicializações.

Quando uma nova versão de hello que SO convidado é publicado, pode levar tempo toofully propagação no Azure. Como os serviços são atualizado toohello novo sistema operacional convidado, eles são reinicializada para respeitar os domínios de atualização. Conjunto de serviços toouse atualizações "Automáticas" receberão uma versão primeiro. Após atualização Olá, você verá a nova versão de sistema operacional convidado Olá listada para seu serviço em Olá portal do Azure. Relançamentos podem ocorrer durante esse período. Algumas versões podem ser implantadas por longos períodos de tempo e reinicializações de atualização automática não podem ocorrer por muitas semanas após a data de lançamento oficial hello. Quando um sistema operacional convidado estiver disponível, você pode escolher explicitamente essa versão do portal de saudação ou no arquivo de configuração.

Para uma grande quantidade de informações valiosas sobre reinicializações e ponteiros toomore informações detalhes técnicos de Host de sistema operacional convidado e atualizações, consulte Olá MSDN postagem em blog intitulada [função reinicializações de instância devido atualizações de tooOS] [ restarts].

Se você atualizar manualmente o sistema operacional convidado, consulte Olá [política de desativação do sistema operacional convidado] [ retirepolicy] para obter informações adicionais.

## <a name="guest-os-supportability-and-retirement-policy"></a>Política de suporte e desativação do SO convidado
Olá política de suporte e desativação do sistema operacional convidado é explicado [aqui][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[corrigir]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
