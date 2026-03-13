# Constituição do Projeto - Diretrizes de Desenvolvimento

## 1. Paradigma de Orientação a Objetos (OO)

### Princípios Obrigatórios
- **Encapsulamento**: Propriedades privadas/protegidas, métodos públicos bem definidos
- **Herança**: Uso hierárquico quando apropriado, preferindo composição quando possível
- **Polimorfismo**: Interfaces e classes abstratas para contatos polimórficos
- **Coesão Alta**: Classes com responsabilidades bem definidas e coesas

### Regras de Design
- Uma classe = Uma responsabilidade principal
- Evitar god objects (classes com muitas responsabilidades)
- Preferir composição sobre herança quando viável
- Usar design patterns reconhecidos (Factory, Strategy, Observer, etc)

---

## 2. Princípios SOLID

### S - Single Responsibility Principle
- Cada classe tem APENAS UMA razão para mudar
- Separação clara de responsabilidades
- Exemplo: Uma classe não valida E persiste ao mesmo tempo

### O - Open/Closed Principle
- Aberto para extensão, fechado para modificação
- Use abstrações (interfaces, classes abstratas)
- Evite modificar classes existentes; crie novas extensões

### L - Liskov Substitution Principle
- Subclasses são substituíveis por suas superclasses
- Contratos respeitados em toda hierarquia
- Não quebrar comportamentos esperados em substituições

### I - Interface Segregation Principle
- Clientes não dependem de interfaces que não usam
- Interfaces pequenas e específicas, não monolíticas
- Múltiplas interfaces específicas > Uma interface grande

### D - Dependency Inversion Principle
- Dependa de abstrações, não de concretos
- Classes de alto nível não dependem de baixo nível
- Use injeção de dependência obrigatoriamente

---

## 3. Object Calisthenics

### Regras Obrigatórias
1. **Um nível de indentação por método** - Lógica simples e legível
2. **Sem variável else** - Use guards e retorno antecipado
3. **Wrapping primitivos** - Tipos criados para conceitos do domínio
4. **Collections como objetos** - Não use arrays/listas diretamente
5. **Um ponto por linha** - Evite encadeamento (ex: `obj.method1().method2()`)
6. **Sem abreviações** - Nomes descritivos e completos
7. **Mantém objetos pequenos** - 10-20 linhas máximo por classe
8. **Sem classes com mais de 2 variáveis de instância** - Quando necessário, refatore
9. **Sem objetos getters/setters públicos** - Use métodos com intenção de negócio
10. **Sem comentários** - Código auto-explicativo é ideal

### Benefícios Esperados
- Código mais testável
- Redução de acoplamento
- Melhor legibilidade
- Facilidade de manutenção

---

## 4. TypeScript - Tipagem Estrita Obrigatória

### Configuração tsconfig.json
```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictBindCallApply": true,
    "strictPropertyInitialization": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "target": "ES2020",
    "module": "commonjs",
    "declaration": true,
    "sourceMap": true
  }
}
```

### Regras de Tipagem
- **Sem `any`**: Exceto em casos excepcionais documentados
- **Tipos explícitos**: Em parâmetros, retornos e variáveis
- **Discriminated Unions**: Para tipos complexos
- **Generics**: Para reutilização type-safe
- **Readonly**: Para imutabilidade quando apropriado
- **Never vs void**: Distinção clara entre não retorno e retorno void

### Padrões Recomendados
```typescript
// ✅ BOM
function processar(dados: Dados): Resultado {
  // ...
}

// ❌ ERRADO
function processar(dados: any): any {
  // ...
}
```

---

## 5. Test Driven Development (TDD)

### Ciclo Obrigatório
1. **Red**: Escrever teste que falha
2. **Green**: Implementar código mínimo para passar
3. **Refactor**: Melhorar sem quebrar testes

### Cobertura de Testes
- Mínimo: **100% cobertura de código**
- Ideal: **100% cobertura**
- Todos os comportamentos críticos precisam de testes
- Um teste por comportamento esperado

### Estrutura de Testes (AAA - Arrange, Act, Assert)
```typescript
describe('ProcessadorDados', () => {
  it('deve transformar dados válidos corretamente', () => {
    // Arrange
    const entrada: Dados = { ... };
    const processador = new ProcessadorDados();
    
    // Act
    const resultado = processador.processar(entrada);
    
    // Assert
    expect(resultado).toEqual(esperado);
  });
});
```

### Tipos de Testes
- **Unitários**: Classe/método isolado, mocked dependencies
- **Integração**: Múltiplos componentes trabalhando juntos
- **E2E**: Fluxos completos do sistema

### Mocking e Test Doubles
- Use mocks para dependências externas
- Use stubs para simular comportamentos
- Use fakes apenas quando apropriado
- Mantenha testes isolados e determinísticos

---

## 6. Clareza e Manutenibilidade

### Nomenclatura
- **Classes**: PascalCase com nomes substantivos (User, ProcessadorDados, ValidadorCPF)
- **Métodos/Funções**: camelCase com verbos (processar, validar, transformar)
- **Constantes**: SCREAMING_SNAKE_CASE
- **Privadas**: Prefixo # (TypeScript) ou _variável

### Estrutura de Diretórios
```
src/
├── domain/          # Entidades e lógica de negócio
├── application/     # Casos de uso
├── infrastructure/  # Integrações e persistência
├── presentation/    # Controllers, Views
└── shared/          # Utilitários e tipos comuns
```

### Documentação
- JSDoc em interfaces públicas
- Comentários explicam "por quê", não "o quê"
- README atualizado com instruções de setup
- CHANGELOG mantido

### Code Review
- Toda mudança passa por review
- Checklist: SOLID, OO, Calisthenics, Tipagem, Testes
- Refutação polida e construtiva

---

## 7. Verificação de Conformidade

### Ferramentas Obrigatórias
- **ESLint**: Enforce regras de código
- **TypeScript Strict**: Validação de tipo
- **Jest/Vitest**: Testes automatizados
- **SonarQube/Codacy**: Análise de qualidade
- **Prettier**: Formatação consistente

### CI/CD Gates
- Testes DEVEM passar (100%)
- Cobertura MÍNIMA 100%
- Sem erros de linting
- TypeScript strict compilation
- Build projeto sem warnings

### Checklist de Commit
- [ ] Testes escritos ANTES do código
- [ ] Todos os testes passando
- [ ] Cobertura mantida ou melhorada
- [ ] Sem violações de SOLID
- [ ] Sem Object Calisthenics violations
- [ ] Código tipado explicitamente
- [ ] Nomes descritivos
- [ ] Sem code duplication

---

## 8. Exceções e Desvios

**Não há exceções aos princípios acima**, exceto:
- Casos documentados e aprovados em PR
- Débito técnico registrado em issue
- Prazo limite para correção definido

**Toda exceção requer:**
1. Documentação clara do porquê
2. Aprovação de code review
3. Issue criada para correção futura
4. Nenhum prazo indefinido

---

## 9. Versões de Referência

- **Node.js**: v18.0.0+
- **TypeScript**: v5.0.0+
- **Jest**: v29.0.0+
- **ESLint**: v8.0.0+

---

## 10. Contato e Evolução

Estas diretrizes são **vivas** e evoluem com o projeto:
- Sugestões via discussion em PRs
- Revisões trimestrais
- Adaptações conforme necessidade do projeto
- Todos podem propor melhorias

**Última atualização**: 13 de março de 2026
