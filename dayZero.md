#  Resolvendo os principais incidentes de segurança das redes brasileiras

## Motivação

# 300 mil roteadores com vulnerabilidades da MikroTik

## Spoofing de endereços

# Pacotes com IP de endereços de origem incorretos
# Esconde a identidade do atacante
# Erros de configuração
# Reflexão

## Ataques de negação de Serviço

# ataque na camada de aplicação
 1. exceder o número máximo de requisições
# ataque de exaustão de recursos de hardware
 1. consumir recursos da CPU e memória
# ataque volumétrico
 1. exaurir a banda disponível

## Observação o Bind em versões antigas anteriors a 9.4.1 deixa allow-recursion { any; }; // o que é muito ruim para a segurança da rede.
# conseguimos ver a versão do bind usando o comando `named -v`

 1. `nmap -6F endereçoIPV6`
 2. `dig +notcp @servidorIPV6 dominio any`
 3. `iptabales -t nat -A POSTROUTING -j SNAT --to-source endereçoSpoof`
 4. `iptables -t nat -S`
 5. `iptables -t nat -L`

## Resolvendo os ataques de negação de serviço

  # Rede da vítima
    1. Comprar uma máquina para fazer limpeza do tráfego ( investimento alto )
    2. Contratar empresa de mitigação de ataque ( custo mensal razoável )
    3. Utilizar filtros Blackhole ( RTBH ) -> só funciona quando o ataque é direcionado a poucos IPs
    4. Usar CDNs para distribuição ser for um serviço específico.
    5. Tem necessidade do serviço usar um BGP ( `nc -v -z IP_BGP 179`)
    

  # Protegendo o BGP
    A porta 179 que é a que o BGP trabalha deve ser apenas visível para o outro serviço BGP, outros equipamentos da internet essa porta não pode estar visível.
    Isolar os roteadores de borda na porta 179 para apenas os computadores BGP tanto para ipv6 quanto para ipv4
    Fazer um ACL, lembrando que cada roteador tem a sua própria configuração.

  # Rede do laranja ( terceiro )
  Caso o laranja que também pode ser uma vítima, estiver sendo explorado para produzir um ataque ele deve verificar quais os serviços estão disponíveis na internet e se os mesmos estão corretamente configurados.
   1. Serviços abertos para o mundo
     DNS recursivo
   2. Má configuração do serviço
     NTP monlist
   3. Serviços que não deveriam ser utilizados
     Chargen ( serviços antigos ou programas desatualizados )

   ## Utilizando Firewall no servidor DNS

    Apenas clientes podem ter acesso na porta 53/udp e tcp , o firewall deve estar configurado.

 ## Vulnerabilidade OpenSSH

   # CVE-2024-6387
     Verificar com `ssh -V`
     
# Verificar sempre o link -> https://cert.br/docs/whitepapers/notificacoes/  
