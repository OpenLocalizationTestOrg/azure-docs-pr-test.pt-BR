<span data-ttu-id="6ee86-101">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="6ee86-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="6ee86-102">Olá contêiner faz parte do nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="6ee86-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="6ee86-103">Por exemplo, `mycontainer` é Olá nome do contêiner de saudação nesses URIs do blob de exemplo:</span><span class="sxs-lookup"><span data-stu-id="6ee86-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="6ee86-104">Um nome de contêiner deve ser um nome DNS válido, toohello conformidade com as regras de nomenclatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee86-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="6ee86-105">Os nomes de contêiner devem começar com uma letra ou número e podem conter apenas letras, números e caracteres de traço (-) hello.</span><span class="sxs-lookup"><span data-stu-id="6ee86-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="6ee86-106">Cada caractere traço (-) deve ser imediatamente precedido e seguido por uma letra ou número. Não são permitidos traços consecutivos em nomes de contêiner.</span><span class="sxs-lookup"><span data-stu-id="6ee86-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="6ee86-107">Todas as letras do nome de um contêiner devem ser minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6ee86-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="6ee86-108">Os nomes de contêiner devem ter de 3 a 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6ee86-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ee86-109">Observe que Olá nome de um contêiner deve sempre estar em minúscula.</span><span class="sxs-lookup"><span data-stu-id="6ee86-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="6ee86-110">Se você incluir uma letra maiuscula em um nome de contêiner ou viola as regras de nomenclatura de contêiner de Olá, você poderá receber um erro 400 (solicitação incorreta).</span><span class="sxs-lookup"><span data-stu-id="6ee86-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

