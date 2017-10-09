---
title: "aaaEncrypting seu conteúdo com criptografia de armazenamento usando a API de REST AMS"
description: "Saiba como tooencrypt seu conteúdo com criptografia de armazenamento usando as APIs de REST AMS."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="0f72b-103">Criptografia do seu conteúdo com criptografia de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0f72b-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="0f72b-104">É altamente recomendável tooencrypt o conteúdo localmente usando AES-256 bits de criptografia e, em seguida, carregá-lo tooAzure armazenamento onde serão armazenado criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="0f72b-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="0f72b-105">Este artigo fornece uma visão geral da criptografia de armazenamento AMS e mostra como o armazenamento de saudação tooupload conteúdo criptografado:</span><span class="sxs-lookup"><span data-stu-id="0f72b-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="0f72b-106">Crie uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-106">Create a content key.</span></span>
* <span data-ttu-id="0f72b-107">Crie um ativo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-107">Create an Asset.</span></span> <span data-ttu-id="0f72b-108">Defina Olá AssetCreationOption tooStorageEncryption ao criar hello ativo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="0f72b-109">Ativos criptografados têm toobe associado às chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="0f72b-110">Ativo de conteúdo toohello chave do link hello.</span><span class="sxs-lookup"><span data-stu-id="0f72b-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="0f72b-111">Definir criptografia Olá relacionados parâmetros em entidades de AssetFile hello.</span><span class="sxs-lookup"><span data-stu-id="0f72b-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="0f72b-112">Considerações</span><span class="sxs-lookup"><span data-stu-id="0f72b-112">Considerations</span></span> 

<span data-ttu-id="0f72b-113">Se você quiser toodeliver um ativo de armazenamento criptografado, você deve configurar a política de entrega do hello ativo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="0f72b-114">Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado a política de distribuição.</span><span class="sxs-lookup"><span data-stu-id="0f72b-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="0f72b-115">Para obter mais informações, confira a seção [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md)(Configurando as Políticas de Entrega de Ativos).</span><span class="sxs-lookup"><span data-stu-id="0f72b-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="0f72b-116">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f72b-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0f72b-117">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0f72b-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="0f72b-118">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="0f72b-118">Connect tooMedia Services</span></span>

