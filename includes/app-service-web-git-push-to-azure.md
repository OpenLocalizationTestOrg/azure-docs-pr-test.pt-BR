## <a name="push-to-azure-from-git"></a><span data-ttu-id="30209-101">Enviar do Git para o Azure</span><span class="sxs-lookup"><span data-stu-id="30209-101">Push to Azure from Git</span></span>

<span data-ttu-id="30209-102">Adicione um Azure remoto ao seu repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="30209-102">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="30209-103">Envie por push para o Azure remoto para implantar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30209-103">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="30209-104">Você recebe uma solicitação pela senha criada anteriormente ao criar o usuário de implantação.</span><span class="sxs-lookup"><span data-stu-id="30209-104">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="30209-105">Verifique se você inseriu a senha que você criou em [Configurar um usuário de implantação](#configure-a-deployment-user), não a senha usada para fazer logon no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="30209-105">Make sure that you enter the password you created in [Configure a deployment user](#configure-a-deployment-user), not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="30209-106">O comando anterior exibe informações semelhantes ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="30209-106">The preceding command displays information similar to the following example:</span></span>
