# Azure Cognitive Search

Organização e pesquisa de documentos por meio de ingestão de dados e indexação.

## Criar recursos

### Azure AI Search

Aceda ao [portal Azure](https://portal.azure.com) e faça login com as suas credênciais.

Selecione a o menu **Create a resource** e procure por **Azure AI Search**.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img1.png)

É necessário preencher a seguinte informação:

	. Subscription
	. Resource Group
	. Service name
	. Location 
	. Pricing tier: Basic

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img2.png)

Selecione **Review + create** e depois validado selecione **Create** para confirmar. Aguarde até que conclua a criação.


### Azure AI Sercices

Volte para a pagine inicial do portal e selecione o menu **Create a resource** e procure por **Azure AI Services**.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img1.JPG)

É necessário preencher a seguinte informação:

	. Subscription
	. Resource group
	. Region 
	. Name 
	. Pricing tier: Standard S0

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img2.JPG)  

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img3.JPG)  

Selecione **Review + create** e depois validado selecione **Create** para confirmar. Aguarde até que conclua a criação.


### Criar uma conta de armazenamento

Volte para a pagine inicial do portal e selecione o menu **All services** e então o item **Storage account**.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img3.png)  

Selecione a opção **Create**.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img4.png)  

É necessário preencher a seguinte informação:

	. Subscription
	. Resource group
	. Storage account name 
	. Region 
	. Performance: Standard
	. Redundancy

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img5.png)  

Selecione **Review + create** e depois validado selecione **Create** para confirmar. Aguarde até que conclua a criação.

No final aceda ao recurso, selecione a opção **Configuration** do menu **Settings**

Selecione o valor **Enable** para a opção **Allow storage anonymous access** e clique em **Save**.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img6.png)  

## Carregar documentos para Azure Storage

No menu selecione a opção **Container** do menu **Data storage**. 

Clique em **Container** para criar um novo "Container".

Preencha a seguinte informação:

	. Name
	. Anonymous access level: Container (anonymous read access for containers and blobs)

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img7.png)  

Clique em **Create** e aguarde até que conclua a criação.

De seguida faça download dos [documentos](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/reviews.zip) e aceda ao container criado para fazer o upload dos documentos.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img8.png)  

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img9.png)  


Depois de armazenar os documentos, pode utilizar o Azure AI Search para extrair insights dos mesmos. 


## Indexar os documentos

No portal Azure, navegue até ao recurso Azure AI Search criado e selecione **Import Data**

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img10.png)  

No separador **Connect to your data** preencha a seguinte informação:

	. Data Source: Azure Blob Storage
	. Data source name
	. Data to extract: Content and metadata
	. Parsing mode: Default
	. Connection string
	. Managed identity authentication: None
	. Container name
	. Blob folder
	. Description

No separador **Add cognitive skills (Optional)**, na secção **Attach AI Services** selecione o Azure AI Service criado anteriormente.

No separador **Add enrichments** preencha:

	. Skillset name
	. Enable OCR and merge all text into merged_content field: Check
	. Source data field: merged_content.
	. Enrichment granularity level: Pages (5000 character chunks).
	. Incremental enrichment: Disable
	. Cognitive Skill: Enable
	. Extract location names: Enable
	. Extract key phrases: Enable
	. Detect sentiment: Enable
	. Generate tags from images: Enable
	. Generate captions from images: Enable

No separador **Save enrichments to a knowledge store** faça check às seguintes opções:

	. Image projections
	. Documents
	. Pages
	. Key phrases
	. Entities
	. Image details
	. Image references
	. Document	

De seguida clique em **Next: Customize target index**. Preencha os campos:

	. Index name: coffee-index
	. Key: metadata_storage_path
	. Suggester name: blank 

Na tabela de indices faça check na coluna **filterable** para todos os campos já selecionados por defeito.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img11.JPG)  

Clique em **Create an indexer**. Altere o nome do índice e selecione **Once** para a opção Schedule.  para "Uma vez". Clique em **Submit**.

### Consultar o índice

Utilize o **Search explore** para escrever e testar consultas.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img12.png)  

Copie o texto o seguinte texto, no menu **View** selecione a opção **Json view** e coloque-o lá
{
 "search": "locations:'Chicago'",
 "count": true
}

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img13.JPG)  

Clique no botão **Search**. A consulta ira pesquisar em todos os documentos no índice e filtra pelas avaliações com localização em Chicago.

![](https://github.com/vicalmeida/MLearnAI900Lab4/blob/main/images/img14.png)  
