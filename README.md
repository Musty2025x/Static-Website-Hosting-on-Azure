# Salone - Free Bootstrap 5 Business Template 

- [Demo](https://themewagon.github.io/Electro-Bootstrap/)

#### Download

- [Download from ThemeWagon](https://themewagon.com/themes/electro-bootstrap/)

## Getting Started

Clone Repository

```
https://github.com/themewagon/Electro-Bootstrap.git
```

## Step 1: Create Storage Account and Container in Azure
- Create a storage account in Azure.
- resource group: mustydev
- storage account name: mustystorage
- location: (us)east us
- Redundancy: locally-redundant storage (LRS)

## screenshot of the storage account in Azure portal
> ![alt text](asset/storage_acccount_ovierview.png)


## Step 2: Enable Static Website Hosting in Azure Storage
- Go to the storage account you created in Azure portal.
- Data management - Static website
- Enable static website hosting: Yes
- Index document name: index.html
- Error document path: 404.html
- Save the primary endpoint URL for later use. e.g https://mustystorage.z13.web.core.windows.net/

## screenshot of the static website hosting configuration in Azure portal
> ![alt text](asset/static_website_hosting_configuration.png)

## Step 3: Upload Website Files
- Go to the storage account you created in Azure portal.
- Data management - Containers
- Click on the container named '$web' (this is the default container for static website hosting)
- Upload all the files from the cloned repository (index.html, 404.html, css folder, js folder, asset folder) to the '$web' container.


## Screenshot of the uploaded files in Azure portal
> ![alt text](asset/uploaded_files.png)


## Step 4: Access Your Website
- After uploading the files, you can access your website using the primary endpoint URL you saved earlier. For example, if your primary endpoint URL is https://mustystorage.z13.web.core.windows.net/, you can open this URL in your web browser to see your website live.


## Screenshot of the live website

> ![alt text](asset/live_website.png)

## Step 5: Create Azure Front Door
- Go to Azure portal and create a new Azure 'Front Door' resource.
- Resource group: mustydev
- Name: mustyfrontdoor
- Endpoint name: mustyfrontdoor
- origin type: Storage (static website)
- origin host: Select from list - mustystorage.z13.web.core.windows.net
- Save and create the Front Door resource.

## Srceenshot of the Azure Front Door configuration in Azure portal
> ![alt text](asset/azure_front_door_configuration.png)
> ![alt text](asset/front_door_deployment_complete.png)

Review Created Route
> ![alt text](asset/route_endpoint.png)

Test Front Door
> ![alt text](asset/frontdoor_url.png)

wait 20 - 40 minutes for the Front Door deployment to complete and then access the Front Door URL (e.g. https://mustyfrontdoor.azurefd.net/) to see your website live through Azure Front Door.

> ![alt text](asset/frontdoor_live.png)

## step 6: Add Custom Domain in Front Door
- Go to the Front Door resource you created in Azure portal.
- Custom domains - Add custom domain
- Domain name: www.mustydevops.com.ng (or any custom domain you want to use
- Hostname: www.mustyfrontdoor.com
- Save the custom domain configuration.

## Screenshot of the custom domain configuration in Azure portal
> ![alt text](asset/custom_domain_configuration.png)

## step 7: Add a new DNS record

Click pending status to verify the custom domain ownership and then follow the instructions to add a CNAME record in your DNS settings.

- Go to your domain registrar (where you purchased your custom domain) and log in to your account.
- Find the DNS management section for your domain.
- Add a new DNS record with the following details:
- Host Name: _dnsauth
- Type: TXT
- Value: (the record value from the pending state ) e.g _ua1wvshon25z1rluwu4cj2g94z75j62
- Save the DNS record.      

## Screenshot of the DNS record configuration in domain registrar
> ![alt text](asset/dns_record_configuration.png)

## Validate Domain Back in Azure
- After adding the DNS record, go back to Azure portal and click on the pending status for the custom domain in Front Door.
- Azure will check for the DNS record you added and verify the ownership of the custom domain.
- Once the verification is successful, the status will change to 'Validated' and your custom domain will be active.

## Screenshot of the validated custom domain in Azure portal (Approved)
> ![alt text](asset/approved_validated_custom_domain.png)

## Front Door manager - Go to the Front Door resource in Azure portal.
- Front Door manager - Default routing rule - Edit
- update Route - Name - thick Enable route - click on the dropdown and select the custom domain you just validated (e.g. www.mustydevops.com.ng)
- Save the routing rule configuration.

## Screenshot of the route configuration in Azure portal
> ![alt text](asset/update_frontdoor_route.png)

## Step 8: DNS Configuration
- After updating the routing rule, you need to add a CNAME record in your DNS settings to point your custom domain to the Front Door endpoint.
- Go to your domain registrar (where you purchased your custom domain) and log in to your account.
- Find the DNS management section for your domain.
- Add a new DNS record with the following details:
- Host Name: www (or the subdomain you want to use)
- Type: CNAME
- Value: (the Front Door endpoint) e.g mustyfrontdoor.azurefd.net
- Save the DNS record.

## Screenshot of the DNS record configuration in domain registrar
> ![alt text](asset/dns_record_configuration_cname.png)

## Access Your Website with Custom Domain
- After updating the routing rule, you can access your website using your custom domain (e.g. www.mustydevops.com.ng) and it should load your website through Azure Front Door.

> ![alt text](asset/custom_domain_live.png)

## Destroy Resources
- After you are done testing, you can go to Azure portal and delete the resources you created (Storage Account, Front Door) to avoid any unnecessary costs.

![alt text](asset/destroy_resources.png)


## License

- Design and Code is Copyright &copy; [HTML Codex](https://htmlcodex.com/).
- Licensed under [MIT](https://opensource.org/licenses/MIT)
- Distributed by [ThemeWagon](https://themewagon.com)


