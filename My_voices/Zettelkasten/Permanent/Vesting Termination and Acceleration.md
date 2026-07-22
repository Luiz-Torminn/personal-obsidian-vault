---
id: 20260722-0915
type: permanent
tags: [vesting, contracts, risk-management]
up: "[[* Startups & Vesting MOC]]"
created: 2026-07-22
references:
  - "Transcription file: conhecimentos_vesting_1.txt"
  - "Faleiros Júnior, José Luiz de Moura. Vesting Empresarial: Aspectos Jurídicos Relevantes à Luz da Teoria dos Contratos Relacionais. 2. ed. Editora Foco, jun. 2022."
---

# Vesting Termination and Acceleration

O contrato de vesting deve prever a hipótese de a empresa se frustrar com a pessoa vinculada. Quando um cliff traz um resultado negativo, esse resultado pode culminar no rompimento da relação — e o contrato precisa antecipar as consequências desse rompimento para cada modalidade.

No [[Inverted Vesting]], o rompimento acelera a reversão do equity: como o beneficiário já exerce o direito desde o início (condição resolutiva), o rompimento provoca a perda imediata e total do equity ainda sujeito a essa condição, de uma só vez, em vez da perda gradual cliff a cliff.

No [[Traditional Vesting]], o rompimento leva à saída do indivíduo sem que ele exerça o equity ainda não adquirido (condição suspensiva não implementada), somado ao direito de recompra que a empresa mantém sobre o equity já adquirido.

Em ambos os casos, o seguro empresarial funciona como mecanismo de prevenção da empresa contra os efeitos financeiros desse rompimento.

> [!NOTE] Ressalva terminológica
> No uso de mercado, "aceleração" (acceleration) costuma designar a antecipação do vesting em favor do beneficiário (ex.: cláusulas de aceleração em caso de change of control). Neste estudo, porém, o termo é usado no sentido oposto — aceleração da reversão/perda do equity no rompimento, conforme a modalidade invertida. A confirmar a nomenclatura correta no livro-fonte (ver [[Next Steps]]).

```mermaid
flowchart TD
    R[Análise no cliff] --> N{Resultado negativo?}
    N -->|Não| K[Cronograma segue]
    N -->|Sim| M{Modalidade}
    M -->|Invertido| A[Rompimento: perda imediata e total do equity - aceleração da reversão]
    M -->|Tradicional| E[Saída sem exercer o equity não adquirido]
    E --> B[Direito de recompra da empresa sobre o equity já adquirido]
    A --> I[Seguro empresarial como prevenção]
    B --> I
```

## Related

- [[Cliffs in Vesting Schedules]] — o cliff negativo é o gatilho que pode levar ao rompimento.
- [[Traditional Vesting]] — consequências do rompimento na modalidade suspensiva.
- [[Inverted Vesting]] — consequências do rompimento na modalidade resolutiva.
