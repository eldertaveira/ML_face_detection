# Face Detection (OpenCV) — Projeto DIO

Pequeno projeto de **Visão Computacional** para **detecção de rostos** usando **OpenCV Haar Cascade** (pré‑treinado). Opcionalmente, há um script que roda **classificação de gênero percebido** (Male/Female) via **OpenCV DNN (Caffe)** — **apenas para fins educacionais**.

---

## ✨ Funcionalidades

* **Detecção de rostos** em imagem única (caminho fixo no script).
* **Anotação da imagem** com caixas e rótulos.
* **Salvar saída** em `outputs/`.
* **(Opcional)** Classificação de gênero percebido (Male/Female) com confiança.

> ⚠️ **Nota ética**: A classificação de gênero aqui representa **gênero percebido** por um modelo treinado e pode errar, refletir vieses e **não contempla identidades não-binárias**. Utilize somente com consentimento e para estudo.

---

## 📁 Estrutura

```
.
├─ models/        # arquivos de modelo (cascades e, opcionalmente, Caffe) – ignorados no Git
├─ outputs/       # imagens anotadas – ignoradas no Git
├─ data/          # (opcional) insumos diversos – ignorados no Git
├─ detect_single_image.py        # detecção de rostos
├─ gender_single_image.py        # (opcional) detecção + classificação de gênero
├─ README.md
└─ .gitignore
```

As pastas `models/`, `outputs/` e `data/` incluem um `.gitkeep` para ficarem versionadas vazias.

---

## 🧰 Requisitos

* **Python 3.9+**
* **OpenCV** (`opencv-python`)
* Para exibir imagem **inline no notebook** sem janela: `Pillow` (ou `matplotlib` se preferir)

Instalação sugerida (Windows / PowerShell):

```bash
python -m venv .venv
.venv\Scripts\activate
pip install opencv-python pillow
```

No Linux/macOS:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install opencv-python pillow
```

> Se usar `gender_single_image.py`, **não precisa** instalar nada além do OpenCV; o script baixa os pesos automaticamente (ver seção abaixo). Em redes corporativas, talvez seja preciso baixar manualmente.

---

## ▶️ Como rodar

### 1) Detecção de rostos (apenas imagem)

Abra `detect_single_image.py` e ajuste:

```python
IMAGE_PATH = r"C:\\Users\\elder\\Downloads\\Mulher_rosto01.jpg"
```

Execute:

```bash
python detect_single_image.py
```

A imagem anotada será salva em `outputs/faces_<nome>.jpg`.

### 2) (Opcional) Detecção + gênero percebido

Abra `gender_single_image.py` e ajuste o mesmo `IMAGE_PATH`. Execute:

```bash
python gender_single_image.py
```

Ele salva em `outputs/gender_<nome>.jpg`.

> Ambos os scripts imprimem no console a quantidade de rostos e (no de gênero) o rótulo e confiança de cada face.

---

## 📓 Uso em Notebook (inline)

Dentro do notebook, após rodar um dos scripts, você pode simplesmente importar e chamar a função principal **ou** copiar o trecho final que usa:

```python
from IPython.display import display
from PIL import Image
# ... após desenhar em 'img' (BGR):
display(Image.fromarray(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)))
```

Se preferir `matplotlib`:

```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)); plt.axis('off')
```

---

## 🔽 Download automático de modelos

Os scripts já tentam carregar os **Haar Cascades** do OpenCV; se falharem, fazem **download automático** para `models/`:

* `haarcascade_frontalface_default.xml`
* `haarcascade_frontalface_alt2.xml`

Para **gênero** (OpenCV DNN), o script baixa para `models/`:

* `gender_deploy.prototxt`
* `gender_net.caffemodel`

Se sua rede bloquear os downloads, baixe manualmente pelos links dentro do script e coloque os arquivos em `models/` com os mesmos nomes.

---

## 🧩 Dicas & Troubleshooting

* **Falha ao carregar cascade** (`!empty()` / `CascadeClassifier.empty()`):

  * Rode o script que já força o download para `models/`.
  * Verifique se o caminho da imagem (`IMAGE_PATH`) está correto (use `r"..."` em Windows).
* **No notebook, quer inline**: use `Pillow` + `IPython.display` (já demonstrado acima) ou instale `matplotlib`.
* **Downloads 404/bloqueados**: pegue os arquivos manualmente e coloque em `models/`.
* **Janela do OpenCV não abre** (em ambientes remotos): use a exibição inline no notebook.

---

## 📝 .gitignore

O repositório ignora por padrão:

* `.venv/`, caches Python, arquivos temporários.
* `models/`, `outputs/`, `data/` (mantidos com `.gitkeep`).
* Checkpoints de notebooks.

Se algum arquivo ignorado já estiver versionado, rode:

```bash
git rm -r --cached .venv models outputs data
git add .
git commit -m "chore: ajusta .gitignore"
```

---

## 📚 Referências & Créditos

* **OpenCV** (Haar Cascades, DNN).
* **Modelos de gênero (Caffe)** originalmente demonstrações educacionais do projeto *LearnOpenCV*.

---

## 📄 Licença

Este projeto é para **fins educacionais** (bootcamp DIO).

---

## ✅ Checklist rápido

* [ ] Criou venv e instalou dependências.
* [ ] Ajustou `IMAGE_PATH` no script.
* [ ] Rodou `detect_single_image.py` com sucesso.
* [ ] (Opcional) Rodou `gender_single_image.py` e gerou saída.
* [ ] Commitou com `.gitignore` correto.
