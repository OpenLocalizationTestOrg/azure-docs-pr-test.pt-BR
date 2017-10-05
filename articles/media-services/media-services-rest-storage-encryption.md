---
title: "Como criptografar seu conteúdo com a criptografia de armazenamento usando a API REST do AMS"
description: "Saiba como criptografar seu conteúdo com criptografia de armazenamento usando as APIs REST do AMS."
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
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="f3f14-103">Criptografia do seu conteúdo com criptografia de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f3f14-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="f3f14-104">Recomendamos que você criptografe seu conteúdo localmente usando a criptografia AES de 256 bits e, em seguida, o carregue no armazenamento do Azure no qual ele será armazenado e criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="f3f14-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="f3f14-105">Este artigo fornece uma visão geral da criptografia de armazenamento do AMS e mostra como carregar o conteúdo de armazenamento criptografado:</span><span class="sxs-lookup"><span data-stu-id="f3f14-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="f3f14-106">Crie uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-106">Create a content key.</span></span>
* <span data-ttu-id="f3f14-107">Crie um ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-107">Create an Asset.</span></span> <span data-ttu-id="f3f14-108">Defina o AssetCreationOption como StorageEncryption ao criar o ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="f3f14-109">Os ativos criptografados precisam ser associados às chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-109">Encrypted assets have to be associated with content keys.</span></span>
* <span data-ttu-id="f3f14-110">Vincular a chave de conteúdo ao ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="f3f14-111">Defina os parâmetros relacionados à criptografia nas entidades AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f3f14-111">Set the encryption related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="f3f14-112">Considerações</span><span class="sxs-lookup"><span data-stu-id="f3f14-112">Considerations</span></span> 

<span data-ttu-id="f3f14-113">Se você quiser entregar um ativo de armazenamento criptografado, configure a política de entrega do ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="f3f14-114">Antes que seu ativo possa ser transmitido, o servidor de streaming remove a criptografia de armazenamento e transmite o conteúdo usando a política de entrega especificada.</span><span class="sxs-lookup"><span data-stu-id="f3f14-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="f3f14-115">Para obter mais informações, confira a seção [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md)(Configurando as Políticas de Entrega de Ativos).</span><span class="sxs-lookup"><span data-stu-id="f3f14-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="f3f14-116">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3f14-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f3f14-117">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f3f14-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-to-media-services"></a><span data-ttu-id="f3f14-118">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="f3f14-118">Connect to Media Services</span></span>

