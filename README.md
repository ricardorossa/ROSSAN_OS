# ROSSAN<img width="910" height="680" alt="ROSSAN" src="https://github.com/user-attachments/assets/3e69b496-7846-4edb-a3b5-a733a7ab8611" />


## Do boot ao desktop, em Assembly

ROSSAN é um sistema operacional 100% brasileiro para x86, desenvolvido por Ricardo Rossa e criado entre 2004/2005, após quase 20 anos de pausa técnica, o projeto está sendo reativado. O SO é construido em Assembly. O projeto acompanha a maquina desde os primeiros passos do boot em 16 bits ate um ambiente grafico em modo protegido de 32 bits, com memoria virtual, interrupcoes, framebuffer, cursor e aplicativos internos.

Versão 1.0.1 26/10/2026
- Suporte nativo a drive USB EHCI 2.0 (OHCI e UHCI não estão nos planos).
- Suporte a FAT32.
- MSC integrado ao EHCI para leitura de arquivos.
- Leitura de arquivos de texto (agora temos o config.cfg, no qual é possível alterar a resolução da tela).
- Leitura de ícones PNG e imagens (background).
- Novo desenho para o cursor do mouse.
- Leitura e execução de arquivos binários.
- Correção do bug do relógio: agora a hora está certa! :)
- App de calendário.
- Tradução para o inglês
- Leitura básica do teclado USB em modo de 32 bits.

Versão 1.0.0 (2004~2026)

# O que já existe

## Inicialização e kernel

Entrada BIOS em modo real de 16 bits.
Transicao para modo protegido x86 de 32 bits.
GDT, IDT, TSS e pilhas do sistema.
Inicializacao dos segmentos de codigo e dados.
Kernel monolitico organizado em modulos Assembly.
Estruturas para processos, threads, objetos, listas e sincronizacao.
Mouse PS2/Touchpad

## Memoria

Preparacao de mapas de paginas e tabelas de pagina.
Mapeamento de regioes de memoria usadas por dispositivos e framebuffer.

## Interrupcoes e hardware

Montagem da tabela de interrupcoes.
Inicializacao do PIC e controle de IRQ.
PIT para temporizacao do sistema.
Codigo de enumeracao do barramento PCI.
Deteccao de recursos do processador via CPUID.
Caminho de inicializacao de mouse PS/2 integrado ao kernel.

## Video

Boot com informacoes de video fornecidas pelo ambiente BIOS/VESA.
Framebuffer de 32 bits com calculo rapido de offsets por linha.
Mapeamento do framebuffer no espaco de enderecos do sistema.
Primitivas de pixel, linhas, retangulos, circulos e imagens 32x32.
Fonte bitmap 8x8 e renderizacao de texto.
Cursores e imagens incorporadas diretamente ao binario.

## Desktop e interacao

Desktop com fundo desenhado em Assembly.
Barra de tarefas, menu inicial e relogio.
Janelas com titulo, bordas, sombra, botoes e area de conteudo.
Gerenciamento basico de foco, arraste e cliques.
Cursor com restauracao do conteudo sob o ponteiro.
Controle de clipping para desenhar dentro das areas corretas.

## Aplicativos internos

Aplicativo de informacoes da CPU, com leitura da marca do processador via folhas estendidas do CPUID.
Icone de CPU e do Desenhador no desktop.
Aplicativo Desenhador com canvas e paleta de cores.
Seletor de resolucao com opcoes de 800x600 e 1024x768.

## Executando no QEMU

Para a imagem fixa:
qemu-system-i386 -m 64 -drive file="rossan-fixed.img",format=raw,if=floppy -boot order=a

Para a imagem FAT32:
qemu-system-i386 -m 64 -drive file="rossan-boot-fat32-superfloppy.img",format=raw,if=ide -boot order=c

## Boot via pendrive

Se preferir, pode também utilizar o RUFUS para gravar a imagem em um pendrive e utilizar em seu computador como pendrive bootavel, executando assim em modo real. 
Configure a BIOS de seu computador para Legacy Mode (desabilite o Boot Secury Mode).


## ROSSAN esta em desenvolvimento ativo.
## Copyright 2004-2026 Ricardo Rosssa. All rights reserved.
## Provided "as is" without warranty of any kind
