# **Projeto EDC On-premisse**



## Preparação e envio para o EDC
Toda informação de mapeamento extraída do PowerDesigner foi documentada no EDC, respeitando os critérios apresentados no plano de entrega:
1. Geração de arquivos CSV contendo os mapeamentos - as origens e destinos, sendo um arquivo CSV por modelo
2. Criação de arquivo ZIP contendo todos os arquivos CSV gerados acima
3. Criação/Atualização de resource tipo “Custom Lineage” via API ou portal web
4. Upload do arquivo ZIP para o resource via API ou portal web
5. Execução resource via API

###Endpoints das APIS do EDC utilizados
Todo o processo foi realizado programaticamente, utilizando os métodos e endpoints abaixo:

- Script para a criação dos CSV
    * GET:		 /2/catalog/data/search
- Criação do Resource
    * POST:		/1/catalog/resources
- Upload dos arquivos CSV
    * POST:		/1/catalog/resources/{Resource-Name}/files
- Execução do Resource
    * POST:		/2/catalog/resources/jobs/loads
- Checagem de connections assignment
    * GET:		/1/catalog/resources/connectionassignments
- Correção de connections assignment
    * PUT:		/1/catalog/resources/connectionassignments