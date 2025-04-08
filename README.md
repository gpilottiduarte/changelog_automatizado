# Gerador de Changelog Automatizado

Este projeto consiste em um sistema automatizado para gerar changelogs a partir de issues do Jira, utilizando a API da OpenAI para criar descrições claras e padronizadas. A implementação está em um único arquivo unificado para facilitar o uso.

## Requisitos

Para instalar todas as dependências necessárias, execute:

## 

```
pip install jira pandas python-docx openai
```

## Credenciais

O script requer as seguintes credenciais que podem ser configuradas como variáveis de ambiente ou através do Google Colab:

- `jira_url` \- URL da instância do Jira  
- `api_token` \- Token de API do Jira  
- `email` \- Email para autenticação no Jira  
- `OPENAI_API_KEY` \- Chave de API da OpenAI

## Uso

### Básico

Para executar o processo completo:

```
python main.py --version 4.1
```

Isso irá:

1. Extrair issues do Jira para a versão especificada  
2. Gerar descrições de changelog usando OpenAI  
3. Criar um documento Word organizado com as entradas

### Opções

```
usage: main.py [-h] [--colab] [--version VERSION] [--jql JQL] [--extract-only] [--generate-only] [--document-only]

Gerador de Changelog Automatizado

optional arguments:
  -h, --help            show this help message and exit
  --colab               Usar Google Colab para credenciais
  --version VERSION, -v VERSION
                        Versão da release para o changelog
  --jql JQL             Consulta JQL personalizada
  --extract-only        Apenas extrair issues do Jira
  --generate-only       Apenas gerar descrições de changelog
  --document-only       Apenas criar documento
```

### Exemplos

#### Usar Google Colab para credenciais:

```
python main.py --colab
```

#### Especificar uma versão diferente:

```
python main.py --version 4.2
```

#### Usar uma consulta JQL personalizada:

```
python main.py --jql "project = PROJ AND fixVersion = v4.1 AND status = Done"
```

#### Executar apenas partes específicas do processo:

```
# Apenas extrair issues do Jira
python main.py --extract-only

# Apenas gerar descrições de changelog
python main.py --generate-only

# Apenas criar documento
python main.py --document-only
```

## Fluxo de Trabalho

1. O script extrai issues do Jira baseado em uma consulta JQL  
2. A API da OpenAI é usada para gerar descrições padronizadas para cada issue  
3. Um documento Word é criado, organizando as entries por tipo de issue e módulo

## Personalização

### Consulta JQL

A consulta JQL padrão pode ser substituída usando o argumento `--jql`:

```
python main.py --jql "project = MYPROJ AND fixVersion = v5.0 ORDER BY priority DESC"
```

### Prompt da OpenAI

O prompt enviado para a API da OpenAI pode ser personalizado modificando a função `gerar_changelog` no código.

### Formato do Documento

O formato do documento Word pode ser personalizado modificando a função `create_document` no código.

## Arquivos Gerados

O script gera os seguintes arquivos:

- `issues_para_changelog.csv` \- Issues extraídas do Jira  
- `changelog_para_revisao.csv` \- Issues com descrições de changelog geradas  
- `Changelog_Release_X.Y_AAAAMMDD.docx` \- Documento final

## Notas

- As chaves de API e credenciais sensíveis devem ser mantidas em segurança  
- Recomenda-se revisar as entradas de changelog geradas pela IA antes da publicação final  
- O script requer conexão com a internet para acessar as APIs do Jira e OpenAI

## Requirements

Pode usar como `requirements.txt`:

```
jira==3.5.2
pandas==2.1.0
python-docx==0.8.11
openai==1.3.0
python-dotenv==1.0.0
argparse==1.4.0
```

Assim, para instalar: `pip install -r requirements.txt`
