![NetBox](netbox_logo.svg "NetBox logo")

# O que é NetBox?

NetBox é um aplicativo da web de código aberto projetado para ajudar a gerenciar e documentar redes de computadores. Inicialmente concebido pela equipe de engenharia de rede da [DigitalOcean](https://www.digitalocean.com/), o NetBox foi desenvolvido especificamente para atender às necessidades dos engenheiros de rede e infraestrutura. Abrange os seguintes aspectos de gerenciamento de rede:

- **Gerenciamento de endereço IP (IPAM)** - redes e endereços IP, VRFs e VLANs
- **Racks de equipamentos** - Organizados por grupo e local
- **Dispositivos** - Tipos de dispositivos e onde estão instalados
- **Conexões** - Rede, console e conexões de energia entre dispositivos
- **Virtualização** - máquinas virtuais e clusters
- **Circuitos de dados** - Circuitos e provedores de comunicações de longa distância
- **Segredos** - Armazenamento criptografado de credenciais confidenciais
  
## O que NetBox não é

Embora o NetBox se esforce para cobrir muitas áreas de gerenciamento de rede, o escopo de seu conjunto de recursos é necessariamente limitado. Isso garante que o desenvolvimento se concentre na funcionalidade central e que o aumento do escopo seja razoavelmente contido.Para esse fim, pode ser útil fornecer alguns exemplos de funcionalidade que o NetBox **não** oferece:

- Monitoramento de rede
- Servidor dns
- Servidor RADIUS
- Gerenciamento de configurações
- Gestão de instalações

Dito isso, o NetBox _pode_ ser usado com grande efeito ao preencher ferramentas externas com os dados de que precisam para executar essas funções.

## Filosofia do desenho (*design*)

NetBox foi projetado com os seguintes princípios em mente.

### Replicar o mundo real

Uma consideração cuidadosa foi dada ao modelo de dados para garantir que ele possa refletir com precisão uma rede do mundo real. Por exemplo, os endereços IP são atribuídos não a dispositivos, mas a interfaces específicas anexadas a um dispositivo, e uma interface pode ter vários endereços IP atribuídos a ela.

### Sirva como uma "fonte da verdade"

NetBox pretende representar o estado _desejado_ de uma rede versus seu estado _operacional_. Como tal, a importação automática do estado da rede ativa é fortemente desencorajada. Todos os dados criados no NetBox devem primeiro ser examinados por um humano para garantir sua integridade. O NetBox pode então ser usado para preencher os sistemas de monitoramento e provisionamento com um alto grau de confiança.

### Mantenha-o simples

Quando dada a escolha entre uma solução relativamente simples [80% de solução](https://pt.wikipedia.org/wiki/Princ%C3%ADpio_de_Pareto) e uma solução completa muito mais complexa, a primeira geralmente será favorecida. Isso garante uma base de código enxuta com uma curva de aprendizado baixa.

## Pilha de aplicativos

NetBox é desenvolvido na plataforma Python [Django](https://djangoproject.com/) e utiliza um banco de dados [PostgreSQL](https://www.postgresql.org/). Ele é executado como um serviço WSGI por trás de um servidor HTTP de sua escolha.

| Função                        | Componente        |
| ----------------------------- | ----------------- |
| Serviço HTTP                  | nginx ou Apache   |
| Serviço WSGI                  | gunicorn ou uWSGI |
| Inscrição                     | Django/Python     |
| Base de dados                 | PostgreSQL 9.6+   |
| Fila de tarefas               | Redis/django-rq   |
| Acesso ao dispositivo ao vivo | NAPALM            |

## Versões Python Suportadas

NetBox suporta ambientes Python 3.6, 3.7 e 3.8 atualmente.(O suporte para Python 3.5 foi removido no NetBox v2.8.)

## Começando

Consulte o [guia de instalação](installation/index.md) para obter ajuda para colocar o NetBox em operação rapidamente.
