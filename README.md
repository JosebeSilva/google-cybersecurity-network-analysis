# Análise de Tráfego de Rede: Incidente de DNS

Este projeto faz parte do meu portfólio de Cibersegurança e foi desenvolvido durante o curso **Google Cybersecurity Professional Certificate**. 

Aqui, assumo o papel de um Analista de Segurança Cibernética investigando uma falha de conexão usando a análise de pacotes de rede.

---

## O Cenário

Clientes de uma empresa provedora de TI começaram a relatar um problema: ninguém conseguia acessar o site `www.yummyrecipesforme.com`. Após um longo tempo de carregamento, o navegador exibia a mensagem de erro **"destination port unreachable"** (porta de destino inalcançável). 

Minha missão foi investigar o tráfego de rede para descobrir exatamente onde a comunicação estava falhando.

## Ferramentas e Tecnologias Exploradas

* **Ferramenta de Análise:** `tcpdump`
* **Protocolos Analisados:** DNS, UDP, ICMP
* **Conceitos:** Resolução de Nomes, Portas de Rede (Porta 53), Troubleshooting de Redes.

---

## A Investigação

Para entender o que estava acontecendo, utilizei o `tcpdump` para capturar os pacotes de rede enquanto tentava acessar o site. 
<img width="1001" height="474" alt="image" src="https://github.com/user-attachments/assets/acac2d31-524b-4f97-a885-3638442d6bc1" />


Ao analisar os logs gerados, observei o seguinte fluxo:
1. **Requisição:** Meu computador enviou uma consulta DNS através de um pacote **UDP** para o IP do servidor DNS, visando a **porta 53** (porta padrão para tráfego DNS).
2. **A Falha:** O servidor não respondeu com o endereço IP do site.
3. **O Erro:** Em vez da resposta esperada, o servidor retornou um pacote **ICMP** com a mensagem de erro: *"udp port 53 unreachable"*.

## Minha Conclusão

Com base nos dados extraídos do tráfego de rede, concluí que as requisições DNS estavam sendo enviadas corretamente pelo cliente via protocolo UDP, mas não havia nenhum serviço escutando na porta 53 do servidor de destino.

**Causas raízes mais prováveis que apontei no meu relatório de incidente:**
* O serviço DNS no servidor caiu ou foi interrompido.
* Existe uma configuração incorreta no servidor de nomes.
* Um firewall está bloqueando indevidamente o tráfego UDP direcionado à porta 53.

> **O que aprendi com isso:** Esta atividade reforçou minha compreensão prática sobre como diferentes protocolos de rede (como DNS, UDP e ICMP) interagem nos bastidores e como a análise de pacotes é vital para isolar e diagnosticar problemas cibernéticos e de infraestrutura.

---
*Fique à vontade para explorar o relatório de incidente completo disponível neste repositório!*
