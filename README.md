# Yerel Yapay Zeka: Bilgisayarım Ne Kaldırır?

ChatGPT gibi bir yapay zekayı internetsiz, kendi bilgisayarında çalıştırabilirsin. Ücret yok, mesajların bilgisayarından çıkmaz.
Tek soru: bilgisayarın hangi boyutu kaldırır? Bu rehber onu cevaplıyor.

**En kolayı:** `PROMPT.md`'yi yapay zekana ver, bilgisayarına bakıp sana uygun modeli o seçsin ve kurulumda yardım etsin.

---

## 1. Bilgisayarın ne kaldırır?

Kural basit: model dosyası belleğe (RAM, Mac'te "birleşik bellek") sığmalı. Dosya boyutunun üstüne bağlam için biraz yer lazım.
llmspeed'in kendi hesabı: Mac'te belleğin yaklaşık **%75'i** modele ayrılabilir (kaynak: github.com/nicorobinreal/llmspeed README).

Önce kendi makinene bak:

| Sistem | Komut |
|---|---|
| Mac | `sysctl -n machdep.cpu.brand_string` ve `sysctl hw.memsize` (bayt cinsinden; 17179869184 = 16 GB) |
| Windows | `systeminfo` (RAM) ve Görev Yöneticisi > Performans > GPU |
| Linux | `free -h` ve `lspci \| grep -i vga` |

Kaba tahmin (4-bit model, benim tahminim, ölçüm değil):

| Belleğin | Rahat çalışan model boyutu |
|---|---|
| 8 GB | 1B - 4B |
| 16 GB | 4B - 8B (12B zorlanır) |
| 24 - 32 GB | 12B - 14B |
| 64 GB ve üstü | 30B ve üstü |

Hız için **llmspeed.dev**: donanımını ve modeli seç, kaç token/sn alacağını ve ilk cevabın ne kadar süreceğini gör. Her sayı etiketli: Measured (o donanımda ölçülmüş), Derived (benzerlerden türetilmiş), Projected (özellikten hesaplanmış).
Not: sitede ekran kartları ve Mac'ler listeli; her Mac modeli ve bellek boyutu yok. Birebir yoksa en yakınını seç, tahmin olduğunu bil.

## 2. Ollama kurulumu

Ollama, modeli indirip çalıştıran ücretsiz program. Resmî sayfa: ollama.com/download

- **macOS / Linux:** `curl -fsSL https://ollama.com/install.sh | sh`
- **Windows (PowerShell):** `irm https://ollama.com/install.ps1 | iex`
- Komut istemiyorsan aynı sayfadan macOS için `Ollama.dmg`, Windows için `OllamaSetup.exe` indir.

Kurunca terminalde dene: `ollama --version`

## 3. İlk 3 model

Boyutlar ollama.com/library sayfalarındaki disk boyutlarıdır.

| Model | Komut | Disk | Kime |
|---|---|---|---|
| Gemma 3 1B | `ollama run gemma3:1b` | 0,8 GB | Çok eski/zayıf bilgisayar, hızlı deneme |
| Llama 3.2 3B | `ollama run llama3.2` | 2,0 GB | 8 GB RAM, genel kullanım |
| Qwen3 8B | `ollama run qwen3:8b` | 5,2 GB | 16 GB RAM, daha akıllı cevap |

İlk komutta model iner, sonra sohbet başlar. Çıkmak için `/bye`. Hızı görmek için `ollama run MODEL --verbose` (sonunda token/sn yazar).
Türkçe kalitesi modele göre değişir; kendi sorunla dene. Gemma 3 sayfası "140'tan fazla dil" diyor; ben Türkçeyi ayrıca ölçmedim.

## 4. LFM3 (1 GB'a sığan model) nasıl denenir

LiquidAI LFM3-1.7B: 1,7 milyar parametre, 4-bit'te yaklaşık 1,1 GB.

```bash
ollama run lfm3
```

Önce bil:
- **Lisans:** LFM Open License v1.0. Yıllık geliri 10 milyon dolar ve üstü şirketlerin ticari kullanımı lisans kapsamı dışında. Altındaysan ticari kullanım serbest. Sürüm: kendi okuyup emin ol (huggingface.co/LiquidAI/LFM3-1.7B/blob/main/LICENSE).
- **Türkçe:** Model kartının resmî dil listesinde (16 dil) Türkçe yok. Ben denedim: anlıyor ve Türkçe yazıyor ama hatalı kelimeler ve yanlış yorumlar var (ölçümler: `motor/videolar/v16-minimodel/KANIT.md`).
- **Düşünme modu açık gelir.** Cevaptan önce İngilizce "Thinking..." bölümü yazar, bu yüzden kısa soruya bile uzun sürebilir.
- Telefona/laptopa sığması için tasarlanmış; çok işlemcili güçlü sunucu gerekmez.

## Sorun giderme
- "model çok yavaş": bir küçük boyuta in (8B yerine 4B).
- Bilgisayar donuyorsa: model belleğe sığmıyor, daha küçük seç.
- Disk doluyorsa: `ollama list` ile gör, `ollama rm MODEL` ile sil.
