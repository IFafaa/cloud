# AWS AppStream 2.0

O **Amazon AppStream 2.0** é um serviço gerenciado da AWS que permite fazer **streaming seguro de aplicações de desktop** para usuários sem necessidade de reescrever esses aplicativos para a nuvem.

---

## Visão Geral

O AppStream 2.0 permite que usuários acessem aplicações desktop através de um navegador web ou cliente nativo, sem precisar instalar as aplicações localmente em seus dispositivos.

---

## Características Principais

- **Streaming de Aplicações**
  - Aplicações Windows rodando na nuvem
  - Acesso via navegador ou cliente
  - Sem necessidade de instalação local

- **Acesso Multi-Device**
  - Windows
  - macOS
  - Linux
  - iOS
  - Android
  - Navegadores web

- **Tipos de Instâncias**
  - **General Purpose**: Uso geral
  - **Graphics**: Aplicações com gráficos
  - **Graphics Pro**: Gráficos de alta performance
  - **Graphics G4**: Gráficos profissionais (CAD, 3D)

- **Fleets e Image Builders**
  - **Fleets**: Pool de instâncias para streaming
  - **Image Builders**: Criar e personalizar imagens
  - Configurações pré-definidas ou customizadas

- **Segurança**
  - Criptografia em trânsito
  - Dados não ficam no dispositivo do usuário
  - Integração com Active Directory
  - Políticas de acesso granulares

---

## Casos de Uso Comuns

- **Aplicações Legacy**
  - Aplicações antigas que não rodam em sistemas modernos
  - Aplicações que requerem configurações específicas
  - Software que não pode ser migrado facilmente

- **Aplicações com Requisitos Especiais**
  - Software que requer hardware específico
  - Aplicações com dependências complexas
  - Software licenciado centralmente

- **Acesso Temporário**
  - Usuários que precisam de acesso esporádico
  - Contratados e parceiros
  - Acesso seguro sem instalação local

- **Desenvolvimento e Design**
  - Ferramentas de design gráfico
  - IDEs e ambientes de desenvolvimento
  - Software de CAD/CAM

---

## Diferenças entre AppStream e WorkSpaces

| AppStream 2.0 | WorkSpaces |
|---------------|------------|
| Streaming de aplicações específicas | Desktop completo |
| Sessões sob demanda | Desktops persistentes |
| Ideal para aplicações isoladas | Ideal para desktops completos |
| Pay-per-use | Hourly ou Monthly |

---

## Benefícios

- **Sem Reescrita**: Use aplicações existentes sem modificação
- **Segurança**: Dados não saem da nuvem
- **Acesso Universal**: Funciona em qualquer dispositivo
- **Gerenciamento Centralizado**: Atualizações e patches em um lugar
- **Custo-Efetivo**: Paga apenas pelo uso

---

## Quando Usar AWS AppStream 2.0

- Quando você tem aplicações desktop que precisa disponibilizar remotamente
- Para aplicações legacy que não podem ser migradas facilmente
- Quando você quer evitar instalação de software nos dispositivos dos usuários
- Para aplicações com requisitos de hardware específicos
- Quando você precisa de acesso seguro a aplicações sem expor dados localmente
