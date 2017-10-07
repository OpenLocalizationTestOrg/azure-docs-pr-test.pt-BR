---
title: "segurança de série 8000 do aaaStorSimple | Microsoft Docs"
description: "Descreve Olá recursos de segurança e privacidade que protegem seu serviço, dispositivos e dados locais e na nuvem de saudação do StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 48dd449d2908c21fe05d0ed37a4dc6f3e306e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>Proteção de dados e segurança de StorSimple

## <a name="overview"></a>Visão geral

A segurança é a principal preocupação para qualquer pessoa que esteja adotando uma nova tecnologia, especialmente quando Olá tecnologia é usada com dados confidenciais ou proprietários. Ao avaliar as diferentes tecnologias, você deve considerar o aumento dos riscos e dos custos para a proteção dos dados. Microsoft Azure StorSimple fornece tanto uma solução de segurança e privacidade para proteção de dados, ajudando tooensure:

* **Confidencialidade** – somente entidades autorizadas podem exibir seus dados.
* **Integridade** – somente entidades autorizadas podem modificar ou excluir seus dados.

Olá solução StorSimple do Microsoft Azure consiste em quatro componentes principais que interagem entre si:

* **Serviço de Gerenciador de dispositivos de StorSimple hospedado no Microsoft Azure** – serviço de gerenciamento de saudação que você use tooconfigure e provisionar Olá dispositivo StorSimple.
* **Dispositivo StorSimple** – Um dispositivo físico instalado no datacenter. Todos os hosts e clientes que geram dados conectam o dispositivo StorSimple toohello e dispositivo Olá gerencia dados hello e move toohello nuvem do Azure conforme apropriado.
* **Clientes/hosts conectados toohello dispositivo** – Olá clientes em sua infraestrutura que conecte o dispositivo StorSimple toohello e gerar dados que precisa toobe protegido.
* **Armazenamento em nuvem** – Olá local Olá nuvem do Azure, onde os dados são armazenados.

Olá seções a seguir descrevem recursos de segurança de StorSimple Olá que ajudam a proteger cada um desses componentes e os dados de saudação armazenados neles. Ele também inclui uma lista de perguntas sobre segurança do Microsoft Azure StorSimple e respostas correspondentes hello.

## <a name="storsimple-device-manager-service-protection"></a>Proteção de serviço Gerenciador de Dispositivos StorSimple

saudação de serviço do Gerenciador de dispositivos de StorSimple é um serviço de gerenciamento hospedado no Microsoft Azure e usado toomanage todos os dispositivos de StorSimple que sua organização adquiriu. Você pode acessar Olá serviço do Gerenciador de dispositivos do StorSimple usando sua credenciais organizacionais toolog toohello portal do Azure por meio de um navegador da web.

Acesso toohello serviço do Gerenciador de dispositivos do StorSimple requer que sua organização tem uma assinatura do Azure que inclui o StorSimple. Sua assinatura determina os recursos de saudação que você pode acessar no portal do Azure de saudação. Se sua organização não tiver uma assinatura do Azure e você desejar toolearn mais sobre eles, consulte [inscrever-se no Azure como uma organização](../active-directory/sign-up-organization.md).

Como Olá serviço do Gerenciador de dispositivos do StorSimple é hospedado no Azure, ele é protegido por recursos de segurança do Azure hello. Para obter mais informações sobre recursos de segurança de saudação fornecidos pelo Microsoft Azure, vá toohello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>Proteção de dispositivos StorSimple

o dispositivo StorSimple Olá é um dispositivo de armazenamento híbrido local que contém unidades de estado sólido (SSDs) e unidades de disco rígido (HDDs), juntamente com controladores redundantes e recursos de failover automático. controladores de saudação gerenciam o armazenamento hierárquico, colocando atualmente usados (ou dados quentes) no armazenamento local (em servidores locais ou Olá dispositivo StorSimple), ao mover dados usados com menos frequência toohello na nuvem.

Apenas autorizados StorSimple dispositivos são permitidos Olá toojoin serviço de Gerenciador de dispositivos do StorSimple que você criou na sua assinatura do Azure. tooauthorize um dispositivo, registre-com hello serviço do Gerenciador de dispositivos de StorSimple, fornecendo a chave de registro do serviço de saudação. chave de registro do serviço de saudação é uma chave aleatória de 128 bits gerada no hello portal do Azure.

