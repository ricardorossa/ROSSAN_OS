
# ROSSAN

## Do boot ao desktop, em Assembly

ROSSAN e um sistema operacional experimental para x86, construido em Assembly
com FASM. O projeto acompanha a maquina desde os primeiros passos do boot em
16 bits ate um ambiente grafico em modo protegido de 32 bits, com memoria
virtual, interrupcoes, framebuffer, cursor e aplicativos internos.

Aqui, cada camada esta exposta: o boot prepara o processador, o kernel assume
o controle da memoria e dos dispositivos, e a interface grafica nasce direto
da escrita no framebuffer. ROSSAN e um laboratorio pratico para entender como
um computador realmente funciona por dentro.

## O que ja existe

### Inicializacao e kernel

- Entrada BIOS em modo real de 16 bits.
- Transicao para modo protegido x86 de 32 bits.
- GDT, IDT, TSS e pilhas do sistema.
- Inicializacao dos segmentos de codigo e dados.
- Kernel monolitico organizado em modulos Assembly.
- Estruturas para processos, threads, objetos, listas e sincronizacao.

### Memoria

- Preparacao de mapas de paginas e tabelas de pagina.
- Mapeamento de regioes de memoria usadas por dispositivos e framebuffer.

### Interrupcoes e hardware

- Montagem da tabela de interrupcoes.
- Inicializacao do PIC e controle de IRQ.
- PIT para temporizacao do sistema.
- Codigo de enumeracao do barramento PCI.
- Deteccao de recursos do processador via CPUID.
- Caminho de inicializacao de mouse PS/2 integrado ao kernel.

### Video

- Boot com informacoes de video fornecidas pelo ambiente BIOS/VESA.
- Framebuffer de 32 bits com calculo rapido de offsets por linha.
- Mapeamento do framebuffer no espaco de enderecos do sistema.
- Primitivas de pixel, linhas, retangulos, circulos e imagens 32x32.
- Fonte bitmap 8x8 e renderizacao de texto.
- Cursores e imagens incorporadas diretamente ao binario.

### Desktop e interacao

- Desktop com fundo desenhado em Assembly.
- Barra de tarefas, menu inicial e relogio.
- Janelas com titulo, bordas, sombra, botoes e area de conteudo.
- Gerenciamento basico de foco, arraste e cliques.
- Cursor com restauracao do conteudo sob o ponteiro.
- Controle de clipping para desenhar dentro das areas corretas.

### Aplicativos internos

- Aplicativo de informacoes da CPU, com leitura da marca do processador via
	folhas estendidas do CPUID.
- Icone de CPU e do Desenhador no desktop.
- Aplicativo Desenhador com canvas e paleta de cores.
- Seletor de resolucao com opcoes de 800x600 e 1024x768.

## Executando no QEMU

Para a imagem fixa:

```powershell
qemu-system-i386 -m 64 -drive file="rossan-fixed.img",format=raw,if=floppy -boot order=a
```

Para a imagem FAT32:

```powershell
qemu-system-i386 -m 64 -drive file="rossan-boot-fat32-superfloppy.img",format=raw,if=ide -boot order=c
```
Se preferir, pode também salvar utilizar o RUFUS para gravar a imagem em um pendrive e utilizar em seu computador como pendrive bootavel,
executando assim em modo real.

## Estado atual

ROSSAN esta em desenvolvimento ativo.
