# Azure Red Shirt Dev Tour Amsterdam 24 May 2017

[![Red Shirt](red-shirt.jpg)](https://twitter.com/carophillips1/status/867287380688064513)

1100 Azure developers turned up for a free talk by Scott Guthrie.
He demonstrated a few new features of Azure that people might not be aware of,
some of which may be still in preview.

## M-series VM

The
[M-series](https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-windows-sizes)
VM is based on 
[Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server)
which allows virtualization inside a VM.
It can have up to 120 cores and 3.5TB of RAM.
He demonstrated a VM inside a VM inside a VM...

I was thinking that this might be useful for running our own Docker containers since the
[Azure Container Service](https://azure.microsoft.com/en-us/services/container-service/)
doesn't support Windows containers.

## Cloud shell in portal

Maybe you didn't notice the shell icon in the portal.

![Azure CLI](azure-cli.png)

This starts a VM with a bash command where you can run Azure CLI commands.
It even lets you run Vim.

## Application Insights exception debugging

You can click down on an exception in App Insights and there's a link that lets you open a debug session in Visual Studio.

## Deploy from git

When you configure an App Service to deploy from git
(which is already quite cool - `git push azure`)
then you can see the history in the portal and choose to redeploy any previous version.

## Staging slots

- it's possible to lock down the staging URL so that only authorized people can access it
- can use any URL for the staging slot, eg a GUID
- can use a custom domain for the staging slot
- can ramp up the swap, rather than swapping all at once. This can also be useful for A/B testing

## CI/CD

There's a tab in App Services for Continuous Delivery.
If CD is not configured then this can start a wizard to set up a release pipeline.
If it is configured then it shows the history of deployments.

![Continuous Delivery](CD.png)

