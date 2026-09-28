# Lista 01 – Exercícios com Redis (Práticas de Laboratório)

Resolução da **Lista 01 de Redis** (Prof. Ricardo Roberto de Lima): 20 exercícios de comandos no `redis-cli`, mais um script Python que valida automaticamente cada exercício.

## Conteúdo

| Bloco | Tema | Exercícios |
|---|---|---|
| 1 | Strings | 01 a 04 |
| 2 | Hashes | 05 a 07 |
| 3 | Lists | 08 a 10 |
| 4 | Sets | 11 a 13 |
| 5 | Sorted Sets | 14 a 16 |
| 6 | Pub/Sub, Transações e Administração | 17 a 20 |

## Estrutura

```
.
├── .env.example                  # modelo das variáveis de ambiente
├── .gitignore
├── docker-compose.yml            # sobe o Redis local
├── requirements.txt
├── README.md
├── docs/
│   ├── Lista_01.docx             # enunciado da lista
│   └── Install_Redis_on_Windows.docx
├── prints/                       # evidências (capturas de tela)
└── scripts/
    └── validar_comandos_redis.py # validador dos 20 exercícios
```

## 1. Subindo o Redis

Opção recomendada (Docker):

```bash
docker compose up -d
docker exec -it redis redis-cli
```

No prompt `127.0.0.1:6379>`, o comando `ping` deve responder `PONG`.

Alternativas descritas em `docs/Install_Redis_on_Windows.docx`: WSL2 (Ubuntu) ou Memurai.

## 2. Fazendo os exercícios manualmente

Dentro do `redis-cli`, execute os comandos de `docs/Lista_01.docx` na ordem. Observações:

- **Ex 03:** rode o `TTL` logo após o `SETEX` (a chave expira em 30 s).
- **Ex 17 (Pub/Sub):** use dois terminais. No primeiro, `SUBSCRIBE notificacoes`; no segundo, `PUBLISH notificacoes "Novo relatorio disponivel"`.
- **Ex 18 (transação):** crie antes as contas com `SET conta:A 100` e `SET conta:B 50`.
- **Ex 19:** depende da chave `sistema:nome` criada no Ex 01.
- **Ex 20:** `FLUSHDB` por último, pois apaga o banco atual.

## 3. Validação automática com Python

Crie o ambiente virtual e instale as dependências:

```bash
python -m venv venv
source venv/Scripts/activate      # Windows (Git Bash)
# source venv/bin/activate        # Linux/Mac
pip install -r requirements.txt
cp .env.example .env
```

Execute o validador:

```bash
python scripts/validar_comandos_redis.py
```

## 4. Evidências (`prints/`)

Sugestão de nomes para os arquivos:

| Arquivo | Conteúdo |
|---|---|
| `01_docker_ping.png` | `docker ps` e `PONG` |
| `02_bloco1_strings.png` | Exercícios 01 a 04 |
| `03_bloco2_hashes.png` | Exercícios 05 a 07 |
| `04_bloco3_lists.png` | Exercícios 08 a 10 |
| `05_bloco4_sets.png` | Exercícios 11 a 13 |
| `06_bloco5_sorted_sets.png` | Exercícios 14 a 16 |
| `07_ex17_pubsub.png` | Dois terminais lado a lado |
| `08_ex18_transacao.png` | `MULTI` / `EXEC` |
| `09_ex19_ex20.png` | `RENAME`/`DEL`, `INFO memory`, `FLUSHDB` |
| `10_script_validacao.png` | Saída completa do script Python |

## 5. Encerrando

```bash
docker compose down
deactivate
```
