# **Projeto EDC On-premisse**

O script será desenvolvido em um ambiente de desenvolvimento integrado disponível na VDI da B3, no caso o VisualStudio. A linguagem utilizada será o Python na versão, sendo necessário a instalação das bibliotecas: Pandas, shutill, os, sys, now, json. (essa etapa pode exigir um certo nível de permissão). 

Os pacotes Python foram divididos em diretórios e subdiretórios.

O diretório ‘edc’ contém o subdiretório ‘models’ e os módulos ‘edc.py’ e ‘http_client.py’. Dentro do subdiretório ‘models’ ficarão os arquivos ‘resource_models.py’ e ‘execute_models.py’, ambos irão definir os parâmetros para a criação e execução, respectivamente, do resource de Custom Lineage. O módulo ‘edc.py’ irá criar as conexões entre as manipulações do EDC e os endpoints de acesso e autenticação, enquanto o “http_client.py” define os parâmetros de conectividade das funções de manipulação do edc e os métodos http GET, POST e PUT.

O diretório ‘custom_lineage’ contém o subdiretório ‘read’ e os módulos ‘main.py’, ‘request_lineage.py’ e ‘setup.py’. No subdiretório ‘read’ estão os módulos de extração de dados dos modelos importados do PowerDesigner, o módulo ‘read_pwd.py’ e ‘to_csv’. O módulo ‘read_pwd.py’ irá realizar a extração e conversão dos dados do modelo para um arquivo json. Este arquivo json será utilizado tanto para a execução do custom lineage como do custom attribute. O módulo ‘to_csv.py’ irá extrair o conteúdo do arquivo json gerado anteriormente para a execução do custom lineage e irá converte-lo para csv, que é o formato reconhecido pelo EDC para essa operação. O módulo ‘main.py’ irá iniciar esse processo de transformação e conversão dos dados, do modelo em pdm até o arquivo csv a ser carregado no EDC.  O módulo ‘request_lineage.py’ executa as funções de manipulação no EDC, , dentre elas listar os resources no EDC, criar um resource, listar as propriedades de um resource específico, alterar o valor de alguma propriedade de um resource .específico, realizar o upload de um arquivo para um resource específico, listar os arquivos presentes em um resource específico e por fim executar o resource. O módulo ‘setup.py’ inicia as transformações no EDC.

O diretório ‘custom_attribute’ contém os módulos ‘json_attribute.py’, ‘request_tt_attribute.py’ e ‘setup_attribute.py’. O primeiro irá extrair o conteúdo necessário para criar o arquivo json que será carregado no EDC para atualizar o valor de um atributo. O módulo ‘request_tt_attribute.py’ fará o request PUT para o EDC. O módulo ‘setup_attribute.py’ inicializa os scripts para atualização do custom attribute. 

Para atualizar o host do EDC procure pelo arquivo .env, lá estão localizadas as informações do host do EDC. 

Para atualizar o host do PowerDesigner procure pelo arquivo ‘connect_to_repository_b3.vbs’ localizado em ‘pwd_models’. Na linha 13 será possível encontrar essas informações.

Para atualizar o local onde serão salvos os arquivos json extraídos do modelo do PowerDesigner procure pelo parâmetro ‘json_directory’ em ‘custom_lineage.read.read_pdm.py’

Para atualizar o local onde serão salvos os arquivos csv que serão carregados para a custom lineage procure pelo parâmetro ‘csv_directory’ em ‘custom_lineage.read.to_csv.py’

Para atualizar o local onde serão salvos os arquivos json que serão carregados para a custom attribute procure pelo parâmetro ‘...’ em ‘custom_attribute.request_attribute.py’

O diretório ‘logs’ contém os arquivos ‘attribute.log’, ‘extract_pdm.log’ e ‘lineage.log’. O script vai escrever nesses arquivos as informações dos processos e os erros que ocorrerem.
