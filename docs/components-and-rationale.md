# Components and Rationale — xsilent風

Este documento descreve **os principais componentes da xsilent風** e, mais importante, **o motivo de cada escolha**.

O objetivo não é ensinar como essas tecnologias funcionam em geral,  
mas explicar **por que foram usadas aqui**, **quais problemas tentam mitigar**  
e **quais limitações permanecem**.

---

## 1. Alpine Linux (Base do Sistema)

**Por que Alpine?**

- Superfície de ataque reduzida
- Base mínima, sem serviços implícitos
- Facilidade para construir um ambiente do zero

**O que isso mitiga**
- Serviços desnecessários rodando por padrão
- Complexidade invisível ao usuário

**O que NÃO mitiga**
- Comprometimento do kernel
- Ataques físicos ou em firmware
- Erros de configuração do próprio usuário

Alpine não é “mais seguro por mágica”; ele é **mais controlável**.

---

## 2. Persistência Controlada

**Por que usar persistência?**

- Permitir configuração manual e consciente
- Evitar reinstalação a cada boot
- Manter consistência de ambiente

**Risco introduzido**
- Rastros locais passam a existir
- Exposição em caso de acesso físico ao dispositivo

A persistência é um **trade-off explícito**, não um padrão silencioso.

---

## 3. Tor (Rede)

**Por que Tor?**

- Roteamento em múltiplos saltos
- Redução de correlação direta entre origem e destino
- Amplamente estudado e auditado

**O que Tor ajuda a mitigar**
- Exposição direta de IP
- Observação passiva simples de tráfego

**O que Tor NÃO resolve**
- Fingerprinting de navegador
- Correlação global de tráfego
- Identificação por comportamento do usuário

Tor é tratado como **camada de transporte**, não como garantia final.

---

## 4. DNSCrypt Proxy

**Por que DNSCrypt?**

- Criptografar consultas DNS
- Evitar vazamentos DNS em texto claro
- Reduzir dependência de resolvers locais

**Limitações**
- O resolvedor ainda pode inferir padrões
- Não oculta o destino final de conexões HTTP(S)
- Pode introduzir falsa sensação de segurança

DNSCrypt protege **consultas**, não identidade.

---

## 5. Spoofing de MAC Address

**Por que MAC spoofing?**

- Evitar correlação simples em redes locais
- Reduzir rastreamento por identificador físico

**Limitações**
- Não protege contra fingerprint de camada superior
- Pode gerar inconsistência comportamental
- Não impede correlação temporal

É uma mitigação **local e limitada**, não anonimato.

---

## 6. Navegadores (Camada de Aplicação)

A xsilent風 **não impõe um único navegador**, pois cada um representa um perfil de risco diferente.

### Tor Browser
- Melhor mitigação de fingerprint
- Menor flexibilidade
- Uso pontual e disciplinado

### qutebrowser
- Controle total pelo usuário
- Alto risco se mal configurado
- Exige entendimento de OPSEC

### Falkon
- Navegador gráfico leve
- Baixo foco em privacidade
- Uso restrito e consciente

### Lynx
- Superfície mínima
- Sem execução de conteúdo ativo
- Usabilidade limitada

Misturar navegadores **aumenta risco comportamental**.

---

## 7. Usuário como Componente Crítico

A xsilent風 assume explicitamente que:
- o usuário é parte da superfície de ataque
- decisões operacionais importam mais que ferramentas
- comportamento quebra ou preserva OPSEC

Nenhuma configuração compensa erro humano consistente.

---

## Considerações Finais

Este projeto não tenta ser:
- automático
- infalível
- confortável

Ele tenta ser **honesto**.

Cada componente foi escolhido não por ser “o melhor”,  
mas por **tornar visíveis os trade-offs** que normalmente ficam ocultos.

Se você busca garantias, este projeto não é para você.  
Se busca compreensão, ele é um ponto de partida.