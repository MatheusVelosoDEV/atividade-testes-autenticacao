# Testes Caixa Cinza — Autenticação Supabase

> Trabalho individual. Os resultados abaixo foram registrados após a execução dos testes.

## Introdução
Este repositório documenta testes funcionais caixa cinza da autenticação por e-mail e senha da API Supabase Auth, executados pelo Postman Desktop.

## Objetivo da Atividade
Configurar um projeto Supabase, enviar requisições HTTP conhecendo endpoint, headers e body, validar respostas de autenticação e registrar os resultados observados.

## Configuração do Supabase
- Projeto: `atividade-testes-autenticacao`
- Referência do projeto: `qtbvyohakedjbnrreyd`
- URL: `https://qtbvyohakedjbnrreyd.supabase.co`
- Tipo de autenticação: e-mail e senha.
- Usuário de teste: usuário de teste criado no Supabase; e-mail omitido para preservar os dados da conta.
- Criação/configuração: projeto Supabase criado para a atividade e autenticação por e-mail e senha habilitada. As capturas da visão geral e do provedor de e-mail estão em `prints/`.
- Chave de API: usar a chave pública `publishable` (`sb_publishable_...`) ou a legada `anon`. Não inserir o valor no README.

## Configuração do Postman
Foi utilizado o Postman Desktop. Workspace: `matheus-saraiva-veloso's Workspace`. Environment: `Supabase - Testes`.

Variáveis do Environment: `base_url` = URL do projeto; `api_key` = chave pública; `email` = e-mail do usuário de teste; `password` = senha de teste. O Environment usado nos testes está em `postman/supabase-local.postman_environment.json`.

Importe `postman/supabase-auth.postman_collection.json` e `postman/supabase-local.postman_environment.json` no Postman Desktop. O Environment contém as variáveis usadas para executar os cenários. A coleção contém os cinco cenários exigidos.

## Configuração das Requisições
- Método: `POST`
- Endpoint: `/auth/v1/token?grant_type=password`
- URL completa: `{{base_url}}/auth/v1/token?grant_type=password`
- Headers: `apikey: {{api_key}}`, `Authorization: Bearer {{api_key}}`, `Content-Type: application/json`
- Body (raw JSON):

```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

Finalidade: autenticar um usuário por e-mail e senha. Sucesso normalmente retorna HTTP 200 e dados da sessão, incluindo `access_token`; falhas retornam erro HTTP/JSON.

## Execução dos Testes
Execute cada item da coleção no Postman Desktop com o Environment selecionado. Copie para a tabela somente o status, a mensagem resumida e a observação real. Redija ou oculte tokens e credenciais nos prints.

| Cenário | Entrada utilizada | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|
| Login válido | Usuário correto | HTTP 200 e access token | HTTP 200; sessão retornada com token (omitido) | OK |
| Senha incorreta | E-mail de teste e senha incorreta | Erro de autenticação | HTTP 400; `invalid_credentials` — `Invalid login credentials` | OK |
| Usuário inexistente | E-mail não cadastrado e senha de teste | Acesso negado | HTTP 400; `invalid_credentials` — `Invalid login credentials` | OK |
| Campos vazios | E-mail e senha vazios | Erro de validação | HTTP 400; `validation_failed` — `missing email or phone` | OK |
| Credenciais inválidas | E-mail em formato inválido e senha inválida | Mensagem de erro | HTTP 400; `invalid_credentials` — `Invalid login credentials` | OK |

## Registro dos Testes
Os cenários estão organizados em `planilha/registro-testes-excel.csv`, com ID, entrada, esperado, obtido, status e observações. O registro permite comparar comportamento esperado e real e identificar falhas. Falhas encontradas: inicialmente houve erro de resolução da URL e depois erro 401 por chave ausente ou inválida; após corrigir a configuração, o login funcionou. O arquivo usa CSV delimitado por ponto e vírgula para abrir em Excel configurado em português.

## Resultados Obtidos
Login válido: HTTP 200 e sessão com access token. Senha incorreta, usuário inexistente e credenciais inválidas: HTTP 400 com `invalid_credentials` e mensagem `Invalid login credentials`. Campos vazios: HTTP 400 com `validation_failed` e mensagem `missing email or phone`. As respostas negativas bloquearam o acesso conforme esperado.

## Conclusão
Os cinco cenários foram executados. A autenticação funcionou com as credenciais válidas e rejeitou as inválidas. A validação de campos vazios retornou `validation_failed`; as demais entradas inválidas retornaram `invalid_credentials`. Uma dificuldade encontrada foi corrigir a chave/URL da API antes de obter respostas válidas. Como melhoria, seria possível adicionar assertions automatizadas no Postman para status e campos JSON. Os testes caixa cinza ajudam a avaliar uma API conhecendo seus endpoints, headers e formatos sem acesso ao código interno.

## Evidências
As capturas reais da visão geral do Supabase, configuração do provedor de e-mail, lista de usuários, requisições do Postman e planilha estão abaixo. O token foi ocultado no print do login válido. As imagens de origem e cópias também foram mantidas na pasta `prints/`.

- [Visão geral do projeto Supabase](prints/supabase-projeto.png)
- [Provedor de e-mail habilitado](prints/supabase-auth-email.jpeg)
- [Lista de usuários no Supabase](prints/usuariosupbase)
- [Planilha preenchida](planilha/planilha-preenchida.jpeg)

- [Login válido — HTTP 200](prints/WhatsApp%20Image%202026-11-07%20at%2014.20.58.jpeg)
- [Senha incorreta](prints/WhatsApp%20Image%202026-11-07%20at%2014.27.21.jpeg)
- [Usuário inexistente](prints/WhatsApp%20Image%202026-11-07%20at%2014.27.44.jpeg)
- [Campos vazios](prints/WhatsApp%20Image%202026-11-07%20at%2014.28.29.jpeg)
- [Credenciais inválidas](prints/WhatsApp%20Image%202026-11-07%20at%2014.28.45.jpeg)