![Chave de registro do serviço](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn como obter um go chave, de registro de serviço muito[etapa 2: chave de registro de serviço Get hello](storsimple-8000-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).

chave de registro do serviço de saudação é uma chave longa que contém a 100 caracteres. Você pode copiar a chave de saudação e salvá-lo em um arquivo de texto em um local seguro para que você pode usá-lo dispositivos adicionais tooauthorize conforme necessário. Se chave de registro do serviço de saudação for perdida, depois de registrar seu primeiro dispositivo, você pode gerar uma nova chave de saudação de serviço do Gerenciador de dispositivos do StorSimple. Isso não afetará a operação de saudação dos dispositivos existentes.

Depois que um dispositivo for registrado, ele usa os tokens toocommunicate com o Microsoft Azure. chave de registro do serviço de saudação não é usado depois do registro do dispositivo.

> [!NOTE]
> É recomendável que você regenerar a chave de registro de serviço de saudação após cada uso.


## <a name="protect-your-storsimple-solution-via-passwords"></a>Proteja sua solução StorSimple por meio de senhas

Senhas são um aspecto importante da segurança do computador e são utilizadas extensivamente na solução do StorSimple Olá toohelp Certifique-se de que seus dados sejam tooauthorized acessível somente a usuários. StorSimple permite Olá tooconfigure senhas a seguir:

* Senha do administrador de dispositivo do StorSimple
* Senhas do iniciador e de destino do protocolo CHAP
* Senha do Gerenciador de instantâneos do StorSimple

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Windows PowerShell para StorSimple e hello senha de administrador do dispositivo StorSimple

O Windows PowerShell para StorSimple é uma interface de linha de comando que você pode usar o dispositivo StorSimple toomanage hello. Windows PowerShell para StorSimple possui recursos que permitem a você tooregister seu dispositivo, configurar a interface de rede Olá no seu dispositivo, instalar determinados tipos de atualizações, solucionar problemas de seu dispositivo acessando a sessão de suporte de saudação e alterar o estado do dispositivo Olá . Você pode acessar o Windows PowerShell para StorSimple conexão console serial do toohello no dispositivo de saudação ou usando o Windows PowerShell remotamente.

A comunicação remota do PowerShell pode ser feita por meio de HTTPS ou HTTP. Se o gerenciamento remoto via HTTPS estiver habilitado, será necessário gerenciamento remoto do toodownload Olá de certificado do dispositivo hello e instalá-lo no cliente remoto hello. Para obter mais informações sobre comunicação remota do PowerShell, vá muito[se conectar remotamente o dispositivo StorSimple tooyour](storsimple-8000-remote-connect.md).

Depois que você usa o Windows PowerShell para StorSimple tooconnect toohello dispositivo, você precisará toolog de senha do administrador do tooprovide Olá dispositivo no dispositivo toohello.

![Senha do administrador do dispositivo](./media/storsimple-security/DeviceAdminPW.png)

Lembre-Olá, seguir as práticas recomendadas em mente:

* O gerenciamento remoto está desativado por padrão. Você pode usar tooenable de serviço do Gerenciador de dispositivos de StorSimple Olá-lo. Como prática recomendada de segurança, acesso remoto deve ser habilitado somente durante a saudação período de tempo que é realmente necessária.
* Se você alterar a senha de hello, ser toonotify-se de que todos os usuários de acesso remoto para que eles não passem por uma perda de conectividade inesperados.
* saudação de serviço do Gerenciador de dispositivos do StorSimple não pode recuperar senhas existentes: ele pode apenas reinicializá-las. É recomendável que você armazene todas as senhas em um local seguro para que você não tem tooreset uma senha se ela for esquecida. Se você precisar tooreset uma senha, ser toonotify-se de que todos os usuários antes de fazer isso.

Você pode acessar a interface do Windows PowerShell hello usando um dispositivo de toohello conexão serial. Você também pode acessá-la remotamente usando HTTP ou HTTPS, o que fornece segurança adicional. HTTPS oferece um nível mais alto de segurança que uma conexão HTTP ou serial. No entanto, toouse HTTPS, você deve primeiro instalar um certificado no computador cliente Olá que irá acessar o dispositivo de saudação. Você pode baixar o certificado de acesso remoto de saudação na página de configuração de dispositivo Olá no hello serviço do Gerenciador de dispositivos do StorSimple. Se o certificado de saudação para acesso remoto for perdido, deve baixar um novo certificado e propagá-lo tooall clientes que são o gerenciamento remoto de toouse autorizados.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Senhas do iniciador e de destino do protocolo CHAP

O CHAP é um esquema de autenticação usado pelo Olá identidade de saudação do StorSimple dispositivo toovalidate de clientes remotos. verificação de saudação baseia-se em uma senha compartilhada. O protocolo CHAP pode ser unidirecional ou bidirecional (mútuo). Com o CHAP unidirecional, o destino de saudação (dispositivo StorSimple do hello) autentica um iniciador (host). CHAP mútuo ou reverso requer que o destino Olá autentique o iniciador de saudação e, em seguida, o iniciador Olá autentique o destino de saudação. O StorSimple pode ser qualquer um dos métodos de toouse configurado.

Lembre-se do seguinte hello quando você configurar o CHAP:

* nome de usuário CHAP Olá deve conter menos de 233 caracteres.
* senha CHAP de saudação deve ter entre 12 e 16 caracteres. Tentativa de toouse um nome de usuário ou a senha mais longo resultará em uma falha de autenticação no host do Windows hello.
* Você não pode usar o hello mesma senha para o iniciador do CHAP hello e o destino do CHAP hello.
* Depois de definir senha hello, pode ser alterada, mas ele não pode ser recuperado. Se Olá senha for alterada, ser toonotify-se de que todos os usuários de acesso remoto para que eles podem se conectar com êxito o dispositivo StorSimple toohello.

Para obter mais informações sobre o protocolo CHAP e como tooconfigure para sua solução do StorSimple saiu muito[configurar o CHAP para seu dispositivo StorSimple](storsimple-8000-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>Senha do Gerenciador de instantâneos do StorSimple

Gerenciador de instantâneos StorSimple é um snap-in do Console de gerenciamento Microsoft (MMC) que usa grupos de volumes e backups consistentes com o aplicativo do toogenerate Olá serviço de cópias de sombra de Volume do Windows. Além disso, você pode usar o clone e Gerenciador de instantâneos StorSimple toocreate agendas de backup ou restaurar volumes.

Quando você configura um toouse dispositivo StorSimple Snapshot Manager, você será senha de Gerenciador de instantâneos StorSimple Olá tooprovide necessária. Essa senha é definida pela primeira vez no Windows PowerShell para o StorSimple durante o registro. senha Olá também pode ser definida e alterada de saudação de serviço do Gerenciador de dispositivos do StorSimple. Essa senha autentica o dispositivo de saudação com o Gerenciador de instantâneos do StorSimple.

![Senha do Gerenciador de instantâneos do StorSimple](./media/storsimple-security/SnapshotMgrPassword.png)

senha do StorSimple Snapshot Manager Olá deve ser 14 too15 caracteres e deve conter 3 ou mais de uma combinação de caracteres maiusculo, minúsculo, numérico e especial. Depois de definir a senha do StorSimple Snapshot Manager hello, pode ser alterada, mas ele não pode ser recuperado. Se você alterar a senha de hello, ser toonotify-se de que todos os usuários remotos.

Para obter mais informações sobre o Gerenciador de instantâneos do StorSimple, ir muito[o que é StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Práticas recomendadas de senha

Recomendamos que você use o seguinte Olá diretrizes toohelp Verifique se StorSimple senhas fortes e bem protegidas:

* Altere suas senhas a cada três meses. Alterando senhas Olá é imposta por ano.
* Use uma senha forte. Para obter mais informações, vá muito[criar senhas de alta segurança e protegê-los](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Sempre use senhas diferentes para diferentes mecanismos de acesso; cada uma das senhas de saudação que você especificar deve ser exclusiva.
* Não compartilhe senhas com alguém que não seja o dispositivo StorSimple autorizado tooaccess hello.
* Não fale sobre uma senha na frente de outros ou dica em formato de saudação de uma senha.
* Se você suspeitar de que uma conta ou senha tiver sido comprometida, relatório departamento de segurança de informações de incidentes tooyour hello.
* Trate todas as senhas como informações sigilosas e confidenciais. 

## <a name="storsimple-data-protection"></a>Proteção de dados do StorSimple

Esta seção descreve os recursos de segurança do StorSimple Olá protegem dados em trânsito e dados armazenados.

Conforme descrito em outras seções, as senhas são usada tooauthorize e autentiquem usuários antes de obterem acesso tooyour StorSimple solução. Outra consideração de segurança é proteger os dados contra usuários não autorizados durante a transferência entre sistemas de armazenamento e enquanto estão sendo armazenados. Olá seções a seguir descrevem recursos de proteção de dados Olá fornecidos com o StorSimple.

> [!NOTE]
> Eliminação de duplicação fornece proteção adicional para dados armazenados no dispositivo do StorSimple hello e no armazenamento do Microsoft Azure. Quando a eliminação de duplicação de dados, objetos de dados de saudação são armazenados separadamente do hello metadados usados toomap e acessá-los: nenhum dado de saudação tooreconstruct contexto de nível de armazenamento disponíveis com base na estrutura de volume, o sistema de arquivos ou o nome do arquivo.


## <a name="protect-data-flowing-through-hello-service"></a>Proteger dados que fluem por meio do serviço de saudação

principal finalidade Olá Olá serviço do Gerenciador de dispositivos de StorSimple é toomanage e configurar o dispositivo StorSimple hello. saudação de serviço do Gerenciador de dispositivos do StorSimple é executado no Microsoft Azure. Use Olá dados de configuração de dispositivo tooenter portal do Azure e Microsoft Azure usa Olá Gerenciador de dispositivos do StorSimple service toosend Olá toohello o dispositivo de dados. StorSimple usa um sistema de pares de chaves assimétricas toohelp Certifique-se de que um comprometimento de saudação do serviço do Azure não resultará em um comprometimento das informações armazenadas.

![Criptografia dos dados em trânsito](./media/storsimple-security/DataEncryption.png)

sistema de chaves assimétricas Olá ajuda a proteger dados de saudação que fluem por meio do serviço de saudação da seguinte maneira:

1. Um certificado de criptografia de dados que usa um par de chaves assimétricas público e privado é gerado no dispositivo hello e dados de saudação tooprotect usado. chaves de saudação são geradas quando o primeiro dispositivo de saudação está registrado.
2. chaves de certificado de criptografia de dados de saudação são exportadas para um arquivo de troca de informações pessoais (. pfx) que é protegido por Olá serviço dados chave de criptografia, que é uma chave forte de 128 bits aleatoriamente gerada pelo primeiro dispositivo de saudação durante o registro.
3. a chave pública do certificado de saudação Olá com segurança torna disponível toohello serviço do Gerenciador de dispositivos do StorSimple e chave privada Olá permanece com dispositivo hello.
4. Dados de serviço de saudação entrando é criptografado usando Olá chave pública e descriptografados com a chave privada de saudação armazenado no dispositivo hello, garantir que saudação do serviço do Azure não pode descriptografar dados de saudação fluindo toohello dispositivo.

chave de criptografia de dados de serviço de saudação é gerado apenas no hello primeiro dispositivo registrado com o serviço de saudação. Todos os dispositivos subsequentes que são registrados com o serviço de saudação devem usar Olá mesma chave de criptografia de dados de serviço.

> [!IMPORTANT]
> É muito importante toomake uma cópia da chave de criptografia de dados de serviço hello e salvá-lo em um local seguro. Uma cópia da chave de criptografia de dados de serviço Olá deve ser armazenada de forma que possa ser acessado por uma pessoa autorizada e pode ser facilmente comunicados toohello administrador do dispositivo.
> 
> Se a chave de criptografia de dados de serviço de saudação for perdida, uma pessoa de suporte da Microsoft pode ajudá-lo tooretrieve ele fornecido que você tenha pelo menos um dispositivo em um estado online. É recomendável que você altere a chave de criptografia de dados de serviço Olá após ele ser recuperado. Para obter instruções, vá muito[alterar chave de criptografia de dados de serviço de saudação](storsimple-service-dashboard.md#change-the-service-data-encryption-key).

Você pode alterar a chave de criptografia de dados de serviço hello e certificado de criptografia de dados correspondente Olá selecionando Olá **alterar chave de criptografia de dados de serviço** opção no painel de serviço hello. tooensure que a segurança de dados não seja comprometida, você deve usar uma físico StorSimple dispositivo toochange Olá serviço dados chave de criptografia. Alterar as chaves de criptografia Olá requer que todos os dispositivos sejam atualizados com a nova chave de saudação. Portanto, recomendamos que você altere a chave de saudação quando todos os dispositivos estão online. Se os dispositivos estiverem offline, suas chaves podem ser alteradas em um momento diferente. dispositivos Olá com chaves desatualizadas ainda será capaz de toorun backups, mas não serão capazes de toorestore dados até que a chave de saudação é atualizada. Para obter mais informações, vá muito[painel de serviço de Gerenciador de dispositivos do StorSimple uso Olá](storsimple-8000-service-dashboard.md).

chave de criptografia de dados de serviço Hello e certificado de criptografia de dados de saudação não expiram. No entanto, recomendamos que você altere a criptografia de dados de serviço Olá chave anualmente toohelp impedir comprometimento da chave.

## <a name="protect-data-at-rest"></a>Proteger dados em repouso

o dispositivo StorSimple Olá gerencia dados armazenando-o em camadas localmente e na nuvem hello, dependendo da frequência de uso. Todas as máquinas que estão conectados toohello dispositivo enviar dados toohello dispositivo, que move dados toohello na nuvem, conforme apropriado de host. Dados são transferidos da saudação dispositivo toohello nuvem com segurança pela Olá da Internet. Cada dispositivo tem um destino iSCSI que mostra todos os volumes compartilhados naquele dispositivo. Todos os dados são criptografados antes de serem enviado toocloud armazenamento. 

![Chave de criptografia de armazenamento em nuvem](./media/storsimple-security/CloudStorageEncryption.png)

toohelp garantir a segurança de saudação e integridade dos dados movidos nuvem toohello, StorSimple permite que você toodefine chaves de criptografia de armazenamento de nuvem da seguinte maneira:

* Você especificar a chave de criptografia de armazenamento de nuvem hello quando você cria um contêiner de volume. chave de saudação não pode ser modificado ou adicionado mais tarde.
* Todos os volumes em um compartilhamento de contêiner de volume Olá a mesma chave de criptografia. Se você quiser uma forma diferente de criptografia para um volume específico, é recomendável que você crie um novo toohost de contêiner de volume nesse volume.
* Quando você insere a chave de criptografia de armazenamento de nuvem Olá no Olá serviço do Gerenciador de dispositivos do StorSimple, chave de saudação é criptografada usando Olá a parte pública da chave de criptografia de dados de serviço hello e, em seguida, enviada toohello dispositivo.
* chave de criptografia de armazenamento de nuvem Olá não é armazenado em qualquer lugar no serviço de saudação e é conhecido apenas toohello dispositivo.
* Especificar uma chave de criptografia de armazenamento em nuvem é opcional. Você pode enviar dados que foram criptografados no dispositivo de toohello Olá host.

### <a name="additional-security-best-practices"></a>Práticas recomendadas de segurança adicionais

* Dividir o tráfego: isolar a rede SAN do iSCSI do tráfego do usuário em uma LAN corporativa implantando uma rede totalmente separada e usando VLANs em que o isolamento físico não é uma opção. Uma rede dedicada para o armazenamento iSCSI garantirá segurança hello e o desempenho de seus dados essenciais aos negócios. Misturar o tráfego de armazenamento e o de usuário em uma LAN corporativa não é recomendado e pode aumentar a latência e causar falhas de rede.
* Para a segurança de rede do lado do host, use as interfaces de rede que dão suporte a TOE (TCP/IP Offload Engine). TOE reduz a carga de CPU processando TCP no adaptador de rede de saudação.

## <a name="protect-data-via-storage-accounts"></a>Proteger dados por meio de contas de armazenamento

Cada assinatura do Microsoft Azure pode criar uma ou mais contas de armazenamento. (Uma conta de armazenamento fornece um namespace exclusivo para trabalhar com dados armazenados na nuvem do Azure do hello.) Conta de armazenamento tooa acesso é controlada pelas chaves de assinatura e de acesso de saudação associadas à conta de armazenamento.

Quando você cria uma conta de armazenamento, o Microsoft Azure gera duas chaves de acesso de armazenamento de 512 bits, um dos quais é usado para autenticação quando o dispositivo StorSimple Olá acessa a conta de armazenamento hello. Observe que apenas uma dessas chaves está em uso. Olá outra chave é mantida em reserva, permitindo que você toorotate Olá chaves periodicamente. toorotate chaves, que ativa de chave secundária hello e chave primária de saudação de exclusão. Em seguida, você pode criar uma nova chave para uso durante o próximo rodízio de saudação. (Por motivos de segurança, muitos data centers exigem a rotação de chaves.)

Recomendamos seguir estas práticas recomendadas para a rotação de chaves:

* Você deve girar chaves conta de armazenamento regularmente toohelp Certifique-se de que sua conta de armazenamento não é acessada por usuários não autorizados.
* Periodicamente, o administrador do Azure deve alterar ou regenerar chave primária ou secundária de saudação usando a seção de armazenamento de saudação do hello conta de armazenamento do Azure toodirectly portal acesso hello.

## <a name="protect-data-via-encryption"></a>Proteger dados por meio de criptografia

StorSimple usa Olá seguintes algoritmos de criptografia tooprotect dados armazenados em ou transportados entre componentes de saudação da sua solução StorSimple.

| Algoritmo | Comprimento da chave | Aplicativos/protocolos/comentários |
| --- | --- | --- |
| RSA |2.048 |O RSA PKCS 1 v 1.5 é usado pelo Olá dados de configuração de tooencrypt portal do Azure que são enviados toohello dispositivo: por exemplo, armazenamento de credenciais, a configuração do dispositivo StorSimple, da conta e chaves de criptografia de armazenamento em nuvem. |
| AES |256 |AES com CBC é usado tooencrypt parte pública do hello da chave de criptografia de dados de serviço de saudação antes de serem enviado do dispositivo do StorSimple Olá toohello portal do Azure. Ele também é usado por Olá StorSimple dispositivo tooencrypt de dados antes de dados saudação são enviados toohello conta de armazenamento de nuvem. |

## <a name="storsimple-cloud-appliance-security"></a>Segurança do Dispositivo de Nuvem StorSimple

[!INCLUDE [storsimple Cloud Appliance security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Perguntas frequentes (FAQ)

Olá seguem algumas perguntas e respostas sobre segurança e o Microsoft Azure StorSimple.

**P:** Meu serviço está comprometido. Qual deve ser minhas próximas etapas?

**R:** você deve alterar chave de criptografia de dados de serviço hello e chaves de conta de armazenamento Olá Olá conta de armazenamento que está sendo usado para colocar dados imediatamente. Para obter instruções, vá para:

* [Alterar a chave de criptografia de dados de serviço Olá](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Rotação de chave de contas de armazenamento](storsimple-8000-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**P:** tiver um dispositivo StorSimple novo que está solicitando a chave de registro do serviço de saudação. Como recuperá-la?

**R:** essa chave foi criada quando você criou o serviço do Gerenciador de dispositivos de StorSimple Olá primeiro. Quando você usa um dispositivo de toohello tooconnect do serviço de Gerenciador de dispositivos de StorSimple Olá, você pode usar o hello tooview de página de início rápido de serviço ou a chave de registro de serviço Olá regenerar. Gerar uma nova chave de registro de serviço não afetarão os dispositivos registrados existentes hello. Para obter instruções, vá para:

* [Exibir ou regenerar a chave de registro de serviço Olá](storsimple-8000-manage-service.md##regenerate-the-service-registration-key)

**P:** Perdi minha chave de criptografia de dados de serviço. O que devo fazer?

**R:** Entre em contato com o Suporte da Microsoft. Eles podem fazer logon tooa a sessão de suporte no seu dispositivo e ajudar você a recuperar chave hello (desde que pelo menos um dispositivo está online). Imediatamente depois de obter a chave de criptografia de dados de serviço hello, você deve alterá-la tooensure essa nova chave de saudação é conhecido apenas tooyou. Para obter instruções, vá para:

* [Alterar a chave de criptografia de dados de serviço Olá](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**P:** autorizei um dispositivo para uma alteração de chave de criptografia de dados serviço, mas não foi iniciado o processo de alteração de chave hello. O que devo fazer?

**R:** se Olá período de tempo limite tiver expirado, será necessário tooreauthorize dispositivo de saudação para alteração de criptografia de dados chave serviço hello e iniciar o processo de saudação novamente.

**P:** alterei a chave de criptografia de dados de serviço hello, mas não foi possível tooupdate Olá outros dispositivos em 4 horas. É necessário toostart novamente?

**R:** Olá o período de tempo de 4 horas é apenas para iniciar a alteração de saudação. Depois de iniciar o processo de atualização de saudação em Olá autorizado dispositivo StorSimple, autorização Olá é válida até que todos os dispositivos sejam atualizados.

**P:** nosso administrador StorSimple saiu da empresa de saudação. O que devo fazer?

**R:** altere e redefina Olá senhas que permitem acessar toohello o dispositivo StorSimple e alterar Olá serviço dados criptografia chave tooensure que novas informações de saudação não são conhecidas toounauthorized pessoal. Para obter instruções, vá para:

* [Usar toochange de serviço do Gerenciador de dispositivos de StorSimple Olá suas senhas de storsimple](storsimple-8000-change-passwords.md)
* [Alterar a chave de criptografia de dados de serviço Olá](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Configure o CHAP para o seu dispositivo StorSimple](storsimple-8000-configure-chap.md)

**P:** tooprovide Olá StorSimple Snapshot Manager senha tooa host que está se conectando o dispositivo StorSimple toohello desejado, mas Olá senha não está disponível. O que posso fazer?

**R:** se você tiver esquecido a senha de saudação, você deve criar um novo. Em seguida, certifique-se de que tooinform todos os usuários existentes que Olá senha foi alterada e que eles devem atualizar seu clientes toouse Olá nova senha. Para obter instruções, vá para:

* [Alterar a senha do StorSimple Snapshot Manager Olá](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)
* [Autenticar um dispositivo](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**P:** certificado Olá para toohello de acesso remoto do Windows PowerShell para StorSimple foi alterado no dispositivo de saudação. Como atualizar meus clientes de acesso remoto?

**R:** você pode baixar o novo certificado de saudação do hello serviço do Gerenciador de dispositivos do StorSimple e depois fornecê-la toobe instalado no repositório de certificados de saudação de seus clientes de acesso remoto. Para obter instruções, vá para:

* [Certificado de importação de cmdlet](https://technet.microsoft.com/library/hh848630.aspx)

**P:** meus dados ficarão protegidos se Olá serviço do Gerenciador de dispositivos do StorSimple estiver comprometido?

**R:** Os dados de configuração de serviço são sempre criptografados com a chave pública quando exibidos em um navegador da Web. Porque o serviço de saudação não tem chave privada do acesso toohello, serviço Olá não poderá ser capaz de toosee todos os dados. Se Olá serviço do Gerenciador de dispositivos do StorSimple estiver comprometido, há nenhum impacto, pois não há nenhuma chave armazenada no hello serviço do Gerenciador de dispositivos do StorSimple.

**P:** se alguém obtiver o certificado de criptografia de dados do access toohello, serão meus dados ficarão comprometidos?

**R:** Microsoft Azure armazena a chave de criptografia de dados do cliente da saudação (arquivo. pfx) em um formato criptografado. Arquivo. pfx de saudação é criptografado e Olá serviço StorSimple tem Olá serviço dados criptografia toodecrypt chave Olá arquivo.pfx, simplesmente obter o arquivo. pfx do access toohello não expõe nenhum segredo.

**P:** O que acontece se uma entidade governamental solicitar meus dados à Microsoft?

**R:** porque todos os dados de saudação são criptografados no serviço hello e Olá chave privada é mantida com dispositivo hello, hello governamental entidade deve solicitar ao cliente Olá dados saudação.

## <a name="next-steps"></a>Próximas etapas

[Implantar o dispositivo StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

