<h1 align="center">Usando Hash em Python</h1>
 
Usando a biblioteca `hashlib` que é nativa do Python, podemos transformar bytes em hash, deixando de ser legível pelos humanos.

## Importando
```python
from hashlib import md5, sha256
```

## Criando um Hash simples
```python
texto = "senha123".encode("utf8")
hash = md5(texto).hexdigest()
print(hash)
```
    e7d80ffeefa212b7c5c55700e4f7193e

***

## Comparando 2 hashs
```python
texto = "senha123".encode("utf8")
texto2 = "senha1234".encode("utf8")

hash = md5(texto).hexdigest()
hash2 = md5(texto2).hexdigest()
print(hash == hash2)
```
    False

***

## Transformando arquivos em hash
```python
def getHashFromFile(file):
    hash = sha256()
    b = bytearray(128*1024)
    mv = memoryview(b)
    with open(file, "rb", buffering=0) as f:
        for n in iter(lambda : f.readinto(mv), 0):
            hash.update(mv[:n])
    return hash.hexdigest()

hash = getHashFromFile("README.md")
print(hash)
```
    3f2d5d0e19ab47362320228c4f611eee29210dc553df7b4ed5d1bf1c4b84f81b

A função `getHashFromFile` foi retirada de uma discussão do Stack Overflow !