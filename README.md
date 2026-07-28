# Scraping de Livros em PDF

Projeto desenvolvido em Python para coletar informações de livros clássicos disponíveis no site InfoLivros.

O script acessa a página de autores clássicos, visita a página de cada autor e coleta informações de até dois livros por autor, com limite máximo de 100 livros.

## Dados coletados

Para cada livro, o script coleta:

- Nome do autor;
- Título do livro;
- Descrição;
- Link para leitura ou download;
- URL da imagem de capa.

Os dados coletados são armazenados no arquivo `livros_autores.json`.

## Tecnologias utilizadas

- Python 3;
- Requests;
- Beautiful Soup 4;
- JSON;
- Expressões regulares.

## Estrutura do projeto

```text
projeto/
├── livros_autores.json
├── requirements.txt
├── scrapingtest.py
└── README.md
```

### Arquivos

- `scraping_books.py`: contém o código responsável pela raspagem dos livros;
- `requirements.txt`: contém as dependências necessárias para executar o projeto;
- `livros_autores.json`: contém os dados coletados;
- `README.md`: documentação do projeto.

## Instalação

Clone o repositório:

```bash
git clone URL_DO_REPOSITORIO
```

Entre na pasta do projeto:

```bash
cd NOME_DO_REPOSITORIO
```

Crie um ambiente virtual:

```bash
python -m venv venv
```

Ative o ambiente virtual.

### Windows

```bash
venv\Scripts\activate
```

### Linux ou macOS

```bash
source venv/bin/activate
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

## Dependências

O arquivo `requirements.txt` deve conter:

```txt
requests
beautifulsoup4
```

## Execução

Execute o script principal:

```bash
python scrapingtest.py
```

Em alguns sistemas, pode ser necessário utilizar:

```bash
python3 scrapingtest.py
```

Durante a execução, o programa mostra a quantidade de livros coletados:

```text
Coletando dados de https://www.infolivros.org/autores/classicos/...
Livros coletados: 1
Livros coletados: 2
Livros coletados: 3
```

Ao atingir o limite definido:

```text
Limite de 100 livros alcançado.
```

Depois da execução, o arquivo `livros_autores.json` será criado ou sobrescrito com os dados coletados.

## Formato do JSON

Exemplo da estrutura gerada:

```json
{
    "livros": [
        {
            "autor": "Guy de Maupassant",
            "titulo": "Bola de Sebo",
            "descricao": "Descrição do livro coletada na página.",
            "link_download": "https://exemplo.com/livro.pdf",
            "imagem_capa": "https://exemplo.com/capa.jpg"
        }
    ]
}
```

Quando o link de download ou a imagem não forem encontrados, o campo correspondente poderá possuir o valor `null`.

## Funcionamento

O processo de raspagem segue estas etapas:

1. Acessa a página de autores clássicos;
2. Localiza os autores disponíveis;
3. Acessa a página individual de cada autor;
4. Seleciona até dois livros por autor;
5. Extrai título, descrição, link e imagem;
6. Remove numerações dos nomes e títulos;
7. Corrige espaços presentes nas URLs;
8. Adiciona os dados ao resultado;
9. Interrompe a coleta ao atingir 100 livros;
10. Salva os dados no arquivo `livros_autores.json`.

## Principais funções

### `corrigir_nome(nome)`

Remove números seguidos de parênteses no começo do nome.

Exemplo:

```python
corrigir_nome("22) Guy de Maupassant")
```

Resultado:

```text
Guy de Maupassant
```

### `corrigir_link(link)`

Substitui espaços presentes na URL por `%20` e ajusta caracteres codificados.

### `pegar_imagem(livro_soup)`

Procura a imagem de capa do livro utilizando os atributos `data-src` ou `src`.

### `scraping_livros_autores()`

Executa todo o processo de raspagem e salva os resultados no arquivo JSON.

## Limitações

O funcionamento depende da estrutura HTML do site.

Caso classes como as seguintes sejam alteradas, o script poderá deixar de encontrar os dados:

```text
content_raiz
content_libro_autor
has-text-align-center
descripcion
btn-descargar
btn-leer
aligncenter
```

Também podem ocorrer falhas devido a:

- Indisponibilidade do site;
- Problemas de conexão;
- Alterações na estrutura das páginas;
- Remoção de links ou imagens;
- Bloqueios contra requisições automatizadas.

## Possíveis melhorias

- Adicionar tempo limite nas requisições;
- Configurar um `User-Agent`;
- Implementar tentativas automáticas após falhas;
- Adicionar pausas entre as requisições;
- Validar se o link encontrado realmente é um PDF;
- Evitar livros duplicados;
- Criar logs de execução;
- Permitir configurar o limite de livros;
- Exportar os dados para CSV ou banco de dados;
- Criar testes automatizados.

## Uso responsável

Este projeto foi desenvolvido para fins educacionais.

Antes de realizar raspagem de dados em qualquer site:

- Consulte os termos de uso;
- Verifique o arquivo `robots.txt`;
- Evite enviar muitas requisições em pouco tempo;
- Respeite direitos autorais e licenças;
- Não redistribua conteúdos protegidos sem autorização.

Este projeto não hospeda arquivos PDF. Ele apenas coleta informações e links presentes nas páginas acessadas.

## Autor

Desenvolvido por [João Felipe](https://github.com/joaofelipes).
