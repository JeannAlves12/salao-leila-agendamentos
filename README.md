# Cabeleleila Leila — Sistema de Agendamentos

🇬🇧 **Summary:** Django web app for a beauty salon: clients book multiple services online, and the owner manages everything in a dashboard. Includes a 48h change-lock rule, same-week booking suggestions and unit tests. Built as a technical challenge for a selection process.

🇧🇷 Sistema web em Django desenvolvido como **desafio técnico de um processo seletivo**. Permite que clientes agendem serviços online, vejam o histórico e alterem agendamentos, e dá à dona do salão um painel gerencial exclusivo.

## Funcionalidades

- **Agendamento de múltiplos serviços** na mesma solicitação
- **Regra de alteração (48h):** o cliente só cancela ou edita pelo sistema com mais de 48h de antecedência; abaixo disso, o sistema bloqueia e orienta a ligar para o salão
- **Sugestão de data:** se o cliente já tem agendamento na mesma semana, o sistema sugere concentrar os serviços no mesmo dia
- **Painel gerencial:** a conta "Staff" (dona) pode alterar status, confirmar agendamentos, ignorar a regra das 48h e ver métricas
- **Testes unitários** para as regras de negócio (validação de data e sugestão de agendamento)

## Tecnologias

| Camada | Tecnologia |
|---|---|
| Back-end | Python, Django |
| Banco de dados | SQLite3 (padrão do Django, facilita rodar localmente) |
| Front-end | HTML5, CSS3, Django Template Engine |
| Testes | `unittest` (nativo do Django) |
| Padronização | Flake8 (PEP 8) |

## Como rodar

```bash
git clone https://github.com/JeannAlves12/salao-leila-agendamentos
cd salao-leila-agendamentos

# ambiente virtual
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # Linux/Mac

pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser   # cria a conta da dona (acesso ao painel gerencial)
python manage.py runserver
```

Acesse: http://127.0.0.1:8000/

Para rodar os testes: `python manage.py test`

## Estrutura

```
salao-leila-agendamentos/
├── appointments/   # app principal (views, models, services.py, testes)
│   └── cbv/        # estudo de Class-Based Views (exploração futura)
├── setup/          # configurações do projeto Django
└── evidencias/     # prints das telas pedidos para avaliação
```

## Decisões de arquitetura

- **MVT do Django:** foquei no ecossistema onde me sinto mais confiante, para entregar dentro do prazo.
- **Regras de negócio isoladas em `services.py`:** a trava de 48h e a sugestão de data ficam fora de Views e Models, o que evita "fat views/models" e facilita testar.
- **Views modulares:** `client_views.py`, `owner_views.py`, `auth_views.py` etc., em vez de um único `views.py` gigante.
- **FBVs em vez de CBVs:** para deixar o fluxo de dados explícito e legível. Pesquisei CBVs por curiosidade, daí a pasta `cbv`.
- **Uso de IA:** como tenho mais domínio do back-end, usei IA como apoio na estruturação/estilização do HTML (onde tenho menos prática) e em erros pontuais. A lógica de negócio é minha.