<span data-ttu-id="0f72b-119">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0f72b-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0f72b-120">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0f72b-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0f72b-121">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="0f72b-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="0f72b-122">Visão geral da criptografia de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0f72b-122">Storage encryption overview</span></span>
<span data-ttu-id="0f72b-123">aplica-se a criptografia de armazenamento Olá AMS **AES CTR** arquivo inteiro do modo criptografia toohello.</span><span class="sxs-lookup"><span data-stu-id="0f72b-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="0f72b-124">O modo AES-CTR é uma codificação de bloco que pode criptografar dados de comprimento arbitrário sem necessidade de preenchimento.</span><span class="sxs-lookup"><span data-stu-id="0f72b-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="0f72b-125">Ele funciona por criptografia de um bloco de contador com o algoritmo AES de saudação e, em seguida, saída de hello ndo XOR de AES com hello dados tooencrypt ou descriptografar.</span><span class="sxs-lookup"><span data-stu-id="0f72b-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="0f72b-126">bloco de contador Olá usado é construído, copie o valor Olá Olá InitializationVector toobytes 0 too7 do valor do contador Olá e too15 bytes 8 do valor do contador Olá são definidos toozero.</span><span class="sxs-lookup"><span data-stu-id="0f72b-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="0f72b-127">Olá 16 bytes contador do bloco de bytes 8 too15 (ou seja, bytes menos significantes Olá) são usados como um inteiro não assinado de 64 bits simples que é incrementado em um para cada bloco subsequente de dados processados e é mantido em ordem de bytes de rede.</span><span class="sxs-lookup"><span data-stu-id="0f72b-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="0f72b-128">Observe que se esse número inteiro atingir o valor para máximo de saudação (0xFFFFFFFFFFFFFFFF), em seguida, incrementando-redefine Olá bloco contador toozero (too15 bytes 8) sem afetar outra Olá 64 bits do contador hello (ou seja, too7 bytes 0).</span><span class="sxs-lookup"><span data-stu-id="0f72b-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="0f72b-129">Na segurança de saudação de toomaintain de ordem de criptografia de modo Olá CTR AES, hello InitializationVector valor para um determinado identificador de chave para cada chave de conteúdo deve ser exclusivo para cada arquivo e arquivos devem ser menor que 2 ^ 64 blocos de comprimento.</span><span class="sxs-lookup"><span data-stu-id="0f72b-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="0f72b-130">Isso é tooensure que um valor de contador nunca é reutilizado com uma determinada chave.</span><span class="sxs-lookup"><span data-stu-id="0f72b-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="0f72b-131">Para obter mais informações sobre o modo CTR hello, consulte [nesta página wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (artigo do wiki Olá usa o termo hello "Nonce" em vez de "InitializationVector").</span><span class="sxs-lookup"><span data-stu-id="0f72b-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="0f72b-132">Use **criptografia de armazenamento** tooencrypt o conteúdo limpo localmente usando AES-256 bits de criptografia e, em seguida, carregá-lo tooAzure armazenamento onde ele está armazenado criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="0f72b-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="0f72b-133">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="0f72b-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="0f72b-134">caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.</span><span class="sxs-lookup"><span data-stu-id="0f72b-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="0f72b-135">Ordem toodeliver um ativo de armazenamento criptografado, você deve configurar a política de distribuição do ativo Olá para que serviços de mídia saibam como você deseja toodeliver seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="0f72b-136">Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado política de entrega (por exemplo, AES, criptografia comum ou sem criptografia).</span><span class="sxs-lookup"><span data-stu-id="0f72b-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="0f72b-137">Criar ContentKeys usadas para criptografia</span><span class="sxs-lookup"><span data-stu-id="0f72b-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="0f72b-138">Ativos criptografados têm toobe associado à chave de criptografia de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f72b-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="0f72b-139">Você deve criar hello conteúdo toobe chave usada para criptografia antes de criar hello arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="0f72b-140">Esta seção descreve como toocreate uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="0f72b-141">Olá, a seguir estão as etapas gerais para a geração de chaves de conteúdo que você associará ativos que você deseja toobe criptografado.</span><span class="sxs-lookup"><span data-stu-id="0f72b-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="0f72b-142">Na criptografia de armazenamento, gere uma chave AES de 32 bytes aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="0f72b-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="0f72b-143">Essa será a chave de conteúdo de saudação para seu ativo, o que significa que todos os arquivos associados com esse ativo será necessário toouse Olá a mesma chave de conteúdo durante a descriptografia.</span><span class="sxs-lookup"><span data-stu-id="0f72b-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="0f72b-144">Chamar hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) e [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget métodos Olá certificado x. 509 correto que deve ser usado tooencrypt sua chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="0f72b-145">Criptografe a chave de conteúdo com a chave pública de saudação do hello certificado x. 509.</span><span class="sxs-lookup"><span data-stu-id="0f72b-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="0f72b-146">SDK do Media Services .NET usa o RSA com OAEP ao usar a criptografia de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="0f72b-147">Você pode ver um exemplo .NET no hello [EncryptSymmetricKeyData função](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="0f72b-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="0f72b-148">Crie um valor de soma de verificação calculado usando o identificador de chave de saudação e a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="0f72b-149">Olá .NET de exemplo a seguir calcula a soma de verificação de saudação usando Olá GUID parte do identificador de chave hello e Olá limpar chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. <span data-ttu-id="0f72b-150">Criar chave de conteúdo Olá com hello **EncryptedContentKey** (convertido a cadeia de caracteres codificada toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, e **Checksum** valores que você recebeu nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="0f72b-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="0f72b-151">Para criptografia de armazenamento, hello propriedades a seguir devem ser incluídas no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="0f72b-152">Propriedade do corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="0f72b-152">Request body property</span></span>    | <span data-ttu-id="0f72b-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f72b-153">Description</span></span>
    ---|---
    <span data-ttu-id="0f72b-154">ID</span><span class="sxs-lookup"><span data-stu-id="0f72b-154">Id</span></span> | <span data-ttu-id="0f72b-155">Olá Id de ContentKey que podemos gerar nós usando Olá após formatar, "NB:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="0f72b-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="0f72b-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="0f72b-156">ContentKeyType</span></span> | <span data-ttu-id="0f72b-157">Isso é o tipo de chave de conteúdo do hello como um inteiro para esta chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="0f72b-158">Passamos o valor de saudação 1 para criptografia de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f72b-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="0f72b-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="0f72b-159">EncryptedContentKey</span></span> | <span data-ttu-id="0f72b-160">Criamos um novo valor de chave de conteúdo, que é um valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="0f72b-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="0f72b-161">chave de saudação é criptografada usando o certificado x. 509 de criptografia de armazenamento de saudação que recuperamos de serviços de mídia do Microsoft Azure, executando uma solicitação HTTP GET para hello GetProtectionKeyId e GetProtectionKey métodos.</span><span class="sxs-lookup"><span data-stu-id="0f72b-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="0f72b-162">Por exemplo, consulte Olá código .NET a seguir: Olá **EncryptSymmetricKeyData** método definido [aqui](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="0f72b-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="0f72b-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="0f72b-163">ProtectionKeyId</span></span> | <span data-ttu-id="0f72b-164">Isso é Olá id de chave de proteção para o certificado x. 509 de criptografia de armazenamento de saudação que foi usado tooencrypt a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="0f72b-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="0f72b-165">ProtectionKeyType</span></span> | <span data-ttu-id="0f72b-166">Este é o tipo de criptografia de saudação para chave de proteção de saudação que foi usado tooencrypt chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="0f72b-167">Em nosso exemplo, este valor será StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="0f72b-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="0f72b-168">Soma de verificação</span><span class="sxs-lookup"><span data-stu-id="0f72b-168">Checksum</span></span> |<span data-ttu-id="0f72b-169">Olá MD5 soma de verificação calculada para a chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="0f72b-170">Ela é computada criptografando a Id do conteúdo Olá com chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="0f72b-171">o código de exemplo Hello demonstra como toocalculate Olá soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="0f72b-172">Recuperar Olá ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="0f72b-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="0f72b-173">saudação de exemplo a seguir mostra como tooretrieve Olá ProtectionKeyId, uma impressão digital, Olá certificado você deve usar ao criptografar a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="0f72b-174">Faça essa toomake etapa-se de que você já tem o certificado apropriado Olá em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0f72b-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="0f72b-175">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="0f72b-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0f72b-176">Resposta:</span><span class="sxs-lookup"><span data-stu-id="0f72b-176">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="0f72b-177">Recuperar hello ProtectionKey para Olá ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="0f72b-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="0f72b-178">Olá exemplo a seguir mostra como certificado de x. 509 Olá tooretrieve usando Olá ProtectionKeyId que você recebeu na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0f72b-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="0f72b-179">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="0f72b-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="0f72b-180">Resposta:</span><span class="sxs-lookup"><span data-stu-id="0f72b-180">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a><span data-ttu-id="0f72b-181">Criar chave de conteúdo Olá</span><span class="sxs-lookup"><span data-stu-id="0f72b-181">Create hello content key</span></span>
<span data-ttu-id="0f72b-182">Depois de recuperar o certificado x. 509 de saudação e usado seu tooencrypt de chave pública a chave de conteúdo, crie um **ContentKey** entidade e defina sua propriedade valores adequadamente.</span><span class="sxs-lookup"><span data-stu-id="0f72b-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="0f72b-183">Um dos valores de saudação que você deve definir quando criar hello conteúdo de chave é o tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f72b-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="0f72b-184">No caso de criptografia de armazenamento hello, o valor de saudação é '1'.</span><span class="sxs-lookup"><span data-stu-id="0f72b-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="0f72b-185">Olá mostrado no exemplo a seguir como toocreate uma **ContentKey** com um **ContentKeyType** definido para criptografia de armazenamento ("1") e hello **ProtectionKeyType** definido muito "0" tooindicate que Olá Id da chave de proteção é a impressão digital do certificado Olá x. 509.</span><span class="sxs-lookup"><span data-stu-id="0f72b-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="0f72b-186">Solicitação</span><span class="sxs-lookup"><span data-stu-id="0f72b-186">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="0f72b-187">Resposta:</span><span class="sxs-lookup"><span data-stu-id="0f72b-187">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="0f72b-188">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="0f72b-188">Create an asset</span></span>
<span data-ttu-id="0f72b-189">Olá mostrado no exemplo a seguir como toocreate um ativo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="0f72b-190">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f72b-190">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="0f72b-191">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f72b-191">**HTTP Response**</span></span>

<span data-ttu-id="0f72b-192">Se for bem-sucedido, a seguir Olá será retornada:</span><span class="sxs-lookup"><span data-stu-id="0f72b-192">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="0f72b-193">Associar a um ativo de saudação ContentKey</span><span class="sxs-lookup"><span data-stu-id="0f72b-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="0f72b-194">Depois de criar hello ContentKey, associe-o seu ativo usando a operação de saudação $links, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="0f72b-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="0f72b-195">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="0f72b-195">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="0f72b-196">Resposta:</span><span class="sxs-lookup"><span data-stu-id="0f72b-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="0f72b-197">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="0f72b-197">Create an AssetFile</span></span>
<span data-ttu-id="0f72b-198">Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="0f72b-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="0f72b-199">Um arquivo de ativo está sempre associado a um ativo e um ativo pode conter um ou vários arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="0f72b-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="0f72b-200">tarefa do Media Services Encoder Olá falhará se um objeto de arquivo do ativo não está associado um arquivo digital em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="0f72b-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="0f72b-201">Observe que Olá **AssetFile** instância e o arquivo de mídia real Olá são dois objetos distintos.</span><span class="sxs-lookup"><span data-stu-id="0f72b-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="0f72b-202">instância de AssetFile Olá contém metadados sobre o arquivo de mídia Olá, enquanto o arquivo de mídia Olá contém conteúdo de mídia real hello.</span><span class="sxs-lookup"><span data-stu-id="0f72b-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="0f72b-203">Depois de carregar o arquivo de mídia digital em um contêiner de blob, você usará Olá **mesclar** Olá tooupdate de solicitação HTTP AssetFile com informações sobre o arquivo de mídia (não mostrado neste tópico).</span><span class="sxs-lookup"><span data-stu-id="0f72b-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="0f72b-204">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f72b-204">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="0f72b-205">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f72b-205">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
