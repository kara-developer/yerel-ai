# Yapay zekana ver

Aşağıdaki bloğu Claude, ChatGPT, Codex ya da Gemini'ye yapıştır:

```
Bilgisayarıma yerel (internetsiz çalışan) bir yapay zeka modeli kurmak istiyorum. Yeni başlayanım, sade anlat.

1. Bilgisayarımın özelliklerine bak. Komut çalıştırabiliyorsan şunları çalıştır, çalıştıramıyorsan bana hangi komutu çalıştırıp çıktıyı yapıştıracağımı söyle:
   - Mac: sysctl -n machdep.cpu.brand_string ; sysctl hw.memsize
   - Windows: systeminfo ve GPU adı (Görev Yöneticisi > Performans)
   - Linux: free -h ; lspci | grep -i vga
2. Bellek miktarıma ve ekran kartıma göre hangi model boyutlarının çalışacağını söyle. Tahmin ile kesin bilgiyi ayır. Hız tahmini için llmspeed.dev'e bakmamı öner.
3. Bana TEK bir model öner (ollama.com/library'den, güncel boyutuna bakarak), neden onu seçtiğini 2 cümleyle yaz.
4. Ollama'yı resmî sayfadan (ollama.com/download) kurmamda adım adım yardım et. Kurulum komutunu çalıştırmadan önce bana göster ve onayımı iste.
5. Modeli indirip bir Türkçe soruyla deneyelim. Çalışmazsa sebebini birlikte bulalım.
6. Disk boyutunu ve ne kadar yer kaplayacağını önceden söyle. Hiçbir şeyi onaysız silme ya da başka yere yükleme.
Şifre, anahtar ya da kişisel dosya isteme.
```