<span data-ttu-id="f3f14-119">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f3f14-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="f3f14-120">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="f3f14-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f3f14-121">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="f3f14-121">You must make subsequent calls to the new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="f3f14-122">Visão geral da criptografia de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f3f14-122">Storage encryption overview</span></span>
<span data-ttu-id="f3f14-123">A criptografia de armazenamento do AMS aplica a criptografia do modo **AES-CTR** no arquivo inteiro.</span><span class="sxs-lookup"><span data-stu-id="f3f14-123">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="f3f14-124">O modo AES-CTR é uma codificação de bloco que pode criptografar dados de comprimento arbitrário sem necessidade de preenchimento.</span><span class="sxs-lookup"><span data-stu-id="f3f14-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="f3f14-125">Ela funciona criptografando um bloco de contador com o algoritmo AES e aplicando XOR à saída do AES com os dados para criptografar ou descriptografar.</span><span class="sxs-lookup"><span data-stu-id="f3f14-125">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="f3f14-126">O bloco de contador usado é construído copiando o valor do InitializationVector para bytes de 0 a 7 do valor do contador e 8 a 15 do valor do contador são definidos como zero.</span><span class="sxs-lookup"><span data-stu-id="f3f14-126">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="f3f14-127">Do bloco de contador de 16 bytes, os bytes de 8 a 15 (ou seja, os bytes menos significativos) são usados como um inteiro sem sinal de 64 bits simples que é incrementado em um para cada bloco subsequente de dados processados e é mantido em ordem de byte da rede.</span><span class="sxs-lookup"><span data-stu-id="f3f14-127">Of the 16 byte counter block, bytes 8 to 15 (i.e. the least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="f3f14-128">Observe que, se esse número inteiro atingir o valor máximo (0xFFFFFFFFFFFFFFFF), incrementá-lo redefinirá o contador de bloco para zero (bytes 8 a 15) sem afetar os 64 bits do contador (ou seja, bytes de 0 a 7).</span><span class="sxs-lookup"><span data-stu-id="f3f14-128">Note that if this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (i.e. bytes 0 to 7).</span></span>   <span data-ttu-id="f3f14-129">Para manter a segurança de criptografia do modo AES-CTR, o valor do InitializationVector de um determinado Identificador Chave para cada conteúdo deve ser exclusivo para cada arquivo e os arquivos devem ser menores do que 2^64 blocos em comprimento.</span><span class="sxs-lookup"><span data-stu-id="f3f14-129">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="f3f14-130">Isso serve para garantir que um valor de contador jamais seja reutilizado com uma determinada chave.</span><span class="sxs-lookup"><span data-stu-id="f3f14-130">This is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="f3f14-131">Para obter mais informações sobre o modo CTR, confira [esta página wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (o artigo da wiki usa o termo "Nonce" em vez de "InitializationVector").</span><span class="sxs-lookup"><span data-stu-id="f3f14-131">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="f3f14-132">Use a **Criptografia de Armazenamento** para criptografar seu conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carregue-a no Armazenamento do Azure no qual ela é armazenada e criptografada em repouso.</span><span class="sxs-lookup"><span data-stu-id="f3f14-132">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="f3f14-133">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um sistema de arquivos criptografado antes da codificação, então opcionalmente criptografados novamente antes do carregamento como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="f3f14-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="f3f14-134">O caso de uso primário para criptografia de armazenamento é quando você deseja proteger seus arquivos de mídia de entrada de alta qualidade com criptografia forte em repouso no disco.</span><span class="sxs-lookup"><span data-stu-id="f3f14-134">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="f3f14-135">Para entregar um ativo de armazenamento criptografado, você deve configurar a política de entrega do ativo para que o Serviços de Mídia saiba como você deseja distribuir seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-135">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="f3f14-136">Antes que seu ativo possa ser transmitido, o servidor de streaming remove a criptografia de armazenamento e transmite o conteúdo usando a política de distribuição especificada (por exemplo, AES, criptografia comum ou sem criptografia).</span><span class="sxs-lookup"><span data-stu-id="f3f14-136">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="f3f14-137">Criar ContentKeys usadas para criptografia</span><span class="sxs-lookup"><span data-stu-id="f3f14-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="f3f14-138">Os ativos criptografados precisam ser associados à chave de criptografia de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f3f14-138">Encrypted assets have to be associated with Storage Encryption key.</span></span> <span data-ttu-id="f3f14-139">Você deve criar a chave de conteúdo a ser usada para criptografia antes de criar os arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-139">You must create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="f3f14-140">Este artigo descreve como criar uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-140">This section describes how to create a content key.</span></span>

