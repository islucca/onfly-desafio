# Declaração de Uso de Inteligência Artificial

## Ferramenta e Modelo Utilizados
* **Ferramenta / Ambiente:** Antigravity
* **Modelo:** *(Claude Sonnet 4.6 (Thinking))*

---

## Divisão de Responsabilidades

### O que a IA fez
* Auxiliou na identificação e no diagnóstico dos erros e falhas, analisando os trechos de código em `src/onfly_report/`.

### O que eu fiz
* Configurei o ambiente local, instalei as dependências e executei a suíte de testes automatizados (`pytest`) para mapear os defeitos iniciais do código.
* Analisei os módulos em `src/onfly_report/`, implementei as correções necessárias no código-fonte e validei o comportamento até que todos os testes passassem.
* Executei o CLI tanto para a base principal (`reservas_hoteis.csv`) quanto para a amostra de validação (`exemplo-validacao.csv`), conferindo manualmente a exatidão dos relatórios JSON gerados.
* Estruturei e revisei toda a documentação final e os arquivos da pasta `entrega/` antes da publicação no repositório.