# **Projeto EDC On-premisse**

Toda a informação de cada modelo exportado do Powerdesigner é armazenada em arquivo com extensão .PDM (formato XML):

1. Um participante deste MVP fornecerá o arquivo PDM
    1. Acessará o acesso ao PowerDesigner e selecionará um modelo na versão desejada
    2. Realizar o checkout deste modelo. Esta ação envolve a indicação onde o arquivo .PDM será exportado/salvo localmente
    3. Entregar o arquivo ao consultor que realizará a construção do automatizador

2. O desenvolvedor do automatizador configurou o script para:
    1. O módulo ‘read_pdm’ localizado no pacote ‘custom_lineage.read’ irá ler o arquivo .PDM
    2. Interpretar onde estão os metadados físicos e lógicos
        - Nome técnico de schemas
        - Nome funcional de schema
        - Comments de schema
        - Nome técnico de tabelas
        - Nome funcional de tabelas
        - Comments de tabelas
        - Nome técnico de colunas
        - Nome funcional de colunas
        - Comments de colunas
    3. Interpretar onde estão os mapeamentos de origem -> destino a partir de análises, object ids ou outro, caso necessário
        - Map. tabelas (destino)
        - Map. tabelas (origem)
        - Map. colunas (destino)
        - Map colunas (origem)
        - Associação entre source -> target
    4. O módulo ‘read_pdm’ irá separar na pasta ‘json_files’ localizado em ‘files.files’ (em memória ou outro meio) o conteúdo que será enviado ao EDC
    5. O módulo ‘to_csv’ localizado no pacote ‘custom_attribute.read”  irá tratar o que for necessário para enriquecer as informações de mapeamento (mandatório) e o módulo ‘request_tt_attributes’ localizado no pacote ‘custom_lineage’ as descrições (desejável) no EDC
    6. Para enviar as informações tratadas para o EDC via API, no caso das lineages será utilizado o módulo ‘request_lineage’ localizado no pacote ‘custom_lineage’ e para as descrições o próprio módulo ‘request_tt_attribute’ irá realizar essa ação.
3. A execução do script é realizada a partir da VDI do desenvolvedor e outros que quiserem executar
    1. Necessário atender os requisitos de hardware/software
    2. Por esta fase focar em um item específico como POC, o script será preparado inicialmente para atender exclusivamente o modelo indicado pela B3. Durante a construção, este poderá ou não ser parametrizado, a depender do esforço. Esta customização será automatizada para outros modelos na Fase 2.

Com isso, a premissa dessa próxima parte é a de buscarmos as informações a partir de arquivos .PDM contendo todos os modelos. A automatização envolvida aqui foca na extração automática do arquivo .PDM:

1. A B3 define um servidor Windows e opcionalmente o diretório na rede para estes arquivo processados estarem disponíveis
2. O desenvolvedor do automatizador configurou o script para:
    1. Acessar o EDC e listar todos os repositórios catalogados, para que posteriormente sejam exportados apenas seus respectivos modelos
    2. Acessar cada banco de dados e consultar na tabela SCHEMA_VERSION a versão do modelo que está produtizado
        - Para a Fase 2 consideramos diretamente a última versão disponível
    3. Acessar o PowerDesigner via OLE ou outro meio facilitador disponível no PowerDesigner, para:
        - Consultar e listar o nome e localização de todos os modelos que estão com os respectivos metadados catalogados no EDC
        - Exportar todos os modelos listados, na versão produtizada, conforme realizado na Fase 1
    4. Gerar logs de execução em diferentes níveis, se possível
    5. Criar estrutura de diretórios contendo os arquivos envolvidos nas últimas execuções
    6. Removendo arquivos processados há mais de 90 dias
    7. Definição de arquivo de parametrização, com informações de acesso ao PowerDesigner ou EDC, minimizando o acesso à codificação