<span data-ttu-id="f3f14-141">A seguir estão as etapas gerais para gerar chaves de conteúdo que você associará aos ativos que você deseja que sejam criptografados.</span><span class="sxs-lookup"><span data-stu-id="f3f14-141">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="f3f14-142">Na criptografia de armazenamento, gere uma chave AES de 32 bytes aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="f3f14-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="f3f14-143">Esta será a chave de conteúdo para o seu ativo, o que significa que será necessário usar a mesma chave de conteúdo com todos os arquivos associados a esse ativo durante a descriptografia.</span><span class="sxs-lookup"><span data-stu-id="f3f14-143">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="f3f14-144">Chame os métodos [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) e [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) para obter o Certificado X.509 correto que deve ser usado para criptografar sua chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-144">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="f3f14-145">Criptografe a chave de conteúdo com a chave pública do certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="f3f14-145">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="f3f14-146">O SDK do .NET dos serviços de mídia usa RSA com OAEP ao fazer a criptografia.</span><span class="sxs-lookup"><span data-stu-id="f3f14-146">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="f3f14-147">Você pode ver um exemplo do .NET na [função EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="f3f14-147">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="f3f14-148">Crie um valor de soma de verificação calculado usando o identificador de chave e a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-148">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="f3f14-149">O exemplo de .NET a seguir calcula a soma de verificação usando a parte GUID do identificador de chave e a chave de conteúdo limpa.</span><span class="sxs-lookup"><span data-stu-id="f3f14-149">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
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

1. <span data-ttu-id="f3f14-150">Crie a chave de conteúdo com os valores **EncryptedContentKey** (convertido em cadeia de caracteres codificada em base64), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** e **Checksum** que você recebeu nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f3f14-150">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="f3f14-151">Na criptografia de armazenamento, as propriedades a seguir devem ser incluídas no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="f3f14-151">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="f3f14-152">Propriedade do corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="f3f14-152">Request body property</span></span>    | <span data-ttu-id="f3f14-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="f3f14-153">Description</span></span>
    ---|---
    <span data-ttu-id="f3f14-154">ID</span><span class="sxs-lookup"><span data-stu-id="f3f14-154">Id</span></span> | <span data-ttu-id="f3f14-155">A ID de ContentKey que nós mesmos geramos usando o seguinte formato, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="f3f14-155">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="f3f14-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="f3f14-156">ContentKeyType</span></span> | <span data-ttu-id="f3f14-157">Esse é o tipo de chave de conteúdo, como um inteiro para esta chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-157">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="f3f14-158">Passamos o valor 1 para a criptografia de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f3f14-158">We pass the value 1 for storage encryption.</span></span>
    <span data-ttu-id="f3f14-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="f3f14-159">EncryptedContentKey</span></span> | <span data-ttu-id="f3f14-160">Criamos um novo valor de chave de conteúdo, que é um valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="f3f14-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="f3f14-161">A chave é criptografada usando o certificado X.509 de criptografia de armazenamento que recuperamos dos Serviços de Mídia do Microsoft Azure por meio da execução de uma solicitação HTTP GET para os métodos GetProtectionKeyId e GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="f3f14-161">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="f3f14-162">Como um exemplo, confira o seguinte código do .NET: o método **EncryptSymmetricKeyData** definido [aqui](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="f3f14-162">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="f3f14-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="f3f14-163">ProtectionKeyId</span></span> | <span data-ttu-id="f3f14-164">Essa é a ID da chave de proteção para o certificado X.509 de criptografia de armazenamento usado para criptografar nossa chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-164">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="f3f14-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="f3f14-165">ProtectionKeyType</span></span> | <span data-ttu-id="f3f14-166">Esse é o tipo de criptografia para a chave de proteção usada para criptografar a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-166">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="f3f14-167">Em nosso exemplo, este valor será StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="f3f14-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="f3f14-168">Soma de verificação</span><span class="sxs-lookup"><span data-stu-id="f3f14-168">Checksum</span></span> |<span data-ttu-id="f3f14-169">A soma de verificação calculada por MD5 para a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-169">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="f3f14-170">Ela é calculada pela criptografia da ID de conteúdo com a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-170">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="f3f14-171">O exemplo de código demonstra como calcular a soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="f3f14-171">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="f3f14-172">Recuperação de ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="f3f14-172">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="f3f14-173">O exemplo a seguir mostra como recuperar o ProtectionKeyId, uma impressão digital de certificado, para o certificado que você deve usar ao criptografar a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-173">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="f3f14-174">Conclua esta etapa para certificar-se de que você já tem o certificado apropriado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f3f14-174">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="f3f14-175">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="f3f14-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="f3f14-176">Resposta:</span><span class="sxs-lookup"><span data-stu-id="f3f14-176">Response:</span></span>

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

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="f3f14-177">Recuperar ProtectionKey para o ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="f3f14-177">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="f3f14-178">O exemplo a seguir mostra como recuperar o certificado X.509 usando o ProtectionKeyId recebido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f3f14-178">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="f3f14-179">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="f3f14-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="f3f14-180">Resposta:</span><span class="sxs-lookup"><span data-stu-id="f3f14-180">Response:</span></span>

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

### <a name="create-the-content-key"></a><span data-ttu-id="f3f14-181">Criar a chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="f3f14-181">Create the content key</span></span>
<span data-ttu-id="f3f14-182">Depois de recuperar o certificado X.509 e usar sua chave pública para criptografar a chave de conteúdo, crie uma entidade **ContentKey** e defina seus valores de propriedade adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f3f14-182">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="f3f14-183">Um dos valores que você deve definir quando criar o conteúdo chave é o tipo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-183">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="f3f14-184">No caso da criptografia de armazenamento, o valor é '1'.</span><span class="sxs-lookup"><span data-stu-id="f3f14-184">In case of the storage encryption, the value is '1'.</span></span> 

<span data-ttu-id="f3f14-185">O exemplo a seguir mostra como criar um **ContentKey** com um **ContentKeyType** definido para criptografia de armazenamento ("1") e o **ProtectionKeyType** definido como "0", para indicar que a ID da chave de proteção é a impressão digital do certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="f3f14-185">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="f3f14-186">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f3f14-186">Request</span></span>

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

<span data-ttu-id="f3f14-187">Resposta:</span><span class="sxs-lookup"><span data-stu-id="f3f14-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="f3f14-188">Criar um ativo</span><span class="sxs-lookup"><span data-stu-id="f3f14-188">Create an asset</span></span>
<span data-ttu-id="f3f14-189">O exemplo a seguir mostra como criar um ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-189">The following example shows how to create an asset.</span></span>

<span data-ttu-id="f3f14-190">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="f3f14-190">**HTTP Request**</span></span>

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

<span data-ttu-id="f3f14-191">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f3f14-191">**HTTP Response**</span></span>

<span data-ttu-id="f3f14-192">Se for bem-sucedido, será retornado o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3f14-192">If successful, the following is returned:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="f3f14-193">Associar o ContentKey com um ativo</span><span class="sxs-lookup"><span data-stu-id="f3f14-193">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="f3f14-194">Depois de criar o ContentKey, associe-o ao seu ativo usando a operação $links, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3f14-194">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="f3f14-195">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="f3f14-195">Request:</span></span>

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

<span data-ttu-id="f3f14-196">Resposta:</span><span class="sxs-lookup"><span data-stu-id="f3f14-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="f3f14-197">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="f3f14-197">Create an AssetFile</span></span>
<span data-ttu-id="f3f14-198">A entidade [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa um arquivo de áudio ou vídeo que é armazenado em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="f3f14-198">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="f3f14-199">Um arquivo de ativo está sempre associado a um ativo e um ativo pode conter um ou vários arquivos de ativo.</span><span class="sxs-lookup"><span data-stu-id="f3f14-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="f3f14-200">A tarefa do Codificador dos serviços de mídia falha se um objeto de arquivo de ativo não estiver associado um arquivo digital em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="f3f14-200">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="f3f14-201">Observe que a instância de **AssetFile** e o arquivo de mídia real são dois objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="f3f14-201">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="f3f14-202">A instância de AssetFile contém metadados sobre o arquivo de mídia, enquanto o arquivo de mídia contém o conteúdo de mídia real.</span><span class="sxs-lookup"><span data-stu-id="f3f14-202">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="f3f14-203">Depois de carregar seu arquivo de mídia digital em um contêiner de blobs, você usará a solicitação HTTP **MERGE** para atualizar o AssetFile com informações sobre o arquivo de mídia (não mostrado neste tópico).</span><span class="sxs-lookup"><span data-stu-id="f3f14-203">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="f3f14-204">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="f3f14-204">**HTTP Request**</span></span>

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

<span data-ttu-id="f3f14-205">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="f3f14-205">**HTTP Response**</span></span>

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
