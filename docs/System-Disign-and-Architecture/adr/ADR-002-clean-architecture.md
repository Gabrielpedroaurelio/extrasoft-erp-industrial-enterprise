ADR-002 - Clean Architecture em vez de MVC simples

DATA: 26-03-2026
STATUS: ACEITE

>>Contexto:

O ERP tem lógica de negócio complexa (cálculos salariais, transacções financeiras, integrações entre módulos). MVC simples mistura lógica de negócio com HTTP.


>>DECISÃO

Adoptar Clean Architecture: Domain → Application (Use Cases) → Infrastructure → Interfaces. A lógica de negócio não depende de Express nem de pg.


>>CONSEQUÊNCIAS

Mais código inicial (interfaces, mappers). Compensado pela testabilidade: Use Cases testados sem DB, e pela manutenibilidade a longo prazo.