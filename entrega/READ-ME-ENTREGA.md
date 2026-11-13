# Entrega do Desafio Técnico — Onfly Report CLI

O problema foi abordado de forma sistemática a partir da execução da suíte de testes automatizados (`pytest -q`). Como os testes iniciais apontavam falhas em múltiplos módulos, utilizei a análise de código para rastrear os *tracebacks* até os serviços específicos em `src/onfly_report/`. Cada falha foi comparada com os requisitos de negócio da aplicação (como conversão correta de câmbio, contagem de diárias em virada de mês, filtragem restrita de status e ordenação de rankings), permitindo isolar e corrigir os quatro bugs independentes identificados no sistema.

---

## Defeitos Corrigidos e Causa Raiz

* **Defeito 1 — Operação de câmbio invertida (`services/currency_converter.py`):**
  * **Causa raiz:** O código realizava uma divisão do valor pela taxa de câmbio em vez de multiplicá-lo.
* **Defeito 2 — Falha no cálculo de noites na virada de mês (`services/stay_calculator.py`):**
  * **Causa raiz:** O cálculo utilizava apenas a diferença numérica dos dias do mês (`checkout.day - checkin.day`), gerando resultados incorretos ou negativos em estadias que cruzavam a virada do mês.
* **Defeito 3 — Tratamento incorreto de status `NO_SHOW` (`services/status_policy.py`):**
  * **Causa raiz:** A regra de validação filtrava apenas o status `CANCELLED`, permitindo incorretamente que reservas com status `NO_SHOW` fossem contabilizadas nos totais financeiros e de ocupação.
* **Defeito 4 — Ordenação invertida no ranking de hotéis (`services/report_builder.py`):**
  * **Causa raiz:** A função de ordenação (`sorted()`) organizava os hotéis em ordem crescente de valor, quando o requisito exigia o ranking do maior para o menor valor (decrescente).

---

## Como Validar

### Pré-requisitos e Ativação do Ambiente
No terminal (Windows PowerShell), ative o ambiente virtual e instale as dependências:

```powershell
.venv\Scripts\Activate.ps1
pip install -r requirements-dev.txt
```

### Execução dos Testes Automatizados
Rode a suíte de testes para certificar-se de que todos passaram:

```powershell
pytest -q
```

### Geração dos Relatórios via CLI
Execute o comando principal para gerar o relatório consolidado da base e da amostra de validação:

```powershell
$env:PYTHONPATH="src"

# Base principal
py -m onfly_report --input data/reservas_hoteis.csv --rates data/taxas_cambio.csv --output output/report.json

# Amostra de validação
py -m onfly_report --input data/exemplo-validacao.csv --rates data/taxas_cambio.csv --output output/exemplo.json
```

---

## Resultado do Pytest
Todos os testes automatizados da suíte foram executados com sucesso após as correções dos quatro bugs mapeados.
