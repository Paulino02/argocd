# Argo CD
 o Argo CD foi projetado especificamente para Continuous Delivery (CD) em ambientes Kubernetes. Aqui estão alguns aspectos que destacam essa especialização:

Integração Profunda com Kubernetes: Argo CD é nativamente integrado com a API do Kubernetes, permitindo a gestão detalhada e eficiente de recursos e aplicativos dentro dos clusters Kubernetes.

Suporte a Configurações Kubernetes: Ele suporta uma ampla variedade de formatos de configuração do Kubernetes, incluindo manifests YAML, Helm Charts, Kustomize, Jsonnet e mais. Isso permite que as equipes usem suas ferramentas e padrões preferidos para definir e gerenciar suas aplicações.

Automação e Sincronização: Argo CD monitora os repositórios Git em busca de alterações nas configurações e aplica essas alterações automaticamente aos clusters Kubernetes. Isso garante que o estado dos aplicativos no cluster esteja sempre alinhado com o estado desejado definido no repositório Git, conforme a abordagem GitOps.

Fluxos de Trabalho de CI/CD: Embora Argo CD seja focado em CD, ele pode ser integrado com ferramentas de CI (Continuous Integration) como Jenkins, GitLab CI, CircleCI, etc. para criar pipelines completos de CI/CD. A ferramenta de CI constrói e testa o código, enquanto o Argo CD gerencia a entrega e a implantação do código em ambientes Kubernetes.

Rollbacks e Rollouts Seguros: Facilita a execução de rollbacks para versões anteriores e rollouts de novas versões de aplicativos, com capacidade de automação e controle granular.

Interface Gráfica e Observabilidade: Oferece uma interface gráfica amigável para visualizar o estado das implantações, ver logs, e monitorar a saúde dos aplicativos, proporcionando uma gestão centralizada e visibilidade das operações.

O foco no Kubernetes permite que o Argo CD ofereça recursos otimizados e uma integração fluida com as práticas e ferramentas comuns no ecossistema Kubernetes, tornando-o uma escolha poderosa para equipes que operam em ambientes baseados em Kubernetes.

## Arquitetura orienta a eventos
o Argo CD pode ser considerado uma aplicação que segue uma arquitetura orientada a eventos. Ele monitora continuamente o estado das aplicações no Kubernetes e reage a eventos, como mudanças de configuração ou de estado dos recursos, para garantir que o estado desejado (definido nos manifests Git) esteja sempre em sincronia com o estado atual das aplicações no cluster.

O Argo CD utiliza mecanismos como webhooks do Git para detectar alterações nos repositórios e acionar processos de sincronização. Esses eventos desencadeiam ações específicas, como atualizações ou rollbacks, com base nas mudanças detectadas.

## Metodologia GitOps
A metodologia GitOps é uma prática emergente de DevOps que utiliza Git como a única fonte de verdade para a infraestrutura e as configurações de aplicativos. O GitOps se baseia em princípios de automação e versionamento fornecidos pelo Git para gerenciar a entrega contínua e a operação de clusters Kubernetes e outros sistemas. Aqui está uma visão geral detalhada da metodologia GitOps:

Princípios do GitOps
Git como Fonte da Verdade:

Todas as configurações de infraestrutura e aplicativos são armazenadas em repositórios Git. Isso inclui manifests Kubernetes, scripts de configuração, políticas de segurança, etc.
Qualquer alteração na infraestrutura ou nos aplicativos é feita por meio de pull requests (PRs) ou commits no repositório Git.
Automação:

Ferramentas de automação monitoram os repositórios Git em busca de alterações e aplicam essas alterações automaticamente aos ambientes de destino (como clusters Kubernetes).
Ferramentas comuns para automação incluem Argo CD, Flux, Jenkins X, etc.
Desacoplamento da Entrega e da Operação:

A entrega contínua (CD) é tratada como uma operação separada, onde as configurações e os aplicativos são implantados em ambientes automatizados.
As operações diárias, como escala, recuperação de falhas e atualizações, são realizadas com base nas configurações versionadas no Git.
Observabilidade e Controle:

Monitoramento contínuo do estado atual do sistema para garantir que ele esteja em conformidade com o estado desejado definido no Git.
Ferramentas de GitOps fornecem visibilidade sobre o estado atual e histórico das alterações, permitindo fácil auditoria e rollback.
Vantagens do GitOps
Consistência e Confiabilidade:

O uso do Git como fonte da verdade garante que todas as alterações sejam rastreadas, auditáveis e versionadas.
Facilita a aplicação de práticas de CI/CD, como revisão de código e integração automatizada.
Automação e Eficiência:

Reduz o erro humano ao automatizar a aplicação de configurações e implantações.
Melhora a eficiência operacional ao eliminar a necessidade de intervenções manuais frequentes.
Recuperação e Rollback:

Facilita a recuperação de falhas e rollback para versões anteriores de configurações e aplicativos.
As configurações versionadas no Git tornam o processo de recuperação mais rápido e confiável.
Escalabilidade e Flexibilidade:

Pode ser aplicado a múltiplos ambientes e clusters, permitindo uma gestão centralizada e escalável da infraestrutura.
Implementação do GitOps
Configuração do Repositório Git:

Crie repositórios Git para armazenar as configurações de infraestrutura e aplicativos.
Organize os repositórios de maneira lógica, separando configurações de ambientes diferentes (produção, staging, etc.).
Automação com Ferramentas de GitOps:

Use ferramentas como Argo CD ou Flux para monitorar os repositórios Git e aplicar as alterações automaticamente aos clusters Kubernetes.
Configure essas ferramentas para sincronizar automaticamente as alterações e fornecer visibilidade sobre o estado atual.
Fluxo de Trabalho GitOps:

Desenvolvedores fazem alterações nas configurações e criam pull requests.
As alterações são revisadas e aprovadas por meio do processo de revisão de código.
As ferramentas de GitOps detectam as alterações e aplicam automaticamente as configurações atualizadas ao ambiente de destino.
Ferramentas Comuns de GitOps
Argo CD:

Ferramenta de entrega contínua para Kubernetes que se integra com Git e aplica automaticamente as alterações de configuração aos clusters.
Flux:

Outra ferramenta de GitOps que monitora repositórios Git e aplica configurações a clusters Kubernetes.
Jenkins X:

Uma plataforma CI/CD que suporta GitOps e facilita a entrega contínua e operações para Kubernetes.
A metodologia GitOps representa uma evolução natural das práticas DevOps, trazendo maior automação, consistência e confiabilidade para a gestão de infraestrutura e aplicativos em ambientes modernos de nuvem e Kubernetes.

## Comandos
- create a namespace 
  - kubectl create -ns argocd

- instalando o argocd dentro do cluster
  - kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

- getting initial admin password
  - kubectl get secret -n argocd argocd-initial-admin-secret -o yaml
  - kubectl get secret -n argocd argocd-initial-admin-secret -o yaml | grep 'password:' | awk '{print $2}' | base64 --decode | xargs echo

- accessing argocd server
  - kubectl port-forward svc/argocd-server -n argocd 8080:443
  - open browser https://localhost:8080