# 3. Hashes e Integridade

Tabela de referência rápida.

| Algoritmo | Tamanho  |
| --------- | -------- |
| MD5       | 128 bits |
| SHA1      | 160 bits |
| SHA256    | 256 bits |
| SHA512    | 512 bits |

**Linux:**
md5sum arquivo.img
sha256sum arquivo.img

**Windows**
Powershell
Get-FileHash arquivo.img -Algorithm SHA256
