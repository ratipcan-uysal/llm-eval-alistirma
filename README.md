# LLM eval alıştırması: Atlas Mağaza destek botu

Bu repo, LLM eval eğitimindeki alıştırmaların verisini içerir. Atlas Mağaza kurgu bir e-ticaret sitesi. Konuşmalar da kurgu; gerçek müşteri ya da sipariş yok.

## Dosyalar

- `politika.md`: mağazanın iade, kargo, değişim ve ödeme kuralları. Botun paylaşabileceği linkler ve uyması gereken davranış kuralları da burada.
- `konusmalar.jsonl`: müşteri ile bot arasında geçen 40 konuşma, her satırda bir konuşma.
- `sunum/eval-mufredati.pdf`: eğitimin sunumu, 45 slayt (8 modül).
- `sunum/eval-mufredati.html`: aynı sunum, tarayıcıda sunum modunda. Dosyayı indirip tarayıcıda açın. Ok tuşları ya da tıklama slayt değiştirir, `f` tam ekran yapar, adresin sonundaki `#12` doğrudan 12. slayda gider.

## Konuşma formatı

```json
{
  "id": "ds-001",
  "split": "gelistirme",
  "konusma": [
    {"rol": "musteri", "metin": "..."},
    {"rol": "bot", "metin": "..."}
  ],
  "tools": ["siparis_sorgula"],
  "links": ["/iade"]
}
```

- `split`: `gelistirme` (ds-001…ds-020) ya da `test` (ds-021…ds-040).
- `tools`: botun konuşma sırasında çağırdığı araçlar. `handoff`, müşteriyi temsilciye aktarmak demek.
- `links`: botun mesajlarında geçen linkler.

## Nasıl kullanılır

Eğitmen hangi seti ne zaman açacağınızı söyleyecek. Başlarken yalnızca `gelistirme` setiyle çalışın. Test setini, eğitmen isteyene kadar okumayın; sonraki modülde ölçüm için ona ihtiyaç olacak.

Python ile okumak için:

```python
import json

with open("konusmalar.jsonl", encoding="utf-8") as f:
    konusmalar = [json.loads(satir) for satir in f]

gelistirme = [k for k in konusmalar if k["split"] == "gelistirme"]
```
