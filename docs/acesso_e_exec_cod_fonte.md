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

##Comandos
Para rodar o projeto, execute o módulo ‘run_script.py’. Este módulo vai indicar 4 opções, uma para executar a extração dos arquivos .pdm do PowerDesigner para o diretório que será usado pelo código. A segunda para a criar o arquivo .csv e a execução do custom_lineage. A terceira vai criar os arquivos .json e a execução do custom_attribute e o quarto para a execução do código completo. As opções serão selecionadas por números de 1 a 4.