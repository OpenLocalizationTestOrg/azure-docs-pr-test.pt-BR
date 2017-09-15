
<span data-ttu-id="cf22d-101">O código para todas as funções em um determinado aplicativo de funções reside em uma pasta raiz que contém um arquivo de configuração de host e uma ou mais subpastas, cada qual contendo o código para uma função distinta, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf22d-101">The code for all of the functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain the code for a separate function, as in the following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="cf22d-102">O arquivo *host.json* contém uma configuração específica de tempo de execução e reside na pasta raiz do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="cf22d-102">The *host.json* file contains some runtime-specific configuration and sits in the root folder of the function app.</span></span> <span data-ttu-id="cf22d-103">Para obter informações sobre as configurações que estão disponíveis, confira [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) no wiki do repositório WebJobs.Script.</span><span class="sxs-lookup"><span data-stu-id="cf22d-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in the WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="cf22d-104">Cada função tem uma pasta que contém arquivos de código, a configuração function.json e outras dependências.</span><span class="sxs-lookup"><span data-stu-id="cf22d-104">Each function has a folder that contains one or more code files, the function.json configuration and other dependencies.</span></span>

