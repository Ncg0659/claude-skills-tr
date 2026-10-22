# 🇹🇷 claude-skills-tr

**Türkçe çalışan yapay zekâ kodlama ajanları için 3 pratik skill.**
Claude Code, claude.ai ve SKILL.md formatını okuyan diğer ajanlarla çalışır.

> Ajanınız hatayı tahminle "düzeltip" çalışan şeyi bozuyor mu? Codex'e geçince ne yapıldığı kayboluyor mu? Mobil oyununuz iPhone'da sensör izni vermiyor mu? Bu paket tam olarak bunlar için.

| Skill | Ne yapar | Ne zaman devreye girer |
|---|---|---|
| 🔎 **hata-avcisi** | Önce hatayı yeniden üretir, kök nedeni kanıtlar, sonra en küçük düzeltmeyi yapar. İki tahmin tutmazsa durur ve veri ister. | "çalışmıyor", hata mesajı, çökme, yanlış değer |
| 📝 **devir-notu** | Asistan değiştirirken dürüst, kopyalanabilir bir devir notu yazar. Gelen notları **iddia** olarak ele alıp dosyalarla doğrular. | "not çıkar", "Codex'e geçiyorum", başka asistandan not yapıştırma |
| 📱 **mobil-oyun-test** | Telefon odaklı web oyunlarını 320–430 px, dokunma, eğim sensörü, mikrofon, ses ve arka plana alma açısından test eder. Emülasyonla gerçek cihazı ayırır. | yayın öncesi, "bitti mi?" kontrolü |

## Neden?

Yapay zekâ ajanlarının en pahalı üç alışkanlığı:

1. **Kör düzeltme** — kanıt olmadan kod değiştirmek, kullanım limitini yakmak.
2. **Hayali ilerleme** — başka sohbette konuşulanı "yapıldı" sanmak.
3. **Sahte test** — gerçek telefonda denenmemiş şeye "test edildi" demek.

Bu skill'lerin hepsi aynı ilkeye dayanır: **gözlenen, doğrulanan ve varsayılan şeyi ayrı etiketle; raporu Türkçe ve dürüst ver.**

## Kurulum

### Claude Code
```bash
git clone https://github.com/Ncg0659/claude-skills-tr.git
cp -r claude-skills-tr/skills/* ~/.claude/skills/
```
Sadece bir projede kullanmak için `~/.claude/skills/` yerine projenin `.claude/skills/` klasörüne kopyalayın.

### claude.ai
Her skill klasörünü (ör. `skills/hata-avcisi`) ayrı bir `.zip` yapın ve claude.ai'nin skill yükleme bölümünden ekleyin.

## Örnek

**Önce:**
> Kullanıcı: Oyunda puan sıfırlanıyor, çalışmıyor.
> Ajan: Puan değişkenini global yaptım, artık düzelmiş olmalı. ✅

**`hata-avcisi` ile:**
> **Belirti:** Sayfa yenilenince puan 0'a dönüyor.
> **Kök neden:** `localStorage`'a `"skor"` anahtarıyla yazılıyor, `"score"` ile okunuyor — `game.js` 42 ve 118. satır (kodda doğrulandı).
> **Değişen dosyalar:** `game.js` — okuma anahtarı düzeltildi.
> **Test sonuçları:** Yenileme senaryosu tarayıcıda tekrar çalıştırıldı, puan korunuyor. Gerçek telefonda denenmedi.
> **Sonraki adım:** Eski anahtarla kaydedilmiş puanları taşıyan küçük bir geçiş eklemek.

## Katkı

Yeni Türkçe skill fikirleri ve düzeltmeler için PR ve issue açabilirsiniz. Her skill:
- tek bir işi çözmeli,
- `SKILL.md` içinde `name` ve `description` taşımalı,
- kullanıcıya Türkçe, kısa ve dürüst rapor vermeli.

---

### English

Three practical agent skills that make AI coding assistants work and report in **Turkish**: an evidence-first bug hunter, an honest cross-assistant handoff note, and a mobile web game tester. Install by copying `skills/*` into `~/.claude/skills/`.

## Lisans
MIT
