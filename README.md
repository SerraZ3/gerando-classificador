# Gerando Classificador

Passo a passo de como gerar classificador no ubuntu 18.04 para o curso da udemy `Detecção de Objetos com Python e OpenCV`.

## Estrutura de diretório

```Diretório
Exemplo1
| - negativas
| - positivas (criar pasta)
| - classificador (criar pasta)
| - bg.txt
| - positivas.txt
| - caneca01.jpg
```

## Gerar o bg.txt

Rodar esse comando no diretório raiz do projeto

```shellscript
ls negativas/*.jpg > bg.txt

```

## Gerar o positivas e arquivo com informações

```shellscript
opencv_createsamples -img caneca01.jpg -bg bg.txt -info positivas/positivas2.txt -maxxangle 0.5 -maxyangle 0.5 -maxzangle 0.5 -num 1800 -bgcolor 255
```

## Cria arquivo com informações das positivas no raiz

Rodar esse código para corrigir o conteúdo do arquivo positivas2.txt

```python
with open('positivas/positivas2.txt', 'r') as istr:
    with open('positivas.txt', 'w') as ostr:
        for i, line in enumerate(istr):
            # Get rid of the trailing newline (if any).
            line = line.rstrip('\n')
            line = "positivas" + "/"+ line
            print(line, file=ostr)
```

## Gerar o positivas.vec

```shellscript
opencv_createsamples -info positivas.txt -num 1800 -w 18 -h 18 -vec positivas.vec
```

## Gerar classificador

```shellscript
opencv_traincascade -data classificador -vec positivas.vec -bg bg.txt -numPos 1600 -numNeg 800 -numStages 10 -w 18 -h 18 -precalcBufSize 1024 -precalcIdxBufSize 1024
```
